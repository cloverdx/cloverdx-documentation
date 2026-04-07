<!-- Development > Component reference > Data Partitioning > Common properties of Data Partitioning components -->

### Common properties of Data Partitioning components

These components are dedicated to data flow management when using **Data Partitioning** or in the **CloverDX Cluster** environment.

| Component | Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [ParallelPartition](clusterpartition.md) | **✓** | **⨯** | 1 | 1[[1]](common-of-cluster-components.md#clusterpartition-fn01) | [[2]](common-of-cluster-components.md#clusterpartition-fn02) | [[2]](common-of-cluster-components.md#clusterpartition-fn02) | **✓** |
| [ParallelLoadBalancingPartition](clusterloadbalancingpartition.md) | **✓** | **⨯** | 1 | 1[[1]](common-of-cluster-components.md#clusterpartition-fn01) | **⨯** | **⨯** | **✓** |
| [ParallelSimpleGather](clustersimplegather.md) | **✓** | **⨯** | 1[[3]](common-of-cluster-components.md#clusterpartition-fn03) | 1 | **⨯** | **⨯** | **✓** |
| [ParallelMerge](clustermerge.md) | **✓** | **✓** | 1[[3]](common-of-cluster-components.md#clusterpartition-fn03) | 1 | **⨯** | **⨯** | **✓** |
| [ParallelRepartition](clusterrepartition.md) | **✓** | **⨯** | 1[[3]](common-of-cluster-components.md#clusterpartition-fn03) | 1[[1]](common-of-cluster-components.md#clusterpartition-fn01) | [[2]](common-of-cluster-components.md#clusterpartition-fn02) | [[2]](common-of-cluster-components.md#clusterpartition-fn02) | **✓** |
| [ParallelSimpleCopy](clustersimplecopy.md) | **✓** | **⨯** | 1 | 1[[1]](common-of-cluster-components.md#clusterpartition-fn01) | **⨯** | **⨯** | **✓** |

| 1 |  The single output port represents multiple virtual output ports. |
| --- | --- |

| 2 |  **ParallelPartition** and **ParallelRepartition** can use either a transformation or two other attributes (**Ranges** or **Partition key**). |
| --- | --- |

| 3 |  The single input port represents multiple virtual input ports. |
| --- | --- |
