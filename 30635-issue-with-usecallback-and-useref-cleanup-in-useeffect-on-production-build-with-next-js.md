# issue with `useCallback` and `useRef` Cleanup in `useEffect` on Production Build with Next.js

> Issue #30635 - Created on 8/8/2024

> Original URL: https://github.com/facebook/react/issues/30635

## Description

We are encountering an issue where a `useCallback` function, managed with `useRef`, does not perform cleanup as expected during component unmount in both development and production builds of a Next.js application.

#### Problematic Code

```javascript
import React, { useCallback, useEffect, useRef } from 'react';

const MyComponent = () => {
  const stopRecordingRef = useRef<() => void>(() => {});

  const [recorder, setRecorder] = React.useState<MediaRecorder | null>(null);
  const [stream, setStream] = React.useState<MediaStream | null>(null);
  const videoRefs = useRef<{ webcam: HTMLVideoElement | null, recordedVideo: HTMLVideoElement | null }>({
    webcam: null,
    recordedVideo: null,
  });

  const stopRecording = useCallback(() => {
    console.log('stopRecording called');
    if (recorder) {
      console.log('Stopping recorder');
      recorder.stop();
    }

    if (stream) {
      console.log('Stopping stream tracks');
      stream.getTracks().forEach(track => track.stop());
      setStream(null);
    }

    if (videoRefs.current?.webcam) {
      console.log('Clearing webcam srcObject');
      videoRefs.current.webcam.srcObject = null;
    }

    if (videoRefs.current?.recordedVideo) {
      console.log('Clearing recorded video src');
      videoRefs.current.recordedVideo.src = '';
    }
  }, [recorder, stream]);

  useEffect(() => {
    stopRecordingRef.current = stopRecording;
  }, [stopRecording]);

  useEffect(() => {
    return () => {
      console.log('Cleaning up in useEffect');
      if (stopRecordingRef.current) {
        stopRecordingRef.current();
      } else {
        console.log('stopRecordingRef.current is not set');
      }
    };
  }, []);

  return (
    <div>
      {/*JSX */}
    </div>
  );
};

export default MyComponent;
```

#### Expected Behavior

The `stopRecording` function should be executed properly during component unmount via `useEffect`. This function should correctly perform all cleanup operations both in development and production builds.

#### Actual Behavior

- **In Development:** The `stopRecording` function executes correctly, and cleanup operations are performed as expected.
- **In Production Build:** The `stopRecording` function does not execute properly during component unmount, resulting in lingering resources and incorrect references.

#### Steps to Reproduce

1. Implement the `stopRecording` function using `useCallback`.
2. Use `useRef` to maintain a reference to the `stopRecording` function.
3. Set the reference in `useEffect`.
4. Verify the cleanup process in the production build.

#### Environment

- **Next.js Version:** 12.0.8
- **React Version:** 17.0.2
- **React DOM Version:** 17.0.2

#### Suggestions and Requests

Please investigate this issue and suggest a resolution if available. If a specific solution is not possible, guidance on correctly implementing resource cleanup during component unmounting using `useCallback` and `useRef` in a Next.js environment would be highly appreciated.
