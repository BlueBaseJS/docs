# BlueBaseHook 📌

Since hooks in BlueBase are based on promises, it may be tedious to handle loading state, error state, etc. It may also become a repetitive task.

To solve this issue, we ship BlueBaseHook component. Just pass name of hook, initial value, and hook arguments as props. The final hooked value will be passed to the children function. This component will handle loading and error states itself.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
<BlueBaseHook hook="math" value={5} args={{ op: 'add' }}>
{(val: number) => (<Text>{val}</Text>)}
</BlueBaseHook>
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| hook | string | _yes_ | - | Name of hook event |
| value | any | _yes_ | - | Initial value of hook |
| args | object | _no_ | - | Hook arguments |
| children | \(value\) =&gt; ReactNode | _yes_ | - | Children as function \(render prop pattern\). Final value is passed as param to this function. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |



