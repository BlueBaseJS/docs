# Developing a Logger Plugin

You can add support for any logging service provider by using the following logger hooks:

* `bluebase.logger.log`
* `bluebase.logger.info`
* `bluebase.logger.debug`
* `bluebase.logger.warn`
* `bluebase.logger.error`

## Example

```typescript
await BB.Hooks.register('bluebase.logger.log', {
	name: 'logger-plugin',
	handler: (message: string, data: any) => {
		// send data to analytics provider here
	}
});
```

