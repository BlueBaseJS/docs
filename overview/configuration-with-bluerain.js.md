# 🎛 Configuration with bluerain.js

All projects created by the BlueRain CLI have a `bluerain.ts` \(or `bluerain.js`\) file. This file serves as a manifest for a BlueRain project. This is where you import all your plugins, hooks, components and configurations.

Practically, this file only exports an object that has props of `BlueRainApp` component. So if you're building or compiling the project without BlueRain CLI, it possible to not have a `bluerain.ts` \(or `bluerain.js`\) file at all and just use any code structure that suits your project.

