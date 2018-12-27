# 📲 Quick Start

## Install BlueBase CLI

The first step to get started is to install BlueBase CLI as a global dependency.

```text
yarn global add @bluebase/cli
```

## Install Target Platform CLI Plugin

Next, you need to install the desired target platform plugin of BlueBase CLI. This plugin adds commands to the CLI that can perform platform specific tasks \(i.e. start project in development mode, build project, etc\).

{% tabs %}
{% tab title="Web" %}
```text
bluebase plugins:add @bluebase/cli-web
```
{% endtab %}

{% tab title="Expo \(iOS & Android\)" %}
```bash
bluebase plugins:add @bluebase/cli-expo
```
{% endtab %}

{% tab title="Electron \(Windows, Linux & macOS\)" %}
```text
bluebase plugins:add @bluebase/cli-electron
```
{% endtab %}
{% endtabs %}

## Start Project

Start the project in development mode.

{% tabs %}
{% tab title="Web" %}
```text
bluebase web:start
```
{% endtab %}

{% tab title="Expo \(iOS & Android\)" %}
```bash
bluebase expo:start
```
{% endtab %}

{% tab title="Electron \(Windows, Linux & macOS\)" %}
```text
bluebase electron:start
```
{% endtab %}
{% endtabs %}

