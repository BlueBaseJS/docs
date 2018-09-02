# 🛂 Migrating from V3

There are some major breaking changes in the new version of BlueRain V4. This page should serve as a guide to migrate BlueRain projects from V3.

## New Version, New Name

The project name has changed in V4. Previous the framework was called `BlueRain OS`. We have decided to drop the `OS` part.

This also means that from V4 onwards, the project will move to it's new homes at:

* [Github](https://github.com/BlueEastCode/bluerain)
* [NPM](https://www.npmjs.com/package/@blueeast/bluerain)

Unfortunately, this also means that all import statements need to be migrated as well. 

```typescript
// Previous
import { BlueRain } from '@blueeast/bluerain-os';

// New
import { BlueRain } from '@blueeast/bluerain';
```

## Hooks

### Return Type

All `BR.Hooks.run` now returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that resolves a value, previously it just returned the value.

```typescript
// Previous
modifier = BR.Hooks.run('movies.edit', modifier);

// New
modifier = await BR.Hooks.run('movies.edit', modifier);
```

### Add/Remove methods

`add` and `remove` methods have been renamed to `register` and `unregister` respectively.

### Set/Remove methods

Behavior of set and remove has changed. 

* `set` method sets the whole array of all listeners of a hook, as opposed to a single listener.
* `remove` method removes the whole array of all listeners of a hook, as opposed to a single listener.

### Filter and Event Registries

Hooks in V3 were made of 2 registries:

* FilterRegistry
* EventRegistry

Both of these have been removed, and we only have a single unified registry now, i.e. HookRegistry.

This also means that there are no `BR.Filters` and `BR.Events` properties in BlueRain context anymore.

### Arguments in handler function

In V3 a hook handler function could receive any number of arguments. This has been changed and now a hook can only receive 3 fixed arguments.

```typescript
// Previous
BR.Hooks.run('movies.edit', movie, actors, collections);

// New
BR.Hooks.run('movies.edit', movie, { actors, collections });
```

More details of about the arguments passed to the [handler function](../key-concepts/hooks.md#handler-function) can be found here.

