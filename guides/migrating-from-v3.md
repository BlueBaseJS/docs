# 🛂 Migrating from V3

BlueBase V4 is a complete rewrite of the whole framework. These have resulted in some major breaking changes. We made a conscious decision to go ahead with it since we a major version, we wanted to do what's right, rather than carry mistakes of previous version.

This page should serve as a guide to migrate BlueBase projects from V3.

## New Version, New Name

The project name has changed in V4. Previous the framework was called `BlueBase OS`. We have decided to drop the `OS` part. So now, it's just `BlueBase`.

![We&apos;re calling it... BlueBase](../.gitbook/assets/toy-story.png)

From V4 onwards, the project will move to it's new homes at:

* [Github](https://github.com/BlueBaseJS/core)
* [NPM](https://www.npmjs.com/package/@blueeast/bluerain)

Unfortunately, this also means that all import statements need to be migrated as well.

```diff
- import { BlueBase } from '@blueeast/bluerain-os';
+ import { BlueBase } from '@blueeast/bluerain';
```

## Bye Bye, withBlueRain

Theres no easy way to say this but... `withBlueRain` HOC is gone! Use `BlueRainConsumer` component instead.

We did this to simplify the API and to keep the bundle size in check.

```diff
- const Button = withBlueRain(({ BR, ...rest }) => {
-     return <BR.Components.Button {...rest} />;
- });

+ const Button = (props) => (
+     <BlueBaseConsumer>
+     {(BR) => <BR.Components.Button {...props} />}
+     </BlueBaseConsumer>
+ );
```

## No Singleton Instance

In V3 we used a single instance of BlueBase. This instance was exported from the library as `default` and `BR`. This has been removed in the V4. This means:

* Now there is not default export in BlueBase 4.
* Now there is no single BlueBase instance exported.

This also allows us to use more than one BlueBase apps in a single project.

## Hooks

### Registry methods

Since registry codebase has been completely revamped, the internal API and methods has changed. So, if you use any of the `BR.Hooks` class methods directly, be sure to check docs for changes.

Some important changes are listed below:

#### Add/Remove methods

`add` and `remove` methods have been renamed to `register` and `unregister` respectively.

#### Set method

Behavior of set and remove has changed.

* `set` method sets the whole array of all listeners of a hook, as opposed to a single listener.

### Filter and Event Registries

Hooks in V3 were made of 2 registries:

* FilterRegistry
* EventRegistry

Both of these have been removed, and we only have a single unified registry now, i.e. HookRegistry.

This also means that there are no `BR.Filters` and `BR.Events` properties in BlueBase context anymore.

### Running a Hook

#### Return Type

All `BR.Hooks.run` now returns a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) that resolves a value, previously it just returned the value.

```diff
- modifier = BR.Hooks.run('movies.edit', modifier);
+ modifier = await BR.Hooks.run('movies.edit', modifier);
```

#### Arguments in handler function

In V3 a hook handler function could receive any number of arguments. This has been changed and now a hook can only receive 3 fixed arguments.

```diff
- BR.Hooks.run('movies.edit', movie, actors, collections);
+ BR.Hooks.run('movies.edit', movie, { actors, collections });
```

More details of about the arguments passed to the [handler function](../key-concepts/hooks.md#handler-function) can be found here.

## Plugins

### Plugin Structure

There is not `initialize` method in the plugin anymore. Use any of the event hooks.

Alternately, use `bluebase.plugins.initialize` hook. But it is not recommended.

### Registry methods

Since registry codebase has been completely revamped, the internal API and methods has changed. So, if you use any of the `BR.Plugins` class methods directly, be sure to check docs for changes.

Some important changes are listed below:

#### Add/Remove methods

`add` and `remove` methods have been renamed to `register` and `unregister` respectively.

#### Set method

Behavior of set and remove has changed.

* `set` method sets the whole array of all listeners of a hook, as opposed to a single listener.

#### initializeAll method

`initializeAll` method has been removed. Use `bluerain.plugins.initialize.all` hook instead.

```diff
- BR.Plugins.initializeAll();
+ await BR.Hooks.run('bluerain.plugins.initialize.all', bootOptions);
```

#### registerMany method

`registerMany` method has been removed. Use `bluerain.plugins.register` hook instead.

```diff
- BR.Plugins.registerMany(plugins);
+ await BR.Hooks.run('bluerain.plugins.register', bootOptions);
```

## Components

### IconEnhanced

IconEnhanced Component has been renamed to `DynamicIcon`

