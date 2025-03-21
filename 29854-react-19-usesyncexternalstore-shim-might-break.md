# [React 19] useSyncExternalStore shim might break

> Issue #29854 - Created on 6/11/2024

> Original URL: https://github.com/facebook/react/issues/29854

## Description

## Summary

I just wanted to bring this to your attention - the `uSES` shim was previously packaged in a way that accessed `__SECRET_INTERNALS_DO_NOT_USE_OR_YOU_WILL_BE_FIRED` and the new 1.4 RC versions directly access `__CLIENT_INTERNALS_DO_NOT_USE_OR_WARN_USERS_THEY_CANNOT_UPGRADE`.

So either way, there will be versions of the `uSES` shim and React that will break when compiling them with each other.

Are there any planned workarounds or things we should know as package authors that rely on the shim, that we should communicate to our consumers? 
Should they pin their version?
