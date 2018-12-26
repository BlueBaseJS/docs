# LoadingState 📌

A component that is used to show a loading state. Shows a spinner by default. If 'timedOut' flag is set then it shows a timeout version.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
import { LoadingState } from '@bluebase/core';

// Then somewhere in your app:
<LoadingState timedOut={false} retry={retryFunction}/>
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| timedOut | boolean | _no_ | - | Flag if loading has timedOut. |
| retry | Function | _no_ | - | Callback function when Retry button is pressed. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

