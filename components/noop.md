# Noop 📌

A component that does... nothing!

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
import { Noop } from '@bluebase/core';

// Then somewhere in your app:
<Noop />
```

A more practical usage of this is as a fallback component:

```typescript
const CustomComponent = BB.Components.resolve('Option1', 'Option2', 'Noop');
```

If none of the components key are found in the Component Registry, and error is thrown. To avoid this, just use `Noop` as that last option. So in the example above, if `Option1` and `Option2` are not found, `Noop` renders null instead.

