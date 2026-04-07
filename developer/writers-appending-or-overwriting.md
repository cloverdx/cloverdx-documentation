<!-- Development > Component reference > Writers > Common properties of Writers > Appending or overwriting -->

#### Appending or overwriting

If the target file exists, there are two options:

1. the existing file can be replaced;
2. the records can be appended to the existing content.

Appending or replacing is configured with the **Append** attribute.

If **Append** is set to `true`, records are appended to the file.

If **Append** is set to `false`,the file is overwritten. The default value is `false`.

You can also append data to files in local (non-remote) zip archives. In server environment, this means [use_local_context_url](../operations/sandboxes.md#execution-properties) has to be set to `true`.

**Append** is available in the following **Writers**:

| [CloverDataWriter](cloverwriter.md) |
| --- |
| [FlatFileWriter](flatfilewriter.md) |
| [StructuredDataWriter](structurewriter.md) |
| [Trash](trash.md) (the **Debug append** attribute) |
| [XMLWriter](extxmlwriter.md) |
