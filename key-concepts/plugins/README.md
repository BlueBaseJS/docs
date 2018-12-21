# 🔌 Plugins

In BlueRain all functionality and features in an app are added as plugins. Each plugin is a separate NPM package.

A plugin can add components, routes and hooks.

## API

A plugin object can have the following properties:

| Key | Type | Required | Description |
| :--- | :---: | :---: | :--- |
| `name` | _string_ | yes | Name of the plugin. |
| `slug` | string | no | This property is used as an ID throughout the system. If a slug is not provided, it will be auto-generated by `name` property. |
| `description` | string | no | Plugin description. |
| `version` | string | no | Plugin version. |
| `categories` | string \| string\[\] | no | [Plugin Categories](./#plugin-categories). |
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
