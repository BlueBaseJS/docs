# JsonSchema 📌

Renders a Component based on JSON schema. This allows developers to create dynamic layouts in their apps, and even save the schema to databases.

Moreover, it also makes that schema hook-able. So that any plugin can modify that schema on runtime.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
import { JsonSchema } from '@bluebase/core';

// Then somewhere in your app:
<JsonSchema
    hook="content-hook"
    args={{ style: { color: 'blue' } }}
    schema={{
     component: 'Text',
     props: {
         style: {
             color: 'red'
         }
     },
     text: 'This is the page content.',
 }} />
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| schema | JsonComponentNode  \| JsonComponentNode\[\] | _yes_ | - | JSON Schema |
| hook | string | _no_ | - | Event name to hook this schema. If this is not provided, the schema is not hooked. |
| args | object | _no_ | - | Arguments for the hook. |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

