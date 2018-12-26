# HoverObserver 📌

A React component that notifies its children of hover interactions.

Initial code taken from: [https://github.com/ethanselzer/react-hover-observer](https://github.com/ethanselzer/react-hover-observer).

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

```jsx
<HoverObserver>
 {({ isHovering }) => (
         <YourChildComponent isActive={isHovering} />
 )}
</HoverObserver>
```

{% hint style="info" %}
`isHovering` is always false on Android or iOS.
{% endhint %}

## Properties

| prop | type | required | default | description |
| :--- | :--- | :--- | :--- | :--- |
| hoverDelayInMs | _number_ | _no_ | 0 | Milliseconds to delay hover trigger. |
| hoverOffDelayInMs | _number_ | _no_ | 0 | Milliseconds to delay hover-off trigger. |
| onHoverChanged | _\(HoverObserverState\) =&gt; void_ | _no_ | - | Called with named argument isHovering when isHovering is set or unset. |
| onMouseEnter | _Function_ | _no_ | - | Defaults to set isHovering. |
| onMouseLeave | _Function_ | _no_ | - | Defaults to unsetting isHovering. |
| onMouseOver | _Function_ | _no_ | - |  |
| onMouseOut | _Function_ | _no_ | - |  |
| children | _ReactNode \| \(HoverObserverState\) =&gt; ReactNode_ | _no_ | - |  |
| testID | _string_ | _no_ | - | Used to locate this view in end-to-end tests. |

