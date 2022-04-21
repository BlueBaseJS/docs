# 3. Create Screens

## &#x20;**Create Screen**

* Create a file with (.tsx extension)  just like PendingTaskScreen.TSX
* Add your file in creating a plugin that makes it register for the navigation process

## &#x20; **Steps:**

* add routes for each screen
* then we make screens separately
* after that, we navigate our screens

### Step 1: Routes

```
import { Noop, RouteConfig } from '@bluebase/components';
import React, { useCallback } from 'react';
import { RouteOptions, useNavigation, useStyles, useTheme } from '@bluebase/core';

import { PlaceProfileSettingsButton } from '../components/exports';

export const routes = async (options: RouteOptions): Promise<RouteConfig[]> => {
	const { intl } = options;

	 return [
		// Second Screen
		{
			exact: true,
			name: 'MyPluginSecond',
			path: '1',
			screen: 'MyPluginSecondScreen',

			options: {
				title: intl.__('Second Screen'),
			},
		},
		//detailed screen
		{
			exact: true,
			name: 'Detailed',
			path: '2',
			screen: 'DetailedScreen',

			options: {
				title: intl.__('Details Screen'),
			},
		},
		//task edit screen
		{
			exact: true,
			name: 'CreateTask',
			path: '3',
			screen: 'CreateTaskScreen',

			options: {
				title: intl.__('CreateTask'),
			},
		},

		{
			exact: true,
			name: 'MyPlugin2',
			path: '4',
			screen: 'MyPluginSecondScreen',

			options: {
				title: intl.__('Edit Screen'),
			},
		},
		{
			exact: true,
			name: 'MyPlugin3',
			path: '5',
			screen: 'MyPluginSecondScreen',

			options: {
				title: intl.__('Details Screen'),
			},
		},

		// Home Page
		{
			// exact: true,
			name: 'MyPluginHome',
			path: '',
			screen: Noop,

			options: ({ route }: any) => {
				const headerRight = () => <PlaceProfileSettingsButton params={route.params} />;
				return {
					headerRight: headerRight,
					title: intl.__('Task'),
				} as any;
			},

			navigator: {
				headerMode: 'none',
				type: 'tab',
				routes: [
					{
						exact: true,
						name: 'PendingTaskScreen',
						path: 'pending',
						screen: 'PendingTaskScreen',
						navigationOptions: {
							title: 'Pending',
						},
					},
					{
						exact: true,
						name: 'CompletedTaskScreen',
						path: 'completed',
						screen: 'MyPluginHomeScreen',
						navigationOptions: {
							title: 'Done',
						},
					},
				],
			},
		},
	];
};
 

```

****

### Step 1: **Screens**

## **PendingTaskScreen.tsx**

```
import { Button, Card, CardActions, Container, Divider, List } from '@bluebase/components'; import React, { useCallback } from 'react'; import { useNavigation, useStyles, useTheme } from '@bluebase/core';
import { ViewStyle } from 'react-native';
export interface MyPluginSecondScreenStyles { root: ViewStyle; avatar: ViewStyle; }
export const MyPluginSecondScreen = (props:any) => { const { push, navigate } = useNavigation(); const { theme } = useTheme(); const {item} = props.navigation.state.params console.log(item,"navigate") const styles: MyPluginSecondScreenStyles = useStyles('MyPluginHomeScreen', {}, { root: { padding: theme.spacing.unit * 2 }, avatar: { backgroundColor: theme.palette.warning.main } });
const goToFirst = useCallback(() => {
	push('MyPluginHome');
}, [push]);

const goToHome = useCallback(() => {
	navigate('Home');
}, [navigate]);

return (
	<Container style={styles.root}>
		<Card>
			<List.Item
				left={
					<List.Avatar
						type="icon"
						icon="file"
						style={styles.avatar}
					/>
				}
				title={item.title}
				description={item.dec}
			/>
			<Divider />
			<CardActions>
				<Button
					title="First Screen"
					size="small"
					variant="outlined"
					icon={{ type: 'icon', name: 'arrow-left' }}
					onPress={goToFirst}
				/>
				<Button
					title="Home Screen"
					size="small"
					variant="outlined"
					icon={{ type: 'icon', name: 'home' }}
					onPress={goToHome}
				/>
			</CardActions>
		</Card>
	</Container>
);
};
MyPluginSecondScreen.displayName = 'MyPluginSecondScreen';
```

****

## &#x20;  **PlaceProfileSettingsButton.tsx**

1. ```
   import { useNavigation, useTheme } from '@bluebase/core';
   import { IconButton } from '@bluebase/components'; import React from 'react';
   export interface PlaceProfileSettingsButtonProps { params: any; }
   export const PlaceProfileSettingsButton = ({ params }: PlaceProfileSettingsButtonProps) => { const { theme } = useTheme(); const { push } = useNavigation(); function onSettingsPress() { return push('CreateTask', params); }
   return <IconButton name="plus" onPress={onSettingsPress} color={theme.palette.text.secondary} />;};
   ```

## **AddButtonPlaces.tsx(Navigation)**

```
import { useNavigation, useTheme } from '@bluebase/core';
import { IconButton } from '@bluebase/components'; import React from 'react';
export interface AddButtonPlaces {}
export const PlacesAppAddButton = (_props: AddButtonPlaces) => { const { theme } = useTheme(); const { navigate } = useNavigation(); function onSettingsPress() { return navigate('CreateTask'); }
return <IconButton name="plus" onPress={onSettingsPress} color={theme.palette.text.secondary} />;
};
```

![](<../../.gitbook/assets/button in header (1).png>)

## **DetailedScreen.tsx**

```
import { Button, Card, CardActions, Container, Divider, List } from '@bluebase/components'; import React, { useCallback } from 'react'; import { useNavigation, useStyles, useTheme } from '@bluebase/core';
import { ViewStyle } from 'react-native';
export const DetailedScreen = () => { const { push, navigate } = useNavigation(); const { theme } = useTheme();
console.log(navigate,"navigate") const goToFirst = useCallback(() => { push('MyPlugin3'); }, [push]);

const goToHome = useCallback(() => {
	navigate('Home');
}, [navigate]);

return (
	<Container>
		<Card>
			<Divider />

			<Divider />
			<CardActions>
				<Button
					title="First Screen"
					size="small"
					variant="outlined"
					icon={{ type: 'icon', name: 'arrow-left' }}
					onPress={goToFirst}
				/>
				<Button
					title="Home Screen"
					size="small"
					variant="outlined"
					icon={{ type: 'icon', name: 'home' }}
					onPress={goToHome}
				/>
			</CardActions>
		</Card>
	</Container>
);
};
DetailedScreen.displayName = 'DetailedScreen';
```

&#x20;                                 ![](<../../.gitbook/assets/detail screen (1).png>)

## **CreateScreen.tsx**

```
import { Button, Card, CardActions, Container, Divider, List } from '@bluebase/components'; import React, { useCallback } from 'react'; import { useNavigation, useStyles, useTheme } from '@bluebase/core';
import { ViewStyle } from 'react-native';
export interface CreateTaskScreenStyles { root: ViewStyle; avatar: ViewStyle; }
export const CreateTaskScreen = () => { const { push, navigate } = useNavigation(); const { theme } = useTheme();s
const styles: CreateTaskScreenStyles = useStyles(
	'MyPluginHomeScreen',
	{},
	{
		root: {
			padding: theme.spacing.unit * 2,
		},
		avatar: {
			backgroundColor: theme.palette.warning.main,
		},
	}
);

const goToFirst = useCallback(() => {
	push('CreateTask');
}, [push]);

const goToHome = useCallback(() => {
	navigate('Home');
}, [navigate]);

return (
	<form>
		<label>Title</label>
		<input type="text" name="name" />

		<label>Description</label>
		<input type="Description" name="Description" />

		<button>Donee</button>
	</form>
);
};
CreateTaskScreen.displayName = 'CreateTaskScreen';
```

&#x20;                                   ![](<../../.gitbook/assets/SS (1).png>)

## **DoneTaskScreen.tsx**

```
import { Card, Container, Divider, List } from '@bluebase/components'; import React, { useCallback } from 'react'; import { useNavigation, useStyles, useTheme } from '@bluebase/core';
import { ViewStyle } from 'react-native';
export interface MyPluginHomeScreenStyles { root: ViewStyle; avatar: ViewStyle; }
export const MyPluginHomeScreen = () => { const { push, navigate } = useNavigation(); const { theme } = useTheme(); function onSettingsPress() { return navigate('CreateTask'); }

const styles: MyPluginHomeScreenStyles = useStyles(
	'MyPluginHomeScreen',
	{},
	{
		root: {
			padding: theme.spacing.unit * 2,
		},
		avatar: {
			backgroundColor: theme.palette.success.main,
		},
	}
);
const goToCreateTask = useCallback(() => {
	navigate('CreateTask');
}, [navigate]);
return (
	<Container style={styles.root}>
		<Card>
			<List.Item
				left={<List.Avatar type="icon" icon="account-circle" style={styles.avatar} />}
				title="Purchase a product"
				description="purchase product which you want"
			/>
			<List.Item
				left={<List.Avatar type="icon" icon="account" style={styles.avatar} />}
				title="Add to Cart "
				description="Add that product to cart "
			/>
			<List.Item
				left={<List.Avatar type="icon" icon="file" style={styles.avatar} />}
				title="Payment method"
				description="Cash on delivery or by debit card or credit cards"
			/>
			<Divider />

			<Divider />
		</Card>
	</Container>
);
};
MyPluginHomeScreen.displayName = 'MyPluginHomeScreen';
```

&#x20;                                  ![](<../../.gitbook/assets/donescreen (1).png>)
