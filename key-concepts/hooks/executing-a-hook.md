# Executing a Hook

Hooks are executed using the `BR.Hooks.run` function:

```typescript
modifier = await BR.Hooks.run(`movies.edit`, modifier, { document, currentUser });
```

In each case, the **first** argument is the key of the hook event, the **second** argument is the one iterated on by each filter function on the hook, while any remaining arguments are just passed along from one iteration to the next.

