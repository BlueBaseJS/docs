# Registering a Component

There are many ways to register new components in BlueBase:

### Through a Plugin

The easiest way to add a new component to BlueBase is to use the 'components'  property of your plugin:

```typescript
import { View } from '@bluebase/core';
​
const Logo = props => {
  return (
    <View>/* component code */</View>
  )
}
​
const Plugin = {
​
    name: 'Example Plugin',
    key: 'example-plugin',
​
    components: {
      Logo
    }
}
```

Note that this may replace any existing components registered with same name.

### Through Registry API

You can add new Components anywhere in the code by calling the set method of ComponentRegistry:

```typescript
const Logo = props => {
  return (
    <View>/* component code */</View>
  )
}
​
await BB.Components.register('Logo', Logo);
```

