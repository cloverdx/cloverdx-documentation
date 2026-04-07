<!-- Development > Component reference > Job Control > KillJobflow -->

### KillJobflow

Jobflow Component

![KillJobflow 64x64](../figures/KillJobflow-64x64.png)

| [Short description](killjobflow.md#short-description) |
| --- |
| [Ports](killjobflow.md#ports) |
| [KillJobflow attributes](killjobflow.md#killjobflow-attributes) |
| [Details](killjobflow.md#details) |
| [See also](killjobflow.md#see-also) |

#### Short description

**KillJobflow** aborts specified jobflows and passes their final status to the output port.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 0-1 | 0-1 | **✓** | **⨯** | **✓** | **✓** |

#### Ports

Please refer to [KillGraph ports](killgraph.md#ports).

#### KillJobflow attributes

Please refer to [KillGraph attributes](killgraph.md#killgraph-attributes).

#### Details

This component works similarly to **KillGraph**. See [KillGraph](killgraph.md#details) component documentation.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
