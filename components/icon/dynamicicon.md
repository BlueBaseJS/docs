# DynamicIcon 📌

An enhanced Icon that can render any of the following:

* BB.Components.Icon
* BB.Components.Image
* A custom component

{% hint style="info" %}
#### System Component 📌

This component is shipped with BlueBase Core.
{% endhint %}

## Usage

### Icon

The following example shows how to use [BlueBase Icon](icon-1.md) component:

```jsx
<DynamicIcon
    type="icon"
    size={250}
    name="rocket"
/>
```

### Image

The following example shows how to use an image as an icon:

```jsx
<DynamicIcon
    type="image"
    size={250}
    source={{ uri: 'https://picsum.photos/200' }}
/>
```

### Component

The following example shows how to use a custom component as an icon:

```jsx
const CustomComponent = ({ size }: { size: number }) => (
	<View style={{ height: size, width: size, backgroundColor: 'red' }} />
);

// Then somewhere in your component:		
<DynamicIcon
    type="component"
    size={250}
    component={CustomComponent}
/>
```

It is also possible to use a component registered in the ComponentRegistry by using it's name:

```jsx
<DynamicIcon
    type="component"
    size={250}
    component="CustomComponent" // equivalent to BB.Components.resolve('CustomComponent')
/>
```

## Properties

<table>
  <thead>
    <tr>
      <th style="text-align:left">prop</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">required</th>
      <th style="text-align:left">default</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">'component' | 'icon' | 'image'</td>
      <td style="text-align:left"><em>yes</em>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">
        <p>If value is:</p>
        <p></p>
        <ul>
          <li><code>component</code>: Icon is a custom component, and looks for 'component'
            prop</li>
          <li><code>icon</code>: Icon is an instance of BB.Components.Icon and looks
            for 'icon' prop</li>
          <li><code>image</code>: Icon is an instance of BB.Components.Image and looks
            for 'source' prop</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">component</td>
      <td style="text-align:left">React Component | string</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Used when type is 'component'. Either a component or a component name
        (string). In case of string, it will be fetched from Component Registry.</td>
    </tr>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Used when type is 'icon'. This is the name prop of the BB.Components.Icon
        component</td>
    </tr>
    <tr>
      <td style="text-align:left">source</td>
      <td style="text-align:left">Image Source Prop Type</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Used when type is 'image'. This is the Image source.</td>
    </tr>
    <tr>
      <td style="text-align:left">size</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">100</td>
      <td style="text-align:left">Icon size.</td>
    </tr>
    <tr>
      <td style="text-align:left">testID</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><em>no</em>
      </td>
      <td style="text-align:left">-</td>
      <td style="text-align:left">Used to locate this view in end-to-end tests.</td>
    </tr>
  </tbody>
</table>

