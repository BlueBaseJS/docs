# 🔌 Plugins

Plugins are the best way to add features to your BlueBase app.

It is recommended to keep all plugins in separate NPM packages. This helps us keep all aspects of an app modular. Adding or removing any feature becomes a matter of enabling or disabling a plugin.

A plugin can be used to do any of the following:

* Subscribe to application's lifecycle events through [Filters](https://github.com/BlueBaseJS/docs/tree/6710d83d9e42436a90100426d36314c69fa496f6/key-concepts/plugins/filters.md) and override/modify application behaviour in a non-invasive way.
* Add new or modify existing [Components](https://github.com/BlueBaseJS/docs/tree/6710d83d9e42436a90100426d36314c69fa496f6/key-concepts/plugins/components.md) in the app. Moreover, plugins can wrap any component in Higher Order Components \(HOCs\).
* Modify an existing [Theme](../themes/) in the app, or extend it to create a new one. It is also possible to create a theme completely from scratch.
* Add new or modify existing routes to the app.

Additionally, plugins can be configurable through [Plugin Configs](making-a-plugin-configurable.md).

