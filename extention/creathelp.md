# Створення власних вузлів ([Creating Nodes](https://nodered.org/docs/creating-nodes/))

## Створення першого вузлу 

# Node help style guide

When a node is selected, its help text is displayed in the info tab. This help should provide the user with all the information they need in order to use the node.

The following style guide describes how the help should be structured to ensure a consistent appearance between nodes.

------

​        This section provides a high-level introduction to the node. It should be        no more than 2 or 3 `` long. The first ``        is used as the tooltip when hovering over the node in the palette.    

Connects to a MQTT broker and publishes messages.

​        If the node has an input, this section describes the properties of the        message the node will use. The expected type of each property can also        be provided. The description should be brief - if further description is        needed, it should be in the Details section.    

### Inputs

- payload                  string | buffer              

   the payload of the message to publish. 

- topic string

   the MQTT topic to publish to.

​         If the node has outputs, as with the Inputs section, this section         describes the properties of the messages the node will send. If the node         has multiple outputs, a separate property list can be provided for each.     

### Outputs

1. Standard output                     

   - payload string

     the standard output of the command.

2. Standard error                     

   - payload string

     the standard error of the command.

This section provides more detailed information about the node. It should        explain how it should be used, providing more information on its inputs/outputs.



### Details

`msg.payload` is used as the payload of the published message.        If it contains an Object it will be converted to a JSON string before being sent.        If it contains a binary Buffer the message will be published as-is.

The topic used can be configured in the node or, if left blank, can be set by `msg.topic`.

Likewise the QoS and retain values can be configured in the node or, if left        blank, set by `msg.qos` and `msg.retain` respectively.

This section can be used to provide links to external resources, such as:

- any relevant additional documentation. Such as how the Template node links          to the Mustache language guide.
- the node's git repository or npm page - where the user can get additional help

### References

- Twitter API docs - full description of `msg.tweet` property
- GitHub - the node's github repository

------

The above example was created with the following HTML.

```
<script type="text/html" data-help-name="node-type">
<p>Connects to a MQTT broker and publishes messages.</p>

<h3>Inputs</h3>
    <dl class="message-properties">
        <dt>payload
            <span class="property-type">string | buffer</span>
        </dt>
        <dd> the payload of the message to publish. </dd>
        <dt class="optional">topic <span class="property-type">string</span></dt>
        <dd> the MQTT topic to publish to.</dd>
    </dl>

 <h3>Outputs</h3>
     <ol class="node-ports">
         <li>Standard output
             <dl class="message-properties">
                 <dt>payload <span class="property-type">string</span></dt>
                 <dd>the standard output of the command.</dd>
             </dl>
         </li>
         <li>Standard error
             <dl class="message-properties">
                 <dt>payload <span class="property-type">string</span></dt>
                 <dd>the standard error of the command.</dd>
             </dl>
         </li>
     </ol>

<h3>Details</h3>
    <p><code>msg.payload</code> is used as the payload of the published message.
    If it contains an Object it will be converted to a JSON string before being sent.
    If it contains a binary Buffer the message will be published as-is.</p>
    <p>The topic used can be configured in the node or, if left blank, can be set
    by <code>msg.topic</code>.</p>
    <p>Likewise the QoS and retain values can be configured in the node or, if left
    blank, set by <code>msg.qos</code> and <code>msg.retain</code> respectively.</p>

<h3>References</h3>
    <ul>
        <li><a>Twitter API docs</a> - full description of <code>msg.tweet</code> property</li>
        <li><a>GitHub</a> - the nodes github repository</li>
    </ul>
</script>
```

#### Section headers

Each section must be marked up with an `` tag. If the `Details` section needs sub headings, they must use `` tags.

```
<h3>Inputs</h3>
...
<h3>Details</h3>
...
 <h4>A sub section</h4>
 ...
```

#### Message properties

A list of message properties is marked up with a `` list. The list must have a class attribute of `message-properties`.

Each item in the list consists of a pair of `` and `` tags.

Each `` contains the property name and an optional `` that contains the expected type of the property. If the property is optional, the `` should have a class attribute of `optional`.

Each `` contains the brief description of the property.

```
<dl class="message-properties">
    <dt>payload
        <span class="property-type">string | buffer</span>
    </dt>
    <dd> the payload of the message to publish. </dd>
    <dt class="optional">topic
        <span class="property-type">string</span>
    </dt>
    <dd> the MQTT topic to publish to.</dd>
</dl>
```

#### Multiple outputs

If the node has multiple outputs, each output should have its own message property list, as described above. Those lists should be wrapped in a `` list with a class attribute of `node-ports`

Each item in the list should consist of a brief description of the output followed by a `` message property list.

**Note**: if the node has a single output, it should not be wrapped in such a list and just the `` used.

```
<ol class="node-ports">
    <li>Standard output
        <dl class="message-properties">
            <dt>payload <span class="property-type">string</span></dt>
            <dd>the standard output of the command.</dd>
        </dl>
    </li>
    <li>Standard error
        <dl class="message-properties">
            <dt>payload <span class="property-type">string</span></dt>
            <dd>the standard error of the command.</dd>
        </dl>
    </li>
</ol>
```

#### General guidance

When referencing a message property outside of a message property list described above, they should be prefixed with `msg.` to make it clear to the reader what it is. They should be wrapped in `` tags.

```
The interesting part is in <code>msg.payload</code>.
```

No other styling markup (e.g. ``,``) should be used within the body of the help text.

The help should not assume the reader is an experienced developer or deeply familiar with whatever the node exposes; above all, it needs to be helpful.