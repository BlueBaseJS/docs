# 🎛 Configs

BlueBase comes with a built-in app configuration system. This is a registry where you can store configurations in key value pairs, as well as subscribe to changes.

## Hooking into config updates

It is possible to hook into any configuration before it is saved into the registry by using the `bluebase.config.beforeSave` hook.

```typescript
await BB.Hooks.register(
	'bluebase.config.beforeSave', 
	{
		handler: (config: { key: string, value: string}) => {
			// Do something here
		},
	}
);
```

## Subscribing to Config updates

It is also possible to subscribe to 

