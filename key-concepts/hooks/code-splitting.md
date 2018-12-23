# Code Splitting

In BlueBase code splitting is done through treating certain objects as [BlueBaseModules](). The following can be BlueBaseModules:

### BR.Hooks.register method param

When registering a hook through `BR.Hooks.register` method, a module can be registered instead of a hook object.

```typescript
await BB.Hooks.register(import('./setEditedAtHook'));
```

But this method may not be as affective, as BlueBase needs to know a hook's key and event name at registration time. So this promise will be resolved immediately, even if the hook event \(e.g. `posts.edit`\) gets executed much later, or never at all. A much better way is to split just the handler function rather than the complete hook object:

### Handler function

It is possible to spilt a hook's handler function. This way the handler's bundle is only downloaded when the hook is executed.

This means that the code is not only **NOT** downloaded at boot time, and never at all if the hook is never executed.

```typescript
BB.Hooks.register({
  event: 'posts.edit',
  key: 'setEditedAt',
  value: import('./setEditedAtHookHandlerFn')
});
```

### Hook Collections

Each Hook in a Hook Collection is also evaluated as a BlueBaseModule:

```typescript
BB.Hooks.registerNestedCollection({
    'posts.create': [
        import('./setCreatedAtHook'),
        import('./setCreatedByHook'),
    ],
    'posts.edit': [
        import('./setEditedAtHook'),
        import('./setEditedByHook'),
    ],
});
```

As explained above, all these hooks will be evaluated at registration time, even if it is only the handler function. To avoid this, split only the handler functions instead:

```typescript
BB.Hooks.registerNestedCollection({
    'posts.create': [
        {
            key: 'set.created.at',
            priority: 5,
            value: import('./setCreatedAtHookFn')
        },
        {
            key: 'set.created.by',
            priority: 6,
            value: import('./setCreatedByHookFn')
        },
    ]
});
```



