# [React 19]: Component-specific Import Restrictions in React

> Issue #32259 - Created on 1/29/2025

> Original URL: https://github.com/facebook/react/issues/32259

## Description

Proposal: Component-specific Import Restrictions in React
Problem:
Currently, there is no built-in mechanism in React to restrict the usage of certain components only within specific folders. For example, we may want a component, say ProductCardImage, to be used exclusively within the product-card/ folder and disallow its import anywhere else in the project. This can help maintain clear component structure and improve maintainability, particularly in large projects.

Current Workaround:
We are using ESLint with no-restricted-imports to restrict the usage of specific components across the project. However, this approach is quite general and requires us to manually configure import restrictions for each component. This can become cumbersome and repetitive as the project grows.

Proposal:
Introduce a feature within React itself (possibly in React DevTools or through a special flag or directive) that allows component authors to mark their components as "folder-specific." When a component is marked this way, React would throw an error or warning if that component is imported outside of its designated folder.

This feature could work as follows:

Developers can add a special flag or decorator to their components to indicate that the component should only be used within a specific folder.
React (or an accompanying tool) would check the folder structure and ensure that the component is only imported within the allowed folder.
If the component is imported outside of its designated folder, React would provide a warning or error message to alert the developer.
Why React?
Tighter Integration: React can have better awareness of the component's structure and usage context compared to an ESLint rule. This would provide more accurate and consistent enforcement of folder-specific usage.
Developer Experience: By embedding this logic directly into React, developers would receive real-time feedback in their development environment, improving productivity and avoiding manual configuration.
Maintainability: A built-in solution would provide a clear, standardized way to enforce folder-specific usage of components, reducing the need for external configuration tools like ESLint.
Benefits:
Improved Component Structure: Forces clear boundaries between components, making it easier to maintain and scale the application.
Enhanced Developer Productivity: React can provide real-time feedback, making it easier to spot incorrect imports during development.
Cleaner Codebase: Reduces the risk of improper imports and usage, leading to a more organized and modular project.
Alternatives:
While ESLint can be used to achieve this functionality, it requires significant manual effort to configure and maintain, especially as the project grows. A native React solution would be more seamless and intuitive.

Conclusion:

This proposal aims to enhance the React ecosystem by providing a built-in solution for restricting component usage based on folder structure. It would simplify the development process, improve code maintainability, and provide more accurate import restrictions than what is currently possible with external tools like ESLint.
