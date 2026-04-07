<!-- Development > Component reference > Readers > DBFDataReader -->

### DBFDataReader

![DBFDataReader 64x64](../figures/DBFDataReader-64x64.png)

| [Short description](dbfdatareader.md#short-description) |
| --- |
| [Ports](dbfdatareader.md#ports) |
| [Metadata](dbfdatareader.md#metadata) |
| [DBFDataReader attributes](dbfdatareader.md#dbfdatareader-attributes) |
| [Details](dbfdatareader.md#details) |
| [See also](dbfdatareader.md#see-also) |

#### Short description

**DBFDataReader** reads data from fixed-length dbase files. It can also read data from remote locations, compressed files, input port, or dictionary.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DBase file | 0-1 | 1-n | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For port reading. See [Reading from input port](examples-of-file-url-in-readers.md#reading-from-input-port). | One field (`byte`, `cbyte`, `string`). |
| Output | 0 | **✓** | For correct data records | Any |
| 1-n | **⨯** | For correct data records | Output 0 |  |

#### Metadata

DBFDataReader does not propagate metadata.

DBFDataReader does not have any metadata template.

Metadata on output ports can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

`source_timestamp` and `source_size` functions work only when reading from a file directly. If the file is an archive or it is stored in a remote location, timestamp will be empty and size will be 0.

It can read only fixed length data records.

#### DBFDataReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | The attribute specifying what data source(s) will be read (dbase file, input port, dictionary). See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| Charset |  | Encoding of records that are read. | IBM850 (default) \| <other encodings> |
| Data policy |  | Determines what should be done when an error occurs. For more information, see [Data policy](data-policy.md). | Strict (default) \| Controlled[[1]](dbfdatareader.md#dbfdatareader-attributes-footnote-1)\| Lenient |
| Advanced |  |  |  |
| Number of skipped records |  | The number of records to be skipped continuously throughout all source files. See [Selecting input records](selecting-input-records.md). | 0-N |
| Max number of records |  | The maximum number of records to be read continuously throughout all source files. See [Selecting input records](selecting-input-records.md). | 0-N |
| Number of skipped records per source |  | The number of records to be skipped from each source file. See [Selecting input records](selecting-input-records.md). | Same as in Metadata (default) \| 0-N |
| Max number of records per source |  | The maximum number of records to be read from each source file. See [Selecting input records](selecting-input-records.md). | 0-N |
| Incremental file | [[2]](dbfdatareader.md#dbfdatareader-attributes-footnote-2) | The name of the file storing the incremental key, including the path. See [Incremental reading](incremental-reading.md). |  |
| Incremental key | [[2]](dbfdatareader.md#dbfdatareader-attributes-footnote-2) | The variable storing the position of the last read record. See [Incremental reading](incremental-reading.md). |  |

| 1 | **Controlled** data policy in **DBFDataReader** does not send error records to the edge. Errors are written into the log. |
| --- | --- |

| 2 |  Either both or neither of these attributes must be specified. |
| --- | --- |

#### Details

**DBFDataReader** can be used to read UTF-8 encoded dBase files. Metadata extraction wizard is able to extract metadata from such file (preview works well and respects selected charset).

In general, DBFDataReader can use any encoding for parsing. Note that every character at any column name (stored at header of the file) must be represented by a single byte. **Example:** set UTF-8 encoding. It is possible to read Japanese characters stored at dBase file but the column name must not contain such a character. Just single byte characters are used for the column name so that some charsets cannot be used (for example UTF-16).

##### Notes and limitations

The metadata used for writing data with **DBFDataWriter** is different from metadata required by **DBFDataReader**. If you read data from `.dbf` files, you need an extra metadata field called **delete flag**.

#### See also

| [DBFDataWriter](dbfdatawriter.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
