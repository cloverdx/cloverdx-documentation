<!-- Development > Component reference > Transformers > Concatenate -->

### Concatenate

![Concatenate 64x64](../figures/Concatenate-64x64.png)

| [Short description](concatenate.md#short-description) |
| --- |
| [Ports](concatenate.md#ports) |
| [Metadata](concatenate.md#metadata) |
| [Compatibility](concatenate.md#compatibility) |
| [See also](concatenate.md#see-also) |

#### Short description

**Concatenate** receives unsorted data records from multiple inputs.

It gathers input records starting with the first input port, continuing with the next one and ending with the last port. Within each input port, the records order is preserved.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| **✓** | **⨯** | 1-n | 1 | - | - | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| 1-n | **⨯** | For input data records | Input 0 |  |
| Output | 0 | **✓** | For gathered data records | Input 0 |
| 1-n | **⨯** | For gathered data records | Input 0 |  |

At least one input port has to be connected. Any other input port can be disabled (changed in **4.1.0-M1**).

#### Metadata

Metadata can be propagated through this component.

Metadata of all input ports must be the same.

#### Details

First, the component receives all of the records incoming through the first input port, sends them to all output ports and, subsequently, adds to them all of the records incoming through the next input port. If the component has more than two input ports, the records are received and sent to the output according to the order of the input ports.

If some of the input ports contain no records, such port is skipped.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.0.x | Until **4.0.x**, you can disable only the last input or output port(s) of **Concatenate**, e.g. you can disable the third and fourth input port, but you cannot disable the first one. |
| 4.1.0-M1 | You can now disable any input or output port provided there is at least one input and output port. |

#### See also

| [Merge](merge.md) |
| --- |
| [SimpleGather](simplegather.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
