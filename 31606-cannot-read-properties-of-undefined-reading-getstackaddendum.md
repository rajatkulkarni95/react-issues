# Cannot read properties of undefined (reading 'getStackAddendum')

> Issue #31606 - Created on 11/21/2024

> Original URL: https://github.com/facebook/react/issues/31606

## Description

After building the application on the production version I get the error Cannot read properties of undefined (reading 'getStackAddendum'). I have split the application into microfronts that are linked using the webpack module federation. 

The error here is because ReactDebugCurrentFrame is undefined.

The problem does not appear in the dev version, only in the production version

```
function printWarning(level, format, args) {
      {
        var ReactDebugCurrentFrame = ReactSharedInternals.ReactDebugCurrentFrame;
        var stack = ReactDebugCurrentFrame.getStackAddendum();
        if (stack !== '') {
          format += '%s';
          args = args.concat([stack]);
        } // eslint-disable-next-line react-internal/safe-string-coercion

        var argsWithFormat = args.map(function (item) {
          return String(item);
        }); // Careful: RN currently depends on this prefix

        argsWithFormat.unshift('Warning: ' + format); // We intentionally don't use spread (or .apply) directly because it
        // breaks IE9: https://github.com/facebook/react/issues/13610
        // eslint-disable-next-line react-internal/no-production-logging

        Function.prototype.apply.call(console[level], console, argsWithFormat);
      }
    }
```

package.json application shell
```
{
  "name": "wes-shell-app",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@cloudbeds/webpack-module-federation-types-plugin": "^1.18.0",
    "@emotion/react": "^11.11.4",
    "@emotion/styled": "^11.11.5",
    "@joint/core": "^4.0.4",
    "@mui/icons-material": "^5.11.6",
    "@mui/lab": "^5.0.0-alpha.125",
    "@mui/material": "^5.15.21",
    "@mui/x-charts": "^7.8.0",
    "@mui/x-date-pickers": "^5.0.18",
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^14.4.3",
    "@types/react": "^18.0.27",
    "@types/react-dom": "^18.0.10",
    "chart.js": "^4.4.3",
    "color": "^4.2.3",
    "date-fns": "^2.29.3",
    "history": "^5.3.0",
    "js-cookie": "^3.0.5",
    "mobx": "^6.7.0",
    "mobx-react": "^7.6.0",
    "mobx-utils": "^6.0.5",
    "notistack": "^3.0.1",
    "path-to-regexp": "^6.2.1",
    "react": "^18.2.0",
    "react-chartjs-2": "^5.2.0",
    "react-custom-scrollbars-2": "^4.5.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.13.0",
    "react-scripts": "^5.0.1",
    "typescript": "^4.9.4",
    "web-vitals": "^3.0.4"
  },
  "scripts": {
    "dev": "npm run make-types && npm run generate-env && craco start --verbose",
    "make-types": "make-federated-types -o public/@types",
    "generate-env": "cd .. && env.sh && cd wes-shell-app",
    "serve": "serve -s build",
    "mock-api": "node \"src/mocks/api.js\"",
    "build": "craco build",
    "test": "craco test",
    "devcert": "set HTTPS=true&&set SSL_CRT_FILE=../wes-shell-app/cert.crt&&set SSL_KEY_FILE=../wes-shell-app/cert.key"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "@craco/craco": "^7.0.0",
    "@types/color": "^3.0.6",
    "@types/lodash": "^4.14.191",
    "connect-api-mocker": "^1.10.0",
    "express": "^4.18.2",
    "i18next": "^22.5.1",
    "i18next-browser-languagedetector": "^7.1.0",
    "jwt-decode": "^3.1.2",
    "lodash": "^4.17.21",
    "react-barcode-reader": "^0.0.2",
    "react-i18next": "^12.1.5",
    "tailwindcss": "^3.3.3",
    "zod": "^3.20.2"
  }
}
```

package.json second aplication

```
{
  "name": "wes-voice-picking-app",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@cloudbeds/webpack-module-federation-types-plugin": "^1.18.0",
    "@emotion/react": "^11.11.4",
    "@emotion/styled": "^11.11.5",
    "@mui/icons-material": "^5.11.16",
    "@mui/material": "^5.15.21",
    "@mui/x-charts": "^7.8.0",
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^14.4.3",
    "external-remotes-plugin": "^1.0.0",
    "mobx": "^6.7.0",
    "mobx-react": "^7.6.0",
    "mobx-utils": "^6.0.5",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.13.0",
    "react-scripts": "5.0.1",
    "typescript": "^4.9.4",
    "web-vitals": "^3.0.4"
  },
  "scripts": {
    "dev": "npm run generate-env && craco start --verbose",
    "generate-env": "cd .. && env.sh && cd wes-voice-picking-app",
    "serve": "serve -s build -p 3003",
    "build": "craco build",
    "test": "craco test"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "@craco/craco": "^7.0.0",
    "i18next": "^23.2.11",
    "i18next-browser-languagedetector": "^7.1.0",
    "react-i18next": "^13.0.2",
    "tailwindcss": "^3.3.3"
  }
}
```





