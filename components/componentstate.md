# ComponentState 📌

A generic component to show different states of a screen or a view. For example, you may need to:

* Show a loading state when data is loading,
* Show an empty state when there is not data to show on a screen.
* Show an error message when an exception occurs during execution.

These are just a few examples. This component displays a message with an image, a title, a description and a call to action button.

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
import { ComponentState } from '@bluebase/core';

// Then somewhere in your app:
<ComponentState
    title="Looks like your'e new here!"
    description="Start by creating your first entry."
    imageSource="https://picsum.photos/200"
    styles={{ image: { width: 100, height: 100 } }}
    actionTitle="Tap to Create"
/>
```

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| actionTitle | string | _no_ | - | Action title |
| actionOnPress | function | _no_ | - | Action onPress callback function |
| description | string | _no_ | - | Description Text |
| image | ReactNode | _no_ | - | A ReactNode to show custom UI, if provided, imageSource will be ignored |
| imageSource | string | _no_ | - | Image URL |
| title | string | _no_ | - | Title text |
| styles | ComponentStateStyles | _no_ | - | Style rules |
| testID | string | _no_ | - | Used to locate this view in end-to-end tests. |

## Styles

It is possible to customise styles of different elements of this component. To learn about how the `styles` prop work in BlueBase, see the [theming](../key-concepts/themes/customise-components.md) section. 

| rule | type | description |
| :--- | :--- | :--- |
| actionRoot | ViewStyle | Action button container styles |
| description | TextStyle | Description text styles |
| image | ImageStyle | Image styles |
| imageRoot | ViewStyle | Styles of image container view |
| root | ViewStyle | Main root container styles |
| title | TextStyle | Title styles |



