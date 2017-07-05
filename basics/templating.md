# Templating

If the widget is created, it will generate it's own `<div />` element in the page. If you inspect the page, you will usually recognize this as `<div id="PackageName_widget_WidgetName_XXX">`.

The root node of the widget is available in the widget as `this.domNode`.

If you want to use more complex templates, it is better to define these in a different template file. Here's how this works:

```js
define([
    "dojo/_base/declare",
    "mxui/widget/_WidgetBase",
    "dijit/_TemplatedMixin",
    "dojo/text!PackageName/templates/template.html"
], function (declare, _WidgetBase, _TemplatedMixin, template) {
    "use strict";

    return declare("packageName.widget.widgetName", [ _WidgetBase, _TemplatedMixin ], {

        templateString: template,
        /* within this object, define your methods and properties */

    });
});

require(["packageName/widget/widgetName"]);
```

- We add `dijit/_TemplatedMixin` to the dependencies.
- We add the path to template, preceded by `dojo/text!`. This will read the template file as a general text file. Note that the path can be a bit tricky. It is calculated from the root folder of the widget, which is usually the folder next to the `package.xml`.
- We make sure both dependencies are linked to a parameter, in this case `_TemplatedMixin` and `template`.
- We add the `_TemplatedMixin` as a Mixin for the package declaration, so the widget will look for a templateString
- We add the `template` as a `templateString` to the widget

Let's consider the following template:

```html
<div class="my_widget">
  <div data-dojo-attach-point="nodeTopBlock" class="my_widget__topblock"></div>
  <div data-dojo-attach-point="nodeBottom" class="my_widget__bottom"></div>
</div>
```

If we add this template to the widget, both the DOM elements are also mapped to internal variables within the widget. So in any method within the widget you can access the top block by `this.nodeTopBlock`.
