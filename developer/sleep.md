<!-- Development > Component reference > Job Control > Sleep -->

### Sleep

![Sleep 64x64](../figures/Sleep-64x64.png)

| [Short description](sleep.md#short-description) |
| --- |
| [Ports](sleep.md#ports) |
| [Metadata](sleep.md#metadata) |
| [Sleep attributes](sleep.md#sleep-attributes) |
| [Details](sleep.md#details) |
| [Examples](sleep.md#examples) |
| [Best practices](sleep.md#best-practices) |
| [See also](sleep.md#see-also) |

#### Short description

**Sleep** slows down data records going through it.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 0-1 | 1-n | **✓** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records. | Any |
| Output | 0 | **✓** | For copied data records. | Input 0 |
| 1-n | **⨯** | For copied data records. | Input 0 |  |

#### Metadata

All metadata must be the same.

Metadata can be propagated through this component.

#### Sleep attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Delay | [[1]](sleep.md#sleep-attributes-fn01) | Delay of processing of each input record; by default in milliseconds, but other [time units](components.md#time-intervals) may be used. Total delay of parsing is equal to this value multiplied by the number of input records. | 0-N or [time units](components.md#time-intervals) |
| Input mapping | [[1]](sleep.md#sleep-attributes-fn01) | Delay for input records processing can be also defined dynamically. You can determine how long should a record be delayed based on an incoming record content. So delay can be dynamically changed by your CTL code. Possible outputs of the mapping are two different values - string value **delay**, which can be populated by a same value as the component’s attribute Delay, for example '15s'. The second output value **delayMillis** can specify delay by number of milliseconds. | CTL code |

| 1 | One of these must be specified. |
| --- | --- |

#### Details

**Sleep** receives data records through its single input port, delays each input record by a specified number of milliseconds and copies each input record to all connected output ports. Total delay does not depend on the number of output ports. It only depends on the number of input records.

The delay can be specified statically by the **Delay** attribute or dynamically based on an incoming record content in the **Input mapping** attribute.

#### Examples

| [Constant delay](sleep.md#constant-delay) |
| --- |
| [Variable delay](sleep.md#variable-delay) |

##### Constant delay

This example shows the way to wait for a specific unit of time before each record.

Use **Sleep** to wait 2 seconds before each record.

###### Solution

Connect the input and output edge to **Sleep** and configure the component.

| Attribute | Value |
| --- | --- |
| Delay (ms) | 2s |

##### Variable delay

This example shows the way to use variable delay in **Sleep**. The delay is received from input edge.

Delay each record. The delay (in milliseconds) is received from the input edge in field `delay` (long).

###### Solution

Connect input and output edge to the component. The input edge contains field `delay`.

| Attribute | Value |
| --- | --- |
| Input mapping | ```ctl function integer transform() {     $out.0.delayMillis = $in.0.delay;      return ALL; } ``` |

#### Best practices

When using **Sleep**, remember that records are sent out from the component only after its buffer gets full (by default). Sometimes you might need to:

1. send a record to **Sleep**
2. have it delayed by a specified number of seconds
3. send this very record to output ports immediately

In such a case, you have to change settings of the edge outgoing from **Sleep** to **Direct fast propagate**. For more information, see [Types of edges](edge.md#types-of-edges).
> [!TIP]
> An unconnected **Sleep** component can be used to insert a pause between different phases of a graph. Put an extra phase between the two phases with single unconnected Sleep component.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
