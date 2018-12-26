# StatefulComponent 📌

This is a swiss army knife component. Intended to be used as a single source of UI state management. It shows empty, loading, error or data states based on the given props.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

### Usage

```jsx
<StatefulComponent data={data} loading={true} delay={200} timeout={10000}>
 <Text>Content</Text>
</StatefulComponent>
```



## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |



