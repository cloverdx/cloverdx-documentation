<!-- Development > Component reference > Writers > DBFDataWriter -->

### DBFDataWriter

![DBFDataWriter 64x64](../figures/DBFDataWriter-64x64.png)

| [Short description](dbfdatawriter.md#short-description) |
| --- |
| [Ports](dbfdatawriter.md#ports) |
| [Metadata](dbfdatawriter.md#metadata) |
| [DBFDataWriter attributes](dbfdatawriter.md#dbfdatawriter-attributes) |
| [Details](dbfdatawriter.md#details) |
| [Best practices](dbfdatawriter.md#best-practices) |
| [See also](dbfdatawriter.md#see-also) |

#### Short description

**DBFDataWriter** writes data to dbase file(s).

Handles `Character/Number/Logical/Date` dBase data types.

The component can write a single file or a partitioned collection of files.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| .dbf file | 1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | Incoming data records | Fixed length |

#### Metadata

**DBFDataWriter** does not propagate metadata.

**DBFDataWriter** has no metadata template.

Input metadata has to be fixed-length as you are writing binary data.

#### DBFDataWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | **✓** | Specifies where data will be written to (a path to a `.dbf` file), see [Supported file URL formats for Writers](examples-of-file-url-in-writers.md). |  |
| Charset |  | Character encoding of records written to the output. See [Details](dbfdatawriter.md#details)  The default encoding depends on DEFAULT_CHARSET_DECODER in defaultProperties. | `ISO-8859-1` \| other 8bit fixed width encoding |
| Append |  | If records are printed into a non-empty file, they replace the previous content by default (`false`). If set to `true`, new records are appended at the end of the existing output file(s). | false (default) \| true |
| DBF type |  | A type of the created DBF file (determined by the first byte of the file header). If you are unsure which type to choose, leave the attribute to default. | `0x03 FoxBASE+ (default) \| Dbase III plus, no memo` \| other dbf type byte |
| Advanced |  |  |  |
| Create directories |  | When `true`, non-existing directories contained in the **File URL** path are automatically created. | `false` (default) \| `true` |
| Records per file |  | The maximum number of records to be written to each output file. If specified, the dollar sign(s) $ ('number of digits' placeholder) must be a part of the file name mask, see [Supported file URL formats for Writers](examples-of-file-url-in-writers.md) | 1 - N |
| Number of skipped records |  | The number of records/rows to be skipped before writing the first record to the output file, see [Selecting output records](selecting-output-records.md). | 0 (default) - N |
| Max number of records |  | The aggregate number of records/rows to be written to all output files, see [Selecting output records](selecting-output-records.md). | 0-N |
| Exclude fields |  | A sequence of field names that will not be written to the output (separated by a semicolon). Can be used when the same fields serve as a part of **Partition key**. |  |
| Partition key | [[1]](dbfdatawriter.md#dbfdatawriter-attributes-fn02) | A sequence of field names defining the record distribution among multiple output files - records with the same **Partition key** are written to the same output file. Use a semicolon ';' as field names separator. Depending on selected **Partition file tag**, use the appropriate placeholder ($ or #) in the file name mask, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md) |  |
| Partition lookup table | [[2]](dbfdatawriter.md#dbfdatawriter-attributes-fn03) | An ID of a lookup table serving for selecting records that should be written to output file(s). For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Partition file tag | [[1]](dbfdatawriter.md#dbfdatawriter-attributes-fn02) | By default, partitioned output files are numbered. If this attribute is set to `Key file tag`, output files are named according to the values of **Partition key** or **Partition output fields**. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | `Number file tag` (default) \| `Key file tag` |
| Partition output fields | [[2]](dbfdatawriter.md#dbfdatawriter-attributes-fn03) | Fields of **Partition lookup table** whose values are used as output file(s) names. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Partition unassigned file name |  | The name of a file which the unassigned records should be written into (if there are any). Unless specified, data records whose key values are not contained in **Partition lookup table** are discarded. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Sorted input |  | In case the partitioning into multiple output files is enabled,all output files are open at once. This could lead to undesirable memory footprint for many output files (thousands). Moreover, for example unix-based OS usually have very strict limitation of number of simultaneously open files (1024) per process. If you run into one of these limitations, consider sorting the data according to a partition key using one of our standard sorting components and set this attribute to true. The partitioning algorithm does not need to keep open all output files, just the last one is open at one time. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | false (default) \| true |
| Create empty files |  | If set to `false`, prevents the component from creating an empty output file when there are no input records. | true (default) \| false |

| 1 | Either both or neither of these two attributes must be specified. |
| --- | --- |

| 2 | Either both or neither of these two attributes must be specified. |
| --- | --- |

#### Details

**DBFDataWriter** can be used to write UTF-8 encoded dBase files.

In general, DBFDataWriter can use any encoding for parsing. Note that every character at any column name (stored at header of the file) must be represented by single byte. **Example:** set UTF-8 encoding. It is possible to write Japanese characters stored at dBase file but the column name must not contain such a character. Since the column name can contain single byte characters only, some charsets cannot be used (for example UTF-16).

##### Notes and limitations

###### Writing to Remote and Compressed Files not Available

Output data can be stored locally only. Uploading via a remote transfer protocol and writing ZIP and TAR archives is not supported.

###### Lists and Maps

The structure of a `.dbf` file is not suitable for reading and writing lists or maps. **DBFDataWriter** converts lists and maps to string before the writing, but there is no easy way to read them back as lists or maps.

#### Best practices

We recommend users to explicitly specify **Charset**.

#### See also

| [DBFDataReader](dbfdatareader.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
