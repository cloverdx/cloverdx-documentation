<!-- Development > Component reference > Data Partitioning > ParallelSimpleCopy -->

### ParallelSimpleCopy

![ParallelSimpleCopy 64x64](../figures/ParallelSimpleCopy-64x64.png)

| [Short description](clustersimplecopy.md#short-description) |
| --- |
| [Ports](clustersimplecopy.md#ports) |
| [Metadata](clustersimplecopy.md#metadata) |
| [Details](clustersimplecopy.md#details) |
| [Compatibility](clustersimplecopy.md#compatibility) |
| [See also](clustersimplecopy.md#see-also) |

#### Short description

**ParallelSimpleCopy** copies incoming data records to all output **CloverDX Cluster** workers. The algorithm of the component is derived from the regular [SimpleCopy](simplecopy.md) component.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| **✓** | **⨯** | 1 | 1[[1]](clustersimplecopy.md#clustersimplecopy-footnote1) | **⨯** | **⨯** | **✓** |

| 1 |  The single output port represents multiple virtual output ports. |
| --- | --- |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For output data records | Input 0 |

#### Metadata

**ParallelSimpleCopy** propagates metadata in both directions. The component does not change priorities of propagated metadata.

The component has no metadata template.

**ParallelSimpleCopy** does not require any specific metadata fields.

#### Details

**ParallelSimpleCopy** copies incoming data records to all output **CloverDX Cluster** workers. Each incoming record is duplicated and sent to all output partitions.

This component is useful whenever you need to have data available for all workers. For example, you decide to process a large number of your business transactions in a parallel way. **ParallelPartition** is the right component to split your data among several workers. Then you need to join your transactions for example with country codes, where the transactions have been performed. You need to have the list of all country codes available on all workers. Each worker can acquire the country codes individually, but if the data reading is very expensive, for example reading from a slow web service, it could be favorable to read them once and copy them among all workers using **CloverDX** functions. So you can read the country codes from a slow data source just once on a single worker and copy them to all workers using **ParallelSimpleCopy**, where they can be used to join with your transactions.

The algorithm of this component is derived from the regular [SimpleCopy](simplecopy.md) component. For more details, see the documentation of the [SimpleCopy](simplecopy.md) component.

This component belongs to a group of Cluster components that allows the change from a single-worker allocation to a multiple-worker allocation. So the allocation of the component preceding the **ParallelSimpleCopy** component has to provide just a single worker. The allocation of the component following the **ParallelSimpleCopy** component can provide multiple workers.
> [!NOTE]
> For more information about this component, see [Data partitioning in cluster](../admin/cluster-setup-index.md#cluster-introduction).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 3.4 | The component is available since version **3.4**. |
| 4.3.0-M2 | **ClusterSimpleCopy** was renamed to **ParallelSimpleCopy**. |

#### See also

| [ParallelLoadBalancingPartition](clusterloadbalancingpartition.md) |
| --- |
| [ParallelMerge](clustermerge.md) |
| [ParallelPartition](clusterpartition.md) |
| [ParallelSimpleGather](clustersimplegather.md) |
| [SimpleCopy](simplecopy.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Data Partitioning components](common-of-cluster-components.md) |
