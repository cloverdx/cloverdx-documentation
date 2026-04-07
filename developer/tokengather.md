<!-- Development > Component reference > Job Control > TokenGather -->

### TokenGather

Jobflow Component

![SimpleGather 64x64](../figures/SimpleGather-64x64.png)

| [Short description](tokengather.md#short-description) |
| --- |
| [Ports](tokengather.md#ports) |
| [Metadata](tokengather.md#metadata) |
| [Details](tokengather.md#details) |
| [See also](tokengather.md#see-also) |

#### Short description

**TokenGather** copies each incoming token from any input port to all connected output ports. If input metadata differs from output metadata, copying based on field names is used. This component is typically used to collect all tokens from several parallel execution branches and send them to one unified output.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 1-n | 1-n | - | - |  |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0-n | at least one | For incoming tokens. | Any |
| Output | 0-n | at least one | For gathered tokens. | Any[[1]](tokengather.md#tokengather-ports-fn01) |

| 1 |  Only fields with identical names with input fields are populated. |
| --- | --- |

#### Metadata

This component has [metadata templates](components.md#metadata-templates) available.

#### Details

The **TokenGather** component receives incoming tokens from any input port and copies them to all connected output ports - each incoming token is copied to all output ports. Input ports and output ports can have any metadata. Copying from input metadata to output metadata is based on field names - a field value is moved to output token if and only if output token has a field with an identical name.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
