# 🎨 Themes

The theme specifies the color of the components, darkness of the surfaces, level of shadow, appropriate opacity of ink elements, etc.

Themes let you apply a consistent tone to your app. It allows you to **customize all design aspects** of your project in order to meet the specific needs of your business or brand.

To promote greater consistency between apps, each theme has light and dark variants By default, components use the light theme type.

### Theme provider <a href="#heading-theme-provider" id="heading-theme-provider"></a>

If you wish to customize the theme, you need to use the `ThemeProvider` component in order to inject a theme into your application. However, this is optional; BlueBase components come with a default theme.

`ThemeProvider` relies on the [context feature of React](https://reactjs.org/docs/context.html) to pass the theme down to the components, so you need to make sure that `ThemeProvider` is a parent of the components you are trying to customize. ~~You can learn more about this in the API section~~.

### Custom Themes

```typescript
import { BlueBaseApp, Theme } from '@bluebase/core';
import React from 'react';

const GreenTheme = new Theme({
	key: 'green-theme',
	name: 'Green Theme',
	light: {
		palette: {
			primary: {
				main: '#00a013',
				dark: '#007d00',
				light: '#49bb47',
			},
			secondary: {
				main: '#a0008d',
				dark: '#830082',
				light: '#be5cad',
			}
		}
	},

	dark: {
		palette: {
			primary: {
				main: '#00a013',
				dark: '#007d00',
				light: '#49bb47',
			},
			secondary: {
				main: '#a0008d',
				dark: '#830082',
				light: '#be5cad',
			}
		}
	},
});

export default function App() {
	return (
		<BlueBaseApp themes={[GreenTheme]} />
	);
}
```

```
import { BlueBaseApp, Theme } from '@bluebase/core';
import React from 'react';
import GreenTheme from './theme';

export default function App() {
	return (
		<BlueBaseApp themes={[GreenTheme]} />
	);
}
```

```
import { createPlugin } from '@bluebase/core';
import GreenTheme from './theme';

export default createPlugin({
	key: 'green-theme-plugin',
	name: 'Green Theme Plugin',

	themes: [GreenTheme]
});
```



### Theme builder <a href="#heading-theme-builder" id="heading-theme-builder"></a>

The community has built great tools to build a theme:

* [mui-theme-creator](https://bareynol.github.io/mui-theme-creator/): A tool to help design and customize themes for the MUI component library. Includes basic site templates to show various components and how they are affected by the theme
* [Material palette generator](https://material.io/inline-tools/color/): The Material palette generator can be used to generate a palette for any color you input.
