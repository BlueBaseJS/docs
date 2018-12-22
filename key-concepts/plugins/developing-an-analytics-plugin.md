# Developing an Analytics Plugin

You can add support for any analytics service provider by using the `bluebase.analytics.track` hook.

```typescript
import { createPlugin } from '@bluebase/core';
​
export const AnalyticsPlugin = createPlugin({
​
    key: 'analytics',
    name: 'Analytics Plugin',
    categories: ['analytics'],
    
    hooks: {
        'bluebase.analytics.track': (data: AnalyticsTrackData) => {
            // send data to analytics provider here
        }
    }
});
```

