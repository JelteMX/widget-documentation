# Minified libraries

## Problem

Minified libraries pose a problem in custom widget, because they lead to a lot of white pages, without a warning. Usually it works locally, even gets through 'Check widgets', only to silently fail in the cloud. The reason for this might not be clear, it has to do with the way Mendix bundles widgets.

When a bundle is created, Dojo Build (which can be found in your Mendix installation folders) is triggered through Grunt. The build task is pretty straightforward:

- Take all Javascript files I can find in the widget
- Check per file if it starts with `define`
- If so, add this to `widgets.js`:

```javascript
'Path/to/your/library': function() {
  /* Code from your widget */
}
```

- If not, add this to `widgets.js`:

```javascript
'Path/to/your/library': function(){
// wrapped by build app
define(["dojo","dijit","dojox"], function(dojo,dijit,dojox){
  /* Code from your widget */
})
}
```

Although this should work fine, in reality this creates problems. So this is the first step in hunting down issues.

## Solution

A lot of libraries nowadays are build using Webpack. Webpack will bundle everything into 1 library file, but it has a UMD structure. The way to fix this is two-fold:

- Set the `output` in the webpack config to `amd`
- Make sure the code does not have comments at the start. When you use copyrighted material (libraries) and want to keep the comments in there, make sure to move them to the end of the file.
