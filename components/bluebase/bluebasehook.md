# BlueBaseFilter 📌

As filters in BlueBase are based on promises, it may be tedious to handle loading state, error state, etc. Not to mention that it may also become a repetitive task.

To solve this issue, we ship `BlueBaseFilter` component. Just pass name of filter, initial value, and filter arguments as props. The final filtered value will be passed to the children function. This component will handle loading and error states itself.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
import { BlueBaseFilter } from '@bluebase/core';

// Then somewhere in your app:
<BlueBaseFilter filter="math" value={5} args={{ op: 'add' }}>
{(val: number) => (<Text>{val}</Text>)}
</BlueBaseFilter>
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| filter | string | _yes_ | - | Name of filter event |
| value | any | _yes_ | - | Initial value of filter |
| args | object | _no_ | - | Filter arguments |
| children | \(value\) =&gt; ReactNode | _yes_ | - | Children as function \(render prop pattern\). Final value is passed as param to this function. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |



