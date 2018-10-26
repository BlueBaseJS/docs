# 🎣 Hooks

Hooks are the backbone of BlueRain. They allows us to modify data or inject custom logic in any part of the application at runtime.

A hook can be [registered](hooks.md#registering-a-hook) by one of the methods listed below. At runtime, when a hook event is executed, each registered hook is run in the order of priority, and given the opportunity to modify a value by returning a new value.

BlueRain provides different lifecycle hooks to the application, but a plugin may define its own hooks as well.

## API

Each hook event can have multiple hooks registered in BlueRain. These hooks are executed in a waterfall sequence, where result of each listener is passed on to the next one.

### Properties

Each hook has the following properties:

| Key | Type | Description |
| :--- | :--- | :--- |
| `name` | _string_ | Name of this hook. Used as an id. |
| `priority` | _number_ | _\(optional\) \(Default = 10\)_ At runtime each hook is executed based on the priority with the lowest number running first and highest running last. |
| `handler` | _function_ | A hook in BlueRain maybe an async function that resolves a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Details of handler function are given [below](hooks.md#listener-handler). |

### Handler function

This is the function that is executed at runtime. Handler functions in BlueRain maybe async functions, i.e. functions that return a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that resolve a value.

Each handler function receives 3 arguments during execution:

| Name | Description |
| :--- | :--- |
| `value` | This is the main value that is being hooked into. A hook expects this value to be returned. If the value is changed during execution, the next listener will receive the new value instead of the original version. |
| `args` | An object that may provide addition context or information of the event. |
| `BR` | This is the BlueRain context. |

## Hook Collections

In BlueRain multiple hooks can be registered for multiple events at once. We do this through the `HookCollections` data structure.

A `HookCollection` is an object that has key-value pairs. Each property is a string that represents the hook event name. And the value of this property can be one of the following:

1. [A hook object](hooks.md#hook-object)
2. [A handler function](hooks.md#handler-function-1)
3. [An array of containing hook object and/or handler functions](hooks.md#array-of-hooks)

Moreover, the collection itself can be a:

1. A `HookCollection` object
2. [A function \(thunk\) that returns a `HookCollection` object](hooks.md#thunks)

### Hook Object

Hooks can be added to the collection as objects. When defining a hook as an object, keep in mind that both `name` and `handler` are required properties.

```javascript
const MyHookCollection = {
    'hook.event': {
        name: 'hook.listener.name',
        priority: 5,
        handler: async (value, args, BR) => {
            // your hook logic here

            return value;
        }
    }
};
```

### Handler Function

There is also a much simpler shorthand version. Rather than setting the whole listener object, the handler function can be set directly. In this case, BlueRain will attempt to auto-generate a hook name.

```javascript
const MyHookCollection = {
    'hook.event': async (value, args, BR) => {
        // your hook logic here

        return value;
    }
}
```

### Array of hooks

It is also possible to add more than one hooks for each hook event. Rather than creating a single hook, just create an array instead.

Note that the array items can either be a hook object or a handler function.

```javascript
const MyHookCollection = {
    'hook.event': [
        {
            name: 'hook.listener.name',
            priority: 5,
            handler: async (value, args, BR) => {
                // your hook logic here

                return value;
            }
        },
        async (value, args, BR) => {
            // your hook logic here

            return value;
        }
    ]
};
```

### Thunks

BlueRain also supports Hook Collection thunks. Which means, a Hook Collection can be a function that returns `HookCollection` object.

This function receives BlueRain context object as the only argument at execution time.

```javascript
const MyHookCollection = (BR) => ({
    'hook.event': async (value, args, BR) => {
        // your hook logic here

        return value;
    }
});
```

## Registering a Hook

There are three ways to register to a hook listener is BlueRain.

1. [Register a hook through Plugin](hooks.md#register-a-hook-through-plugin)
2. [Register a hook through `hooks` property in `bluerain.js` file](hooks.md#register-a-hook-through-hooks-prop-in-bluerain-js-file)
3. [Register a hook through HookRegistry API](hooks.md#register-a-hook-through-api)

### Register a hook through Plugin

The easiest way to register a hook is through the `hooks` property in the plugin. This property expects a [HookCollection](hooks.md#hook-collections) object.

```typescript
const MyPlugin = {
    hooks: {
        'hook.event': {
            name: 'hook.listener.name',
            priority: 5,
            handler: async (value, args, BR) => {
                // your hook logic here

                return value;
            }
        }
    }
}
```

### Register a hook through hooks prop in "bluerain.js" file

Hooks can be registered directly in `bluerain.js` as well. Just create a hooks property in the main BootOptions object. Like plugins, this property is also expected to be a [`HookCollection`](hooks.md#hook-collections).

{% hint style="warning" %}
The hooks added directly to the hooks property in `bluerain.js` are registered before any other code execution during boot. This means, that they have to ability to override some core internal process \(including the boot logic itself\).

This is not possible through plugin hooks, as they are registered and executed much later in execution.

For this reason, use this with caution. Unless extremely necessary, it is best to just register hooks through plugins.
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="bluerain.js" %}
```javascript
export default {

    // ...other bluerain.js properties

    hooks: {
        'hook.event': {
            name: 'hook.listener.name',
            priority: 5,
            handler: async (value, args, BR) => {
                // your hook logic here

                return value;
            }
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Register a hook through API

A single hook can be registered through the `BR.Hooks.register` function:

```typescript
BR.Hooks.register('posts.edit', {
  name: 'setEditedAt',
  handler: async (post, { user }) => {
    post.editedAt = new Date();
    return post;
  }
});
```

It is also possible to register multiple hooks at once by using the `BR.Hooks.registerCollection` function:

```typescript
BR.Hooks.registerCollection({
    'hook.event': [
        {
            name: 'hook.listener.name',
            priority: 5,
            handler: async (value, args, BR) => {
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

## Unregistering a Hook

Hook Listeners can be unregistered through the `BR.Hooks.unregister` function:

```typescript
BR.Hooks.unregister('posts.edit', 'setEditedAt');
```

## Executing a Hook

Hooks are executed using the `BR.Hooks.run` function:

```typescript
modifier = await BR.Hooks.run(`movies.edit`, modifier, { document, currentUser });
```

In each case, the **first** argument is the name of the hook event, the **second** argument is the one iterated on by each filter function on the hook, while any remaining arguments are just passed along from one iteration to the next.

Note that each filter function should return the main argument to pass it on to the next function.

## Code Splitting

In BlueRain code splitting is done through treating certain objects as [BlueRainModules](bluerain-modules.md). The following can be BlueRainModules:

### BR.Hooks.register method param

When registering a hook through `BR.Hooks.register` method, a module can be registered instead of a hook object.

```typescript
BR.Hooks.register('posts.edit', import('./setEditedAtHook'));
```

But this method may not be as affective, as BlueRain needs to know a hook's name at registration time. So this promise will be resolved immediately, even if the hook event \(e.g. `posts.edit`\) gets executed much later, or never at all. A much better way is to split just the handler function rather than the complete hook object:

### Handler function

It is possible to spilt a hook's handler function. This way the handler's bundle is only downloaded when the hook is executed.

This means that the code is not only **NOT** downloaded at boot time, but never at all if the hook is never executed.

```typescript
BR.Hooks.register('posts.edit', {
  name: 'setEditedAt',
  handler: import('./setEditedAtHookHandlerFn')
});
```

### Hook Collections

Each Hook in a Hook Collection is also evaluated as a BlueRainModule:

```typescript
BR.Hooks.registerCollection({
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
BR.Hooks.registerCollection({
    'posts.create': [
        {
            name: 'set.created.at',
            priority: 5,
            handler: import('./setCreatedAtHookFn')
        },
        {
            name: 'set.created.by',
            priority: 6,
            handler: import('./setCreatedByHookFn')
        },
    ]
});
```

