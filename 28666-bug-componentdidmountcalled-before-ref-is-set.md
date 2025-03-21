# Bug: componentDidMountCalled before ref is set

> Issue #28666 - Created on 3/28/2024

> Original URL: https://github.com/facebook/react/issues/28666

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

I have encountered an issue where a class componentDidMount method is called before a ref is set in another. Also I am seeing sometimes it is being called twice, but not always. The ref is set in a class called Ex1 and the componentDidMount in a class called Ex2. There is also a forwardRef function component in the mix.

React version: 18.2.0

## Steps To Reproduce

1. Run "npx create-react-app my-app"
2. Copy the code I have provided into app.js
3. Run 'npm start'
4. Open the dev tools and reload the page and follow the debugger points.

Here is a fiddle with the issue. Please note that I was having issues with jsFiffle.net not fully loading. I don't think it was my fiddle, but it was acting weird. If that happens just create your own fiddle from scratch and it should work.
https://jsfiddle.net/CodeMedic42/d50mnjz8/4/

Here is a copy of my code
```
import React, { useRef, Component, forwardRef } from 'react';

class Ex1 extends Component {
	render() {
		const {
			innerRef,
			children,
		} = this.props;

		return (
			<div
				ref={(element) => {
					console.log('This line is called after the componentDidMount in Ex2.');
					innerRef.current = element;
					debugger;
				}}
				className="ex1"
			>
				{children}
			</div>
		);
	}
}

class Ex2 extends Component {
	componentDidMount() {
		const { targetRef } = this.props;

		console.log('This line is hit before targetRef is set.');
        console.log('Also it appears to be called twice. Once before the ref is set and once after.');

		debugger;
	}
	
	render() {
		const {
			innerRef,
		} = this.props;

		return <div className="ex2">I do my own thing</div>;
	}
}

const Bar1 = forwardRef((props, ref) => {
	const {
		children,
	} = props;

	return (
		<Ex1 innerRef={ref}>
			{children}
		</Ex1>
	);
});

function Test() {
	const targetRef = useRef();

	return (
		<Bar1 ref={targetRef}>
			<Ex2 targetRef={targetRef}/>
		</Bar1>
	);
}

export default Test;
```

## The current behavior
The componentDidMount method in Ex2 is called before, and sometimes after, the call to the ref function in Ex1.

## The expected behavior
The componentDidMount method in Ex2 should be called once and after the ref is set in Ex1.

