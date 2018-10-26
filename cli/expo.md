---
description: >-
  Expo is a development tool for Mobile specific Apps using React and React
  Native. BlueBase Cli v4 has it's own builtin commands that integrate Expo
  within itself.
---

# Expo

## Installation

First of all @blueeast/bluerain-cli-expo plugin must be installed using globally installed bluerain-cli by executing the following commands in your terminal.

```text
bluerain plugins:add @blueeast/bluerain-cli-expo
```

This will install the latest Expo Plugin for global usage and will install the necessary dependencies to run expo on your system.

## Usage

After done setting up this plugin. You can go ahead and utilize this cli feature in your newly created or already existing project using BlueBase.

```text
bluerain expo:init
```

Let's start with the init command. This command makes your project ready to be used using expo. It initializes basic bluerain/expo \(configuration\) and assets/expo \(images, icons etc\) needed to get your app up and running. It also install some required dependencies and devDependencies to be fully operational.

```text
bluerain expo:start
```

this command creates a build/expo directory and generates necessary files like app.json, App.js and AppEntry.js under that directory. After it is done generating these files, it will execute the start command on expo using expo's own start command. once Expo is up & running, you will be able to see a QR code and some other options to get you along with expo. you need to install Expo App on your remote android/ iOS device or simulator like GenyMotion and follow the procedure given on expo official docs to pursue with it.

## Build

Once you are done creating your app & you have tested your app on expo in production mode and is fully functional, You can go ahead and generate an installation file of your app for your android/ iOS device using following commands:-

for Android.

```text
bluerain expo:build:android
```

for iOS

```text
bluerain expo:build:ios
```

These commands will instantiate expo's own build commands. Follow up the official expo build procedure and you will end up having apk \(for android\) and ipa \(for iOS\) installation files ready to be loaded in your device.

