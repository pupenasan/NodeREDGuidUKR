# node-red-node-ui-list

https://github.com/node-red/node-red-ui-nodes/tree/master/node-red-node-ui-list

A Node-RED widget node for showing a list of items.

![](/media/uilistexample.png)

![](/media/uilistcfg.png)

`ui-list` node is a UI widget that can be used to display a list of items in the Node-RED dashboard.

An array of Items is passed in by `msg.payload`.  It consists of objects containing the following properties.

- `title` - title of the item,
- `description` - description of the item. optional if line type is `Single-line ` or action type is `menu`,
- `icon` - URL of icon (optional),
- `icon_name` - Font Awesome 4.7 icon name (optional),
- `icon_unicode` - text to use as icon - useful for unicode symbols like flags, etc (optional).
- `menu` - list of menu items (optional).

If you just need a simple text list then `msg.payload` can be a simple array of strings, e.g. `["Item1","Item2","Item3"]`

The type of item display can be selected by `List Type` selector in the node configuration panel.

An action to be taken for a displayed item can be selected by the `Action` selector:

- `none` - No action is performed,
- `click to send an item` - sends the selected item to output port if clicked,
- `checkbox to send changed item` - sends an item to output port if checkbox is changed.  The checkbox state is included in the `isChecked` flag of the output `payload` object,
- `switch to send changed item` - sends an item to output port if switch is changed.  The switch state is included in the `isChecked` flag of the output `payload` object,
- `menu to send selected item` - sends an item to output port is item in menu is selected.  The selected item is included in the `selected` property of the output payload object.

If `Allow HTML in displayed text` checkbox is selected, HTML tags can be used in `title` and `description`.

Icon can be specified by `icon` or `icon_name` property.  `icon` specifies URL of icon image.  If `icon` is `null`, blank icon is displayed. `icon_name` specifies an icon name of Font Awesome 4.7 icons (e.g. `fa-home`). `icon_unicode` specifies text character to use as an icon, useful for displaying unicode symbols like flags, etc. `icon` has precedence over `icon_name` and `icon_unicode`.



