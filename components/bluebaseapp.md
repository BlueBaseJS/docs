# BlueBaseApp 📌

The main BlueBase app. This is the top level component that takes care of initialisation, and renders either children, or it's own views with routing.

As BlueBaseApp is just a react component, it is possible for 

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

Use BlueBase by passing 

```jsx
import { BlueBase, BlueBaseApp } from '@bluebase/core';

export const App = () => (
    <BlueBaseApp
        components={{ /* Components Collection */ }}
        configs={{ /* Configs Collection */ }}
        hooks={{ /* Hooks Collection */ }}
        plugins={{ /* Plugin Collection */ }}
        themes={{ /* Theme Collection */ }}
    />
);
```

### Custom Context

```jsx
import { BlueBase, BlueBaseApp } from '@bluebase/core';

const BB = new BlueBase();

// Custom business logic on BB object. i.e. Add hooks, etc.

export const App = () => (<BlueBaseApp BB={BB} />);
```

### Children



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

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| BB | BlueBase | _no_ | - | BlueBase context. If one is not provided a new object will be created. |
| children | number | _no_ | - | If this prop is provided, BlueBase's own App view will not be rendered, and nodes in this prop will be rendered instead. |
| components | ComponentCollection | _no_ | - | Collection of components to add in BlueBase's Component Registry. |
| configs | ConfigCollection | _no_ | - | Collection of configs to add in BlueBase's Config Registry. |
| hooks | HookNestedCollection | _no_ | - | Collection of Hook to add in BlueBase's Hook Registry. |
| plugins | PluginCollection | _no_ | - | Collection of plugins to add in BlueBase's Plugin Registry. |
| themes | ThemeCollection | _no_ | - | Collection of themes to add in BlueBase's Theme Registry. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |



