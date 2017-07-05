# AMD structure

A Mendix widget follows a certain structure, called AMD ([Asynchronous Module Definition](https://github.com/amdjs/amdjs-api/blob/master/AMD.md)). All widgets since Mendix 5.18 should follow the following pattern:

```js
define([
    "dojo/_base/declare",
    "mxui/widget/_WidgetBase"
], function (declare, _WidgetBase) {
    "use strict";

    return declare("packageName.widget.widgetName", [ _WidgetBase], {

        /* within this object, define your methods and properties */

    });
});

require(["packageName/widget/widgetName"]);
```

The `define` and `declare` are mandatory, the `require` is there for Mendix 5 compatibility.
