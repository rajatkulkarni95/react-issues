# Bug: responsive images not supported in link preload headers

> Issue #32437 - Created on 2/21/2025

> Original URL: https://github.com/facebook/react/issues/32437

## Description

Browsers does not yet support preloading responsive images from link headers. Currently React can produce link headers for resource preloading and in particular can do so for images. However if an image uses srcset or sizes it's preload won't correctly load the right variant if preloaded using a link header so we should exclude these image preloads from the headers mechanism.
