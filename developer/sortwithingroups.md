<!-- Development > Component reference > Transformers > SortWithinGroups -->

### SortWithinGroups

![SortWithinGroups 64x64](../figures/SortWithinGroups-64x64.png)

| [Short description](sortwithingroups.md#short-description) |
| --- |
| [Ports](sortwithingroups.md#ports) |
| [SortWithinGroups attributes](sortwithingroups.md#sortwithingroups-attributes) |
| [Details](sortwithingroups.md#details) |
| [See also](sortwithingroups.md#see-also) |

#### Short description

**SortWithinGroups** sorts input records within groups of records according to a sort key.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **✓** | 1 | 1-n | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For sorted data records | Input 0 |
| 1-n | **⨯** | For sorted data records | Input 0 |  |

#### SortWithinGroups attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Group key | yes | The key defining groups of records. Non-adjacent records with the same key value are considered to be of different groups and each of these different groups is processed separately and independently on the others. For more information, see [Group key](components.md#group-key). |  |
| Sort key | yes | A key according to which the records are sorted within each group of adjacent records. For more information, see [Sort key](components.md#sort-key). |  |
| Advanced |  |  |  |
| Buffer capacity |  | The maximum number of records parsed in memory. If there are more input records than this number, external sorting is performed. | 10485760 (default) \| 1-N |
| Number of tapes |  | The number of temporary files used to perform external sorting. Even number higher than 2. | 8 (default) \| 2*(1-N) |

#### Details

**SortWithinGroups** receives data records (that are grouped according to a group key) through the single input port, sorts them according to a sort key separately within each group of adjacent records and copies each record to all connected output ports.

##### Sorting Null values

Remember that **SortWithinGroups** processes records in which same fields of the **Sort key** attribute have `null` values as if these `nulls` were equal.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
