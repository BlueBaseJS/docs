# 🔌 Plugins

In BlueBase all functionality and features in an app are added as plugins. 

It is recommended to keep all plugins in separate NPM packages. This helps us keep all aspects of an app modular. Adding or removing any feature becomes a matter of enabling or disabling a plugin.

A plugin can be used to do any of the following:

* Subscribe to application's lifecycle events through [Hooks](hooks.md) and override/modify application behaviour in a non-invasive way.
* Add or modify Themes.
* Add or override [Components](components.md).

Additionally, plugins can be configurable through Plugin Configs.

## API

A plugin object can have the following properties:

| Key | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| `name` | _string_ | yes | Name of the plugin. |
| `key` | string | no | This property is used as an ID throughout the system.  |
| `description` | string | no | Plugin description. |
| `version` | string | no | Plugin version. |
| `categories` | string \| string\[\] | no | [Plugin Categories](plugins.md#plugin-categories). |
| `icon` |  |  |  |
| `enabled` | boolean | no | _\(Default = true\)_ Flag to check if a plugin is enabled. |
| `hooks` |  |  |  |
| `components` |  |  |  |
|  |  |  |  |

## Plugin Categories

* app
* store
* router
* logger
* theme
* analytics







Plugins are the best way to add or extend BlueRain functionalities (apps and system). For example, track visits using Google Analytics, etc.

