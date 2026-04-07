<!-- Development > Component reference > Transformers > LoadBalancingPartition -->

### LoadBalancingPartition

![Partition 64x64](../figures/Partition-64x64.png)

| [Short description](loadbalancingpartition.md#short-description) |
| --- |
| [Ports](loadbalancingpartition.md#ports) |
| [Metadata](loadbalancingpartition.md#metadata) |
| [Details](loadbalancingpartition.md#details) |
| [See also](loadbalancingpartition.md#see-also) |

#### Short description

**LoadBalancingPartition** distributes incoming input data records among different output ports according to workload of downstream components.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-n | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For output data records | Input 0 |
| 1-N | **⨯** | For output data records | Input 0 |  |

#### Metadata

LoadBalancingPartition propagates metadata in both directions. LoadBalancingPartition does not change the priority of propagated metadata.

The component has no metadata template.

The component does not require any specific metadata fields.

Metadata on all output ports must be the same. Metadata name and field names may differ, but the field datatypes must correspond to each other.

#### Details

**LoadBalancingPartition** distributes incoming input data records among different output ports according to workload of all attached output components.

Each incoming record is sent to one of the attached output ports. The output port is chosen according to speed of the attached components. The component starts separate working threads for each output port, which concurrently read incoming data records from single input port and send them to dedicated output port.

Consider different edge implementations and theirs consequences for the described algorithm. For example, direct edge implementation has a cache for hundreds or even thousands of records, so a transformation processing just a small number of data records can send all incoming records to a single output branch. System thread scheduler causes all data to be processed by a single thread. In general, this component is useful in the case of a large number of data records.

If you process only several and records, it may appear that the distribution of records is not equal. It is expected behavior. The advantage of **LoadBalancingPartition** is significant if many records are processed. If you need to distribute records equally, use [Partition](partition.md).

#### See also

| [ParallelLoadBalancingPartition](clusterloadbalancingpartition.md) |
| --- |
| [Partition](partition.md) |
| [Merge](merge.md) |
| [SimpleCopy](simplecopy.md) |
| [SimpleGather](simplegather.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
