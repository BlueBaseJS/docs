# ⚡️ Progressive Web Apps

## Plugin Info

[Workbox](https://developers.google.com/web/tools/workbox/guides/get-started) is a set of libraries and Node modules that make it easy to cache assets and take full advantage of features used to build Progressive Web Apps. Workbox provide different modes to enable PWA like CLI, Node Module and webpack. We are using [workbox-webpack-plugin](https://developers.google.com/web/tools/workbox/modules/workbox-webpack-plugin).

## **Basic Usage**

PWA mode is enabled by default. All you have to do is host the _sw.js_ file genearted in your dist to the root of your site and its done. You can verify the registered service worker from the application tab in chrome developer tools.

Talking about the caching strategy, Bluebase has one of the recommended caching strategy by workbox built-in for you. The below strategy is just for understating the cache rules currently implemented, you don't have to add these anywhere :\)

### Implemented Caching Strategy

**Google Fonts**

```javascript
// Cache the Google Fonts stylesheets with a stale-while-revalidate strategy.
workbox.routing.registerRoute(
  /^https:\/\/fonts\.googleapis\.com/,
  new workbox.strategies.StaleWhileRevalidate({
    cacheName: 'google-fonts-stylesheets',
  })
);

// Cache the underlying font files with a cache-first strategy for 1 year.
workbox.routing.registerRoute(
  /^https:\/\/fonts\.gstatic\.com/,
  new workbox.strategies.CacheFirst({
    cacheName: 'google-fonts-webfonts',
    plugins: [
      new workbox.cacheableResponse.Plugin({
        statuses: [0, 200],
      }),
      new workbox.expiration.Plugin({
        maxAgeSeconds: 60 * 60 * 24 * 365,
        maxEntries: 30,
      }),
    ],
  })
);
```

**Caching Images**

```javascript
workbox.routing.registerRoute(
  /\.(?:png|gif|jpg|jpeg|svg)$/,
  new workbox.strategies.CacheFirst({
    cacheName: 'images',
    plugins: [
      new workbox.expiration.Plugin({
        maxEntries: 60,
        maxAgeSeconds: 30 * 24 * 60 * 60, // 30 Days
      }),
    ],
  })
);
```

**Cache CSS and JavaScript Files**

```javascript
workbox.routing.registerRoute(
  /\.(?:js|css)$/,
  new workbox.strategies.StaleWhileRevalidate({
    cacheName: 'static-resources',
  })
);
```

The above is enough for you to get going with service workers but if you want to add another cache rule to existing config or you want to replace the built-in rules, you can do that.

## **Advanced Usage**

Configuration File path =&gt; _./bluebase/web/client.config.ts_

### Default implementation

```javascript
export default function (input: any) {
    return input;
}
```

### Change Existing Config

```javascript
export default function (input: any) {
    input.workBox.config.runtimeCaching.push({
   {
        // Match any request ends with .png, .jpg, .jpeg or .svg.
        urlPattern: /\.(?:png|jpg|jpeg|svg)$/,

        // Apply a cache-first strategy.
        handler: 'CacheFirst',

        options: {
          // Use a custom cache name.
          cacheName: 'images',

          // Only cache 10 images.
          expiration: {
            maxEntries: 10,
          },
        },
      } 
  })
  return input;
}
```

### Custom configs

Full configuration options can be found [**here**](https://developers.google.com/web/tools/workbox/modules/workbox-webpack-plugin#full_generatesw_config)

Below is a sample with an exclude option and a runtime caching strategy.

```javascript
export default function (input: any) {
  input.workbox.config = {
      // Exclude images from the precache
      exclude: [/\.(?:png|jpg|jpeg|svg)$/],

      // Define runtime caching rules.
      runtimeCaching: [{
        // Match any request ends with .png, .jpg, .jpeg or .svg.
        urlPattern: /\.(?:png|jpg|jpeg|svg)$/,

        // Apply a cache-first strategy.
        handler: 'CacheFirst',

        options: {
          // Use a custom cache name.
          cacheName: 'images',

          // Only cache 10 images.
          expiration: {
            maxEntries: 10,
          },
        },
      }],
    }
    return input;
}
```

## Disable PWA

Believe me that is the last thing you want to do :\(

```typescript
  export default function (input: any) {
      input.workbox.disable = true
      return input;
  }
```

