<!-- Development > Component reference > Joiners -->

## 39. Joiners

| [Common properties of Joiners](common-of-joiners.md) |
| --- |

**Joiners** serve to join data from more data sources according to key values.

We can distinguish **Joiners** according to how they process data. Most **Joiners** work using key values.

- Some **Joiners** read data from two or more input ports and join them according to the equality of key values.
  - [ExtHashJoin](exthashjoin.md) joins two or more data inputs according to the equality of key values.
  - [ExtMergeJoin](extmergejoin.md) joins two or more sorted data inputs according to the equality of key values.
- Other **Joiners** read data from one input port and another data source and join them according to the equality of key values.
  - [DBJoin](dbjoin.md) joins one input data source and a database according to the equality of key values.
  - [LookupJoin](lookupjoin.md) joins one input data source and a lookup table according to the equality of key values.
- One **Joiner** joins data according to the user-defined relation of key values.
  - [RelationalJoin](relationaljoin.md) joins two or more sorted data inputs according to the user-defined relation of key values (`!=`, `>`, `>=`, `<`, `<=`).
- [Combine](combine.md) joins data flows by tuples.
- [CrossJoin](crossjoin.md) creates a Cartesian product of records from connected input ports.

### See also

| [Components](components.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Transformers](transformers.md) |
