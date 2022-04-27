# Settings & Configurations

@bluebase/plugin-config-persist

@bluebase/plugin-apollo-cache-persist





Let's go back to our TaskList component from [Chapter 4.2](../4.-building-ui/4.1-creating-task-list.md).

```typescript
import { QueryResult } from '@apollo/client';
import { Divider } from '@bluebase/components';
import { getComponent } from '@bluebase/core';
import { GraphqlConnection, GraphqlListProps } from '@bluebase/plugin-json-graphql-components';
import React from 'react';
import { ListRenderItemInfo } from 'react-native';

import { Tasks, TasksCollectionQueryQuery, TasksCollectionQueryQueryVariables } from '../../graphql-types';
import TaskListEmptyState from '../TaskListEmptyState';
import { TaskListItem, TaskListItemProps } from '../TaskListItem';
import { TasksCollectionQuery, TasksCollectionQueryUpdateQueryFn } from './TasksCollectionQuery.graphql';

const GraphqlList = getComponent<GraphqlListProps<TaskListItemProps, TasksCollectionQueryQuery>>('GraphqlList');

function mapQueryResultToConnection(result: QueryResult<TasksCollectionQueryQuery>) {
	return result.data?.tasksCollection as GraphqlConnection<Tasks>;
}

function renderItem({ item }: ListRenderItemInfo<TaskListItemProps>) {
	return <TaskListItem {...item} />;
}

const renderDivider = () => <Divider inset />;

export interface TaskListProps {
	completed: boolean;
}

export const TaskList = (props: TaskListProps) => {
	const { completed } = props;
	const itemsPerPage = 10;

	const variables: TasksCollectionQueryQueryVariables = {
		filter: {
			completed: { 'eq': completed }
		}
	};

	return (
		<GraphqlList
			key="task-list"
			pagination="infinite"
			itemsPerPage={itemsPerPage}
			query={TasksCollectionQuery}
			updateQueryInfinitePagination={TasksCollectionQueryUpdateQueryFn}
			mapQueryResultToConnection={mapQueryResultToConnection}
			renderItem={renderItem}
			ItemSeparatorComponent={renderDivider}
			ListEmptyComponent={TaskListEmptyState}
			queryOptions={{
				variables
			}}
		/>
	);
};

TaskList.displayName = 'TaskList';
```

Change line number from:

```
const itemsPerPage = 10;
```

To:

```
const [itemsPerPage] = useConfig('tasks.itemsPerPage');
```

Final result:

```
import { QueryResult } from '@apollo/client';
import { Divider } from '@bluebase/components';
import { getComponent, useConfig } from '@bluebase/core';
import { GraphqlConnection, GraphqlListProps } from '@bluebase/plugin-json-graphql-components';
import React from 'react';
import { ListRenderItemInfo } from 'react-native';

import { Tasks, TasksCollectionQueryQuery, TasksCollectionQueryQueryVariables } from '../../graphql-types';
import TaskListEmptyState from '../TaskListEmptyState';
import { TaskListItem, TaskListItemProps } from '../TaskListItem';
import { TasksCollectionQuery, TasksCollectionQueryUpdateQueryFn } from './TasksCollectionQuery.graphql';

const GraphqlList = getComponent<GraphqlListProps<TaskListItemProps, TasksCollectionQueryQuery>>('GraphqlList');

function mapQueryResultToConnection(result: QueryResult<TasksCollectionQueryQuery>) {
	return result.data?.tasksCollection as GraphqlConnection<Tasks>;
}

function renderItem({ item }: ListRenderItemInfo<TaskListItemProps>) {
	return <TaskListItem {...item} />;
}

const renderDivider = () => <Divider inset />;

export interface TaskListProps {
	completed: boolean;
}

export const TaskList = (props: TaskListProps) => {
	const { completed } = props;
	const [itemsPerPage] = useConfig('tasks.itemsPerPage');

	const variables: TasksCollectionQueryQueryVariables = {
		filter: {
			completed: { 'eq': completed }
		}
	};

	return (
		<GraphqlList
			key="task-list"
			pagination="infinite"
			itemsPerPage={itemsPerPage}
			query={TasksCollectionQuery}
			updateQueryInfinitePagination={TasksCollectionQueryUpdateQueryFn}
			mapQueryResultToConnection={mapQueryResultToConnection}
			renderItem={renderItem}
			ItemSeparatorComponent={renderDivider}
			ListEmptyComponent={TaskListEmptyState}
			queryOptions={{
				variables
			}}
		/>
	);
};

TaskList.displayName = 'TaskList';

```



```
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

	defaultConfigs: {
		'tasks.itemsPerPage': 10,
	}
});

```

![](<../../.gitbook/assets/Screenshot 2022-04-25 at 8.22.21 PM.png>)

Now add your own config:

```
export const configs = {

	'tasks.itemsPerPage': 5,

	// ... other configs
};

```

![](<../../.gitbook/assets/Screenshot 2022-04-25 at 8.24.05 PM.png>)

{% code title="src/components/TaskSettingsForm/TaskSettingsForm.tsx" %}
```
import { getComponent, useConfig } from '@bluebase/core';
import { JsonFormProps } from '@bluebase/plugin-json-schema-components';
import { FormikHelpers } from 'formik';
import React from 'react';

interface TaskSettingsFormValues {
	itemsPerPage: number;
}

const JsonForm = getComponent<JsonFormProps<TaskSettingsFormValues>>('JsonForm');

export interface TaskSettingsFormProps {}

export const TaskSettingsForm = (props: TaskSettingsFormProps) => {
	const [itemsPerPage, setItemsPerPage] = useConfig('tasks.itemsPerPage');

	return (
		<JsonForm
			{...props}
			schema={{
				validateOnBlur: false,
				validateOnChange: false,

				fields: [
					{
						autoFocus: true,
						label: 'Items per page',
						name: 'itemsPerPage',
						required: true,
						type: 'number',
					},
					{
						schema: { component: 'Divider' },
						type: 'component',
					},
					{
						direction: 'right',
						name: 'form-actions',
						type: 'inline',

						fields: [
							{
								name: 'reset',
								type: 'reset',
							},
							{
								name: 'submit',
								title: 'Save',
								type: 'submit',
							},
						],
					},
				],

				initialValues: {
					itemsPerPage,
				},

				onSubmit: (values: TaskSettingsFormValues, helpers: FormikHelpers<TaskSettingsFormValues>) => {
					const { setSubmitting } = helpers;
					setItemsPerPage(values.itemsPerPage);

					// Wait one second and then setSubmitting to false
					setTimeout(() => setSubmitting(false), 1000);
				}
			}}
		/>
	);
};

TaskSettingsForm.displayName = 'TaskSettingsForm';
```
{% endcode %}

{% code title="src/components/TaskSettingsForm/index.ts" %}
```
export * from './TaskSettingsForm';

import { TaskSettingsForm } from './TaskSettingsForm';
export default TaskSettingsForm;
```
{% endcode %}

{% code title="src/filter.ts" %}
```
import { SettingsPageProps } from '@bluebase/plugin-settings-app';

import TaskSettingsForm from './components/TaskSettingsForm';

export const filters = {
	'bluebase.plugin.setting-app.pages': [
		{
			key: 'bluebase-settings-todo-page',
			priority: 20,

			value: (pages: SettingsPageProps[]) => [
				{
					name: 'TaskSettings',
					path: 'task',

					options: {
						drawerIcon: { type: 'icon', name: 'checkbox-multiple-marked' },
						title: 'Tasks',
					},

					items: [
						{
							name: 'task-settings',
							component: TaskSettingsForm,
							title: 'Task Settings',
							description: 'Configure your tasks',
						},
					],
				},
				...pages,
			],
		},
	],
};
```
{% endcode %}

```
import { createPlugin } from '@bluebase/core';

import { ToDoAppIcon } from './components/ToDoAppIcon';
import { filters } from './filters';
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
		...filters,
		...lang,
	},

	defaultConfigs: {
		'tasks.itemsPerPage': 10,
	}
});

```

![](<../../.gitbook/assets/Screenshot 2022-04-25 at 8.56.01 PM.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-25 at 8.53.11 PM.png>)

