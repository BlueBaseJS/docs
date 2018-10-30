# 📲 Quick Start

## Install BlueRain CLI

The first step to get started is to install BlueRain CLI as a global dependency.

```text
yarn global add @blueeast/bluerain-cli
```

## Install Target Platform CLI Plugin

Next, you need to install the desired target platform plugin of BlueRain CLI. This plugin adds commands to the CLI that can perform platform specific tasks \(i.e. start project in development mode, build project, etc\).

{% tabs %}
{% tab title="Web" %}
```text
bluerain plugins:add @blueeast/bluerain-cli-web
```
{% endtab %}

{% tab title="Expo \(iOS & Android\)" %}
```bash
bluerain plugins:add @blueeast/bluerain-cli-expo
```
{% endtab %}

{% tab title="Electron \(Windows, Linux & macOS\)" %}
```text
bluerain plugins:add @blueeast/bluerain-cli-electron
```
{% endtab %}
{% endtabs %}

## Start Project

Start the project in development mode.

{% tabs %}
{% tab title="Web" %}
```text
bluerain web:start
```
{% endtab %}

{% tab title="Expo \(iOS & Android\)" %}
```bash
bluerain expo:start
```
{% endtab %}

{% tab title="Electron \(Windows, Linux & macOS\)" %}
```text
bluerain electron:start
```
{% endtab %}
{% endtabs %}



