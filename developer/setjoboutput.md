<!-- Development > Component reference > Job Control > SetJobOutput -->

### SetJobOutput

![SetJobOutput 64x64](../figures/SetJobOutput-64x64.png)

| [Short description](setjoboutput.md#short-description) |
| --- |
| [Ports](setjoboutput.md#ports) |
| [Metadata](setjoboutput.md#metadata) |
| [SetJobOutput attributes](setjoboutput.md#setjoboutput-attributes) |
| [See also](setjoboutput.md#see-also) |

#### Short description

The component **SetJobOutput** writes incoming records to output dictionary entries. Output dictionary entries are populated according to mapping.

First input record sets values of dictionary entries, and subsequent input records override the existing values.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | - | 1 | 0 | - | **⨯** | **✓** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For records to be written to dictionary. | Any |

#### Metadata

You can use any metadata fields.

#### SetJobOutput attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Mapping | no | This attribute specifies mapping from input record metadata to output dictionary entries. Each incoming record is processed by this mapping and its values are mapped to a dictionary. In fact, mapping attribute is a regular CTL transformation from input metadata structure to record, which represents output dictionary entries. |  |

#### See also

| [GetJobInput](getjobinput.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
