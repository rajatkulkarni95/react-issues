# Bug: Unexpected axios.get request and wrong AxiosInstance stored in state

> Issue #31389 - Created on 10/31/2024

> Original URL: https://github.com/facebook/react/issues/31389

## Description

The following content is from automatic translation and may be grammatically incorrect
### React Version:

- React 18.3.1 (Vite)
- React 19.0.0 (Next.js)

## Steps To Reproduce:

1. Use `useState` in a component to create an `axiosInstance`.
2. Use `setState` to set the axios instance. Example code:

   ```typescript
   const [instance, setInstance] = useState<AxiosInstance|null>(null);

   setInstance(axios.create({ baseURL: "https://api.example.com" }));
3. This issue can be reproduced in React 18.3.1 (Vite) and React 19.0.0 (Next.js).


## Code Example 
  ```typescript
  import React, { useState } from "react";
  import axios, { AxiosInstance } from "axios";
  
  const ExampleComponent = () => {
    const [instance, setInstance] = useState<AxiosInstance | null>(null);
  
    setInstance(axios.create({
      baseURL: "https://api.example.com"
    }));
  
    return <div>Axios Instance Issue</div>;
  };
  
  export default ExampleComponent;
```
## The Current Behavior
When setting axiosInstance using setState, the instance.get method is automatically triggered, causing an API request. This makes it impossible to store the axiosInstance properly in the state and may lead to the instance being recreated on every render, resulting in unnecessary requests.
![img_v3_02g6_205cd365-bda6-4340-9723-717218a6504g](https://github.com/user-attachments/assets/0f1ad170-bf11-4f76-94f7-e8ecd05439ca)
You'll then see that your browser automatically sends a GET method request to baseUrl endpoint.
Not only that, but the value of the original instance will automatically refer to a Promise object (which looks like the GET method request)

## The Expected Behavior 
axiosInstance should be properly stored in the state, not a Promise object, and not automatically trigger a get request or cause any unintended side effects.
