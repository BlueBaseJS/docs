# Customise Themes

BlueBase supports different types of theme customisation requirements so that a developer can do a single usage customisation or globally override a theme.

## Override all themes

There may be use cases where you may need to keep specific values same, n matter which theme is selected, i.e. primary colours, etc.

To do this, use the `theme.overrides` config. This change is global, and overrides all installed themes.

{% code-tabs %}
{% code-tabs-item title="bluebase.ts" %}
```typescript
const bootOptions = {

    configs: {
        'theme.overrides': {
            components: {
                // component styles
            }
        }
    },
};

export default bootOptions;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Specific variation, global usage

Extend a theme

```typescript
import { createTheme } from '@bluebase/core';

// ... TODO: current api may change
```

## Specific variation, one time usage

Using the `ThemeProvider` overrides prop. This change is only for this tree.

* Nesting themes
* Overriding themes

### Nesting Themes

It is possible to nest multiple themes in a single project. To theme a specific portion of your app, use the `ThemeProvider` component.

```jsx
<View>
    <Text>Default light theme here</Text>
    <ThemeProvider theme="bluebase-dark">
        <View style={{ backgroundColor: theme.palette.background.default }}>
            <Text>Dark theme here</Text>
        </View>
    </ThemeProvider>
<View>
```

In the example above, we pass the `theme` prop to the `ThemeProvider` component. This prop takes the key of the theme to use for children components. If this prop is not set, the globally selected theme is used.

### Overriding Themes

The `ThemeProvider` component can also be used to override a theme for a one time usage.

```jsx
<ThemeProvider theme="bluebase-dark" overrides={{ palette: { background: { default: 'red' } } }} >
    {/* All components here will now have a red background color */}
</ThemeProvider>
```

