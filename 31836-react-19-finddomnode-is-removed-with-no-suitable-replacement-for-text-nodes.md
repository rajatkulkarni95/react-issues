# [React 19] `findDOMNode` is removed, with no suitable replacement for text nodes

> Issue #31836 - Created on 12/18/2024

> Original URL: https://github.com/facebook/react/issues/31836

## Description

## Summary

In React 18 and below, the only way to obtain a reference to a text node rendered by a React component is with `findDOMNode`. [The docs](https://18.react.dev/reference/react-dom/findDOMNode#adding-a-wrapper-div-element) indicated that the reason `findDOMNode` hadn't been removed was because there were no alternatives to use cases like this.

This seems like an extremely narrow edge case (why would you need a ref to a text node, right?), but [@nytimes/react-prosemirror](https://github.com/nytimes/react-prosemirror) is heavily reliant on this API. Because this is a rich text editing library, we can't wrap text nodes with ref-able elements without introducing complexity/edge cases.

What should we do here? I understand the desire to remove a long-deprecated API, but React ProseMirror is now somewhat in a lurch.

A simplified version of how React ProseMirror uses `findDOMNode`:

```ts
export class TextNodeView extends Component<Props> {
  private viewDescRef: null | TextViewDesc | CompositionViewDesc = null;
  private renderRef: null | JSX.Element = null;

  updateEffect() {
    const { view, decorations, siblingsRef, parentRef, getPos, node } =
      this.props;
    // There simply is no other way to ref a text node
    // eslint-disable-next-line react/no-find-dom-node
    const dom = findDOMNode(this);

    let textNode = dom;
    while (textNode.firstChild) {
      textNode = textNode.firstChild as Element | Text;
    }

    // We construct a view descriptor tree to integrate with ProseMirror.
    // This is essentially ProseMirror's virtual DOM implementation. It
    // needs to contain references to each node that it's responsible for,
    // just like the React virtual DOM.
    if (!this.viewDescRef) {
      this.viewDescRef = new TextViewDesc(
        undefined,
        [],
        () => getPos.current(),
        node,
        decorations,
        DecorationSet.empty,
        dom,
        textNode
      );
    } else {
      this.viewDescRef.parent = parentRef.current;
      this.viewDescRef.children = [];
      this.viewDescRef.node = node;
      this.viewDescRef.getPos = () => getPos.current();
      this.viewDescRef.outerDeco = decorations;
      this.viewDescRef.innerDeco = DecorationSet.empty;
      this.viewDescRef.dom = dom;
      // @ts-expect-error We have our own ViewDesc implementations
      this.viewDescRef.dom.pmViewDesc = this.viewDescRef;
      this.viewDescRef.nodeDOM = textNode;
    }

    if (!siblingsRef.current.includes(this.viewDescRef)) {
      siblingsRef.current.push(this.viewDescRef);
    }

    siblingsRef.current.sort(sortViewDescs);
  }

  shouldComponentUpdate(nextProps: Props): boolean {
    return !shallowEqual(this.props, nextProps);
  }

  componentDidMount(): void {
    this.updateEffect();
  }

  componentDidUpdate(): void {
    this.updateEffect();
  }

  componentWillUnmount(): void {
    const { siblingsRef } = this.props;
    if (!this.viewDescRef) return;
    if (siblingsRef.current.includes(this.viewDescRef)) {
      const index = siblingsRef.current.indexOf(this.viewDescRef);
      siblingsRef.current.splice(index, 1);
    }
  }

  render() {
    const { node, decorations } = this.props;

    // This may wrap the text in, e.g., a span,
    // but usually returns a string
    return decorations.reduce(
      wrapInDeco,
      node.text
    );
  }
}
```

