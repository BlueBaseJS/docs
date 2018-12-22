# Register a Plugin

There are many ways to register new plugins in BlueBase:

### Through BlueBaseApp Component

The easiest way to add a new plugin is pass it as a prop to `BlueBaseApp`.

{% code-tabs %}
{% code-tabs-item title="app.ts" %}
```typescript
import { BlueBaseApp } from '@bluebase/core';
​
const ExamplePlugin = {
​
    name: 'Example Plugin',
    key: 'example-plugin',
​
    // ... other plugin properties
}

export const App = () => (
  <BlueBaseApp plugins={[ExamplePlugin]} />
);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Typically, in a large project you would be using the `bluebase.ts` file to inject props to your main `BlueBaseApp` component. It is basically same thing as above.

{% code-tabs %}
{% code-tabs-item title="bluebase.ts" %}
```typescript
export default {

    // ...other bluebase.ts properties

    plugins: [{
​
        name: 'Example Plugin',
        key: 'example-plugin',
    ​
        // ... other plugin properties
    }]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Through Registry API

You can add new Plugins anywhere in the code by calling the set method of PluginRegistry:

```typescript
const ExamplePlugin = {
​
    name: 'Example Plugin',
    key: 'example-plugin',
​
    // ... other plugin properties
}
​
await BB.Plugins.register(ExamplePlugin);
await BB.Hooks.run('bluebase.plugins.initialize', ExamplePlugin);
```

Beware though, it is important when a plugin is added to the registry in the system lifecycle. Because all plugins must be initiated, adding them to the registry is not enough. 

Plugins are initialised with the `bluebase.plugins.initialize.all` hook, which in turn calls the `bluebase.plugins.initialize` hook for each plugin. So you'll either need to run this hook yourself, or add a plugin before the main hook is executed by the system.

Even so, to avoid unknown issues it is recommended to use the first method \([Through BlueBaseApp Component](register-a-plugin.md#through-bluebaseapp-component)\).

