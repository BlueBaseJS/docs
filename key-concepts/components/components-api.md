# Components API

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
await BB.Components.register({
  key: 'Logo',
  value: Logo,
  preload: true,
  hocs: [withRouter],
  styles: {},
  source: {},
});
```

