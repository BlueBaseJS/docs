# Translations



![](<../../.gitbook/assets/Screenshot 2022-04-24 at 11.35.58 PM.png>) ![](<../../.gitbook/assets/Screenshot 2022-04-24 at 11.36.21 PM.png>)

{% code title="configs.ts" %}
```typescript
export const configs = {

	'locale.options': {
		en: 'English',
		ur: 'اُردُو',
	},

	// ... Other configs
};
```
{% endcode %}

![](<../../.gitbook/assets/Screenshot 2022-04-24 at 11.35.26 PM.png>) ![](<../../.gitbook/assets/Screenshot 2022-04-24 at 11.35.29 PM.png>)



{% code title="" %}
```typescript
import { ComponentState, ComponentStateProps } from '@bluebase/components';
import { useIntl, useNavigation } from '@bluebase/core';
import React, { useCallback } from 'react';

export interface TaskListEmptyStateProps extends ComponentStateProps {}

export const TaskListEmptyState = (props: TaskListEmptyStateProps) => {
	const { __ } = useIntl();
	const { navigate } = useNavigation();

	const goToCreate = useCallback(() => navigate('CreateTask'), []);

	return (
		<ComponentState
			title={__('No tasks')}
			imageProps={{ resizeMode: 'contain' }}
			description={__('Start by creating a new task')}
			imageSource="TaskListEmptyImage"
			actionTitle={__('Create Task')}
			actionOnPress={goToCreate}
			actionProps={{ size: 'small', color: 'success', variant: 'outlined' }}
			{...props}
		/>
	);
};

TaskListEmptyState.displayName = 'TaskListEmptyState';
```
{% endcode %}

{% code title="" %}
```typescript
import { IntlMessages } from '@bluebase/core';

export const ur = (messages: IntlMessages) => ({
	...messages,

	'Title': 'عنوان',
	'Description': 'تفصیل',
	'Pending': 'زیر التواء',
	'Completed': 'مکمل',

	'Tasks': 'کام',
	'My Tasks': 'میری ٹاسکس',
	'No tasks': 'کوئی کام نہیں',
	'Start by creating a new task': 'ایک نیا کام بنا کر شروع کریں۔',
	'Create Task': 'ٹاسک بنائیں',
	'Edit Task': 'ٹاسک ترمیم کریں',
	'Update Task': 'ٹاسک تدوین کریں',
});

export default ur;
```
{% endcode %}

{% code title="" %}
```typescript
import { ur } from './ur';

export const lang = {
	'bluebase.intl.messages.ur': ur,
};

```
{% endcode %}

{% code title="" %}
```typescript
import { createPlugin } from '@bluebase/core';

import { ToDoAppIcon } from './components/ToDoAppIcon';
import { lang } from './lang';
import { routes } from './routes';
import { screens } from './screens';

export default createPlugin({
	key: 'tasks',
	name: 'Tasks',
	description: 'A todo app made with BlueBase framework.',

	components: {
		// Components
		ToDoAppIcon,

		// Screens
		...screens,
	},

	icon: {
		component: 'ToDoAppIcon',
		type: 'component',
	},

	indexRoute: 'TasksApp',

	routes,

	filters: {
		...lang,
	},
});

```
{% endcode %}

![](<../../.gitbook/assets/Screenshot 2022-04-24 at 11.36.42 PM.png>) ![](<../../.gitbook/assets/Screenshot 2022-04-24 at 11.36.53 PM.png>)
