# Bug: Different file (/usr/share/nodejs/react-is/index.js ) contents when installing via "apt install" and build from source, install package.

> Issue #27852 - Created on 12/20/2023

> Original URL: https://github.com/facebook/react/issues/27852

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
17.0.2

OS: Ubuntu 22.04

Version of package source: 
17.0.2+dfsg+~cs106.66.62-1

Files of package:
node-react-17.0.2+dfsg+~cs106.66.62/
node-react_17.0.2+dfsg+~cs106.66.62-1.debian.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62-1.dsc
node-react_17.0.2+dfsg+~cs106.66.62.orig-react-shallow-renderer.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-create-subscription.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-cache.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-devtools.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-dom.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-is.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-reconciler.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-typesreact.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-test-renderer.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-scheduler.tar.xz
node-react_17.0.2+dfsg+~cs106.66.62.orig-types-use-subscription.tar.xz

## Steps To Reproduce

1. **sudo apt-get install node-react**
_output of command:_
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  node-prop-types
The following NEW packages will be installed:
  node-prop-types node-react
0 upgraded, 2 newly installed, 0 to remove and 54 not upgraded.
Need to get 0 B/528 kB of archives.
After this operation, 13,8 MB of additional disk space will be used.
Do you want to continue? [Y/n] 
Selecting previously unselected package node-react.
(Reading database ... 206340 files and directories currently installed.)
Preparing to unpack .../node-react_17.0.2+dfsg+~cs106.66.62-1_all.deb ...
Unpacking node-react (17.0.2+dfsg+~cs106.66.62-1) ...
Selecting previously unselected package node-prop-types.
Preparing to unpack .../node-prop-types_15.7.2+~15.7.4-2_all.deb ...
Unpacking node-prop-types (15.7.2+~15.7.4-2) ...
Setting up node-react (17.0.2+dfsg+~cs106.66.62-1) ...
Setting up node-prop-types (15.7.2+~15.7.4-2) ...

2. **cat /usr/share/nodejs/react-is/index.js**
_output:_
'use strict';

if (process.env.NODE_ENV === 'production') {
  module.exports = require('./cjs/react-is.production.min.js');
} else {
  module.exports = require('./cjs/react-is.development.js');
}

3. **apt-get source -b node-react** maybe required to call "sudo apt-get build-dep node-react" before.
_some output:_
dpkg-source: info: extracting node-react in node-react-17.0.2+dfsg+~cs106.66.62
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-react-shallow-renderer.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-create-subscription.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-cache.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-devtools.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-dom.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-is.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-reconciler.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-react-test-renderer.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-scheduler.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-types-use-subscription.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62.orig-typesreact.tar.xz
dpkg-source: info: unpacking node-react_17.0.2+dfsg+~cs106.66.62-1.debian.tar.xz
dpkg-source: info: using patch list from debian/patches/series
....
dpkg-deb: building package 'node-react' in '../node-react_17.0.2+dfsg+~cs106.66.62-1_all.deb'.
 dpkg-genbuildinfo --build=binary -O../node-react_17.0.2+dfsg+~cs106.66.62-1_amd64.buildinfo
 dpkg-genchanges --build=binary -O../node-react_17.0.2+dfsg+~cs106.66.62-1_amd64.changes
dpkg-genchanges: info: binary-only upload (no source code included)
 dpkg-source --after-build .
dpkg-buildpackage: info: binary-only upload (no source included)

4. **sudo dpkg -i ./node-react_17.0.2+dfsg+~cs106.66.62-1_all.deb**
_output:_
(Reading database ... 206652 files and directories currently installed.)
Preparing to unpack .../node-react_17.0.2+dfsg+~cs106.66.62-1_all.deb ...
Unpacking node-react (17.0.2+dfsg+~cs106.66.62-1) over (17.0.2+dfsg+~cs106.66.62-1) ...
Setting up node-react (17.0.2+dfsg+~cs106.66.62-1) ...

5. **cat /usr/share/nodejs/react-is/index.js** 
_output:_
/**
 * Copyright (c) Facebook, Inc. and its affiliates.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 *
 * @flow
 */

'use strict';

export * from './src/ReactIs';


<!--
  Your bug will get fixed much faster if we can run your code and it doesn't
  have dependencies other than React. Issues without reproduction steps or
  code examples may be immediately closed as not actionable.
-->

Link to code example:

<!--
  Please provide a CodeSandbox (https://codesandbox.io/s/new), a link to a
  repository on GitHub, or provide a minimal code example that reproduces the
  problem. You may provide a screenshot of the application if you think it is
  relevant to your bug report. Here are some tips for providing a minimal
  example: https://stackoverflow.com/help/mcve.
-->

## The current behavior
Different contents of file cat /usr/share/nodejs/react-is/index.js during installation node-react via "sudo apt-get install" and install from source.

## The expected behavior
Equal contents of file cat /usr/share/nodejs/react-is/index.js
