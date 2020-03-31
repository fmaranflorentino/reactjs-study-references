## Root import

Improve your path resolvers with root import

- `yarn add customize-cra react-app-rewired -D`

Now install the desired babel plugin

- `yarn add babel-plugin-root-import -D`

In your root folder you must create a `config-overrides.js`file with the following content

```js
const { addBabelPlugin, override } = require("customize-cra");

module.exports = override(
  addBabelPlugin([
    "babel-plugin-root-import",
    {
      rootPathSuffix: "src"
    }
  ])
);
```

You need to add config to eslint to recognize the root-imports

- `yarn add eslint-import-resolver-babel-plugin-root-import -D`

```js
settings: {
  'import/resolver': {
    'babel-plugin-root-import': {
      rootPathSuffix: 'src',
    },
  },
},
```

Create a file on the root folder `jsconfig.json` - this file intend to configure vscode file trace

```json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "~/*": ["*"],
    }
  }
}
```

You need to change the react-scripts in `package.json`for the following content

```json
"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test",
  "eject": "react-scripts eject"
},
```

Now restart your development server and it's done.