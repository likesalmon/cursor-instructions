# /instructions/install-prettier.md

This guide explains how to install and configure Prettier for consistent code formatting.

## Installation

Install Prettier and the recommended plugins:

```bash
npm install --save-dev prettier @trivago/prettier-plugin-sort-imports@^4.3.0 prettier-plugin-tailwindcss@^0.6.6
```

## Configuration

Create a `.prettierrc` file in your project root:

```json
{
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": false,
  "trailingComma": "es5",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "arrowParens": "avoid",
  "plugins": [
    "prettier-plugin-tailwindcss",
    "@trivago/prettier-plugin-sort-imports"
  ],
  "tailwindConfig": "./tailwind.config.js",
  "importOrder": ["^react$", "^@?\\w", "^[./]"],
  "importOrderSeparation": true,
  "importOrderSortSpecifiers": true
}
```

## Create .prettierignore

Create a `.prettierignore` file to exclude certain files from formatting:

```text
node_modules
.expo
dist
build
coverage
```
