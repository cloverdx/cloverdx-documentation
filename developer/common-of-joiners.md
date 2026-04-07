<!-- Development > Component reference > Joiners > Common properties of Joiners -->

### Common properties of Joiners

| [Join types](join-types.md) |
| --- |
| [Slave duplicates](slave-duplicates.md) |
| [CTL templates for Joiners](ctl-templates-for-joiners.md) |
| [Java interfaces for Joiners](java-interfaces-for-joiners.md) |

**Joiners** serve to put together records with potentially different metadata according to the specified key and the specified transformation.

**Joiners** have both input and output ports. The first input port is called master (driver), the other(s) are called slave(s).

**Joiners** join records from a master port with particular records from an error port. Joiners do not join records between slave ports.

They can join records incoming through at least two input ports ([ExtHashJoin](exthashjoin.md), [ExtMergeJoin](extmergejoin.md) and [RelationalJoin](relationaljoin.md)). The others can also join records incoming through a single input port with those from a lookup table ([LookupJoin](lookupjoin.md)) or database table ([DBJoin](dbjoin.md)). In them, their slave data records are considered to be incoming through a virtual second input port.

#### Sorted or unsorted records

Two of these **Joiners** require that incoming records are sorted: [ExtMergeJoin](extmergejoin.md) and [RelationalJoin](relationaljoin.md).

#### Matching on equality and non-equality

Generally, joiners match on equality: all join key fields from a master must match the corresponding fields from a slave.

[RelationalJoin](relationaljoin.md) joins data records based on the non-equality conditions.

#### Output port for unmatched records

[DBJoin](dbjoin.md), [ExtHashJoin](exthashjoin.md), [ExtMergeJoin](extmergejoin.md) and [LookupJoin](lookupjoin.md) have optional output ports for unmatched master data records, as well.

#### Metadata

Joiners propagate metadata between a master input port and output port for unmatched records. Joiners do not propagate metadata in any other direction.

Joiners have no metadata templates.

You must assign metadata on input edges to be able to specify the transformation. The metadata on an output edge can be created and edited in a transformation editor.

#### Transformation

These components use transformations that are described in the section concerning transformers. For detailed information about how transformation should be defined, see [Defining transformations](transformations.md#defining-transformations). All transformations in **Joiners** use a common transformation template ([CTL templates for Joiners](ctl-templates-for-joiners.md)) and common Java interface ([Java interfaces for Joiners](java-interfaces-for-joiners.md)).

Here is an overview of all **Joiners**:

| Component | Same input metadata | Sorted inputs | Slave inputs | Outputs | Output for drivers without slave | Output for slaves without driver | Joining based on equality | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [Combine](combine.md) | **⨯** | **⨯** | 1–n | 1-n |  |  |  | **⨯** |
| [CrossJoin](crossjoin.md) | **⨯** | **⨯** | 0-n | 1 | **⨯** | **⨯** | **⨯** | **✓** |
| [DBJoin](dbjoin.md) | **⨯** | **⨯** | 1 (virtual) | 1-2 | **✓** | **⨯** | **✓** | **✓** |
| [ExtHashJoin](exthashjoin.md) | **⨯** | **⨯** | 1-n | 1 | **⨯** | **⨯** | **✓** | **✓** |
| [ExtMergeJoin](extmergejoin.md) | **⨯** | **✓** | 1-n | 1 | **⨯** | **⨯** | **✓** | **✓** |
| [LookupJoin](lookupjoin.md) | **⨯** | **⨯** | 1 (virtual) | 1-2 | **✓** | **⨯** | **✓** | **✓** |
| [RelationalJoin](relationaljoin.md) | **⨯** | **✓** | 1 | 1 | **⨯** | **⨯** | **⨯** | **⨯** |
