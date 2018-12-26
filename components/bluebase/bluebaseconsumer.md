# BlueBaseConsumer 📌

Since BlueBase is build using React's context functionality, it is possible to access the BlueBase context \(often referred to as `BB`\) using the same API used by any other context consumer. This is done by using the `BlueBaseConsumer` component.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

Use it just like any other react component.

```jsx
import { BlueBase, BlueBaseConsumer } from '@bluebase/core';

export const CustomComponent = () => (
    <BlueBaseConsumer>
    {(BB: BlueBase) => {
        // Use Context here
    }}
    </BlueBaseConsumer>
);
```



