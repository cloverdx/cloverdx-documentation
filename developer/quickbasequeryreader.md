<!-- Development > Component reference > Readers > QuickBaseQueryReader -->

### QuickBaseQueryReader

![QuickBaseReader 64x64](../figures/QuickBaseReader-64x64.png)

| [Short description](quickbasequeryreader.md#short-description) |
| --- |
| [Ports](quickbasequeryreader.md#ports) |
| [Metadata](quickbasequeryreader.md#metadata) |
| [QuickBaseQueryReader attributes](quickbasequeryreader.md#quickbasequeryreader-attributes) |
| [Details](quickbasequeryreader.md#details) |
| [See also](quickbasequeryreader.md#see-also) |

#### Short description

**QuickBaseQueryReader** gets records fulfilling given conditions from a **QuickBase** online database table.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| QuickBase | 0 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | For correct data records. | any |

#### Metadata

QuickBaseQueryReader does not propagate metadata.

QuickBaseQueryReader has no metadata template.

Metadata cannot use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### QuickBaseQueryReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| QuickBase connection | **✓** | The ID of the connection to the QuickBase online database, see [QuickBase connections](quickbase-connections.md) |  |
| Table ID | **✓** | The ID of the table in the QuickBase application data records are to be get from. Select a table in the QuickBase UI and copy the table ID from the browser URL: `https://mydomain.quickbase.com/db/TABLE_ID`. | e.g. `bqib669xe` |
| Query |  | Determines which records are returned (all, by default) using the form {*<field_id>.<operator>*.'*<matching_value>'*}. | e.g. `{'6'.CT.'Birdie'}` |
| CList |  | The *column list* specifies which columns will be included in each returned record and how they are ordered in the returned record aggregate. Use *field_id*s separated by a period. |  |
| SList |  | The *sort list* determines the order in which the returned records are displayed. Use *field_id* separated by a period. |  |
| Options |  | Options used for data records that are read. For more information, see [Options](quickbasequeryreader.md#options). |  |

![tableID](../figures/tableID.png)
*Figure 362. Obtaining Table ID*

#### Details

**QuickBaseQueryReader** gets records from a **QuickBase** online database. You can use the component attributes to define which columns will be returned, how many records will be returned and how they will be sorted, and whether the QuickBase should return structured data. Records that meet the requirements are sent out through the connected output port.

This component wraps the `API_DoQuery` HTTP interaction (*[http://www.quickbase.com/api-guide/do_query.html](http://www.quickbase.com/api-guide/do_query.html)*).

##### Options

**Options** attributes can be as follows:

- `skp-n`
  Specifies `n` records from the beginning that should be skipped.
- `num-n`
  Specifies `n` records that should be read.
- `sortorder-A`
  Specifies the order of sorting as ascending.
- `sortorder-D`
  Specifies the order of sorting as descending.
- `onlynew`
  This parameter cannot be used by an anonymous user. The component reads only new records. The results can be different for different users.

#### See also

| [QuickBaseRecordReader](quickbaserecordreader.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
