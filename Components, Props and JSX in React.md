# Getting Started
## Overview
Vite (French word for "quick", pronounced /vit/, like "veet") is a build tool that aims to provide a faster and leaner development experience for modern web projects. It consists of two major parts:

A dev server that provides rich feature enhancements over native ES modules, for example extremely fast Hot Module Replacement (HMR).

A build command that bundles your code with Rollup, pre-configured to output highly optimized static assets for production.

Vite is opinionated and comes with sensible defaults out of the box. Read about what's possible in the Features Guide. Support for frameworks or integration with other tools is possible through Plugins. The Config Section explains how to adapt Vite to your project if needed.

```terminal
npm create vite@latest
```

Then install
```terminal
npm i
```

Then we would see npm node modules and then we have to run 
```
npm run dev
```
to start the server

Edit `src/App.jsx` and save to test HMR

# Basic app syntax

```javascript


function App() {
  const [count, setCount] = useState(0)

  return (
    <>

    </>
  )
}

export default App
```
