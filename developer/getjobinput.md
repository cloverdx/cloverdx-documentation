<!-- Development > Component reference > Job Control > GetJobInput -->

### GetJobInput

![GetJobInput 64x64](../figures/GetJobInput-64x64.png)

| [Short description](getjobinput.md#short-description) |
| --- |
| [Ports](getjobinput.md#ports) |
| [GetJobInput attributes](getjobinput.md#getjobinput-attributes) |
| [See also](getjobinput.md#see-also) |

#### Short description

The component **GetJobInput** retrieves requested job parameters and sends them to the output port. The component produces a single output record which is populated with a dictionary content or graph parameters.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | - | 0 | 1 | - | **⨯** | **✓** | - |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | For a record with a job input. | Any |

#### Metadata

You can use any metadata fields.

#### GetJobInput attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Mapping | no | Mapping populates the output record of the component. Input dictionary entries and graph parameters are natural input values for the mapping. In fact, a mapping attribute is a regular CTL transformation from a record which represents input dictionary entries to a record with an output metadata structure. Mapping is invoked exactly once. |  |

#### See also

| [SetJobOutput](setjoboutput.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
