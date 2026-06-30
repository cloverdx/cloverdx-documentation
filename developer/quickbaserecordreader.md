<!-- Development > Component reference > Readers > QuickBaseRecordReader -->

### QuickBaseRecordReader

![QuickBaseReader 64x64](../figures/QuickBaseReader-64x64.png)

| [Short description](quickbaserecordreader.md#short-description) |
| --- |
| [Ports](quickbaserecordreader.md#ports) |
| [Metadata](quickbaserecordreader.md#metadata) |
| [QuickBaseRecordReader attributes](quickbaserecordreader.md#quickbaserecordreader-attributes) |
| [Details](quickbaserecordreader.md#details) |
| [See also](quickbaserecordreader.md#see-also) |

#### Short description

**QuickBaseRecordReader** reads data from a **QuickBase** online database.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| QuickBase | 0-1 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For getting application table record IDs to be read. | first field: `integer \| long` |
| Output | 0 | **✓** | For correct data records. | Data types and positions of fields must fit the table field types.[[1]](quickbaserecordreader.md#qbrr-out0) |
| 1 | **⨯** | information about rejected records | [Error metadata for QuickBaseRecordReader](quickbaserecordreader.md#quickbaserecordreader-error-metadata)[[2]](quickbaserecordreader.md#quickbase-eachtoall-2) |  |

| 1 | Only `source_row_count` autofilling function returning the record ID can be used. |
| --- | --- |

| 2 | Error metadata cannot use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions). |
| --- | --- |

#### Metadata

QuickBaseRecordReader does not propagate metadata.

QuickBaseRecordReader has no metadata template.

Metadata fields on error port have to have the following structure:

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 0 | <any_name1> | integer \| long | ID of the erroneous record |
| 1 | <any_name2> | integer \| long | error code |
| 2 | <any_name3> | string | error message |

#### QuickBaseRecordReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| QuickBase connection | **✓** | The ID of the connection to the QuickBase online database, see [QuickBase connections](quickbase-connections.md). |  |
| Table ID | **✓** | The ID of the table in the QuickBase application data records are to be get from. Select a table in the QuickBase UI and copy the table ID from the browser URL: `https://mydomain.quickbase.com/db/TABLE_ID`. | e.g. `bqib669xe` |
| Records list |  | The list of record IDs (separated by a semicolon) to be read from the specified database table. These records are read first, before the records specified in the input data. |  |

![tableID](../figures/tableID.png)
*Figure 361. Obtaining Table ID*

#### Details

**QuickBaseRecordReader** reads data from a **QuickBase** online database. Records, the IDs of which are specified in the **Records list** component attribute, are read first. Records with IDs specified in the input are read afterward.

The read records are sent through the connected first output port. If the record is erroneous (e.g. not present in the database table), it can can be sent out through the optional second port if it is connected.

This component wraps the `API_GetRecordInfo` HTTP interaction (*[http://www.quickbase.com/api-guide/getrecordinfo.html](http://www.quickbase.com/api-guide/getrecordinfo.html)*).

#### See also

| [QuickBaseRecordWriter](quickbaserecordwriter.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
