#  Introducing `UseConstantState()` - A Novel Approach to Permanent State Management 🚀

> Issue #28357 - Created on 2/16/2024

> Original URL: https://github.com/facebook/react/issues/28357

## Description

👋 Hi there, esteemed Facebook/React maintainers,

I hope this message finds you well. My name is Mahdi Hazrati, and I'm a software engineer at [nextproduction.dev](http://nextproduction.dev/). I'm reaching out to share an innovative concept for enhancing state management within the React library.

I'd like to introduce the notion of `useConstantState()` - a novel approach to state management that tackles the persistent challenge of data loss upon page reloads or route changes. This concept aims to provide developers with a seamless experience in managing state within React applications.

At its core, `useConstantState()` functions akin to `useState()`, but with an added layer of durability. It ensures that state remains accessible even amidst browser refreshes or navigation transitions by leveraging IndexedDB for data storage.

Allow me to shed some light on the workings of this concept. Upon initialization, `useConstantState()` generates a unique key and utilizes IndexedDB to store the state object associated with this key. Subsequently, upon each component render, it retrieves and updates the state from this persistent storage, thus preserving its integrity across sessions.

The genesis of this idea stems from real-world scenarios encountered within my development endeavors at nextproduction.dev. Often, our team found the need to retain certain application states across page reloads, prompting me to explore innovative solutions within the React ecosystem.

To illustrate the practical application of this concept, I've crafted an initial implementation as follows:

```jsx
import React, { useState, useEffect } from "react";

/**
 * Custom React hook for managing state persistence using IndexedDB.
 * @param {*} initialValue - The initial value of the state.
 * @returns {[*, function]} - A tuple containing the state value and a function to update it.
 */
function useConstantState(initialValue) {
    // Define state variable and setter
    const [state, setState] = useState(initialValue);
    // Generate a unique key for this state
    const key = "state_" + Math.random().toString(36).substr(2, 9);

    // Effect to handle state persistence
    useEffect(() => {
        // Open IndexedDB database
        const openRequest = indexedDB.open("ReactIndexedDB", 1);

        // Handle database upgrade
        openRequest.onupgradeneeded = function (event) {
            const db = event.target.result;
            // Create object store
            db.createObjectStore("state", { keyPath: "key" });
        };

        // Handle database opening success
        openRequest.onsuccess = function (event) {
            const db = event.target.result;
            const transaction = db.transaction(["state"], "readwrite");
            const objectStore = transaction.objectStore("state");
            // Get state value from IndexedDB
            const getRequest = objectStore.get(key);

            getRequest.onsuccess = function (event) {
                // Set state to retrieved value if available, otherwise use initial value
                if (getRequest.result) {
                    setState(getRequest.result.value);
                } else {
                    setState(initialValue);
                }
            };

            // Close database connection
            transaction.oncomplete = function () {
                db.close();
            };
        };

        // Handle database opening error
        openRequest.onerror = function (event) {
            console.error("Error opening IndexedDB", event);
        };
    }, [initialValue, key]);

    // Function to update state and persist to IndexedDB
    const setConstantState = (newValue) => {
        const openRequest = indexedDB.open("ReactIndexedDB", 1);

        // Handle database opening success
        openRequest.onsuccess = function (event) {
            const db = event.target.result;
            const transaction = db.transaction(["state"], "readwrite");
            const objectStore = transaction.objectStore("state");

            // Update state value in IndexedDB
            objectStore.put({ key, value: newValue });

            // Close database connection
            transaction.oncomplete = function () {
                db.close();
            };
        };

        // Handle database opening error
        openRequest.onerror = function (event) {
            console.error("Error opening IndexedDB", event);
        };

        // Update state locally
        setState(newValue);
    };

    // Return state and setter
    return [state, setConstantState];
}

export default useConstantState;

```

I firmly believe that integrating this concept into React could significantly enhance developer productivity and user experience. Should the React maintainers express interest in exploring this idea further, I am more than willing to collaborate in refining and incorporating it into the React core.

Thank you for considering this proposal, and I eagerly await your feedback.

Warm regards,
Mahdi Hazrati
Software Engineer
mahdi@nextproduction.dev
