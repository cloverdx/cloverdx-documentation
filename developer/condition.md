<!-- Development > Component reference > Job Control > Condition -->

### Condition

Jobflow Component

![Condition 64x64](../figures/Condition-64x64.png)

| [Short description](condition.md#short-description) |
| --- |
| [Ports](condition.md#ports) |
| [Metadata](condition.md#metadata) |
| [Condition attributes](condition.md#condition-attributes) |
| [Details](condition.md#details) |
| [See also](condition.md#see-also) |

#### Short description

The **Condition** component routes incoming tokens to one of its output ports based on a result of a specified condition. It is similar to `if` statement in programming languages.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| – | **⨯** | 1 | 1–2 | **⨯** | – | – | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input tokens | Any |
| Output | 0 | **✓** | For tokens compliant with the condition | Input 0 |
| 1 | **⨯** | For tokens not satisfying the condition | Input 0 |  |

#### Metadata

Metadata can be propagated through this component.

All output metadata must be the same.

This component has [metadata templates](components.md#metadata-templates) available.

#### Condition attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Condition | yes | Boolean expression according to which the tokens are filtered. Expressed as a sequence of individual expressions for individual input fields separated from each other by a semicolon. |  |

#### Details

For each incoming token, the **Condition** component evaluates a specified Boolean condition and if the result is `true`, the token is sent to the first output port, otherwise to the second (optional) output port.

**Condition** works the same way as the [**Filter**](extfilter.md) component.

For more details about the Condition attribute, see [Filter Expression](extfilter.md#details) of the **Filter** component.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job control comparison](common-of-job-control.md#job-control-comparison) |
