<!-- Development > Component reference > Readers > ParallelReader -->

### ParallelReader

![ParallelReader 64x64](../figures/ParallelReader-64x64.png)

| [Short description](parallelreader.md#short-description) |
| --- |
| [Ports](parallelreader.md#ports) |
| [Metadata](parallelreader.md#metadata) |
| [ParallelReader attributes](parallelreader.md#parallelreader-attributes) |
| [Details](parallelreader.md#details) |
| [Examples](parallelreader.md#examples) |
| [Best practices](parallelreader.md#best-practices) |
| [Compatibility](parallelreader.md#compatibility) |
| [See also](parallelreader.md#see-also) |

#### Short description

**ParallelReader** reads text files from local or remote sources using multiple parallel threads. It splits the input file into chunks, with each thread reading and processing a portion to improve performance. For more information, see [Details](parallelreader.md#details).

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Flat file | 0 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | For correct data records. | any |
| 1 | **⨯** | For incorrect data records. | specific structure, see table bellow. |  |

Parsed data records are sent to the first output port.

The component has an optional output logging port for getting detailed information about incorrect records. To get all incorrect records together with the information about the incorrect value, its location, and the error message to error port, [Data policy](data-policy.md) has to be **controlled** and an edge has to be connected to the error port.

#### Metadata

ParallelReader has metadata template on the second output port.

| Field Number | Field Content | Data Type | Description |
| --- | --- | --- | --- |
| 0 | record number | long | The position of the erroneous record in the dataset (record numbering starts at 1). |
| 1 | field number | integer | The position of the erroneous field in the record (1 stands for the first field, i.e. that of index 0). |
| 2 | original data | string | The erroneous record in raw form (including delimiters). |
| 3 | error message | string | The error message - detailed information about the error. |
| 4 | reading thread offset | long | Indicates the initial file offset of the parsing thread (optional field). |

#### ParallelReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | **✓** | Data source(s) will be read. See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| Charset |  | Encoding of records that are read in.  The default encoding depends on DEFAULT_CHARSET_DECODER in defaultProperties. | UTF-8 \| <other encodings> |
| Data policy |  | Determines what should be done when an error occurs. For more information, see [Data policy](data-policy.md). | Strict (default) \| Controlled \| Lenient |
| Trim strings |  | Specifies whether leading and trailing whitespace should be removed from strings before setting them to data fields, see [Trimming data](flatfilereader.md#trimming-data). If `true`, the use of the robust parser is forced. | false (default) \| true |
| Quoted strings |  | Fields containing a special character (comma, newline, or double quote) have to be enclosed in quotes. Only single/double quote is accepted as the quote character. If `true`, special characters are removed when read by the component (they are not treated as delimiters).  Example: To read input data `"25"\|"John"`, switch **Quoted strings** to `true` and set **Quote character** to ". This will produce two fields: `25\|John`.  By default, the value of this attribute is inherited from metadata on output port 0. See also [Record details](metadata-editor.md#record-details). | false \| true |
| Quote character |  | Specifies which kind of quotes will be permitted in **Quoted strings**. By default, the value of this attribute is inherited from metadata on output port 0. See also [Record details](metadata-editor.md#record-details). | both \| " \| ' |
| Advanced |  |  |  |
| Skip leading blanks |  | Specifies whether to skip a leading whitespace (blanks e.g.) before setting input strings to data fields. If not explicitly set (i.e. having the default value), the value of the **Trim strings** attribute is used. See [Trimming data](flatfilereader.md#trimming-data). If `true`, the use of the robust parser is enforced. | false (default) \| true |
| Skip trailing blanks |  | Specifies whether to skip a trailing whitespace (blanks e.g.) before setting input strings to data fields. If not explicitly set (i.e. having the default value), the value of the **Trim strings** attribute is used. See [Trimming data](flatfilereader.md#trimming-data). If `true`, the use of the robust parser is enforced. | false (default) \| true |
| Number of skipped records per source |  | Skips the first `n` records/rows from each source file. See [Selecting input records](selecting-input-records.md). | 0 (default) - N |
| Max error count |  | The maximum number of tolerated error records in input file(s); applicable only if `Controlled`**Data policy** is set. | 0 (default) - N |
| Treat multiple delimiters as one |  | If a field is delimited by a multiplied delimiter char, it will be interpreted as a single delimiter when setting to `true`. | false (default) \| true |
| Verbose |  | By default, a less comprehensive error notification is provided and the performance is slightly higher. However, if switched to `true`, more detailed information with less performance is provided. | false (default) \| true |
| Level of parallelism |  | The number of threads used to read input data files. The order of records is not preserved if it is 2 or higher. If the file is too small, this value will be switched to 1 automatically. | 2 (default) \| 1-n |
| Distributed file segment reading |  | In case the component is running in a Cluster environment and a shared file is read, each component’s instance process the appropriate part of the file. The whole file is divided into segments by **CloverDX Server** and each Cluster worker processes only one proper part of the file. By default, this option is turned off. This attribute is ignored for partitioned files. | false (default) \| true |
| Parser |  | By default, the most appropriate parser is applied. Besides, the parser for processing data may be set explicitly. If an improper one is set, an exception is thrown and the graph fails. See [Data parsers](flatfilereader.md#data-parsers) | auto (default) \| `<other>` |

#### Details

**ParallelReader** reads delimited flat files (e.g. CSV, tab delimited, etc.), fixed-length, or mixed text files. The component can read a single file as well as a collection of files placed on a local disk or remotely, remote files are accessible via FTP and S3 protocol.

Reading goes in several parallel threads, which improves the reading speed. Input file is divided into set of chunks and each reading thread parses just records from this part of file.

The component can use either the fast simplistic parser (`SimpleDataParser`) or the robust (`CharByteDataParser`) one. Which parser is used depends on the component settings and data structure.

##### Speedup

If you use ParallelReader instead of FlatFileReader, the speed up is more significant with metadata of many date data fields.

##### Quoted strings

The attribute considerably changes the way your data is parsed. If it is set to `true`, all field delimiters inside quoted strings will be ignored (after the first **Quote character** is actually read). Quote characters will be removed from the field.

Example input:

`1;"lastname;firstname";gender`

Output with Quoted strings == true:

{1}, {`lastname;firstname`}, {`gender`}

Output with Quoted strings == false:

{1}, {`"lastname`}, {`firstname";gender`}

#### Examples

##### Reading a file with ParallelReader

This example shows the basic use of ParallelReader.

Read file `file.txt` using ParallelReader.

###### Solution

In ParallelReader, specify **File URL** and connect an edge to the first output port.

**ParallelReader** will read it using two threads.

#### Best practices

We recommend users to explicitly specify **Charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 2.8.1 | **ParallelReader** is included in 2.8.1 and higher. |
| 4.4.0-M1 | **ParallelReader** support reading files from S3. |

#### See also

| [FlatFileReader](flatfilereader.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
