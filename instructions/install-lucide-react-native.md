# /instructions/install-lucide-react-native.md

Install lucide-react-native and a code generator that will wrap icons in the `iconWithClassName` function so they can be styled with the `className` prop.

1. Install the dependencies:

```bash
npx expo install react-native-svg lucide-react-native
```

2. Add the iconWithClassName function in the ~/lib/icons/iconWithClassName.ts file:

```ts
import type { LucideIcon } from "lucide-react-native";
import { cssInterop } from "nativewind";

export function iconWithClassName(icon: LucideIcon) {
  cssInterop(icon, {
    className: {
      target: "style",
      nativeStyleToProp: {
        color: true,
        opacity: true,
      },
    },
  });
}
```

3. Install the `plop` code generator:

```bash
npm install plop
```

4. Configure `plop` by adding the following to `/plopfile.mjs`:

```js
export default function (
  /** @type {import('plop').NodePlopAPI} */
  plop
) {
  plop.setGenerator("icon", {
    description: "Create a new icon in ./lib/icons",
    prompts: [
      {
        type: "input",
        name: "name",
        message: 'Name of a Lucide icon in UppercaseCamelCase, e.g. "Copy":',
      },
    ],
    actions: [
      {
        type: "add",
        path: "lib/icons/{{name}}.tsx",
        templateFile: "plop-templates/icon.tsx.hbs",
      },
    ],
  });
}
```

5. Exclude the `.plopfile.mjs` file from eslint by adding it to the `.eslintignore` file:

```js
plop - templates;
```

6. Create the icon plop template in `/plop-templates/icon.tsx.hbs`:

```hbs
import {
{{name}}
} from "lucide-react-native"; import { iconWithClassName } from
"./iconWithClassName"; iconWithClassName({{name}}); export {
{{name}}
};
```

7. Add the plop command to the `package.json` file:

```json
"scripts": {
  "generate": "plop"
}
```

9. Add code comments explaining each addition and why the change was made.

10. Run the plop command to create the `House` icon:

```bash
npm run generate -- --name=House
```
