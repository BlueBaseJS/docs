# 🎣 Hooks

Hooks are the backbone of BlueBase. They allows us to modify data or inject custom logic in any part of the application at runtime.

A hook can be [registered](./#registering-a-hook) by one of the methods listed below. At runtime, when a hook event is executed, each registered hook is run in the order of _priority_, and given the opportunity to modify a value by returning a new value.

BlueBase provides different lifecycle hooks to the application, but a plugin may define its own hooks as well.



