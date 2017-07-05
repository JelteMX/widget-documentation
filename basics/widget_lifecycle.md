# Widget lifecycle

A Mendix widget is a [Dojo Widget](https://dojotoolkit.org/reference-guide/1.10/dijit/_WidgetBase.html) which has a few extra's on top of the WidgetBase. The following methods are used in a Mendix Widget in the lifecycle:

- **constructor**

The **constructor** method is rarely used, will be called before the parameters are mixed into the widget. In this stage it does not have the values that are set in the Modeler. It does not even have an ID.

- **postCreate**

This stage is where the initialization of the widget begins and is usually reserved for initial setup of the widget. Event handlers are being set up.

- **update**

Client reference: [update](https://apidocs.mendix.com/7/client/mxui_widget__WidgetBase.html#update)

This method forms the heart of the widget. The update method always has the following structure:

```js
  update: function (mxObject, callback) {}
```

The `mxObject` can either be an [MxObject](https://apidocs.mendix.com/7/client/mendix_lib_MxObject.html) or null. Typically, when the widget is used in a context (e.g. Data View), the `mxObject` will be the context object.

The `callback` is rather important, something that is overlooked in a lot of instances. The `update` method is called by the client to notify the widget it has an updated context. The update method is also called at the initial load of the page.

If the `update` method receives a `callback`, this function **must** be executed. This lets the client know the widget has finished rendering. If you fail to execute the callback, it will stay on a loading indicator.

- **uninitialize**

Uninitialize is called when the widget is to be destroyed. Typically, event handlers that are associated with elements within the widget don't have have to be removed. Yet, event handlers that could exist, even when the widget is destroyed, should be removed. In older (<6) versions of Mendix we also do `mx.data.release`, see an example [here](https://github.com/mendix/ChartJS/blob/master/src/ChartJS/widgets/Core.js#L270)
