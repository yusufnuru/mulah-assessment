# mulah-assessment

This project demonstrates handling CSV data in a Vue 3 + TypeScript + Vite setup. The application parses a CSV file, displays its contents in Table One, and computes derived data shown in Table Two.

## Features

- 📄 **CSV Parsing** with [PapaParse](https://www.papaparse.com/)
- 🔗 **Parent-Child Communication** via props and custom events
- ⚡️ **Reactive Computation** in Table Two based on Table One data
- 💡 Built with Vue 3 Composition API & TypeScript

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Structure

src/
├── components/
│   ├── TableOne.vue    # Loads and parses CSV, emits loaded data
│   └── TableTwo.vue    # Computes derived values based on TableOne data
├── types.ts            # Shared TypeScript types
├── App.vue             # Parent component coordinating TableOne and TableTwo
└── main.ts             # Application entry point

## CSV File

public/
└── data/
    └── Table_Input.csv    # Sample CSV file to be loaded by TableOne


## Project Setup

```sh
pnpm install
```

### Compile and Hot-Reload for Development

```sh
pnpm dev
```

### Type-Check, Compile and Minify for Production

```sh
pnpm build
```

### Lint with [ESLint](https://eslint.org/)

```sh
pnpm lint
```
