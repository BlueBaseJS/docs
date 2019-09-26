# Making a Plugin Configurable

Some times developers may need to make their plugins configurable, this may even be necessary in some cases. For example, a Google Analytics plugin may need to have a configuration for tracking code, as this value is different for every project.

In BlueBase it is very each to achieve this using the [Configs](../configs.md) API. Just set or get a config value anywhere in the plugin's business logic.

There are times, when you may need to define default values for plugin configurations as well. To do this, create a `defaultConfigs` property in your plugin as shown below:

```typescript
import { createPlugin } from '@bluebase/core';

export const ExamplePlugin = createPlugin({

    key: 'example',
    name: 'Example Plugin',

    defaultConfigs: {
        'plugin.example.foo': 'bar'
    },

    // ... add other configs, i.e. themes, filters, etc
});
```

BlueBase will automatically set this value in the Config registry, if a custom value isn't provided.

## Plugin Configs Nomenclature

In BlueBase, we use the following naming convention for configs belonging to plugins:

```text
plugin.{key}.{config}
```

So, as shown in the example plugin above, a config `foo` for a plugin with key `example` becomes:

```text
pluign.example.foo
```

