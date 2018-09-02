# 🎣 Hooks

Hooks are the backbone of BlueRain. They allows us to modify data or inject custom logic in any part of the application at runtime. 

A plugin can modify data by binding a listener to a hook. When the hook is later executed, each bound listener is run in the order of priority, and given the opportunity to modify a value by returning a new value.

BlueRain provides different lifecycle hooks to the application, but a plugin may define its own hooks as well.

## Hook Listeners

Each hook event can have multiple listeners registered in BlueRain. These listeners are executed in a waterfall sequence, where result of each listener is passed on to the next one. This way 

### Properties

Each hook has the following properties:

| Key | Type | Description |
| :--- | :--- | :--- |
| `name` | _string_ | Name of this listener. Used as an id. |
| `priority` | _number_ | _\(optional\) \(Default = 10\)_ At runtime each hook is executed based on the priority with the lowest number running first and highest running last. |
| `handler` | _function_ | A hook in BlueRain is an async function that resolves a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Details of handler function are given [below](hooks.md#listener-handler). |

### Handler function

This is the function that is executed at runtime. Handler functions in BlueRain are async functions, i.e. functions that return a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that resolve a value. 

Each handler function receives 3 arguments during execution

| Name | Description |
| :--- | :--- |
| `value` | This is the main value that is being hooked into. A hook expects this value to be returned. If the value is changed during execution, the next listener will receive the new value instead of the original version. |
| `args` | An object that may provide addition context or information of the event. |
| `BR` | This is the BlueRain context. |

## Registering a Hook Listener

There are two ways to register to a hook listener is BlueRain.

### Through Plugin

The easiest way to register a hook listener is through the `hooks` property in the plugin. 

The `hooks` property in the plugin is an object. Each key of this object represents the hook name we want to subscribe to, while the value is the hook listener.

```typescript
const MyPlugin = {
    hooks: {
        'hook.event': {
            name: 'hook.listener.name',
            position: 5,
            handler: async (value, args, BR) => {
                // your hook logic here
                
                return value;
            }
        }
    }
}
```

There is also a much simpler shorthand version. Rather than setting the whole listener object, the handler function can be set directly.

```typescript
const MyPlugin = {
    hooks: {
        'hook.event': async (value, args, BR) => {
            // your hook logic here
            
            return value;
        }
    }
}
```

In this case, the listener name can be auto generated and default priority is used.

{% hint style="warning" %}
TODO: 

* [ ] Add an example of adding multiple listeners against a single hook.
* [ ] Add an example of using BlueRain Modules.
{% endhint %}

### Through API

Hook Listeners are registered through the `BR.Hooks.register` function:

```typescript
BR.Hooks.register('posts.edit', 'setEditedAt' , async (post, { user }) => {
  post.editedAt = new Date();
  return post;
});
```

## Executing a Hook

Hooks are executed using the `BR.Hooks.run` function:

```typescript
modifier = await BR.Hooks.run(`movies.edit`, modifier, { document, currentUser });
```

In each case, the **first** argument is the name of the hook event, the **second** argument is the one iterated on by each filter function on the hook, while any remaining arguments are just passed along from one iteration to the next.

Note that each filter function should return the main argument to pass it on to the next function.

## Removing a Hook Listener

Hook Listeners can be removed through the `BR.Hooks.unregister` function:

```typescript
BR.Hooks.unregister('posts.edit', 'setEditedAt');
```

