# babel-plugin-vue-jsx-hmr [![npm](https://img.shields.io/npm/v/babel-plugin-vue-jsx-hmr)]((https://www.npmjs.com/package/babel-plugin-vue-jsx-hmr))
Babel Plugin for Vue3 JSX & TSX HMR 

## Usage

### Webpack 
```bash
npm i -D babel-loader @vue/babel-plugin-jsx babel-plugin-vue-jsx-hmr
```

```js
// webpack.config.js
{
    test: /\.(?:jsx|tsx)(\.js)?$/,
    exclude: /node_modules/,
    use: {
        loader: 'babel-loader',
        options: {
            plugins: ['@vue/babel-plugin-jsx', 'babel-plugin-vue-jsx-hmr']
        }
    }
}
```
In your webpack config, be sure to have the following options:
```js
devServer: {
    liveReload: false,
    hot: true,
}
```


### Rspack
```bash
npm i -D babel-loader @vue/babel-plugin-jsx babel-plugin-vue-jsx-hmr
```

```js
// rspack.config.js
{
    test: /\.(?:jsx|tsx)(\.js)?$/,
    exclude: /node_modules/,
    use: {
        loader: 'babel-loader',
        options: {
            plugins: ['@vue/babel-plugin-jsx', 'babel-plugin-vue-jsx-hmr']
        }
    }
},
```

### Vite
[@vitejs/plugin-vue-jsx](https://npmjs.com/package/@vitejs/plugin-vue-jsx)

## HMR Detection
The same principle as [@vitejs/plugin-vue-jsx](https://npmjs.com/package/@vitejs/plugin-vue-jsx), so to speak, and its version of the babel plugin, whose [README](https://github.com/vitejs/vite-plugin-vue/blob/fff40f67f05763d24e8c752fa98bcd08e19f7c82/packages/plugin-vue-jsx/README.md?plain=1#L38) is referenced here.

This plugin supports HMR of Vue JSX components. The detection requirements are:

- The component must be exported.
- The component must be declared by calling `defineComponent` via a root-level statement, either variable declaration or export declaration.

### Supported patterns

```jsx
import { defineComponent } from 'vue'

// named exports w/ variable declaration: ok
export const Foo = defineComponent({})

// named exports referencing variable declaration: ok
const Bar = defineComponent({ render() { return <div>Test</div> }})
export { Bar }

// default export call: ok
export default defineComponent({ render() { return <div>Test</div> }})

// default export referencing variable declaration: ok
const Baz = defineComponent({ render() { return <div>Test</div> }})
export default Baz
```

### Non-supported patterns

```jsx
// not using `defineComponent` call
export const Bar = { ... }

// not exported
const Foo = defineComponent(...)
```
