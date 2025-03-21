# TestUtils.Simulate alternatives

> Issue #30478 - Created on 7/26/2024

> Original URL: https://github.com/facebook/react/issues/30478

## Description

Hi team. 

We're using `Simulate` from 'react-dom/test-utils' in our package, which is a dependency for other packages. However, `Simulate` is deprecated, and it's recommended to use @testing-library/react's fireEvent (https://react.dev/warnings/react-dom-test-utils). The problem is that we need to support React starting from version ^16.8, but @testing-library/react requires React ^18.0.0 as a peer dependency. Given this constraint, do you have any recommendations for what we should use as an alternative to Simulate?
