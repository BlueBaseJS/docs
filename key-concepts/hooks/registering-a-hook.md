# Registering a Hook

There are three ways to register to a hook listener is BlueBase.

1. [Register a hook through Plugin](./#register-a-hook-through-plugin)
2. [Register a hook through `hooks` property in `bluebase.js` file](./#register-a-hook-through-hooks-prop-in-bluebase-js-file)
3. [Register a hook through HookRegistry API](./#register-a-hook-through-api)

## Through Plugin

The easiest way to register a hook is through the `hooks` property in the plugin. This property expects a [HookNestedCollection](./#hook-collections) object.

```typescript
const MyPlugin = {
    hooks: {
        'hook.event': {
            key: 'hook.listener.name',
            priority: 5,
            value: async (value, args, BR) => {
                // your hook logic here

                return value;
            }
        }
    }
}
```

## Through hooks prop in "bluebase.ts" file

Hooks can be registered directly in `bluebase.ts` as well. Just create a hooks property in the main BootOptions object. Like plugins, this property is also expected to be a [`HookNestedCollection`](./#hook-collections).

{% hint style="warning" %}
The hooks added directly to the hooks property in `bluebase.js` are registered before any other code execution during boot. This means, that they have to ability to override some core internal process \(including the boot logic itself\).

This is not possible through plugin hooks, as they are registered and executed much later in execution.

For this reason, use this with caution. Unless extremely necessary, it is best to just register hooks through plugins.
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="bluebase.js" %}
```javascript
export default {

    // ...other bluebase.js properties

    hooks: {
        'hook.event': {
            key: 'hook.listener.name',
            priority: 5,
            value: async (value, args, BR) => {
                // your hook logic here

                return value;
            }
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Through Registry API

A single hook can be registered through the `BR.Hooks.register` function:

```typescript
await BB.Hooks.register({
  event: 'posts.edit',
  key: 'setEditedAt',
  value: async (post, { user }) => {
    post.editedAt = new Date();
    return post;
  }
});
```

It is also possible to register multiple hooks at once by using the `BR.Hooks.registerNestedCollection` function:

```typescript
await BB.Hooks.registerNestedCollection({
    'hook.event': [
        {
            key: 'hook.listener.name',
            priority: 5,
            value: async (value, args, BR) => {
                // your hook logic here

                return value;
            }
        },
        async (value, args, BR) => {
            // your hook logic here

            return value;
        }
    ]
});
```

