# 🎁 Components

React as a UI library puts a lot of emphasis on components. BlueBase stores components which can be dynamically used and replaced. This plays a major role in creating a pluggable and modular system.

## API

Each component in BlueBase has the following properties:

| Key | Type | Description |
| :--- | :--- | :--- |
| `key` | _string_ | The key is used as an ID. |
| `value` | _React.ComponentType_ | The raw React component. This may also be a promise \(for code splitting\) that resolves a React component. |
| `preload` | _boolean_ | _\(optional\) \(Default = false\)_ Should this component be preloaded at app initialization. This is useful for components that are wrapped in promises \(for code splitting\). |
| `hocs` | _Array_ | An array of React Higher Order Components. At runtime, each component is resolved with wrapping raw component in all HOCs in this array. |
| `styles` | _{ \[string: key\]: Styles }_ | An object containing key value pairs of style rules. Each rule maybe a `ViewStyle`, `TextStyle` or an `ImageStyle`. |
| `source` | _ComponentSource_ | This property represents the source that registered this component. |

## Structure

```typescript
const Logo = props => {
  return (
    <View>/* component code */</View>
  )
}
​
BB.Components.register({
  key: 'Logo',
  value: Logo,
  preload: true,
  hocs: [withRouter],
  styles: {},
  source: {},
});
```

## Registering a Component

There are many ways to register new components in BlueRain:

### Through a Plugin

The easiest way to add a new component to BlueRain is to use the 'components' static property of you app or plugin:

```typescript
import { View } from '@bluebase/core';
​
const Logo = props => {
  return (
    <View>/* component code */</View>
  )
}
​
const Plugin = {
​
    name: 'Example Plugin',
    key: 'example-plugin',
​
    components: {
      Logo
    }
}
```

Note that this may replace any existing components registered with same name.

### Through Registery API

You can add new Components anywhere in the code by calling the set method of ComponentRegistry:

```typescript
const Logo = props => {
  return (
    <View>/* component code */</View>
  )
}
​
BB.Components.register('Logo', Logo);
```

## Accessing Raw Components

Going back to our example:

```typescript
const WrappedComponent = withCurrentUser(MyComponent);
```

This would result a new WrappedComponent component that has MyComponent as a child. This has the consequence that properties and objects you set on MyComponent might not exist on WrappedComponent.

For that reason, BlueRain provides a getRawComponent utility that lets you access the unwrapped “raw” component, provided said component has been registered with set:

```typescript
MyComponent.foo = "bar";
const WrappedComponent = BR.Components.set(MyComponent, withCurrentUser);
console.log(WrappedComponent.foo); // undefined
console.log(BR.Components.getRawComponent(WrappedComponent).foo); // "bar"
```

## Components & HoCs

To understand how theming works in BlueRain, it's important to understand how components and higher-order components \(HoCs\) interact.

A higher-order component's role is to wrap a regular component to pass it a specific prop \(such as a list of posts, the current user, the Router object, etc.\). You can think of HoCs as specialized assistants that each hand the component a tool it needs to do its job.

The first argument of set is the component's name, the second is the component itself, and any successive arguments will be interpreted as higher-order components and wrapped around the component.

For example, this is how you'd pass the currentUser object to the Logo component:

```typescript
BR.Components.set('Logo', Logo, withCurrentUser);
```

### "Delayed" HoCs

There are a few subtle differences between registering a component with set and the more standard export default Foo and import Foo from './Foo.jsx' ES6 syntax.

First, you can only override a component if it's been registered using set. This means that if you're building any kind of theme or plugin and would like end users to be able to replace specific components, you shouldn't use import/export.

Second, both techniques also lead to different results when it comes to higher-order components \(more on this below\). If you write export withCurrentUser\(Foo\), the withCurrentUser function will be executed immediately, which will trigger an error because the fragment it depends on isn't properly initialized yet.

On the other hand, set\('Foo', Foo, withCurrentUser\) doesn't execute the function \(note that we write withCurrentUser and not withCurrentUser\(\)\), delaying execution until app's initialization.

But what about HoC functions that take arguments? For example if you were to write:

```typescript
BR.Components.set('PostsList', PostsList, withList(options));
```

The withList\(options\) would be executed immediately, and you would have no way of overriding the options object later on \(a common use case being overriding a fragment\).

For that reason, to delay the execution until the start of the app, you can use the following alternative syntax:

```typescript
BR.Components.set('PostsList', PostsList, [withList, options]);
```

### Add HOCs to existing Components

You can add new Hocs to the already registered components any time by using the addHocs method.

```typescript
BR.Components.addHocs('PostsList', withCurrentUser , withList(options));
```

