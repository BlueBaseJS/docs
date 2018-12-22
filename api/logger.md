# 📔 Logger

BlueBase's Logger API allows you to log messages to any number of logging services.

## Working with the API

You can call logger for different console message modes:

```typescript
BB.Logger.log('log bar');
BB.Logger.info('info bar');
BB.Logger.debug('debug bar');
BB.Logger.warn('warn bar');
BB.Logger.error('error bar');
```

When handling an error:

```typescript
try {
    ...
} catch(e) {
    BB.Logger.error('error happened', e);
}
```

## Integrations

To add support for a Logging Provider see this [guide](../key-concepts/plugins/developing-a-logger-plugin.md).

