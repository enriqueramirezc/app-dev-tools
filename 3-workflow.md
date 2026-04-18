# Workflow

## Running your app on Android devices

- 1) Enable Debugging over USB.
- 2) Plug in your device via USB (see documentation for more detailed instructions).
- 3) From the root of your project, type the following in your command prompt to install and launch your app on the device: `npm run android`.

## Metro

React Native uses Metro to build your JavaScript code and assets.

Configuration options for Metro can be customized in your project's metro.config.js file.

## Using Libraries

React Native libraries are typically installed from the npm registry using a Node.js package manager such as npm CLI or Yarn Classic.

f you have Node.js installed on your computer then you already have the npm CLI installed.

### Installing a Library

To install a library in your project, navigate to your project directory in your terminal and run the installation command. Let's try this with react-native-webview: `npm install react-native-webview`

### Using Typescript

TypeScript is a language which extends JavaScript by adding type definitions. New React Native projects target TypeScript by default, but also support JavaScript and Flow.

New projects created by the React Native CLI or popular templates like Ignite will use TypeScript by default.

TypeScript may also be used with Expo, which maintains TypeScript templates, or will prompt you to automatically install and configure TypeScript when a .ts or .tsx file is added to your project.

