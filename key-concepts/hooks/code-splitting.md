# Code Splitting

In BlueBase code splitting is done through treating certain objects as [BlueBaseModules](). The following can be BlueBaseModules:

### BB.Filters.register method param

When registering a filter through `BB.Filters.register` method, a module can be registered instead of a filter object.

```typescript
await BB.Filters.register(import('./setEditedAtFilter'));
```

But this method may not be as affective, as BlueBase needs to know a filter's key and event name at registration time. So this promise will be resolved immediately, even if the filter event \(e.g. `posts.edit`\) gets executed much later, or never at all. A much better way is to split just the handler function rather than the complete filter object:

### Handler function

It is possible to spilt a filter's handler function. This way the handler's bundle is only downloaded when the filter is executed.

This means that the code is not only **NOT** downloaded at boot time, and never at all if the filter is never executed.

```typescript
BB.Filters.register({
  event: 'posts.edit',
  key: 'setEditedAt',
  value: import('./setEditedAtFilterHandlerFn')
});
```

### Filter Collections

Each Filter in a Filter Collection is also evaluated as a BlueBaseModule:

```typescript
BB.Filters.registerNestedCollection({
    'posts.create': [
        import('./setCreatedAtFilter'),
        import('./setCreatedByFilter'),
    ],
    'posts.edit': [
        import('./setEditedAtFilter'),
        import('./setEditedByFilter'),
    ],
});
```

As explained above, all these filters will be evaluated at registration time, even if it is only the handler function. To avoid this, split only the handler functions instead:

```typescript
BB.Filters.registerNestedCollection({
    'posts.create': [
        {
            key: 'set.created.at',
            priority: 5,
            value: import('./setCreatedAtFilterFn')
        },
        {
            key: 'set.created.by',
            priority: 6,
            value: import('./setCreatedByFilterFn')
        },
    ]
});
```



