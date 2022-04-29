# 🚇 Filters

**Filters** are functions that BlueBase passes data through, at certain points in execution, just before taking some action with the data (such as adding it to the database or rendering some views). Most input and output in BlueBase pass through at least one filter. BlueBase does some filtering by default, and your plugin can add its own filtering.

The basic steps to add your own filters to BlueBase (described in more detail below) are:

1. Create the JavaScript function that filters the data.
2. Hook to the filter in BlueBase, by any of the following methods:
   1. Put your JavaScript function in the `filters` object of your plugin.
   2. Call BB.Filters.register() function.

{% hint style="info" %}
The BlueBase Filters feature is heavily inspired by WordPress [Filters](https://codex.wordpress.org/Plugin\_API#Filters).
{% endhint %}

### Create a Filter Function

A filter function takes as input the unmodified data and returns modified data (or in some cases, a null value to indicate the data should be deleted or disregarded). If the data is not modified by your filter, then the original data must be returned so that subsequent plugins can continue to modify the value if necessary.

So, the first step in creating a filter in your plugin is to create a JavaScript function to do the filtering, and put it in your plugin file. For example, if you want to make sure that your posts and comments contain no profanity, you might define a variable with a list of forbidden words, and then create the following function:

```typescript
function filter_profanity(content: string) {
	const profanities = array('badword','alsobad','...');
	return content.replace(profanities, '{censored}');
}
```

### Register your Filter

After your function is defined, the next step is to register it with BlueBase. There are two ways to do this:

#### 1. Put the function in the filters property of the plugin

```typescript
createPlugin({
	// ... Other properties

	filters: {
		'post.comment': [{
			key: 'post-comment-profanity-remover',
			value: filter_profanity,
			priority: 2,
		}]
	},
});
```

#### 2 Call BB.Filters.register() function

```typescript
await BB.Filters.register({
	event: 'post.comment',
	key: 'post-comment-profanity-remover',
	value: filter_profanity,
	priority: 2,
});
```

where:

* **event**\
  ****The name of a filter event that is provided by the developer. Defines when your filter should be applied.
* **key**\
  ****A unique ID of the function that you want to use for filtering. Keep in mind that other plugins or the BlueBase core may already be using the function key you have thought of, in that case, one filter will overwrite the other.
* **value**\
  ****The filter function. This function may or may not be an async function. The function will always have 3 params:
  1. **value**: The value that is being filtered
  2. **context**: An object that may have extra arguments or data, passed at the time of execution.
  3. **BB**: The BlueBase instance.
* **priority**\
  ****An optional integer argument that can be used to specify the order in which the functions associated with a particular filter are executed (default: 10). Lower numbers correspond with earlier execution, and functions with the same priority are executed in the order in which they were added to the filter.
* **Return Value**\
  ****The (optionally modified) value of the first argument is passed to the filter function.

You can also remove filters from filter hooks using the BB.Filters.delete() function. See Removing Actions and Filters.

### Executing a Filter

#### BB.Filters.run function

You may define and execute your own filters by calling the following method

```typescript
const newValue = await BB.Filters.run(event, value, [context])
```

where

* **event**\
  ****The name of a filter event
* **value**\
  ****The value that is being filtered
* **context**\
  ****An optional object that may have extra arguments or data

In the example above, we would put the following params in the function:

```typescript
await BB.Filters.run(
    'post.comment',
    'A comment with profanity',
    { postId: '123' }
);
```

#### useFilter hook

Since BB.Filters.run() function returns a Promise, it gets a bit tricky to handle in a component. For this reason we provide a useFilter hook as well:

```typescript
const { value, loading, error } = useFilter(
    'post.comment',
    'A comment with profanity',
    { postId: '123' }
);
```

where the return value is an object with following properties:

* **value**\
  The (optionally modified) value of the first argument is passed to the filter function.
* **loading**\
  A flag that indicates if data is currently loading.
* **error**\
  If an error occurs, it will be set in this variable.&#x20;

### Removing Filters

In some cases, you may find that you want your plugin to disable one of the actions or filters built into BlueBase, or added by another plugin. You can do that by calling `BB.Filters.delete('key')`.

Note that in general, you shouldn't remove anything unless you know what it does and why it does it -- check the BlueBase or other plugin source code to be sure.
