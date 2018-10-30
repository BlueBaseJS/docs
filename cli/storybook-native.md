---
description: >-
  Storybook Native is a UI development environment for UI components. The tool
  enables users to create and showcase components independently in an isolated
  development environment on a mobile device.
---

# Storybook Native \(Expo\)

## Installation

First of all @blueeast/bluerain-cli-storybook-native plugin must be installed using globally installed bluerain-cli by executing the following commands in your terminal.

```text
bluerain plugins:add @blueeast/bluerain-cli-storybook-native
```

This will install the necessary dependencies to run storybook native on your system.

## Usage

After done setting up this plugin. You can go ahead and utilize this cli feature in your newly created or already existing project using BlueRainOS.

```text
bluerain storybook-native:init
```

Let's start with the init command. This command makes your project ready to be used using native storybook. It initializes basic bluerain specific configurations, storybook specific configurations and some sample components under bluerain/storybook-native directory. assets/storybook-native directory carrying images, icons etc to get your native storybook up and running. It also install some required dependencies and devDependencies to be fully operational.

```text
bluerain storybook-native:start
```

this command creates a build/storybook-native directory and generates necessary files like app.json, App.js and AppEntry.js under that directory. After it is done generating these files, it will execute the start command on expo using expo's own start command. once Expo is up & running, you will be able to run storybook on your expo app installed on your mobile device or GenyMotion.

## Customizations

#### App.js

User can add his own custom App.js under bluerain/storybook-native directory. So whenever any App.js file found under this directory, It will be the one getting used while running storybook-native:start command instead of the files generated under bluerain/storybook-native/storybook directory.

