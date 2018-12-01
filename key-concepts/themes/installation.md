# Installation

## In bluebase.js

The easiest way to install themes in BlueBase is to import your theme into the `themes` property in the _bluebase_ file in your project.

{% code-tabs %}
{% code-tabs-item title="bluebase.ts" %}
```typescript
const bootOptions = {

	themes: [
		import('path/to/theme-1'),
		import('path/to/theme-2'),
	]
};

export default bootOptions;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This method is especially useful if you're developing a theme or have a custom theme in your project.

But this is not how other developers may distribute their themes. As some themes may come with their components, configs, and other customisations. 

Another problem with this method is that these themes cannot be disabled, while themes installed by plugins get disabled when plugins are disabled.

Hence, a better option is to package your theme as a plugin.

## Creating a Theme Plugin

To register themes via plugin, you need need to create a new plugin or modify an existing one. Follow this [guide](../plugins/developing-a-theme-plugin.md) to learn more.

