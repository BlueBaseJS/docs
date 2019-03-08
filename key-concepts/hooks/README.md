# 🚇 Filters

Filters are the backbone of BlueBase. They allows us to modify data or inject custom logic in any part of the application at runtime.

A filter can be [registered](./#registering-a-filter) by one of the methods listed below. At runtime, when a filter event is executed, each registered filter is run in the order of _priority_, and given the opportunity to modify a value by returning a new value.

BlueBase provides different lifecycle filters to the application, but a plugin may define its own filters as well.



