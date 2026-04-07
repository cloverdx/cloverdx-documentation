<!-- Development > Component reference > Transformers -->

## 37. Transformers

| [Common properties of Transformers](common-of-transformers.md) |
| --- |

**Transformers** are intermediate nodes of the graph.

**Transformers** receive data through the connected input port(s), process it in the user-specified way and send it out through the connected output port(s).

We can distinguish **Transformers** according to what they can do.

- One **Transformer** only copies each input data to all connected outputs.
  - [SimpleCopy](simplecopy.md) copies each input data record to all connected output ports.
- One **Transformer** passes only some input records to the output.
  - [DataSampler](datasampler.md) passes some input records to the output based on one of the selected filtering strategies.
- One **Transformer** removes duplicate data records.
  - [Dedup](dedup.md) removes duplicate data. Duplicate data can be sent out through the optional second output port.
- Other components filter data according to the user-defined conditions:
  - [Filter](extfilter.md) compares data with the user-defined condition and sends out records matching this condition. Data records not matching the condition can be sent out through the optional second output port.
- Other **Transformer** sort data each in different way:
  - [ExtSort](extsort.md) sorts input data;
  - [FastSort](fastsort.md) sorts input data faster than **ExtSort**;
  - [SortWithinGroups](sortwithingroups.md) sorts input data within groups of sorted data.
- One **Transformer** is able to aggregate information about data:
  - [Aggregate](aggregate.md) aggregates information about input data records.
- One **Transformer** distributes input records among connected output ports:
  - [Partition](partition.md) distributes individual input data records among different connected output ports;
  - [LoadBalancingPartition](loadbalancingpartition.md) distributes incoming input data records among different output ports according workload of downstream components.
- One **Transformer** receives data through two input ports and sends it out through three output ports. Data contained in the first port only, in both ports, or in the second port go to corresponding output port.
  - [DataIntersection](dataintersection.md) intersects sorted data from two inputs and sends it out through three connected output ports as defined by the intersection.
- Other **Transformers** can receive data records from multiple input ports and send them all through the unique output port:
  - [Concatenate](concatenate.md) receives data records with the same metadata from one or more input ports, puts them together and sends them out through the unique output port. Data records from each input port are sent out after all data records from previous input ports;
  - [SimpleGather](simplegather.md) receives data records with the same metadata from one or more input ports, puts them together, and sends them out through the unique output port as fast as possible
  - [Merge](merge.md) receives sorted data records with the same metadata from two or more input ports, sorts them all, and sends them out through the unique output port.
- Other **Transformers** receive data through connected input port, process it in the user-defined way and send it out through the connected output port(s).
  - [Denormalizer](denormalizer.md) creates single output data record from a group of input data records.
  - [Pivot](pivot.md) is a simple form of Denormalizer which creates a pivot table, summarizing input records.
  - [Normalizer](normalizer.md) creates one or more output data record(s) from a single input data record.
  - [MetaPivot](metapivot.md) works similarly to Normalizer, but it always performs the same transformation and the output metadata is fixed to data types.
  - [Map](reformat.md) processes input data in the user-defined way. Can distribute output data records among different or all connected output ports in the user-defined way.
  - [Rollup](rollup.md) processes input data in the user-defined way. Can create a number of output records from another number of input records. Can distribute output data records among different or all connected output ports in the user-defined way.
  - [DataSampler](datasampler.md) passes only some input records to the output. You can select from one of the available filtering strategies that suits your needs.
- One **Transformer** can transform input data using stylesheets.
  - [XSLTransformer](xsltransformer.md) transforms input data using stylesheets.

### See also

| [Components](components.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Joiners](joiners.md) |
