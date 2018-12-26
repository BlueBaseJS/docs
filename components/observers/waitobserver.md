# WaitObserver 📌

This component is used to do the following:

* WaitObserver a certain period of time before rendering a component
* Show timeout state, if the component is visible for a certain time period

A use case for this can be to show a loading state after waiting a certain period of time for data to load, and if the loading takes too long, show a timeout state.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

### Usage

```jsx
<WaitObserver
 delay={1000}
 timeout={3000}
 onTimeout={onTimeout}
 onRetry={onRetry}
 children={(props: WaitObserverChildrenProps) => <LoadingState {...props} />}
/>
```



## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| delay | _number_ | _no_ | - | Delay before rendering a component. |
| timeout | _number_ | _no_ | - | Timeout duration |
| onTimeout | _Function_ | _no_ | - | A callback function executed when a timeout occurs. |
| onRetry | _Function_ | _no_ | - | A callback function executed when retry method is called from the child component. |
| children | ReactNode \| \(\(\) =&gt; ReactNode\) | _no_ | - |  |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

