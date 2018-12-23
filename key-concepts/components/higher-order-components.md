# Higher Order Components

A higher-order component's role is to wrap a regular component to pass it a specific prop \(such as a list of posts, the current user, the Router object, etc.\). You can think of HOCs as specialised assistants that each hand the component a tool it needs to do its job.

The first argument of set is the component's name, the second is the component itself, and any successive arguments will be interpreted as higher-order components and wrapped around the component.

For example, this is how you'd pass the currentUser object to the Logo component:

```typescript
await BB.Components.register({
    key: 'Logo',
    value: LogoComponent,
    hocs: [withCurrentUser]
});
```

## "Delayed" HoCs

There are a few subtle differences between registering a component with `register` and the more standard `export default Foo` and `import Foo from './Foo.jsx'` ES6 syntax.

First, you can only override a component if it's been registered using `register`. This means that if you're building any kind of theme or plugin and would like end users to be able to replace specific components, you shouldn't use import/export.

Second, both techniques also lead to different results when it comes to higher-order components \(more on this below\). If you write export `withCurrentUser(Foo)`, the `withCurrentUser` function will be executed immediately, which will trigger an error because the fragment it depends on isn't properly initialised yet.

On the other hand, `register` doesn't execute the function \(note that we write `withCurrentUser` and not `withCurrentUser()`\), delaying execution until app's initialisation.

But what about HoC functions that take arguments? For example if you were to write:

```typescript
await BB.Components.register({
    key: 'PostsList',
    value: PostsList,
    hocs: [withList(options)]
});
```

The `withList(options)` would be executed immediately, and you would have no way of overriding the options object later on \(a common use case being overriding a fragment\).

For that reason, to delay the execution until the start of the app, you can use the following alternative syntax:

```typescript
await BB.Components.register({
    key: 'PostsList',
    value: PostsList,
    hocs: [
        [withList, options]
    ]
});
```

## Add HOCs to existing Components

You can add new HOCs to the already registered components any time by using the `addHocs` method.

```typescript
BB.Components.addHocs('PostsList', withCurrentUser);
```



