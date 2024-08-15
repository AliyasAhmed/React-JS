# Install Tailwind CSS
Install `tailwindcss` and its peer dependencies, then generate your `tailwind.config.js` and `postcss.config.js` files.

  ```terminal
  npm install -D tailwindcss postcss autoprefixer
  npx tailwindcss init -p
  ```

# Configure your template paths
Add the paths to all of your template files in your `tailwind.config.js` file.

  ```tailwind.config.js
  /** @type {import('tailwindcss').Config} */
  export default {
    content: [
      "./index.html",
      "./src/**/*.{js,ts,jsx,tsx}",
    ],
    theme: {
      extend: {},
    },
    plugins: [],
  }
  ```
# Add the Tailwind directives to your CSS
Add the `@tailwind` directives for each of Tailwind’s layers to your `./src/index.css` file.
  ```index.css
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  ```

# Start your build process
  Run your build process with npm run dev.
  ```terminal
  npm run dev
  ```

# Start using Tailwind in your project
Start using Tailwind’s utility classes to style your content.

```app.jsx
export default function App() {
  return (
    <h1 className="text-3xl font-bold underline">
      Hello world!
    </h1>
  )
}
```
