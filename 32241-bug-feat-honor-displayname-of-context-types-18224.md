# Bug: feat: honor displayName of context types #18224

> Issue #32241 - Created on 1/28/2025

> Original URL: https://github.com/facebook/react/issues/32241

## Description

Honor displayName of context types #18224

## Description and Significance:

In the current implementation, the displayName property of context types is not properly respected, which hampers debugging efforts. The displayName property is important in development environments for improving the readability and traceability of context types in tools like React DevTools. Without it, developers may struggle to identify which context is being used, especially when debugging complex component trees with multiple contexts. This fix improves the debugging experience and overall developer experience.

##React version:

18.0.0

##Search Terms / Keywords:

- displayName
- context types
- React
- debugging
- React DevTools
- developer tools
- feature enhancement

##Current Behavior: 

The displayName property of context types is either not applied or not correctly reflected in debugging tools. When inspecting context types in developer tools, they may appear as generic or unnamed contexts, making it difficult to distinguish between them.

##Expected Behavior: 

The displayName property of context types should be honored and properly displayed in developer tools, allowing developers to easily identify and debug the context used in the application.

## Steps To Reproduce

1.Create a context type without setting the displayName property.

2.Render a component that uses the context.

3.Inspect the component tree using React DevTools (or other relevant debugging tool).

4.Observe that the context type appears with a generic or no name.

##Use Cases and Motivating Examples (for feature requests):

Use Case 1: A developer working on a large-scale React application with multiple context providers struggles to identify which context is causing an issue in the component tree. With displayName properly honored, the context names will be easily visible in developer tools, making it easier to diagnose and fix issues.

Use Case 2: During a code review, a team member wants to understand which context types are being used in a given component. By looking at the context type name in the DevTools, they can quickly identify and review the relevant context logic.

