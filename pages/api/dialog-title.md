---
filename: /src/Dialog/DialogTitle.js
---

<!--- This documentation is automatically generated, do not try to edit it. -->

# DialogTitle



## Props

| Name | Type | Default | Description |
|:-----|:-----|:--------|:------------|
| children | Node |  | The content of the component. |
| classes | Object |  | Useful to extend the style applied to components. |
| <span style="color: #31a148">disableTypography *</span> | boolean | false | If `true`, the children won't be wrapped by a typography component. For instance, that can be useful to can render an h4 instead of a |
| theme | Object |  |  |

Any other properties supplied will be [spread to the root element](/customization/api#spread).

## CSS API

You can override all the class names injected by Material-UI thanks to the `classes` property.
This property accepts the following keys:
- `root`

Have a look at [overriding with classes](/customization/overrides#overriding-with-classes) section
and the [implementation of the component](https://github.com/callemall/material-ui/tree/v1-beta/src/Dialog/DialogTitle.js)
for more detail.

If using the `overrides` key of the theme as documented
[here](/customization/themes#customizing-all-instances-of-a-component-type),
you need to use the following style sheet name: `MuiDialogTitle`.

## Demos

- [Dialogs](/demos/dialogs)
