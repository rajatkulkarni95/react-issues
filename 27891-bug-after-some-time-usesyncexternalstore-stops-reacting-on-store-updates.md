# Bug: After some time useSyncExternalStore stops reacting on store updates

> Issue #27891 - Created on 1/8/2024

> Original URL: https://github.com/facebook/react/issues/27891

## Description

I'm using React+Redux, as everyone else. Initially, I assumed it's a react-redux problem, but this bug is only reproduced on versions 8.x and 9.x of react-redux, where useSyncExternalStore was added, and react-redux team suggested me to ask you about this. The issue:

The UI is working perfectly fine, but after a while it just stops receiving store updates. The Redux DevTools shows that the action was successfully dispatched, but no re-renders are triggered by that. We have a setState bound to a blur event on the root component, and when I move my cursor over DevTools, causing blur event, the UI re-renders. Any change in store do not trigger re-render. It is a rare bug, happens after user spends some time on the site without reloads. One of the code examples:

```
const { selectedItemId } = useSelector(getComponentProps);
```
```
const getComponentProps = createStructuredSelector({ selectedItemId: (state) => state.path.to.selectedItemId })
```
Looks like the problem is in forceUpdate somewhere inside the codebase, but I don't really know.

React version: 18.2.0 (react-redux@8.1.3 or @9.0.4, redux@4.1.8, and as a dependency of react-redux, the actual use-sync-external-store@1.2.0 is installed)
There are no clear steps to reproduce, just don't reload the page and after a while it happens.

I tried to figure out the problem by myself, but the flow inside useSyncExternalStore is just too complex. I'm not the first one who faced this issue (on react-redux repo: [2060](https://github.com/reduxjs/react-redux/issues/2060), [1981](https://github.com/reduxjs/react-redux/issues/1981)). There are also a couple of demos: [1](https://www.loom.com/share/89b5849a9f054933b439c902ba2fcfd6?sid=90fca031-a1d3-44e8-828a-deb5c75f13a3), [2](https://www.loom.com/share/ac1594bc24144d4287518fd922ac2c90?sid=b70b64d4-4a6b-4717-8238-7fc4f2bb7dad).

I'm not sure if this information will be helpful, but we can only catch this bug on production (i.e., NODE_ENV === 'production'). Maybe this helps.

