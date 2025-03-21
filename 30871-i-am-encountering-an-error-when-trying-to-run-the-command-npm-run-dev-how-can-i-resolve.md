# I am encountering an error when trying to run the command npm run dev. How can I resolve

> Issue #30871 - Created on 9/4/2024

> Original URL: https://github.com/facebook/react/issues/30871

## Description

I utilized vite to create a frontend template. The package.json resides in the frontend directory and includes development tools, but I'm encountering an error. This project involves Django and React. I am using a Python virtual environment, and the backend is running smoothly. I have also installed React dependencies in the environment, so I am unsure of what the issue could be.

```
{
  "name": "frontend",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "axios": "^1.6.8",
    "jwt-decode": "^4.0.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.22.3",
    "react-scripts": "^3.0.1"
  },
  "devDependencies": {
    "@types/react": "^18.2.66",
    "@types/react-dom": "^18.2.22",
    "@vitejs/plugin-react": "^4.2.1",
    "eslint": "^8.57.0",
    "eslint-plugin-react": "^7.34.1",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.6",
    "vite": "^5.2.0"
  }
}
```
error:

```
(env) PS C:\Users\Abdul\Documents\Personal Projects\API-test\Django&React FS\frontend> npm run dev

> <a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="7117031e1f05141f1531415f415f41">[email protected]</a> dev
> vite

'React' is not recognized as an internal or external command,
operable program or batch file.
node:internal/modules/cjs/loader:1146
  throw err;
  ^

Error: Cannot find module 'C:\Users\Abdul\Documents\Personal Projects\API-test\vite\bin\vite.js'
    at Module._resolveFilename (node:internal/modules/cjs/loader:1143:15)
    at Module._load (node:internal/modules/cjs/loader:984:27)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:135:12)
    at node:internal/main/run_main_module:28:49 {
  code: 'MODULE_NOT_FOUND',
  requireStack: []
}

Node.js v20.12.1
(env) PS C:\Users\Abdul\Documents\Personal Projects\API-test\Django&React FS\frontend>
```

Try https://reacter.space/questions/i-am-encountering-an-error-when-trying-to-run-the-command-npm-run-dev-how-can-i-resolve
