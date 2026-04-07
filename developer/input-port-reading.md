<!-- Development > Component reference > Readers > Common properties of Readers > Input port reading -->

#### Input port reading

**Input port reading** allows you to read file names or data from an optional input port. This feature is available in most of **Readers**.

To use input port mapping, connect an edge to an input port. Assign metadata to the edge. In the **Reader**, edit the File URL attribute.

The attribute value has the syntax `port:$0.FieldName[:processingType]`. You can enter the value directly or with help of [URL file dialog](common-dialogs.md#url-file-dialog).

Here `processingType` is optional and defines if the data is processed as plain data or URL addresses. It can be `source`, `discrete`, or `stream`. If not set explicitly, `discrete` is applied by default.

##### Processing type

- `discrete`
  Each data record field from an input port represents one particular data source.
- `source`
  Each data record field from an input port represents a URL to be loaded in and parsed.
- `stream`
  All data fields from an input port are concatenated and processed as one input file. If the `null` value of this field is met, it is replaced by the `EOF`. Following data record fields are parsed as another input file in the same way, i.e. until the `null` value is met. The Reader starts parsing data as soon as first bytes come by the port and process it progressively until EOF comes. For more information about writing with `stream` processing type, see [Output port writing](output-port-writing.md).

##### Input port metadata

In input port reading, only metadata field of some particular data types can be used. The type of the `FieldName` input field can only be `string`, `byte` or `cbyte`.

##### Processing of input port record

When graph runs, data is read from original data source (according to metadata of an edge connected to an optional input port of **Readers**) and received by a **Reader** through its optional input port. Each record is read independently of the other records. The specified field of each one is processed by the **Reader** according to the output metadata.

##### Readers with input port reading
> [!IMPORTANT]
> Remember that port reading can also be used by **DBExecute** for receiving SQL commands. **Query URL** will be as follows: `port:$0.fieldName:discrete.` Also an SQL command can be read from a file. Its name, including path, is then passed to DBExecute from an input port and the **Query URL** attribute should be the following: `port:$0.fieldName:source`.

| [CloverDataReader](cloverreader.md) |
| --- |
| [ComplexDataReader](complexdatareader.md) |
| [DBFDataReader](dbfdatareader.md) |
| [DatabaseReader](dbinputtable.md) |
| [EDIFACTReader](edifactreader.md) |
| [FlatFileReader](flatfilereader.md) |
| [JSONExtract](jsonextract.md) |
| [JSONReader](jsonreader.md) |
| [MongoDBReader](mongodbreader.md) |
| [MultiLevelReader](multilevelreader.md) |
| [QuickBaseRecordReader](quickbaserecordreader.md) |
| [SpreadsheetDataReader](spreadsheetreader.md) |
| [X12Reader](x12reader.md) |
| [XMLExtract](xmlextract.md) |
| [XMLReader](xmlreader.md) |
| [XMLXPathReader](xmlxpathreader.md) |

Metadata on the input port of [EmailReader](emailreader.md) can have only one field.
