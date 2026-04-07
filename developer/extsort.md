<!-- Development > Component reference > Transformers > ExtSort -->

### ExtSort

![ExtSort 64x64](../figures/ExtSort-64x64.png)

| [Short description](extsort.md#short-description) |
| --- |
| [Ports](extsort.md#ports) |
| [Metadata](extsort.md#metadata) |
| [ExtSort attributes](extsort.md#extsort-attributes) |
| [Details](extsort.md#details) |
| [Examples](extsort.md#examples) |
| [See also](extsort.md#see-also) |

#### Short description

**ExtSort** sorts input records according to a sort key.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-N | - | - | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | for input data records | the same input and output metadata |
| Output | 0 | **✓** | for sorted data records |  |
| 1-N | **⨯** | for sorted data records |  |  |

This component has one input port and at least one output port.

If more output ports are connected, **ExtSort** sends each record to all connected output ports.

#### Metadata

Metadata can be propagated through this component. All output metadata must be same as the input metadata. **ExtSort** does not change metadata.

#### ExtSort attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Sort key | **✓** | Key according to which the records are sorted. For more information, see [Sort key](components.md#sort-key). | name(a);age(d) |
| Advanced |  |  |  |
| Buffer capacity |  | The maximum number of records parsed in memory. If there are more input records than this number, external sorting is performed. | 8000 (default) \| 1-N |
| Number of tapes |  | The number of temporary files used to perform external sorting. Even number higher than 2. | 6 (default) \| 2*(1-N) |
| Deprecated |  |  |  |
| Sort order |  | Order of sorting (`Ascending` or `Descending`). Can be denoted by the first letter (`A` or `D`) only. Same for all key fields. | Ascending (default) \| Descending |
| Sorting locale |  | Locale that should be used for sorting. | none (default) \| any locale |
| Case sensitive |  | In the default setting of **Case sensitive** (`true`), upper-case and lower-case characters are sorted as distinct characters. Lower-cases precede corresponding upper-cases. If **Case sensitive** is set to `false`, upper-case characters and lower-case characters are sorted as if they were identical.  The **Case sensitive** attribute value is taken into account only if **Locale** is set. | true (default) \| false |
| Sorter initial capacity |  | does the same as **Buffer capacity** | 8000 (default) \| 1-N |

#### Details

**ExtSort** receives data records through the single input port, sorts them according to a specified sort key and copies each of them to all connected output ports.

The **Sort key** is defined by one or more input fields and the sorting order (ascending or descending) for each field. The resulting sequence also depends on the key field type: `string` fields are sorted in ASCIIbetical order while other fields are sorted alphabetically.

##### Sorting null values

In ascending order, null values are sorted before strings, numbers, booleans or dates. If you sort data in descending order, null values are sorted after strings, numbers, booleans or dates.

Remember that **ExtSort** processes records in which the same fields of the **Sort key** attribute have `null` values as if these `nulls` were equal.

#### Examples

| [Sorting according to a single field](extsort.md#sorting-according-to-a-single-field) |
| --- |
| [Sorting according to multiple fields](extsort.md#sorting-according-to-multiple-fields) |
| [Sorting with locale](extsort.md#sorting-with-locale) |

##### Sorting according to a single field

This example shows the basic usage of **ExtSort**.

Input records contains file names and their size. Sort the files according to their size starting with the biggest one.

Input records

```
file.txt  |    2048
file.docx | 1048576
file.xml  |   65536
```

###### Solution

In **ExSort**, set **Sort key** attribute: drag the field name from the left list to the right one and change **Order** to **Descending**.

| Attribute | Value |
| --- | --- |
| Sort key | FileSize(d) |

The result would be:

```
file.docx | 1048576
file.xml  |   65536
file.txt  |    2048
```

##### Sorting according to multiple fields

This example shows sorting values according to a multiple-part key.

Each record contains first name, last name and year of birth. Sort the records according to all three fields. Sort the records according to last name and first name in ascending order. If there are more records with the same first and last name, the youngest one should be the first.

```
Jane | Doe | 1843
John | Doe | 1798
John | Doe | 1859
```

###### Solution

Set the **Sort key** attribute. In the dialog to define the key. The first part of the key (last name) should be on the top of the list on the right side. The first name should be the second and the year of birth should be the last one.

| Attribute | Value |
| --- | --- |
| Sort key | Surname(a);FirstName(a);YearOfBirth(d) |

The result would be:

```
Jane | Doe | 1843
John | Doe | 1859
John | Doe | 1798
```

##### Sorting with locale

This example shows sorting records with locale.

Input records contains a list of French words. Sort the words according to the French collation.

```
parler
être
aller
```

###### Solution

In **ExtSort**, set **Sort key** and **Sorting locale** attributes.

| Attribute | Value |
| --- | --- |
| Sort key | Word(a); |
| Sorting locale | fr.FR |

The result will be:

```
aller
être
parler
```

Without the proper sorting locale, the result would be *aller, parler, être*.

#### See also

| [FastSort](fastsort.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
