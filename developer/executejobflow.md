<!-- Development > Component reference > Job Control > ExecuteJobflow -->

### ExecuteJobflow

Jobflow Component

![ExecuteJobflow 64x64](../figures/ExecuteJobflow-64x64.png)

| [Short description](executejobflow.md#short-description) |
| --- |
| [Ports](executejobflow.md#ports) |
| [ExecuteJobflow attributes](executejobflow.md#executejobflow-attributes) |
| [Details](executejobflow.md#details) |
| [Best practices](executejobflow.md#best-practices) |
| [See also](executejobflow.md#see-also) |

#### Short description

**ExecuteJobflow** allows running of jobflows with user-specified settings and provides execution results and tracking details to output ports.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 0-1 | 0-2 | **✓** | **⨯** | **✓** | **✓** |

#### Ports

Please refer to [ExecuteGraph Ports](executegraph.md#ports).

#### ExecuteJobflow attributes

Please refer to [ExecuteGraph attributes](executegraph.md#executegraph-attributes).

#### Best practices
> [!TIP]
> If you drag a `.jbf` file and drop it into the jobflow pane, you will add the **ExecuteJobflow** component.

#### Details

This component works similarly to **ExecuteGraph.** See [ExecuteGraph](executegraph.md) component documentation.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
