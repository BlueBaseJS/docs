# Getting Started

We will learn concepts of BlueBase by creating a production-ready To-Do app.

## Setup

We will use Expo CLI to create a new project and add BlueBase to it. If Expo CLI is not installed, go to the [Expo CLI Installation](https://docs.expo.dev/get-started/installation/) guide before proceeding.

### Step 1: Initialize the project

Initialize an expo app by executing the following commands:

```shell
# Create a project named my-app.
# Select the "blank (Typescript)" template when prompted
expo init bluebase-todo-app

# Navigate to the project directory
cd bluebase-todo-app
```

More info [here](https://docs.expo.dev/get-started/create-a-new-app/).

### Step 2: Install BlueBase package

```shell
yarn add @bluebase/core
```

### Step 3: Update App File

{% code title="App.tsx" %}
```typescript
import React from 'react';
import { BlueBaseApp } from '@bluebase/core';

export default function App() {
  return (
    <BlueBaseApp />
  );
}
```
{% endcode %}

### Step 4: Run App

```shell
expo start
```

This will open the expo console.&#x20;

![](<../.gitbook/assets/Screenshot 2022-04-22 at 12.51.00 AM.png>)

You can launch the web or native version of the app from here.

![Web](<../.gitbook/assets/Screenshot 2022-04-22 at 12.51.33 AM.png>) ![iPhone](<../.gitbook/assets/Screenshot 2022-04-22 at 12.58.53 AM.png>)

## Adding Plugins

All functionality in BlueBase is added via plugins. Let us add some ready-made plugins to our project to take a head start on building our app.

### Step 1: Install plugins

Start by adding following devDependencies:

```shell
yarn add --dev @bluebase/plugin-launcher @bluebase/plugin-material-ui @bluebase/plugin-react-native-paper @bluebase/plugin-responsive-grid @bluebase/plugin-vector-icons @bluebase/plugin-settings-app @bluebase/plugin-react-router @bluebase/plugin-react-navigation @bluebase/plugin-responsive-grid @bluebase/plugin-json-schema-components
```

Some of the plugins (react-navigation) require some more dependencies to be installed:

```shell
expo install react-native-safe-area-context react-native-gesture-handler react-native-reanimated
```

### Step 2: Create plugin files

Now in the root folder create the following file `plugins.ts`:

{% code title="plugins.ts" %}
```typescript
import BlueBasePluginJsonSchemaComponents from '@bluebase/plugin-json-schema-components';
import BlueBasePluginLauncher from '@bluebase/plugin-launcher';
import BlueBasePluginMaterialUI from '@bluebase/plugin-material-ui';
import BlueBasePluginReactRouter from '@bluebase/plugin-react-router';
import BlueBasePluginResponsiveGrid from '@bluebase/plugin-responsive-grid';
import BlueBasePluginSettingsApp from '@bluebase/plugin-settings-app';
import { MaterialCommunityIcons } from '@bluebase/plugin-vector-icons';

export const plugins = [
	BlueBasePluginJsonSchemaComponents,
	BlueBasePluginLauncher,
	BlueBasePluginMaterialUI,
	BlueBasePluginReactRouter,
	BlueBasePluginResponsiveGrid,
	MaterialCommunityIcons,
	BlueBasePluginSettingsApp,
];
```
{% endcode %}

The file above exports an array of plugins, imported from their respective modules.

Create another file similar to the one above and name it `plugins.native.ts`. This way react-native compiler will load this version rather than `plugins.ts` on native platforms.&#x20;

So by doing this, we can add web specific plugins in `plugins.ts` and native specific code in `plugins.native.ts`.

{% code title="plugins.native.ts" %}
```typescript
import BlueBasePluginJsonSchemaComponents from '@bluebase/plugin-json-schema-components';
import BlueBasePluginLauncher from '@bluebase/plugin-launcher';
import BlueBasePluginReactNativePaper from '@bluebase/plugin-react-native-paper';
import BlueBasePluginReactNavigation from '@bluebase/plugin-react-navigation';
import BlueBasePluginResponsiveGrid from '@bluebase/plugin-responsive-grid';
import BlueBasePluginSettingsApp from '@bluebase/plugin-settings-app';
import { MaterialCommunityIcons } from '@bluebase/plugin-vector-icons';

export const plugins = [
	BlueBasePluginJsonSchemaComponents,
	BlueBasePluginLauncher,
	BlueBasePluginReactNativePaper,
	BlueBasePluginReactNavigation,
	BlueBasePluginResponsiveGrid,
	MaterialCommunityIcons,
	BlueBasePluginSettingsApp,
];
```
{% endcode %}

In this case, the only difference in the above 2 files is that `plugins.ts` uses `@bluebase/plugin-react-router`, while `plugins.native.ts` uses `@bluebase/plugin-react-navigation`.

### Step 3. Import plugins

Now edit the `App.tsx` file and add the following content.

{% code title="App.tsx" %}
```typescript
import 'react-native-gesture-handler';

import React from 'react';
import { BlueBaseApp } from '@bluebase/core';
import { plugins } from './plugins';

export default function App() {
  return (
    <BlueBaseApp plugins={plugins} />
  );
}
```
{% endcode %}

Here, we import the plugins array and pass them to the `BlueBaseApp` component as a prop.

### Step 4: Add Babel plugin

Lastly, modify the contents of `babel.config.js` file to:

{% code title="babel.config.js" %}
```javascript
module.exports = function(api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['react-native-reanimated/plugin'],
  };
};
```
{% endcode %}

### Step 5: Run

Now run the app again:

```
expo start
```

You should see the following screen on launch:

#### Home Screen

![Web](<../.gitbook/assets/Screenshot 2022-04-22 at 1.24.56 AM.png>) ![iOS](<../.gitbook/assets/Screenshot 2022-04-22 at 1.36.51 AM.png>)

#### Settings App

![Web](<../.gitbook/assets/Screenshot 2022-04-22 at 1.36.59 AM.png>) ![iOS](<../.gitbook/assets/Screenshot 2022-04-22 at 1.37.11 AM.png>)

### Explanation

So as you can see, by just installing a few plugins, we were able to add a lot of functionality in a very short span of time, by writing very few lines of code.

I'll try to briefly describe what purpose each plugin serves.

| Plugin                                  | Purpose                                                                                                               |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| @bluebase/plugin-launcher               | Adds Android-like "launcher" home screen, that shows app icons.                                                       |
| @bluebase/plugin-settings-app           | Adds the Settings section to the app. If you remove this plugin, the settings icon on the home screen will disappear. |
| @bluebase/plugin-json-schema-components | Provides components that help us build layouts by writing JSON. This is used by the settings plugin.                  |
| @bluebase/plugin-material-ui            | Provides Material UI components on web.                                                                               |
| @bluebase/plugin-react-native-paper     | Provides Material UI components on native.                                                                            |
| @bluebase/plugin-react-navigation       | Provides Navigation capability on native.                                                                             |
| @bluebase/plugin-react-router           | Provides Navigation capability on web.                                                                                |
| @bluebase/plugin-responsive-grid        | Provides Grid components (Column, Row, etc). Used by Launcher plugin.                                                 |
| @bluebase/plugin-vector-icons           | Provides SVG vector icons used in various screen, as shown above.                                                     |
