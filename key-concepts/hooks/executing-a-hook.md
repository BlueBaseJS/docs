# Executing a Filter

Filters are executed using the `BB.Filters.run` function:

```typescript
modifier = await BB.Filters.run(`movies.edit`, modifier, { document, currentUser });
```

In each case, the **first** argument is the key of the filter event, the **second** argument is the one iterated on by each filter function on the filter, while any remaining arguments are just passed along from one iteration to the next.

