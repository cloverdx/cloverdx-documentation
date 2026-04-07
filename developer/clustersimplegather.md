<!-- Development > Component reference > Data Partitioning > ParallelSimpleGather -->

### ParallelSimpleGather

![ParallelSimpleGather 64x64](../figures/ParallelSimpleGather-64x64.png)

| [Short description](clustersimplegather.md#short-description) |
| --- |
| [Ports](clustersimplegather.md#ports) |
| [Metadata](clustersimplegather.md#metadata) |
| [Details](clustersimplegather.md#details) |
| [Compatibility](clustersimplegather.md#compatibility) |
| [See also](clustersimplegather.md#see-also) |

#### Short description

**ParallelSimpleGather** gathers data records from multiple **CloverDX Cluster** workers. The algorithm of the component is derived from the regular [SimpleGather](simplegather.md) component.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| **✓** | **⨯** | 1[[1]](clustersimplegather.md#clustersimplegather-footnote1) | 1 | **⨯** | **⨯** | **✓** |

| 1 |  The single input port represents multiple virtual input ports. |
| --- | --- |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For gathered data records | Input 0 |

#### Metadata

**ParallelSimpleGather** propagates metadata in both directions. The component does not change priorities of propagated metadata.

**ParallelSimpleGather** has no metadata templates.

**ParallelSimpleGather** does not require any specific metadata fields.

#### Details

**ParallelSimpleGather** gathers data records from multiple **CloverDX Cluster** workers.

The algorithm of this component is derived from the regular [SimpleGather](simplegather.md) component. For more details about attributes and other component specific behavior, see the documentation of the [SimpleGather](simplegather.md) component.

This component belongs to a group of Cluster components that allows the change from a multiple-workers allocation to a single-worker allocation. So the allocation of the component preceding the **ParallelSimpleGather** component can provide multiple workers. The allocation of the component following the **ParallelSimpleGather** component has to provide a single worker.
> [!NOTE]
> For more information about this component, see [Data partitioning in cluster](../admin/cluster-setup-index.md#cluster-introduction).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 3.4 | The component is available since **3.4**. |
| 4.3.0-M2 | **ClusterSimpleGather** was renamed to **ParallelSimpleGather**. |

#### See also

| [ParallelMerge](clustermerge.md) |
| --- |
| [ParallelLoadBalancingPartition](clusterloadbalancingpartition.md) |
| [ParallelPartition](clusterpartition.md) |
| [ParallelSimpleCopy](clustersimplecopy.md) |
| [SimpleGather](simplegather.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Data Partitioning components](common-of-cluster-components.md) |
