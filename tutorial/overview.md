# Overview

Bluebase applications are based on modular approach exhibiting the cocept of 'Plug n Play'. Every feature is imported as a separate module (plugin) which makes Bluebase a pluggable and modular system. 

A plugin represents an indepedent module which acts as an add-on in a host program. For bluebase, all plugins are injected in one host program. This approach provides a better architecture in terms of reusability and modularity. We can add or modify any feature (plugin) anytime dependimg upon desired requirements.
Bluebase is capable to run apps on mobile, web and desktop using its platform specific plugins. Its project structure consists of a bluebase.ts file which consists a list of all the imports of plugins, filters,configs and components which will be required within the entire project. This file exports an object called BlueBaseApp and can be accessed anywhere in the application. It can be added as a top most component or as an embeded component within a project making it a pluggable system.

