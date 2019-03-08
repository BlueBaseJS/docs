# FavIcon

## BlueBase has builtin Favicon generator. 

BlueBase is using **favicons-webpack-plugin(0.0.9)** for this purpose. Current implemntation will generate the favicons in your dist picking up the icon.png file from the "assets" folder followed up by the subfolder "web". The Favicons' links will be injected in the final index.html.

### Using Custome Favicon:
Bluebase picks the icon to generate the Favicons from /assets/web/icon.png

**There are two ways:**
Replace the current icon.png with your desired one.
Override the configs in /bluebase/web/client.config.ts. This file provides all the configs as an input and expects an altered configs if the user desires so. The config object to change in the favicon settings is "favIconConfig"
e.g input.favIconConfig.logo = 'path to your file';


#### Full configuration options are as follow:
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

