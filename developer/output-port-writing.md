<!-- Development > Component reference > Writers > Common properties of Writers > Output port writing -->

#### Output port writing

Some **Writers** allow you to write data to the optional output port.

Below is the list of **Writers** allowing output port writing:

| [CloverDataWriter](cloverwriter.md) |
| --- |
| [FlatFileWriter](flatfilewriter.md) |
| [JSONWriter](jsonwriter.md) |
| [KafkaWriter](kafkawriter.md) |
| [SpreadsheetDataWriter](spreadsheetwriter.md) |
| [StructuredDataWriter](structurewriter.md) |
| [XMLWriter](extxmlwriter.md) |

The attributes for the output port writing in these components may be defined using the [URL file dialog](common-dialogs.md#url-file-dialog).

Set the **File URL** attribute of the **Writer** to `port:$0.FieldName[:processingType]`.

Here, `processingType` is optional and can be set to one of the following: `discrete` or `stream`. If it is not set explicitly, it is `discrete` by default.

- `discrete`
  The file content is stored into a field (of one record). The data should be small enough to fit into this one field.
  If the data is partitioned into multiple files, multiple output records are sent out. Each output record contains input data of one partition.
- `stream`
  The file content is written to a stream, which is split into chunks. The chunks are written into a user-specified output field. One chunk goes to one output record, therefore your data does not have to fit into a single data field.
  The stream is terminated with another record with null in the field (as a sentinel). If the data is partitioned into multiple files, null also serves as a delimiter between the files.
  The count of output records depends on the value of the `PortReadingWriting.DATA_LENGTH` parameter. The default value is 2,048 B.

If you connect the optional output port of any **Writer** with an edge to another component, metadata of the edge must contain the specified `FieldName` of a `string`, `byte` or `cbyte` data type.

When a graph runs, data is read through the input according to the input metadata, processed by the **Writer** according to the specified processing type and sent subsequently to the other component through the optional output port of the **Writer**.
