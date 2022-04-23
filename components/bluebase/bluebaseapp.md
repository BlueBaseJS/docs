# BlueBaseApp 📌

This is the main app in the BlueBase framework. It is just a React Component, and can either be used as the top most component of your project or it can be embedded in your existing code base.

This component takes care of initialisation and renders the [⛩Main App Layout](../../overview/main-app-layout.md). If children prop is provided, then it renders the children prop instead of the Main App Layout.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

Use it just like any other react component.

```jsx
import { BlueBase, BlueBaseApp } from '@bluebase/core';

export const App = () => (
    <BlueBaseApp
        components={{ /* Components Collection */ }}
        configs={{ /* Configs Collection */ }}
        filters={{ /* Filters Collection */ }}
        plugins={{ /* Plugin Collection */ }}
        themes={{ /* Theme Collection */ }}
    />
);
```

### Custom Context

Sometimes, you may want to use custom context. This is especially important when some system functionality may need to be modified before the boot process.

Just create a new object of BlueBase class. And send pass it to the BlueBaseApp component as `BB` prop when ready.

```jsx
import { BlueBase, BlueBaseApp } from '@bluebase/core';

const BB = new BlueBase();

// Custom business logic on BB object. i.e. Add filters, etc.

export const App = () => (<BlueBaseApp BB={BB} />);
```

### Children

If children are provided to this component, then the children node is rendered instead of [⛩Main App Layout](../../overview/main-app-layout.md). The child components can use [BlueBaseConsumer](bluebaseconsumer.md) to access BlueBase context.

```jsx
import { BlueBase, BlueBaseApp } from '@bluebase/core';

export const App = () => (
    <BlueBaseApp>
        {/* This child component will have access to BlueBase context */}
        <CustomComponent />
    </BlueBaseApp>
);
```

## Properties

| prop       | type                   | required | default | description                                                                                                              |
| ---------- | ---------------------- | -------- | ------- | ------------------------------------------------------------------------------------------------------------------------ |
| BB         | BlueBase               | _no_     | -       | BlueBase context. If one is not provided a new object will be created.                                                   |
| children   | number                 | _no_     | -       | If this prop is provided, BlueBase's own App view will not be rendered, and nodes in this prop will be rendered instead. |
| components | ComponentCollection    | _no_     | -       | Collection of components to add in BlueBase's Component Registry.                                                        |
| configs    | ConfigCollection       | _no_     | -       | Collection of configs to add in BlueBase's Config Registry.                                                              |
| filters    | FilterNestedCollection | _no_     | -       | Collection of Filter to add in BlueBase's Filter Registry.                                                               |
| plugins    | PluginCollection       | _no_     | -       | Collection of plugins to add in BlueBase's Plugin Registry.                                                              |
| themes     | ThemeCollection        | _no_     | -       | Collection of themes to add in BlueBase's Theme Registry.                                                                |
| testID     | string                 | _no_     | -       | Used to locate this view in end-to-end tests.                                                                            |
