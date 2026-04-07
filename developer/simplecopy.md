<!-- Development > Component reference > Transformers > SimpleCopy -->

### SimpleCopy

![SimpleCopy 64x64](../figures/SimpleCopy-64x64.png)

| [Short description](simplecopy.md#short-description) |
| --- |
| [Ports](simplecopy.md#ports) |
| [Metadata](simplecopy.md#metadata) |
| [Details](simplecopy.md#details) |
| [See also](simplecopy.md#see-also) |

#### Short description

**SimpleCopy** copies data to all connected output ports.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-n | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For copied data records | Input 0 |
| 1-n | **⨯** | For copied data records | Output 0 |  |

#### Metadata

**SimpleCopy** propagates metadata in both directions. SimpleCopy does not change a priority of propagated metadata.

SimpleCopy does not have any **metadata template**.

SimpleCopy does not require any specific metadata fields.

Metadata on all output ports must be the same. The metadata name and field names may differ but the field datatypes must correspond to each other.

Metadata on the output port(s) can be fixed-length or mixed even when those on the input are delimited, and vice versa.

#### Details

**SimpleCopy** receives data records through the single input port and copies each of them to all connected output ports.
> [!TIP]
> You can use SimpleCopy to transform fixed length metadata to delimited metadata, and vice versa. But the number of fields and their data types must be preserved.

#### See also

| [SimpleGather](simplegather.md) |
| --- |
| [Merge](merge.md) |
| [Partition](partition.md) |
| [LoadBalancingPartition](loadbalancingpartition.md) |
| [ParallelSimpleCopy](clustersimplecopy.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
