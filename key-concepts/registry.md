# Registry

BlueBase uses an internal data structure to store everything.

| Registry | Item | Value |
| :--- | :--- | :--- |
| Component | hocs, source, styles, isAsync, preload | BlueBaseModule&lt;React.Component&gt; |
| Config | subscriptions | BlueBaseModule&lt;any&gt; ⁉️ |
| Hook | name, priority | BlueBaseModule&lt;Handler&gt; |
| Intl ⁉️ |  | BlueBaseModule&lt;string&gt; |
| Plugin |  | BlueBaseModule&lt;Plugin&gt; |
| Route ⁉️ |  |  |
| Theme | name, slug, mode, alternate | BlueBaseModule&lt;Theme&gt; |

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

