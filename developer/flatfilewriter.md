<!-- Development > Component reference > Writers > FlatFileWriter -->

### FlatFileWriter

![FlatFileWriter 64x64](../figures/FlatFileWriter-64x64.png)

| [Short description](flatfilewriter.md#short-description) |
| --- |
| [Ports](flatfilewriter.md#ports) |
| [Metadata](flatfilewriter.md#metadata) |
| [FlatFileWriter attributes](flatfilewriter.md#flatfilewriter-attributes) |
| [Details](flatfilewriter.md#details) |
| [Examples](flatfilewriter.md#examples) |
| [Best practices](flatfilewriter.md#best-practices) |
| [Compatibility](flatfilewriter.md#compatibility) |
| [See also](flatfilewriter.md#see-also) |

#### Short description

**FlatFileWriter** writes data to flat files. The output flat file can be in form of CSV (character separated values), fixed-length format or mixed-length format (combination of mixed-length and fixed-length formats).

The component supports partitioning, compression, writing to output port or to remote destination.

[UniversalDataWriter](datawriter.md) is an alias for **FlatFileWriter**.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| flat file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | for received data records | any |
| Output | 0 | **⨯** | For port writing. See [Writing to output port](examples-of-file-url-in-writers.md#writing-to-output-port). | include specific `byte`/ `cbyte`/ `string` field |

#### Metadata

**FlatFileWriter** does not propagate metadata.

The component has no metadata template.

**FlatFileWriter** requires `string`, `byte` or `cbyte` field in the output metadata.

#### FlatFileWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | **✓** | Where the received data to be written (flat file, output port, dictionary) are specified, see [Supported file URL formats for Writers](examples-of-file-url-in-writers.md). |  |
| Charset |  | Character encoding of records written to the output.  The default encoding depends on DEFAULT_CHARSET_DECODER in defaultProperties. | ISO-8859-1 \| UTF-8 \| <other encodings> |
| Append |  | If records are printed into an existing non-empty file, they replace the older ones by default (`false`).  If set to `true`, new records are appended to the end of the existing output file(s) content.  Some remote locations or compressed files do not support appending. See [Appending to files](flatfilewriter.md#appending-to-files). | false (default) \| true |
| Quoted strings |  | When switched to `true`, all field values (except from `byte` and `cbyte`) will be quoted. If you do not set this attribute, its value is inherited from metadata on the input port (and displayed in faded gray text, see also [Record details](metadata-editor.md#record-details)). | false \| true |
| Quote character |  | Specifies which kind of quotes will enclose output fields. Applies only if **Quoted strings** is `true`. By default, the value of this attribute is inherited from metadata on input port. See also [Record details](metadata-editor.md#record-details). | " \| ' |
| Advanced |  |  |  |
| Create directories |  | If set to `true`, non-existing directories in the **File URL** attribute path are created. | false (default) \| true |
| Write field names |  | Field labels are not written to output file(s) by default. If set to `true`, labels of individual fields are printed as the first row of each newly created output file. When **Append** is `true` and the output file already exists and is non-empty, the header row is **not** written again.  If set to `force`, field labels are always written — including when appending to an existing non-empty file. This is useful when combining multiple different record structures (e.g. HEADER, BODY, FOOTER) into one file across several graph phases using separate writer components.  Please note that field labels differ from field names: labels can be duplicate and you can use any character in them (e.g. accents, diacritics). See [Record pane](metadata-editor.md#record-pane). | false (default) \| true \| force |
| Records per file |  | The maximum number of records to be written to each output file. If specified, the dollar sign(s) $ (number of digits placeholder) must be a part of the file name mask, see [Supported file URL formats for Writers](examples-of-file-url-in-writers.md) | 1 - N |
| Bytes per file |  | The maximum size of each output file in bytes. If specified, the dollar sign(s) $ (number of digits placeholder) must be a part of the file name mask, see [Supported file URL formats for Writers](examples-of-file-url-in-writers.md) To avoid splitting a record into two files, the maximum size can be slightly overreached. | 1 - N |
| Number of skipped records |  | How many records/rows to be skipped before writing the first record to the output file, see [Selecting output records](selecting-output-records.md). | 0 (default) - N |
| Max number of records |  | How many records/rows to be written to all output files, see [Selecting output records](selecting-output-records.md). | 0-N |
| Exclude fields |  | A sequence of field names separated by a semicolon that will not be written to the output. Can be used when the same fields serve as a part of **Partition key**. |  |
| Partition key | [[1]](flatfilewriter.md#partition-udw) | A sequence of field names separated by a semicolon defining the records distribution into different output files - records with the same **Partition key** are written to the same output file. According to the selected **Partition file tag**, use a proper placeholder ($ or #) in the file name mask, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md) |  |
| Partition lookup table | [[2]](flatfilewriter.md#increment-w) | An ID of a lookup table serving for selecting records that should be written to output file(s). For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Partition file tag | [[1]](flatfilewriter.md#partition-udw) | By default, output files are numbered. If the attribute is set to `Key file tag`, output files are named according to the values of **Partition key** or **Partition output fields**. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | Number file tag (default) \| Key file tag |
| Partition output fields | [[2]](flatfilewriter.md#increment-w) | Fields of **Partition lookup table** whose values serve to name output file(s). For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Partition unassigned file name |  | The name of a file into which unassigned records should be written, if there are any. If not specified, data records whose key values are not contained in **Partition lookup table** are discarded. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Sorted input |  | If **partitioning into multiple output files** is turned on, all output files are open at once. This can lead to undesirable memory footprint for many output files (thousands). Moreover, for example unix-based OS usually have a very strict limitation of the number of simultaneously open files (1,024) per process. In case you run into one of these limitations, consider sorting the data according to a partition key using one of our standard sorting components and set this attribute to true. The partitioning algorithm does not need to keep open all output files, just the last one is open at one time. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | false (default) \| true |
| Create empty files |  | If set to `false`, prevents the component from creating an empty output file when there are no input records. | true (default) \| false |
| Skip last record delimiter |  | If set to `true`, the last record delimiter in a file is not written. If set to `false`, the last record delimiter in a file is written. | false (default) \| true |

| 1 | Either both or neither of these attributes must be specified. |
| --- | --- |

| 2 | Either both or neither of these attributes must be specified |
| --- | --- |

#### Details

The type of formatting is specified in metadata for the input port data flow.

##### Appending to files

Appending to files is supported, if you write data to:

- local files
- local zipped files
- remote files via smb protocol

Appending to files is not supported in, if you write data to:

- local gzipped files
- remote files via ftp protocol
- remote files via webdav protocol
- remote files via Amazon S3 protocol
- remote files via hdfs protocol

##### Null values

Empty strings and `null` values are written to a file as empty strings.

##### Notes and limitations

###### Field size limitation

**FlatFileWriter** can write fields of a size up to 4kB.

- To enable bigger fields to be written into a file, increase the `DataFormatter.FIELD_BUFFER_LENGTH` property, see [Engine configuration](../admin/designer-configuration.md#engine-configuration). Increasing the size of this buffer does not cause any significant increase of the graph memory consumption.
- Another way to solve the issue with fields too big to be written is the utilization of the [Normalizer](normalizer.md) component that can split large fields into several records.

###### Maps, Lists and Variants

**FlatFileWriter** cannot write maps, lists and variants. If you do not need a field with map, list or variant datatype in the output file, you can omit it using **Exclude fields** attribute. If you need to write the content of the map, list or variant field, convert the field into string using [Map](reformat.md) first.

#### Examples

| [Writing records to file](flatfilewriter.md#writing-records-to-file) |
| --- |
| [Producing quoted strings](flatfilewriter.md#producing-quoted-strings) |
| [Writing records without delimiters](flatfilewriter.md#writing-records-without-delimiters) |
| [Writing fixed-length records to output port](flatfilewriter.md#writing-fixed-length-records-to-output-port) |

##### Writing records to file

Write records to a file `objects.txt` using **FlatFileWriter**. The input metadata fields are **color**, **shape** and **material**.

###### Solution

Use the **File URL** attribute to define a path to the file to be created.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/objects.txt |

An example of the output file, delimited input metadata:

```
gray|cylinder|steel
brown|cube|wood
transparent|sphere|glass
```

The separators "|" depend on metadata on the input edge.

An example of the output file, fixed input metadata:

```
gray           cylinder      steel
brown          cube          wood
transparent    sphere        glass
```

##### Producing quoted strings

Write data from the previous example to a file. Each field value has to be surrounded by a quote character ' (apostrophe).

###### Solution

Use the attributes **File URL**, **Quoted strings** and **Quote character**.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/objects-in-quotes.txt |
| Quoted strings | true |
| Quote character | ' |

If a string to be quoted contains a quote character, the quote character in the string is doubled. E.g. o’clock is quoted as 'o''clock'.

##### Writing records without delimiters

This example shows writing records without writing record delimiters.

You receive an output from **XMLWriter** in a streaming mode. The records have to be seamlessly written to the file. No delimiter should be written between the records.

###### Solution

The solution to the problem depends on metadata. The input metadata of **FlatFileWriter** must have no **Record delimiter**, no **Default delimiter** and must use **EOF as delimiter**.

In **FlatFileWriter**, enter **File URL**.

The records will be written without delimiters as no delimiters are specified in metadata.

##### Writing fixed-length records to output port

Write several fields of fixed-length metadata into one field of the output port (provided one input record creates one output record).

###### Solution

Make sure that input metadata has no record delimiter set. Select metadata on the input edge and open the **Edit Metadata** window. Select the first row in the **Record pane** of the editor and make sure that the **Record delimiter** property is empty.

Create metadata on the output edge with a single field.

Use the attributes **File URL** and **Records per file**.

| Attribute | Value |
| --- | --- |
| File URL | port:$0.field1:discrete |
| Records per file | 1 |

#### Best practices

We recommend to explicitly specify encoding of the output file (with the **Charset** attribute). It ensures better portability of the graph across systems with different default encoding.

The recommended encoding is UTF-8.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | The last record delimiters in a file can now be skipped. |
| 4.2.0-M1 | **FlatFileWriter** is available since **4.2.0-M1**. In **4.2.0-M1**, **UniversalDataWriter** was renamed to **FlatFileWriter**. |
| 7.5.0 | The **Write field names** attribute now accepts a third value `force`. |

#### See also

| [FlatFileWriter](flatfilewriter.md) |
| --- |
| [UniversalDataReader](datareader.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
