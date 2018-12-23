# 📦 BlueBase Modules

One of the main purpose of BlueBase is to have all functionality broken up into separate modules. So that adding or removing any feature may become as simple as press of a button.

Moving forward, from our experience with previous versions, it also became evident that code splitting was a necessity in web environments. And with the latest version, we wanted to support it out of the box.

So, BlueBase has been rewritten from the ground up to replace fixed pieces of code \(i.e. functions or React components\) to BlueBase Modules.

A BlueBase module is any piece of code that:

* Maybe a CommonJS module or an ES Module.
* Maybe the module itself, or a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that resolves a module.

## Module Types

A challenge we faced in the earlier versions was the different module types in the Javascript ecosystem. We decided back then that BlueBase must support these out of the box.

BlueBase supports both Common JS and ES modules. We do this by checking `.default` property on the imported modules.

If the `.default` property does exist, we do `module = module.default`.

## Dynamic Imports

Code splitting is achieved through [dynamic imports](https://github.com/tc39/proposal-dynamic-import). All major bundlers \(e.g. [Webpack](https://webpack.js.org/guides/code-splitting/), [Parcel](https://parceljs.org/code_splitting.html)\) already support it. An `import` function in dynamic import specification returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

So we check if a module is a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), we resolve it automatically, when the module is resolved internally.

## Usage Matrix

The table below list where BlueBase Modules are used internally, and their behaviour.

| Type | Maybe ES Module | Maybe Promise | Must be resolved at boot? |
| :--- | :--- | :--- | :--- |
| Plugin | Yes | Yes | Yes |
| Hook | Yes | Yes | Yes |
| Routes | Yes | Yes | Yes |
| Components | Yes | Yes | No |
| Assets | No | Yes | No |
| Theme | Yes | Yes | No |
| Intl | Yes | Yes | No |

Hooks may have individual listeners as promises too.

