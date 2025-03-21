# Proposal: Include Error Boundary Lifecycle Hooks in React's Core API

> Issue #28482 - Created on 3/3/2024

> Original URL: https://github.com/facebook/react/issues/28482

## Description

Hey there,
I've got an idea that I believe could improve the way Error Boundaries work in React. 

Right now, dealing with errors in React apps can be a bit of a hassle, especially when you have to handle them manually within each error boundary component.

So here's what I'm thinking: what if React provided some built-in hooks for common error-handling tasks? 
That way, developers could spend less time reinventing the wheel and more time building awesome apps.

Here's why I think this could be a game-changer:

- Standardization: It would establish a standard way of handling errors across different projects, making life easier for developers.
- Convenience: Instead of writing the same error-handling code over and over again, devs could just use these built-in hooks.
- Abstraction: The hooks would abstract away all the low-level error-handling details, giving us a cleaner and more manageable codebase.
- Customization: Developers could still customize the error handling behavior to fit their app's specific needs.
- Future-proofing: By including these hooks in React's core API, we ensure that they're supported and maintained for years to come.

Here are the hooks I'm proposing:

1. **onError**
- This hook would be invoked when an error is caught by the error boundary. 
- Developers could use this hook to perform custom error handling logic, such as logging the error, displaying a user-friendly error message, or triggering error reporting mechanisms.

2. **onRetry**
- This hook would be invoked when a retry action is triggered within the error boundary. 
- Developers could use this hook to implement custom retry logic, such as reloading data or retrying failed network requests.

3. **onReset**
- This hook would be invoked when the error boundary is reset, either manually or automatically after a certain period of time. 
- Developers could use this hook to clean up resources or reset the error boundary state.

I believe that including these hooks in React would make error handling a whole lot easier for everyone. 
I'd love to hear what the community thinks about this idea!

Thanks for considering it
