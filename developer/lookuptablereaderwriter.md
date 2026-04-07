<!-- Development > Component reference > Others > LookupTableReaderWriter -->

### LookupTableReaderWriter

![LookupTableReaderWriter 64x64](../figures/LookupTableReaderWriter-64x64.png)

| [Short description](lookuptablereaderwriter.md#short-description) |
| --- |
| [Ports](lookuptablereaderwriter.md#ports) |
| [LookupTableReaderWriter attributes](lookuptablereaderwriter.md#lookuptablereaderwriter-attributes) |
| [Details](lookuptablereaderwriter.md#details) |
| [See also](lookuptablereaderwriter.md#see-also) |

#### Short description

**LookupTableReaderWriter** reads data from a lookup table and/or writes it to a lookup table.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs[[1]](lookuptablereaderwriter.md#lookuptablereaderwriter-footnote1) | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 0-1 | 0-n | **✓** | **⨯** | **⨯** | **✓** |

| 1 |  Component sends each data record to all connected output ports. |
| --- | --- |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](lookuptablereaderwriter.md#lookuptablereaderwriter-ports-fn01) | For data records to be written to a lookup table | Any |
| Output | 0-n | [[1]](lookuptablereaderwriter.md#lookuptablereaderwriter-ports-fn01) | For data records to be read from a lookup table | Input 0[[1]](lookuptablereaderwriter.md#lookuptablereaderwriter-ports-fn01) |

| 1 |  At least one of them has to be connected. If the input port is connected, the component receives data through it and writes it to the lookup table. If an output port is connected, the component reads data from the lookup table and sends it out through this port. |
| --- | --- |

If the input port is connected and the component cannot write into the **Lookup table** (see [LookupTableReaderWriter attributes](lookuptablereaderwriter.md#lookuptablereaderwriter-attributes)) you have specified, an error will be shown.
> [!IMPORTANT]
> Please note **writing** into **Database lookup table** is not supported. You should use [DatabaseWriter](dboutputtable.md) instead.

#### Metadata

**LookupTableReaderWriter** propagates metadata of used lookup table to all ports.

#### LookupTableReaderWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Lookup table | yes | ID of the lookup table to be used as  - a source of records when the component is used as a reader, or - a deposit when the component is used as a writer, or - both when it is used for both reading and writing. |  |
| Advanced |  |  |  |
| Clear lookup table after finishing |  | When set to `true`, memory caches of the lookup table will be emptied at the end of the execution of this component. This has different effects on different lookup table types. Simple lookup table and Range lookup table will contain 0 entries after this operation. For the other lookup table types this will only erase cached data and therefore make more memory available, but the lookup table will still contain the same entries. | false (default) \| true |

#### Details

**LookupTableReaderWriter** works in one of the three following ways:

- Receives data through connected single input port and writes it to the specified lookup table.
- Reads data from the specified lookup table and sends it out through all connected output ports.
- Receives data through connected single input port, updates the specified lookup table, reads updated lookup table, and sends data out through all connected output ports.

#### See also

| [Lookup tables](lookup-tables.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
