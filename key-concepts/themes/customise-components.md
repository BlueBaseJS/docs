# Customise Components

Theming in BlueBase provides an elaborate mechanism to customise component styles. Following is a list of options to do this in a sequence of lowest to highest priority.

{% hint style="info" %}
Component styles in all of the following methods can be thunks as well.
{% endhint %}

### 1. Through `defaultStlyes` static prop

In BlueBase it is possible to provide a `defaultStyles` static property to a component. This is very similar to the `defaultProps` concept of React.

```typescript
import React from 'react';
import { Card } from '@bluebase/components';

export class ThemedCard extends React.Component {

    static defaultStyles = {
        'root': {
            backgroundColor: 'blue'
        },
        'hover': {
            backgroundColor: 'green'
        }
    }
    
    render() {
        const { styles, isHovering } = this.props;
        
        return (<Card style={isHovering ? styles.hover : styles.root} />);
    }
}
```

#### Priority

In terms of priority, this method has the least priority, and these styles may be overwritten by any of the following methods.

#### Use When

Use this method to define the default styles of the components. These will represent a state of the component without any customisation.

### Through Component Registry

```typescript
BB.Components.setStyles('ThemedCard', {
    root: {
        backgroundColor: 'orange'
    }
});
```

### Through theme

```typescript
export const theme = {
    // ...other theme props
    components: {
        ThemedCard: {
            root: {
                backgroundColor: 'yellow'
            }
        }
    }
};
```

### Through `styles` prop

```typescript
const Foo = () => (
    <ThemedCard styles={{
        root: {
            backgroundColor: 'red'
        }
    }} />
);
```

## Component Styles Structure

In BlueBase, ComponentStyles have the following structure:

```typescript
interface ComponentStyles {
	// rule
	[key: string]: ViewStyle | TextStyle | ImageStyle | { [prop: string]: string };
}
```

This is very similar to React Native's [StyleSheet.create](https://facebook.github.io/react-native/docs/stylesheet) API.

#### Example

```typescript
const styles = {
  root: {
    borderRadius: 4,
    borderWidth: 0.5,
    borderColor: '#d6d7da',
  },
  title: {
    fontSize: 19,
    fontWeight: 'bold',
  },
  activeTitle: {
    color: 'red',
  },
};
```

Thunks

Describe best practices: root, hover, etc.

