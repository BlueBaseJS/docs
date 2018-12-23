# Hooks API

Each hook event can have multiple hooks registered in BlueBase. These hooks are executed in a waterfall sequence, where result of each listener is passed on to the next one.

## Structure

Each hook has the following properties:

| Key | Type | Description |
| :--- | :--- | :--- |
| `key` | _string_ | The key is used as an ID. |
| `event` | _string_ | This is the name of event to hook into. |
| `priority` | _number_ | _\(optional\) \(Default = 10\)_ At runtime each hook is executed based on the priority with the lowest number running first and highest running last. |
| `value` | _function_ | This is the handler function that is called when a hook is executed. This function maybe an async function that resolves a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). Details of handler function are given [below](./#listener-handler). |

### Handler function

This is the function that is executed at runtime. Handler functions in BlueBase maybe async functions, i.e. functions that return a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that resolve a value.

Each handler function receives 3 arguments during execution:

| Name | Description |
| :--- | :--- |
| `value` | This is the main value that is being hooked into. A hook expects this value to be returned. If the value is changed during execution, the next listener will receive the new value instead of the original version. |
| `args` | An object that may provide addition context or information of the event. |
| `BR` | BlueBase context. |

## Hook Collections

In BlueBase multiple hooks can be registered for multiple events at once. We do this through the `HookNestedCollection` data structure.

A `HookNestedCollection` is an object that has key-value pairs. Each property is a string that represents the hook event name. And the value of this property can be one of the following:

1. [A hook object](./#hook-object)
2. [A handler function](./#handler-function-1)
3. [An array of containing hook object and/or handler functions](./#array-of-hooks)

Moreover, the collection itself can be a:

1. A `HookNestedCollection` object
2. [A function \(thunk\) that returns a `HookNestedCollection` object](./#thunks)

### Hook Object

Hooks can be added to the collection as objects. When defining a hook as an object, keep in mind that both `key` and `value` are required properties.

```javascript
const MyHookCollection = {
    'hook.event': {
        key: 'hook.listener.name',
        priority: 5,
        value: async (value, args, BR) => {
            // your hook logic here

            return value;
        }
    }
};
```

### Handler Function

There is also a much simpler shorthand version. Rather than setting the whole listener object, the handler function can be set directly. In this case, BlueBase will attempt to auto-generate a hook key.

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
};
```

### Thunks

BlueBase also supports Hook Collection thunks. Which means, a Hook Collection can be a function that returns `HookNestedCollection` object.

This function receives BlueBase context object as the only argument at execution time.

```javascript
const MyHookCollection = (BR) => ({
    'hook.event': async (value, args, BR) => {
        // your hook logic here

        return value;
    }
});
```

