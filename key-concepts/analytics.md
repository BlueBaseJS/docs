# 📈 Analytics

The Analytics API enables you to collect analytics data for your app.

## Track Events

To record an event use the `track` method of BlueBase's Analytics API.

```typescript
BB.Analytics.track({ name: 'albumVisit' });
```

## **Record a Custom Event with Attributes**

The `track` method lets you add additional attributes to an event. For example, to record _artist_ information with an _albumVisit_ event:

```typescript
BB.Analytics.track({
    name: 'albumVisit', 
    // Attribute values must be strings
    attributes: { genre: '', artist: '' }
});
```

## **Record Engagement Metrics**

Data can also be added to an event:

```typescript
BB.Analytics.track({
    name: 'albumVisit', 
    attributes: {}, 
    metrics: { minutesListened: 30 }
});
```

## Integrations

To add support for an Analytics Provider see this [guide](plugins/developing-an-analytics-plugin.md).

