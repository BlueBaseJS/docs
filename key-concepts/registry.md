# Registry

BlueBase uses an internal data structure to store everything.

| Registry  | Item                                   | Value                            |
| --------- | -------------------------------------- | -------------------------------- |
| Component | hocs, source, styles, isAsync, preload | BlueBaseModule\<React.Component> |
| Config    | subscriptions                          | BlueBaseModule\<any> ⁉️          |
| Filter    | name, priority                         | BlueBaseModule\<Handler>         |
| Intl ⁉️   |                                        | BlueBaseModule\<string>          |
| Plugin    |                                        | BlueBaseModule\<Plugin>          |
| Route ⁉️  |                                        |                                  |
| Theme     | name, slug, mode, alternate            | BlueBaseModule\<Theme>           |

## Components

Render prop component that resolves and returns a value.

* Automatically re-renders on value change.
* Shows loading & error states while resolving

```typescript
const Foo = () => (
    <RegistryValue registry="Components" key="View">
    {
        (Component) => <Component />; 
    }
    </RegistryValue>
);
```
