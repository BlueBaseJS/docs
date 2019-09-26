# Plugin API

A plugin is just a JavaScript object that has the following properties:

| Key | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| `name` | _string_ | _yes_ | Name of the plugin. |
| `key` | _string_ | _no_ | This property is used as an ID throughout the system. |
| `description` | _string_ | _no_ | Plugin description. |
| `version` | _string_ | _no_ | Plugin version. |
| `categories` | _string\[\]_ | _no_ | [Plugin Categories](https://github.com/BlueBaseJS/docs/tree/6710d83d9e42436a90100426d36314c69fa496f6/key-concepts/plugins/plugins.md#plugin-categories). |
| `icon` | _DynamicIconProps_ | _no_ | These are props of the DynamicIcon component. This value can also be a thunk, i.e. a function that should return the props object. This function receives BlueBase context as param. |
| `enabled` | _boolean_ | _no_ | _\(Default = true\)_ Flag to check if a plugin is enabled. |
| `filters` | _FilterNestedCollection_ | _no_ |  |
| `components` | _ComponentCollection_ | _no_ |  |
| `themes` | _ThemeCollection_ | _no_ |  |
| `defaultConfigs` | _ConfigCollection_ | _no_ |  |

## Plugin Categories

Categories are used in plugin listing pages. Currently, we recognise the following kind of plugins, but a developer may define his own category as well.

| Key | Description |
| :--- | :--- |
| app | A plugin that is a sub-app in the system. This applies that when BlueBase is used as a bigger platform, and different features are represented as individuals apps inside the platform. |
| store | A plugin that provides a state store functionality. i.e. Redux. |
| router | A plugin that provides routing mechanism. i.e. react-router or React Navigation. |
| logging | A plugin that provides integration with a logging service. i.e. Sentry. |
| theme | A plugin that provides a single or multiple themes. |
| analytics | A plugin that provides integration with a logging service. i.e. Google Analytics. |

## Example

```typescript
import { createPlugin } from '@bluebase/core';

export const ExamplePlugin = createPlugin({

    key: 'example',
    name: 'Example Plugin',
    description: 'This is just an example plugin.',
    version: '1.0.0',
    categories: ['theme', 'app'],

    icon: () => ({
        type: 'icon',
        name: 'rocket',
    }),

    defaultConfigs: {
        'plugin.example.foo': 'bar'
    },

    // ... any components come here
    components: [{
        key: 'Logo',
        value: import('./Logo')
    }],

    // ... add other configs, i.e. themes, filters, etc
});
```

