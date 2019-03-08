# Developing a Logger Plugin

You can add support for any logging service provider by using the following logger filters:

* `bluebase.logger.log`
* `bluebase.logger.info`
* `bluebase.logger.debug`
* `bluebase.logger.warn`
* `bluebase.logger.error`

## Example

```typescript
import { createPlugin } from '@bluebase/core';
​
export const LoggerPlugin = createPlugin({
​
    key: 'logger',
    name: 'Logger Plugin',
    categories: ['logging'],
    
    filters: {
        'bluebase.logger.log': (message: string, data: any) => {
            // send data to logging provider here
        }
    }
});
```

