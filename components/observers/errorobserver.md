# ErrorObserver 📌

Observes any exceptions in child tree hierarchy. When an exception is caught, displays an Error state to gracefully handle it on the frontend.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
<ErrorObserver>
 <Text>Rendered if there is no error here</Text>
</ErrorObserver>
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| error | Error | _no_ | - | If an error is passed as a prop, shows an error state. |
| checkError | \(props\) =&gt; Error | _no_ | - | A function to check error based on props. |
| errorComponent | Component | _no_ | - | Component to show the error state. |
| children | ReactNode \| \(\(\) =&gt; ReactNode\) | _no_ | - | Children are rendered when there are no error. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

