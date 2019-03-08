# 🎛 Configuration with bluebase.js

All projects created by the BlueBase CLI have a `bluebase.ts` \(or `bluebase.js`\) file. This file serves as a manifest for a BlueBase project. This is where you import all your plugins, filters, components and configurations.

Practically, this file only exports an object that has props of `BlueBaseApp` component. So if you're building or compiling the project without BlueBase CLI, it possible to not have a `bluebase.ts` \(or `bluebase.js`\) file at all and just use any code structure that suits your project.

