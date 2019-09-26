# 🏛 Favicon

BlueBase is using [**favicons-webpack-plugin@0.0.9**](https://github.com/jantimon/favicons-webpack-plugin) for this purpose. Current implementation will generate the favicons in your dist picking up the icon.png file from the "assets" folder followed up by the subfolder "web". The Favicons' links will be injected in the final index.html.

## Basic Usage:

Bluebase picks the icon to generate the Favicons from /assets/web/icon.png

**Changing the FavIcon:**

1.\) Replace the current icon.png with your desired one.

2.\) Override the configs in /bluebase/web/client.config.ts and provide a custom path to your favicon.

For Example:

```javascript
//Configuration File path => ./bluebase/web/client.config.ts

  export default function (input: any) {
      input.favIconConfig = {...input.favIconConfig,
      logo:'path to your favicon'}
    return input;
  }
```

## Advance Usage

### Full configuration options are as follow:

```javascript
        {
            // Your source logo
            logo: 'my-logo.png',
            // The prefix for all image files (might be a folder or a name)
            prefix: 'icons-[hash]/',
            // Emit all stats of the generated icons
            emitStats: false,
            // The name of the json containing all favicon information
            statsFilename: 'iconstats-[hash].json',
            // Generate a cache file with control hashes and
            // don't rebuild the favicons until those hashes change
            persistentCache: true,
            // Inject the html into the html-webpack-plugin
            inject: true,
            // favicon background color (see https://github.com/haydenbleasel/favicons#usage)
            background: '#fff',
            // favicon app title (see https://github.com/haydenbleasel/favicons#usage)
            title: 'Webpack App',

            // which icons should be generated (see https://github.com/haydenbleasel/favicons#usage)
            icons: {
            android: true,
            appleIcon: true,
            appleStartup: true,
            coast: false,
            favicons: true,
            firefox: true,
            opengraph: false,
            twitter: false,
            yandex: false,
            windows: false
            }
        }
```

