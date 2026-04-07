<!-- Development > Component reference > Readers > MultiLevelReader -->

### MultiLevelReader

![MultiLevelReader 64x64](../figures/MultiLevelReader-64x64.png)

| [Short description](multilevelreader.md#short-description) |
| --- |
| [Ports](multilevelreader.md#ports) |
| [Metadata](multilevelreader.md#metadata) |
| [MultiLevelReader attributes](multilevelreader.md#multilevelreader-attributes) |
| [Details](multilevelreader.md#details) |
| [Best practices](multilevelreader.md#best-practices) |
| [Compatibility](multilevelreader.md#compatibility) |
| [See also](multilevelreader.md#see-also) |

#### Short description

**MultiLevelReader** reads data from flat files with a heterogeneous structure.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Flat file | 1 | 1-n | **⨯** | **✓** | **✓** | **✓** | **✓** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For port reading. See [Reading from input port](examples-of-file-url-in-readers.md#reading-from-input-port). | One field (`byte`, `cbyte`, `string`). |
| Output | 0 | **✓** | For correct data records | Any(Out0) |
| 1-N | **⨯** | For correct data records | Any(Out1-OutN) |  |

#### Metadata

MultiLevelReader does not propagate metadata.

MultiLevelReader has no metadata template.

Metadata on all output ports can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

`source_timestamp` and `source_size` functions work only when reading from a file directly (if the file is an archive or it is stored in a remote location, timestamp will be empty and size will be 0).

#### MultiLevelReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | Attribute specifying what data source(s) will be read (flat file, input port, dictionary). See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| Charset |  | Encoding of records that are read.  The default encoding depends on DEFAULT_CHARSET_DECODER in defaultProperties. | UTF-8 \| <other encodings> |
| Data policy |  | Determines what should be done when an error occurs. For more information, see [Data policy](data-policy.md). | Strict (default) \| Lenient |
| Selector code | [[1]](multilevelreader.md#multilevelreader-attributes-fn01) | Transformation of rows of input data file to data records written in the graph in Java. |  |
| Selector URL | [[1]](multilevelreader.md#multilevelreader-attributes-fn01) | The name of an external file, including the path, defining the transformation of rows of input data file to data records written in Java. |  |
| Selector class | [[1]](multilevelreader.md#multilevelreader-attributes-fn01) | The name of an external class defining the transformation of rows of input data file to data records. | PrefixMultiLevelSelector (default) \| other class |
| Selector properties |  | The list of the `key=value` expressions separated by a semicolon when the whole is surrounded by flower brackets. Each value is the number of the port through which data records should be sent out. Each key is a serie of characters from the beginning of the row contained in the flat file that enables differentiate groups of records. |  |
| Advanced |  |  |  |
| Number of skipped records |  | Number of records to be skipped continuously throughout all source files. See [Selecting input records](selecting-input-records.md). | 0-N |
| Max number of records |  | Maximum number of records to be read continuously throughout all source files. See [Selecting input records](selecting-input-records.md). | 0-N |
| Number of skipped records per source |  | Number of records to be skipped from each source file. See [Selecting input records](selecting-input-records.md). | Same as in Metadata (default) \| 0-N |
| Max number of records per source |  | Maximum number of records to be read from each source file. See [Selecting input records](selecting-input-records.md). | 0-N |

| 1 |  If you do not define any of these three attributes, the default **Selector class** (`PrefixMultiLevelSelector`) will be used. |
| --- | --- |

`PrefixMultiLevelSelector` class implements `MultiLevelSelector` interface. The interface methods can be found below.

For more information, see [Java interfaces for MultiLevelReader](multilevelreader.md#java-interfaces-for-multilevelreader).

For detailed information about transformations, see [Defining transformations](transformations.md#defining-transformations).

#### Details

**MultiLevelReader** reads information from flat files with a heterogeneous and complicated structure (local or remote which are delimited, fixed-length, or mixed). It can also read data from compressed flat files, input port, or dictionary.

Unlike **FlatFileReader** or the two deprecated readers (**DelimitedDataReader** and **FixLenDataReader**), **MultiLevelReader** can read data from flat files whose structure contains different structures including both delimited and fixed length data records even with different numbers of fields and different data types. It can separate different types of data records and send them through different connected output ports. Input files can also contain non-record data.

Component also uses the **Data policy** option. For more detailed information, see [Data policy](data-policy.md).

Consider using a newer **ComplexDataReader** component if you find some limitation of this component.

##### Selector Properties

You also need to set some series of parameters that should be used (**Selector properties**). They map individual types of data records to output ports. All of the properties must have the form of a list of the `key=value` expressions separated by a semicolon. The whole sequence is in curly brackets. To specify these **Selector properties**, you can use the dialog that opens after clicking the button in this attribute row. By clicking the **Plus** button in this dialog, you can add new key-value pairs. Then you only need to change both the default name and the default value. Each value must be the number of the port through which data records should be sent out. Each key is a series of characters from the beginning of the row contained in the flat file that enable differentiate groups of records.

#### Java interfaces for MultiLevelReader

Following are the methods of the `MultiLevelSelector` interface:

- `int choose(CharBuffer data, DataRecord[] lastParsedRecords)`
  A method that peeks into `CharBuffer` and reads characters until it can either determine metadata of the record which it reads, and thus return an index to metadata pool specified in `init()` method, or runs out of data returning `MultiLevelSelector.MORE_DATA`.
- `void finished()`
  Called at the end of selector processing after all input data records were processed.
- `void init(DataRecordMetadata[] metadata, Properties properties)`
  Initializes this selector.
- `int lookAheadCharacters()`
  Returns the number of characters needed to decide the (next) record type. Usually it can be any fixed number of characters, but dynamic lookahead size, depending on previous record type, is supported and encouraged whenever possible.
- `int nextRecordOffset()`
  Each call to `choose()` can instrument the parent to skip a certain number of characters before attempting to parse a record according to metadata returned in `choose()` method.
- `void postProcess(int metadataIndex, DataRecord[] records)`
  In this method, the selector can modify the parsed record before it is sent to a corresponding output port.
- `int recoverToNextRecord(CharBuffer data)`
  This method instruments the selector to find the offset of the next record which is possibly parsable.
- `void reset()`
  Resets this selector completely. This method is called once, before each run of the graph.
- `void resetRecord()`
  Resets the internal state of the selector (if any). This method is called each time a new choice needs to be made.

You can use [Public CloverDX API](genericcomponent.md#public-cloverdx-api) in this component too.

#### Best practices

We recommend users to explicitly specify **Charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 2.2 | **MultilevelReader** is available since 2.2. |

#### See also

| [ComplexDataReader](complexdatareader.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
