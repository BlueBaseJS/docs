# DataObserver 📌

Observes data to check if it is data is loading, loaded or empty. The resulting flags are passed on to the children function. These flags may be used to show different UIs, i.e. loading state, empty state, etc.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
<DataObserver data={dataObj} >
{
    ({data, loading, empty}) => {
        // Render UI based on params
    }
}
</DataObserver>
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| isLoading | \(props\) =&gt; boolean | _no_ | - | A function used to check if data is loading. |
| isEmpty | \(props\) =&gt; boolean | _no_ | - | A function used to check if data is empty. |
| loading | boolean | _no_ | - | Loading flag. |
| data | any | _no_ | - | Input data. |
| children | ReactNode \| Function | _no_ | - | Children, data is passed in the param object of the render prop function. This object is typed as `DataObserverChildrenProps`. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

