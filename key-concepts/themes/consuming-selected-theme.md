# Consuming Selected Theme

BlueBase exports a `ThemeConsumer` component to utilise current theme. This is a render prop component, which means it takes a function as a child. The function gets an object in the param with the following interface:

```typescript
interface ThemeContextData {

    // Helper method to change current theme.
    changeTheme: (slug: string) => void,

    // Current theme
    theme: Theme
}
```

## Usage

The following snippet illustrates how to use a `ThemeConsumer` component.

```typescript
const ThemedComponent = () => (
    <ThemeConsumer>
    {
        ({ theme, changeTheme }: ThemeContextData) => {
            // Use theme context here..
        }
    }
    </ThemeConsumer>
);
```

## Example: ThemePicker

The following example shows how to use `ThemeConsumer` component to create a theme picker. This renders a picker component with a list of all installed themes. It not only uses the current theme to style itself, but also utilises the `changeTheme` method to switch themes.

```typescript
import { BlueBase, BlueBaseContext, ThemeConsumer, ThemeContextData } from '@bluebase/core';
import { Picker } from 'react-native';
import React from 'react';

export class ThemePicker extends React.PureComponent {

    static contextType = BlueBaseContext;

    render() {
        const BB: BlueBase = (this as any).context;
        const themes = [...BB.Themes.entries()];
        return (
            <ThemeConsumer children={({ theme, changeTheme }: ThemeContextData) => (
                <BB.Components.View style={{ backgroundColor: theme.palette.background.default }}>
                    <BB.Components.Text>Select Theme</BB.Components.Text>
                    <Picker
                        selectedValue={BB.Configs.getValue('theme.name')}
                        style={{ width: 150 }}
                        onValueChange={changeTheme}>
                        {themes.map(entry => <Picker.Item label={entry[1].name} value={entry[0]} key={entry[0]} />)}
                    </Picker>
                </BB.Components.View>
            )} />
        );
    }
}
```

