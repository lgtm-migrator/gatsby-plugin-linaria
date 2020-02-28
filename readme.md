# Linaria plugin for Gatsby

This plugin modifies Gatsby's webpack configuration to support [Linaria][].

Install the plugin and Linaria:

```sh
yarn add gatsby-plugin-linaria linaria
```

Add it to your plugins in `gatsby-config.js`:

```js
plugins: [
  'gatsby-plugin-linaria',
]
```

Finally, make sure to add `.linaria-cache` to your `.gitignore` file.

That's it! gatsby-plugin-linaria configures Linaria's webpack plugin to use
[babel-preset-gatsby][], which contains Gatsby's Babel configuration.

## TypeScript

If you're using gatsby-plugin-typescript, make sure to include it **before**
gatsby-plugin-linaria:

```js
plugins: [
  'gatsby-plugin-typescript',
  'gatsby-plugin-linaria',
]
```

Happy styling! :art:y'

[Linaria]: https://github.com/callstack/linaria
[babel-preset-gatsby]: https://github.com/gatsbyjs/gatsby/tree/master/packages/babel-preset-gatsby

## FAQ

### `Error: Cannot find module 'core-js/modules/<polyfill>'` (#50)

This error is caused by:

  1. a discrepancy between Linaria's and Gatsby's version of core-js
  2. stable versions of Linaria being built with an incorrect Babel configuration

A workaround is to update Linaria to at least `1.4.0-beta.3` and install the latest version of core-js (v3):

```sh
yarn add linaria@^1.4.0-beta.3
yarn add core-js
```

### `warning  'css' is defined but never used  no-unused-vars`

At the time of this writing, Gatsby comes with [eslint-loader](https://github.com/webpack-contrib/eslint-loader) built-in, which seems to be unable to detect the modified Babel configuration. So far the fastest way to fix this is to add both ESLint and Babel configuration file to your project. Configure ESLint to extend [eslint-config-react-app](https://github.com/facebook/create-react-app/tree/master/packages/eslint-config-react-app) (this is the one that Gatsby uses) and configure Babel according to Gatsby's instructions [how to add a custom Babel configuration](https://www.gatsbyjs.org/docs/babel/), and add [linaria/babel](https://github.com/callstack/linaria/blob/master/docs/CONFIGURATION.md#linariababel-preset) as well.

[Read #15](https://github.com/silvenon/gatsby-plugin-linaria/issues/15) for more context.
