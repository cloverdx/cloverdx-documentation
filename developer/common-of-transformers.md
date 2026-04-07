<!-- Development > Component reference > Transformers > Common properties of Transformers -->

### Common properties of Transformers

**Transformers** have both input and output ports. They can:

- put together more data flows with the same metadata ([Concatenate](concatenate.md), [SimpleGather](simplegather.md) and [Merge](merge.md));
- remove duplicate records ([Dedup](dedup.md));
- filter data records ([Filter](extfilter.md) and [EmailFilter](emailfilter.md));
- create samples from input records ([DataSampler](datasampler.md)), sort data records ([ExtSort](extsort.md), [FastSort](fastsort.md) and [SortWithinGroups](sortwithingroups.md));
- multiply existing data flow ([SimpleCopy](simplecopy.md));
- split one data flow into more data flows ([Partition](partition.md) at all, but optionally also [Dedup](dedup.md), [Filter](extfilter.md) and [Map](reformat.md));
- intersect two data flows (even with different metadata on inputs) ([DataIntersection](dataintersection.md)), aggregate data information ([Aggregate](aggregate.md));
- and perform much more complicated transformations of data flows ([Map](reformat.md), [Denormalizer](denormalizer.md), [Normalizer](normalizer.md), [Rollup](rollup.md) and [XSLTransformer](xsltransformer.md)).

Metadata can be propagated through some of these transformers, whereas the same is not possible in such components that transform data flows in a more complicated manner. You must have the output metadata defined prior to configuring these components.

Some of these transformers use transformations that have been described above. For detailed information about how transformation should be defined, see [Defining transformations](transformations.md#defining-transformations).

- Some **Transformers** can have a transformation attribute defined, it may be optional or required. For information about transformation templates for transformations written in CTL, see [CTL templates for Transformers](ctl-templates-for-transformers.md).
- Some **Transformers** can have a transformation attribute defined, it may be optional or required. For information about transformation interfaces that must be implemented in transformations written in Java, see: [Java interfaces for Transformers](java-interfaces-for-transformers.md).

Below is an overview of all **Transformers**:

| Component | Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Aggregate](aggregate.md) | - | **⨯** | 1 | 1 | **⨯** | **⨯** | **⨯** |
| [Concatenate](concatenate.md) | **✓** | **⨯** | 1-n | 1 | **⨯** | **⨯** | **✓** |
| [DataIntersection](dataintersection.md) | **⨯** | **✓** | 2 | 3 | **✓** | **✓** | **✓** |
| [DataSampler](datasampler.md) | - | **⨯** | 1 | n | **⨯** | **⨯** | **✓** |
| [Dedup](dedup.md) | - | **✓** | 1 | 1-2 | **⨯** | **⨯** | **✓** |
| [Denormalizer](denormalizer.md) | - | **⨯** | 1 | 1 | **✓** | **✓** | **⨯** |
| [ExtSort](extsort.md) | - | **⨯** | 1 | 1-n | **⨯** | **⨯** | **✓** |
| [FastSort](fastsort.md) | - | **⨯** | 1 | 1-n | **⨯** | **⨯** | **✓** |
| [Filter](extfilter.md) | - | **⨯** | 1 | 1-2 | **⨯** | **⨯** | **✓** |
| [LoadBalancingPartition](loadbalancingpartition.md) | - | **⨯** | 1 | 1-n | **⨯** | **⨯** | **✓** |
| [Merge](merge.md) | **✓** | **✓** | 2-n | 1 | **⨯** | **⨯** | **✓** |
| [MetaPivot](metapivot.md) | - | **⨯** | 1 | 1 | **⨯** | **⨯** | **✓** |
| [Normalizer](normalizer.md) | - | **⨯** | 1 | 1 | **✓** | **✓** | **⨯** |
| [Partition](partition.md) | - | **⨯** | 1 | 1-n | [[1]](common-of-transformers.md#common-of-transformers-fn01) | [[1]](common-of-transformers.md#common-of-transformers-fn01) | **✓** |
| [Pivot](pivot.md) | - | **⨯** | 1 | 1 | **✓** | **✓** | **⨯** |
| [Map](reformat.md) | - | **⨯** | 1 | 1-n | **✓** | **✓** | **✓** |
| [Rollup](rollup.md) | - | **⨯** | 1 | 1-n | **✓** | **✓** | **⨯** |
| [SimpleCopy](simplecopy.md) | - | **⨯** | 1 | 1-n | **⨯** | **⨯** | **✓** |
| [SimpleGather](simplegather.md) | **✓** | **⨯** | 1-n | 1 | **⨯** | **⨯** | **✓** |
| [SortWithinGroups](sortwithingroups.md) | - | **✓** | 1 | 1-n | **⨯** | **⨯** | **✓** |
| [XSLTransformer](xsltransformer.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **⨯** | **⨯** |

| 1 |  **Partition** can use either a transformation or two other attributes (**Ranges** or **Partition key**). The transformation must be defined unless one of these is specified. |
| --- | --- |
