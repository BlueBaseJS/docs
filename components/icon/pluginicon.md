# PluginIcon 📌

Displays an icon of a Plugin. The icon properties are taken from plugin.icon property of plugin. 

* If no plugin is found, renders an error message. 
* If a plugin has no icon, renders null.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
import { PluginIcon } from '@bluebase/core';

// Then somewhere in your app:
<PluginIcon id="redux-plugin" />
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| id | string | _yes_ | - | Plugin key |
| size | number | - | - | Icon size |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

 

