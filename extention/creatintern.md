# Створення власних вузлів ([Creating Nodes](https://nodered.org/docs/creating-nodes/))

## Створення першого вузлу 

# Internationalisation

If a node is [packaged](https://nodered.org/docs/creating-nodes/packaging) as a proper module, it can include a message catalog in order to provide translated content in the editor and runtime.

For each node identified in the module’s `package.json`, a corresponding set of message catalogs and help files can be included alongside the node’s `.js` file.

Given a node identified as:

```
"name": "my-node-module",
"node-red": {
    "myNode": "myNode/my-node.js"
}
```

The following message catalogs may exist:

```
myNode/locales/__language__/my-node.json
myNode/locales/__language__/my-node.html
```

The `locales` directory must be in the same directory as the node’s `.js` file.

The `__language__` part of the path identifies the language the corresponding files provide. By default, Node-RED uses `en-US`.

#### Message Catalog

The message catalog is a JSON file containing any pieces of text that the node may display in the editor or log in the runtime.

For example:

```
{
    "myNode" : {
        "message1": "This is my first message",
        "message2": "This is my second message"
    }
}
```

The catalog is loaded under a namespace specific to the node. For the node defined above, this catalog would be available under the `my-node-module/myNode` namespace.

The core nodes use the `node-red` namespace.

#### Help Text

The help file provides translated versions of the node’s help text that gets displayed within the Info sidebar tab of the editor.

### Using i18n messages

In both the runtime and editor, functions are provided for nodes to look-up messages from the catalogs. These are pre-scoped to the nodes own namespace so it isn’t necessary to include the namespace in the message identifier.

#### Runtime

The runtime part of a node can access messages using the `RED._()` function. For example:

```
console.log(RED._("myNode.message1"));
```

#### Status messages

If a node sends [status messages](https://nodered.org/docs/creating-nodes/status) to the editor, it should set the `text` of the status as the message identifier.

```
this.status({fill:"green",shape:"dot",text:"myNode.status.ready"});
```

There are a number of commonly used status messages in the core node-red catalog. These can be used by including the namespace in the message identified:

```
this.status({fill:"green",shape:"dot",text:"node-red:common.status.connected"});
```

#### Editor

Any HTML element provided in the node template can specify a `data-i18n` attribute to provide the message identify to use. For example:

```
<span data-i18n="myNode.label.foo"></span>
```

By default, the text content of an element is replace by the message identified. It is also possible to set attributes of the element, such as the `placeholder` of an ``:

```
<input type="text" data-i18n="[placeholder]myNode.placeholder.foo">
```

It is possible to combine these to specifiy multiple substitutions For example, to set both the title attribute and the displayed text:

```
<a href="#" data-i18n="[title]myNode.label.linkTitle;myNode.label.linkText"></a>
```

As well as the `data-i18n` attribute for html elements, all node definition functions (for example, `oneditprepare`) can use `this._()` to retrieve messages.