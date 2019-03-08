# Registering a Filter

There are three ways to register to a filter listener is BlueBase.

1. [Register a filter through Plugin](./#register-a-filter-through-plugin)
2. [Register a filter through `filters` property in `bluebase.js` file](./#register-a-filter-through-filters-prop-in-bluebase-js-file)
3. [Register a filter through FilterRegistry API](./#register-a-filter-through-api)

## Through Plugin

The easiest way to register a filter is through the `filters` property in the plugin. This property expects a [FilterNestedCollection](./#filter-collections) object.

```typescript
const MyPlugin = {
    filters: {
        'filter.event': {
            key: 'filter.listener.name',
            priority: 5,
            value: async (value, args, BB) => {
                // your filter logic here

                return value;
            }
        }
    }
}
```

## Through filters prop in "bluebase.ts" file

Filters can be registered directly in `bluebase.ts` as well. Just create a filters property in the main BootOptions object. Like plugins, this property is also expected to be a [`FilterNestedCollection`](./#filter-collections).

{% hint style="warning" %}
The filters added directly to the filters property in `bluebase.js` are registered before any other code execution during boot. This means, that they have to ability to override some core internal process \(including the boot logic itself\).

This is not possible through plugin filters, as they are registered and executed much later in execution.

For this reason, use this with caution. Unless extremely necessary, it is best to just register filters through plugins.
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="bluebase.js" %}
```javascript
export default {

    // ...other bluebase.js properties

    filters: {
        'filter.event': {
            key: 'filter.listener.name',
            priority: 5,
            value: async (value, args, BB) => {
                // your filter logic here

                return value;
            }
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Through Registry API

A single filter can be registered through the `BB.Filters.register` function:

```typescript
await BB.Filters.register({
  event: 'posts.edit',
  key: 'setEditedAt',
  value: async (post, { user }) => {
    post.editedAt = new Date();
    return post;
  }
});
```

It is also possible to register multiple filters at once by using the `BB.Filters.registerNestedCollection` function:

```typescript
await BB.Filters.registerNestedCollection({
    'filter.event': [
        {
            key: 'filter.listener.name',
            priority: 5,
            value: async (value, args, BB) => {
                // your filter logic here

                return value;
            }
        },
        async (value, args, BB) => {
            // your filter logic here

            return value;
        }
    ]
});
```

