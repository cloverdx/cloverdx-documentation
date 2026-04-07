<!-- Development > Component reference > Transformers > MetaPivot -->

### MetaPivot

![MetaPivot 64x64](../figures/MetaPivot-64x64.png)

| [Short description](metapivot.md#short-description) |
| --- |
| [Ports](metapivot.md#ports) |
| [Metadata](metapivot.md#metadata) |
| [MetaPivot attributes](metapivot.md#metapivot-attributes) |
| [Details](metapivot.md#details) |
| [Examples](metapivot.md#examples) |
| [See also](metapivot.md#see-also) |

#### Short description

**MetaPivot** converts every incoming record into several output records, each one representing a single field from the input.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1 | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any1 |
| Output | 0 | **✓** | For transformed data records | Any2 |

#### Metadata

**MetaPivot** does not propagate metadata.

**MetaPivot** has a metadata template on its output port.
> [!IMPORTANT]
> When working with **MetaPivot**, you have to use a fixed format of the output metadata. The metadata fields represent particular data types. Field names and data types have to be set *exactly as follows* (otherwise unexpected `BadDataFormatException` will occur):

| Field Name | Type | Description |
| --- | --- | --- |
| recordNo | long | The serial number of a record (outputs can be later grouped by this) - fields of the same record share the same number. |
| fieldNo | integer | The current field number: 0…​n-1 where n is the number of fields in the input metadata. |
| fieldName | string | The name of the field as it appears on the input |
| fieldType | string | The field type, e.g. `string`, `date`, `decimal` |
| valueBoolean | boolean | The boolean value of the field. |
| valueByte | byte | the byte value of the field |
| valueDate | date | the date value of the field |
| valueDecimal | decimal | the decimal value of the field |
| valueInteger | integer | the integer value of the field |
| valueLong | long | the long value of the field |
| valueNumber | number | the number value of the field |
| valueString | string | the string value of the field |

#### MetaPivot attributes

**MetaPivot** has no transformation-affecting attributes.

#### Details

On its single input port, **MetaPivot** receives data that does not have to be sorted. Each *field* of the input record is written as a new *line* on the output. The metadata represents data types and is restricted to a fixed format, see [Details](metapivot.md#details). All in all, **MetaPivot** can be used to effectively transform your records to a neat data-dependent structure.

Unlike [Normalizer](normalizer.md), which **MetaPivot** is derived from, no transformation is defined. **MetaPivot** always does the same transformation: it takes the input records and rotates them from input columns to output rows.

The total number of output records produced by **MetaPivot** equals to (number of input records) * (number of input fields).

Some of the fields only make the output look better arranged. These can be omitted if required. The fields that do not have to be included in the output metadata are: `recordNo`, `fieldNo` and `fieldType`.

#### Examples

##### Converting line to list

Convert records with metadata fields `username`, `surname` and `first name`.

```
doejohn|Doe  |John
smithel|Smith|Elisabeth
...
```

into lines having each field value on a separate line:

```
username |doejohn
surname  |John
firstname|Doe
username |smithel
surname  |Elisabeth
firstname|Smith
...
```

###### Solution

Place the component into a graph and connect edges. The component does not need to be set up.

**Note:** You need [Map](reformat.md) to exclude unnecessary output fields.

#### See also

| [Pivot](pivot.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
