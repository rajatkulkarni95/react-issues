# Bug: useState,  state does not update inside websocket.onmessage rather the state value is preserved untill the next render 

> Issue #30454 - Created on 7/25/2024

> Original URL: https://github.com/facebook/react/issues/30454

## Description

<!--

-->

React version:

## Steps To Reproduce

1.
2.

<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
    useEffect(() => {
    let preservedId;
    ws.onmessage = (event) => {
      const receivedMessage = JSON.parse(event.data);
      console.log("receivedMessage", receivedMessage);
// getUser func returns id because the state is preservec so I have put the whole function with a dependency and when I receive the message id becomes null again
      preservedId = getUser();
      if (
        !receivedMessage.status &&
        receivedMessage.sender_id === preservedId
      ) {
        setActiveChat((prevMessages) => {
          const filteredMessages = prevMessages.filter(
            (msg) =>
              msg?.message_identifier !== receivedMessage.message_identifier,
          );
          return [...filteredMessages, receivedMessage];
        });
      }
    };
  }, [newUserId]);
-->

## The current behavior
state is not updated inside ws.onmessage , state is preserved inside we.onmessage and the state is working perfectly fine outside ws.onmessage


## The expected behavior
state should get updated


