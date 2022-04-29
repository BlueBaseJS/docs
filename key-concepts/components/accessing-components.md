# Accessing Components

## Through `resolve` method

In order to access a BlueBase component, just use the `resolve` method of Component Registry.

```typescript
const Logo = BB.Components.resolve('Logo');
```

This will return a component wrapped in all the HOCs, and will receive a `styles` prop that has all the [themed styles](../themes/customise-components.md).

But in order to get access this component in your code, you will need to use a BlueBaseConsumer component to access `BB` context first. This is how the final code may look like:

```typescript
import { BlueBase, BlueBaseConsumer } from '@bluebase/core';

const Header = () => (
    <BlueBaseConsumer>
    {(BB: BlueBase) => {
        const Logo = BB.Components.resolve('Logo');
        return <Logo />;
    }}
    </BlueBaseConsumer>
);
```

This adds unnecessarily long and repetitive code. Not to mention the overall ugliness and unreadability. To solve this problem, we export a helper function called `getComponent` .

## Through `getComponent` function

The `getComponent` function returns a component from BlueBase context. By using this function we can rewrite the example above as:

```typescript
import { getComponent } from '@bluebase/core';

const Logo = getComponent('Logo');

const Header = () => (<Logo />);
```

See how this makes the code much more developer friendly.

It is also possible to get a typed component by providing it props interface:&#x20;

```typescript
import { getComponent } from '@bluebase/core';

interface LogoProps {
    // ... props
}

const Logo = getComponent<LogoProps>('Logo');
```

To make it even more convenient, we export some basic components out of box. This helps developers not only write even less code, but also port react-native apps to BlueBase by just changing the import statement.

```diff
- import { Image, Text, View } from 'react-native';
+ import { Image, Text, View } from '@bluebase/components';
```

## Fallback Components

Sometimes, you may need to have fallback components. So if they desired component is not found, a back up component can be used. In BlueBase it is very easy to achieve this. Just provide multiple arguments to the resolve function.&#x20;

```typescript
const Logo = BB.Components.resolve('AnimatedLogo', 'SingleColorLogo', 'Logo');
```

The first param acts as the key of the desired, with the following ones acting at fallback components in sequence.

So in the example above, first BlueBase will try to find `AnimatedLogo` . If it doesn't exist, BlueBase will look for `SingleColorLogo` . If even that isn't found, it will try to get `Logo` component.

This works with the `getComponent` function. So the code above can be written as:

```typescript
const Logo = getComponent('AnimatedLogo', 'SingleColorLogo', 'Logo');
```

## Accessing Raw Components

As explained in the above, the resolve method returns a component wrapped in the registered HOCs, and styles. But sometimes, you may need to access the raw component that was originally registered.

For that reason, BlueRain provides a `getValue` method that lets you access the unwrapped “raw” component.

```typescript
const rawLogoComponent = await BB.Components.getValue('Logo');
```

Note that, we used the `await` keyword. This is because the getValue method will return the component wrapped in a promise. This is because some components may in different bundles (because of code splitting).
