# Developing an Analytics Plugin

You can add support for any analytics service provider by using the `bluebase.analytics.track` hook.

```typescript
await BB.Hooks.register('bluebase.analytics.track', {
	name: 'analytics-plugin',
	handler: (data: AnalyticTrackData) => {
		// send data to analytics provider here
	}
});
```



