# instructions/install-nativewind.md

Use the following instructions to install nativewind in the project.

1. Install the dependencies:

```bash
npm install nativewind tailwindcss react-native-reanimated@3.16.2 react-native-safe-area-context @tailwind/postcss postcss
```

2. Run `npx tailwindcss init` to create a `tailwind.config.js` file.

3. Add the following to the `tailwind.config.js` file:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  // NOTE: Update this to include the paths to all of your component files.
  content: ["./app/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

4. Create a `global.css` file and add the Tailwind directives:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

5. Import the `global.css` file in the `app/_layout.tsx` file:

```tsx
import "./global.css";
```

6. Add the Babel preset to the `babel.config.js` file:

```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: [
      ["babel-preset-expo", { jsxImportSource: "nativewind" }],
      "nativewind/babel",
    ],
  };
};
```

7. Modify your metro.config.js:

```js
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require("nativewind/metro");

const config = getDefaultConfig(__dirname);

module.exports = withNativeWind(config, { input: "./global.css" });
```

8. Modify your app.json to use the metro bundler:

```json
{
  "expo": {
    "web": {
      "bundler": "metro"
    }
  }
}
```

9. NativeWind extends the React Native types via declaration merging. Create a new nativewind-env.d.ts file and add a triple-slash directive referencing the types.

```ts
/// <reference types="nativewind/types" />
```

10. Add the following to the `postcss.config.js` file:

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```
