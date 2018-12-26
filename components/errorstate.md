# ErrorState 📌

Display an error message. Used by UIs when an exception is caught, and an error message needs to be displayed. If in development mode, the actual error is displayed, otherwise displays a generic message in production mode.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
<ErrorState retry={retryCallback} error={Error('Bang!')} />
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| error | Error | _no_ | - | The error to display |
| retry | Function | _no_ | - | Callback function, called when retry button is pressed. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

