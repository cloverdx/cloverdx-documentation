<!-- Development > Component reference > Writers > QuickBaseImportCSV -->

### QuickBaseImportCSV

![QuickBaseWriter 64x64](../figures/QuickBaseWriter-64x64.png)

| [Short description](quickbaseimportcsv.md#short-description) |
| --- |
| [Ports](quickbaseimportcsv.md#ports) |
| [Metadata](quickbaseimportcsv.md#metadata) |
| [QuickBaseImportCSV attributes](quickbaseimportcsv.md#quickbaseimportcsv-attributes) |
| [Details](quickbaseimportcsv.md#details) |
| [See also](quickbaseimportcsv.md#see-also) |

#### Short description

**QuickBaseImportCSV** adds and updates a **QuickBase** online database table records.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| QuickBase | 1 | 0-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records. | any |
| Output | 0 | **⨯** | For accepted data records. | integer or long field for the table *Record ID#* field values of the imported records |
| Output | 1 | **⨯** | for rejected data records | Input metadata enriched by up to three [Error fields for QuickBaseImportCSV](quickbaseimportcsv.md#quickbaseimportcsv-error-fields) |

#### Metadata

**QuickBaseImportCSV** does not propagate metadata.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| optional[[1]](quickbaseimportcsv.md#opt1) | specified in the **Error code output field** | integer \| long | error code |
| optional[[1]](quickbaseimportcsv.md#opt1) | Specified in the **Error message output field**. | string | error message |
| optional[[1]](quickbaseimportcsv.md#opt1) | specified in the **Batch number output field** | integer \| long | index (starting from 1) of the failed batch |

| 1 | The error fields must be placed behind the input fields. |
| --- | --- |

#### QuickBaseImportCSV attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| QuickBase connection | **✓** | The ID of the connection to the QuickBase online database, see [QuickBase connections](quickbase-connections.md). |  |
| Table ID | **✓** | The ID of the table in the QuickBase application data records are to be written into. Select a table in the QuickBase UI and copy the table ID from the browser URL: `https://mydomain.quickbase.com/db/TABLE_ID`. | e.g. `bqib669xe` |
| Batch size |  | The maximum number of records in one batch | 100 (default) \| 1-N |
| Clist |  | A period-delimited list of table *field_id*s to which the input data columns map. The order is preserved. Thus, enter a `0` for columns not to be imported. If not specified, the database tries to add unique records. It must be set if editing records. The input data must include a column that contains the record ID for each record that you are updating. |  |
| Error code output field |  | The name of the error metadata field for storing the error code, see [Error fields for QuickBaseImportCSV](quickbaseimportcsv.md#quickbaseimportcsv-error-fields). |  |
| Error message output field |  | The name of the error metadata field for storing the error message, see [Error fields for QuickBaseImportCSV](quickbaseimportcsv.md#quickbaseimportcsv-error-fields). |  |
| Batch number output field |  | The name of the error metadata field for storing the index of the corrupted batch, see [Error fields for QuickBaseImportCSV](quickbaseimportcsv.md#quickbaseimportcsv-error-fields). |  |

![tableID](../figures/tableID.png)
*Figure 381. Obtaining Table ID*

#### Details

**QuickBaseImportCSV** receives data records through the input port and writes them into a **QuickBase** online database. Generates record IDs for successfully written records and sends them out through the first optional output port if connected. The first field on this output port must be of a string data type. Into this field, generated record IDs will be written. Information about rejected data records can be sent out through the optional second port if connected.

This component wraps the `API_ImportFromCSV` HTTP interaction (*[http://www.quickbase.com/api-guide/importfromcsv.html](http://www.quickbase.com/api-guide/importfromcsv.html)*).

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
