# 📲 Quick Start

We will use Expo CLI to create a new project and add BlueBase to it. If Expo CLI is not installed, go to the [Expo CLI Installation](https://docs.expo.dev/get-started/installation/) guide before proceeding.

### Step 1: Initialize the project

Initialize an expo app by executing following commands:

```shell
# Create a project named my-app. Select the "blank" template when prompted
expo init my-app

# Navigate to the project directory
cd my-app
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
