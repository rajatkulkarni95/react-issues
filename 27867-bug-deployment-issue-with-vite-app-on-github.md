# Bug: Deployment issue with vite.app on github

> Issue #27867 - Created on 1/2/2024

> Original URL: https://github.com/facebook/react/issues/27867

## Description

Following is my package.json

{
  "name": "3d-portfolio-app",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "homepage": "https://narendrawadhwa.github.io",
  "scripts": {
    "dev": "vite --host 0.0.0.0",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
    "deploy": "vite build && gh-pages -d dist"
  },
  
  "dependencies": {
    "@emailjs/browser": "^3.11.0",
    "@emotion/react": "^11.11.1",
    "@emotion/styled": "^11.11.0",
    "@mui/material": "^5.14.18",
    "@react-spring/three": "^9.7.3",
    "@react-three/drei": "^9.88.17",
    "@react-three/fiber": "^8.15.11",
    "@types/three": "^0.158.3",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-icons": "^4.12.0",
    "react-loader-spinner": "^6.1.1-0",
    "react-router-dom": "^6.20.0",
    "react-spring": "^9.7.3",
    "react-vertical-timeline-component": "^3.6.0",
    "three": "^0.158.0"
  },
  "devDependencies": {
    "@types/react": "^18.2.37",
    "@types/react-dom": "^18.2.15",
    "@vitejs/plugin-react": "^4.2.1",
    "autoprefixer": "^10.4.16",
    "eslint": "^8.53.0",
    "eslint-plugin-react": "^7.33.2",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.4",
    "gh-pages": "^6.1.1",
    "postcss": "^8.4.31",
    "tailwindcss": "^3.3.5",
    "vite": "^5.0.10"
  }
}

I am facing the issue while deployment of following one: Failed to load module script: Expected a JavaScript module script but the server responded with a MIME type of "text/jsx". Strict MIME type checking is enforced for module scripts per HTML spec.


