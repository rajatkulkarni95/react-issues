# Unexpected state behavior when updating nested state objects

> Issue #30414 - Created on 7/20/2024

> Original URL: https://github.com/facebook/react/issues/30414

## Description

Title:
Unexpected state behavior when updating nested state objects

Description:
I'm experiencing an issue where state updates do not propagate correctly under certain conditions when updating nested objects in state. This seems to be a bug in React's state handling.

Steps to Reproduce:

1.Create a new React component with nested state objects.
2.Update the nested state object using a setState function.
3.Observe that the state update does not reflect correctly in the component.

Code Examble
import React, { useState } from 'react';

const NestedStateComponent = () => {
  const [state, setState] = useState({ nested: { value: 0 } });

  const updateNestedState = () => {
    setState(prevState => ({
      ...prevState,
      nested: { value: prevState.nested.value + 1 }
    }));
  };

  return (
    <div>
      <p>Value: {state.nested.value}</p>
      <button onClick={updateNestedState}>Increment</button>
    </div>
  );
};

export default NestedStateComponent;

Expected Behavior:
The state.nested.value should increment by 1 every time the button is clicked.

Actual Behavior:
The state.nested.value does not update correctly, and the component does not re-render as expected.

Dependencies
  "dependencies": {
    "@emotion/cache": "^11.11.0",
    "@emotion/react": "^11.11.4",
    "@emotion/styled": "^11.11.5",
    "@hookform/resolvers": "^3.2.0",
    "@iconify/react": "^4.1.0",
    "@mui/icons-material": "^5.15.20",
    "@mui/lab": "^5.0.0-alpha.139",
    "@mui/material": "^5.15.20",
    "@mui/x-date-pickers": "^7.8.0",
    "@reduxjs/toolkit": "^2.2.5",
    "apexcharts": "^3.49.2",
    "autosuggest-highlight": "^3.3.4",
    "axios": "^1.4.0",
    "date-fns": "^2.30.0",
    "framer-motion": "^10.15.1",
    "history": "^5.3.0",
    "lodash": "^4.17.21",
    "mui-one-time-password-input": "^2.0.2",
    "notistack": "^3.0.1",
    "nprogress": "^0.2.0",
    "numeral": "^2.0.6",
    "prop-types": "^15.8.1",
    "react": "^18.2.0",
    "react-apexcharts": "^1.4.1",
    "react-dom": "^18.2.0",
    "react-dropzone": "^14.2.3",
    "react-helmet-async": "^1.3.0",
    "react-hook-form": "^7.45.4",
    "react-lazy-load-image-component": "^1.6.0",
    "react-redux": "^9.1.2",
    "react-router": "^6.14.2",
    "react-router-dom": "^6.14.2",
    "react-scripts": "^5.0.1",
    "simplebar-react": "^3.2.4",
    "stylis": "^4.2.0",
    "stylis-plugin-rtl": "^2.0.2",
    "yup": "^1.2.0",
    "yup-phone-lite": "^2.0.1"
  },

