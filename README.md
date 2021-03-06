# docz-plugin-stencil
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
Docz plugin to integrate easily with [stenciljs](https://stenciljs.com)

[Example](https://github.com/danielnetzer/docz-plugin-stencil/tree/master/example)

## Installation

 1. install the plugin and dev dependencies:

```bash
$ yarn add docz-plugin-stencil wait-on concurrently --dev
```

2. add the plugin on your `doczrc.js`:

```js
// doczrc.js
import { stencil } from 'docz-plugin-stencil'

export default {
  plugins: [
    stencil()
  ]
}
```

3. modify `package.json` scripts to run docz in parallel with stencil

```json
"scripts": {
    "docz:dev": "wait-on http://localhost:3333/ && docz dev",
    "docz:build": "docz build",
    "stencil:dev": "stencil build --watch --serve --docs",
    "stencil:build": "stencil build --docs",
    "build": "npm run stencil:build && npm run docz:build",
    "start": "concurrently \"npm run stencil:dev\" \"npm run docz:dev\"",
    ...
  }
```

5. update `stencil.config.ts` file
* if you want to use `docz` as the development platform you can remove the red diff
```diff
 outputTargets: [
    { type: "dist", esmLoaderPath: "../docs/loader" },
    ...
-   {
-     type: 'www',
-     serviceWorker: null, // disable service workers
-   },
    ]
```

## Api
### Playground files

each component that will have a `playground.md` file in his root directory, the plugin will auto generate a `docz` playground section accordingly.

### Params
-- no params are allowed at the moment besides `outputPath` but it's preffered not to change it, if you do want to change that outputPath from `docs` then don't forget to update your `stencil.config.js` in the `esmLoaderPath: "../<outputPath>/loader"`.

## Contribution
All contribs are welcome, whether its unit tests for the plugin, further enhancements on the file system operations, better API control, enhancements to the props generated by the plugin so it'll support inner routes and auto generate playground's based on component's props.

### License : MIT