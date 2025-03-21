# Bug: "React Developer Tools" Chrome Extension unable to profile page rendering

> Issue #28917 - Created on 4/26/2024

> Original URL: https://github.com/facebook/react/issues/28917

## Description

I'm unable to profile the rendering of a page in a Chrome browser launched from Visual Studio Code ("VSC"). I think I'm using the most recent stable versions of Chrome and the "React Developer Tools" extension.

I'm attaching screenshots to help explain the behavior I'm seeing.

The page I'm rendering takes less than a second to render in "production" mode (created by "yarn build") and more than 90 seconds to render when launched from VSC. I want to profile the development version in hopes of finding a workaround to whatever is causing this 100x slowdown.

Here is what I'm seeing:

1. Wait until the page renders ("Rendered page")
2. Open Profiler tab in Chrome Developer Tools ("Initial Profiler tab")
3. Click the "record" button ("Profiling in progress")
4. Enter "CNTRL r" to cause a reload. The developer tools is stuck on the "Sources" tab and flashes uncontrollably, apparently as source files are loaded ("Flashing while re-rendering").
5. Wait until the page renders. Note the console errors at the bottom ("Stable after re-rendering completes, two console complaints")
6. Attempt to open the "Profiler" tab -- it now says "Profiling not supported" ("Profiler tab now says "Profiling not supported"")

I note that the complaint in the final screenshot references a very old version of React (16.5+). Its embedded link goes to an old and stale React documentation page.

React version: "^18.2.0"
React DeveloperTools version: b566064da on 4/15/2024

Screenshots follow:

![00_rendered_page](https://github.com/facebook/react/assets/64976799/80f4a284-af81-439e-be15-93c11345c7a3)
**Rendered page**

![01_initial_profiler](https://github.com/facebook/react/assets/64976799/ce3ee4bd-743d-4c29-bd5b-9549d38b37ae)
**Initial Profiler tab**

![02_in_progress](https://github.com/facebook/react/assets/64976799/a3e4ae85-a8f5-416a-96b9-5df4fd233fc4)
**Profiling in progress**

![03_flashing](https://github.com/facebook/react/assets/64976799/729a2f99-ae81-4845-a1ac-6cc3bc0e49ac)
**Flashing while re-rendering**

![04_stable_with_console_error_after_rendering](https://github.com/facebook/react/assets/64976799/c7866b5a-e7b0-45cd-a91d-dc8ff9647d01)
**Stable after re-rendering completes, two console complaints"

![05_Profiling_not_supported_after_render](https://github.com/facebook/react/assets/64976799/7d66d632-c001-4ed5-8c9e-04a6b55031da)
**Profiler tab now says "Profiling not supported"**

## Steps To Reproduce

See above

Link to code example:

Too hard to create, see screenshots above

## The current behavior

See screenshots above

## The expected behavior

I expect to see a profile report

