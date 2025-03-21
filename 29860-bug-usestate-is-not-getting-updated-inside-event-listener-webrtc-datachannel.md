# Bug:  useState is not getting updated inside Event Listener (Webrtc DataChannel).

> Issue #29860 - Created on 6/12/2024

> Original URL: https://github.com/facebook/react/issues/29860

## Description

useState is not getting updated inside Event Listener.
inside it stores previous value 
I'm developing simple tiic-tac-toe multi player react app using webrtc datachannel
where when i reset the game the peer game should have to be reset at that moment but inside the event it has some other value stored (previous)
React version:18.2.0

this is an rtcdatachannel event call
const receiveChannelCallback = (event) => {
      receiveChannel.current = event.channel;
      if(receiveChannel.current.label === "mouseChannel"){
        console.log('inside mouse channel receive side');
        handleMouseChannel(receiveChannel.current);
    }else if(receiveChannel.current.label === "messageChannel"){
      receiveChannel.current.onmessage = handleDChat;
      }else if(receiveChannel.current.label === "gameChannel"){
      receiveChannel.current.onmessage = handleDGame;

      }else if(receiveChannel.current.label === "resetChannel"){
      receiveChannel.current.onmessage = handleDReset;
      }
    }
  
      receivePc.ondatachannel = receiveChannelCallback;

const handleDGame = (e) => {
  console.log(matrix);
  const { data } = JSON.parse(e.data);
  const { preVal, r, c } = data;
 
    if (matrix[r][c] === "-") {
      setDisable(false);

      // Update preVal
      const newPreVal = preVal === "X" ? "O" : "X";
      setPreVal(newPreVal);

      // Use functional update to ensure the latest state
      setMatrix((prevMatrix) => {
          const newMatrix = [...prevMatrix];
          newMatrix[r][c] = preVal;
          
          const winner = checkWinner(newMatrix);
          if (winner) {
              setWinner(true);
              setWinVal(winner);
              setDraw(false);
              setDisable(true);
          } else if (!handleDraw(newMatrix)) {
              setDraw(true);
          }

          return newMatrix;
      });
  } 


Link to code example:

https://github.com/michaelnadar/tic_tac-tsc/blob/main/frontend-tsc/src/components/Room.tsx

## The current behavior
inside handleDGame while i m resetting the matrix value to its initial val it stores prev val

## The expected behavior
it has to update reset the matrix value inside handleDGame
