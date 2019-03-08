# 🎡 Lifecycle Events

## BlueBase Boot Lifecycle Events

* **`bluebase.boot`** **Internal Filter:** `bluebase-boot-default` _\(Priority = 5\)_  
  * bluebase.boot.start
    * bluebase.components.register.internal
  * bluebase.configs.load
  * bluebase.components.register
  * bluebase.filters.register
  * bluebase.routes.register
  * bluebase.plugins.register
  * bluebase.plugins.initialize.all
    * bluebase.plugins.initialize
  * bluebase.boot.end

|  |  |
| :--- | :--- |
|  |  |

