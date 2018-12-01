# Developing a Theme Plugin

A plugin can register any number of themes. To do this simple set the `themes` property of your plugin class.

```typescript
class MaterialUIPlugin extends Plugin {

    public themes = [{
        name: 'Material UI (Light)',
        slug: 'material-ui-light',
        mode: 'light',
        
        // .. other theme props
    }, {
        name: 'Material UI (Dark)',
        slug: 'material-ui-dark',
        mode: 'dark',
        
        // .. other theme props
    }]
}
```

{% hint style="warning" %}
The following guide needs to be added to [Themes](../themes/) section.
{% endhint %}

Each object in the theme property can be a [BlueBase Module](../bluerain-modules.md). This mean each theme's code can be split into different bundles on web.

```typescript
class MaterialUIPlugin extends Plugin {

    public themes = [
		import('path/to/theme-1'),
		import('path/to/theme-2'),
	]
}
```

Be aware though, that if you use this approach, these bundles will be downloaded during boot time. This is because BlueBase needs know each theme's `name` and `slug` to store them in registry.

If you want to split the theme so that they are downloaded only when selected, spilt the internal `theme` property.

```typescript
class MaterialUIPlugin extends Plugin {

    public themes = [{
        name: 'Material UI (Light)',
        slug: 'material-ui-light',
        mode: 'light',
        
        theme: import('./theme-rules-light'),

        // .. other theme props
    }, {
        name: 'Material UI (Dark)',
        slug: 'material-ui-dark',
        mode: 'dark',
        
        theme: import('./theme-rules-dark'),
        
        // .. other theme props
    }]
}
```

