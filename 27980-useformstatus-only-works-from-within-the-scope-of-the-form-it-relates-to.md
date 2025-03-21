# useFormStatus only works from within the scope of the form it relates to

> Issue #27980 - Created on 1/17/2024

> Original URL: https://github.com/facebook/react/issues/27980

## Description

As the docs stipulate [[here](https://react.dev/reference/react-dom/hooks/useFormStatus#usage)]:
> The useFormStatus Hook only returns status information for a parent <form> and not for any <form> rendered in the same component calling the Hook, or child components.
> Instead call useFormStatus from inside a component that is located inside <form>.

I understand this is limited as a pitfall, but I also think it's a pretty big limitation. It's possible to render a form's submit button outside of the scope of the form... anywhere on a page even... with the `form` attribute. I wanted to suggest that we should be offered the same affordances with this API, otherwise we are forced to render our markup differently to use React to the fullest extent.
