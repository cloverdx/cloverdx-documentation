<!-- Development > Component reference > Data Partitioning -->

## 44. Data Partitioning

| [Common properties of Data Partitioning components](common-of-cluster-components.md) |
| --- |

Components from this category are primarily dedicated for data flow management when using **Data Partitioning** or in **CloverDX Cluster** environment, which provides an ability of massive parallelization of data transformation processing. Each component in a transformation graph running with data partitioning enabled or in Cluster environment can be executed in multiple instances - this is called component allocation. Component allocation specifies how many instances will be executed, and where (on which Cluster nodes) will they be running. For more information, see [Data partitioning (parallel running)](parallel-running.md) or [Data partitioning in cluster](../admin/cluster-setup-index.md#cluster-introduction).

In general, data partitioning components can be divided into two sub-categories - **partitioners** and **gatherers**.

**Parallel partitioners** distribute data records from a single worker among various Cluster workers. Parallel partitioners are used to change a single-worker allocation to multiple-worker allocation.

- [ParallelPartition](clusterpartition.md) distributes data records among various workers, algorithm of the component is based on the [Partition](partition.md) component.
- [ParallelLoadBalancingPartition](clusterloadbalancingpartition.md) distributes data records among various workers, algorithm of the component is based on the [LoadBalancingPartition](loadbalancingpartition.md) component.
- [ParallelSimpleCopy](clustersimplecopy.md) copies data records among various workers, algorithm of the component is based on the [SimpleCopy](simplecopy.md) component. So incoming data is duplicated and sent to all output workers.

**Parallel gatherers** collect data records from various Cluster workers to a single worker. Parallel gatherers are actually used to change a multiple-worker allocation to single-worker allocation.

- [ParallelSimpleGather](clustersimplegather.md) gathers data records from various Cluster workers; algorithm of the component is based on the [SimpleGather](simplegather.md) component.
- [ParallelMerge](clustermerge.md) gathers data records from various Cluster workers; algorithm of the component is based on the [Merge](merge.md) component.

Out of both basic parallel component groups stands the ParallelRepartition component.

- [ParallelRepartition](clusterrepartition.md) changes partitioning of already partitioned data, data is re-partitioned. For example, if you have data already partitioned according to a key by the **ParallelPartition** component, and you would like to change the key or number of partitions, this component can do it in one step, without necessity to gather all partitioned data to a single worker (avoiding bottleneck) by a parallel gather and partition the data again according new rules by a parallel partitioner.

### See also

| [Components](components.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
