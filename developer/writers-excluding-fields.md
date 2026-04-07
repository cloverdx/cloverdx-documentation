<!-- Development > Component reference > Writers > Common properties of Writers > Excluding fields -->

#### Excluding fields

Some components without output mapping let you omit particular fields from results. Use the **Exclude fields** attribute and specify metadata fields that should not be written to the output. It has a form of a sequence of field names separated by a semicolon. The field names can be typed manually of created using a key dialog.

**Excluding fields** attribute is available in:

| [CloverDataWriter](cloverwriter.md) |
| --- |
| [FlatFileWriter](flatfilewriter.md) |
| [DBFDataWriter](dbfdatawriter.md) |

If you part data and **Partition file tag** is set to **Key file tag**, values of **Partition key** form the names of output files, and the values are written to the corresponding files as well. To avoid saving the same information twice, you can select the fields that will be excluded from writing.

Use the **Exclude fields** attribute to specify fields that should not be written into output files. The fields will only be a part of file or sheet names, but will not be written to the contents of these files.

When you read these files back, you can acquire the values with an autofilling function `source_name`.

**Example:** when you have files created using **Partition key** set to `City` and the output files are `London.txt`, `Stockholm.txt`, etc., you can get these values (`London`, `Stockholm`, etc.) from the file names. The `City` field values do not need to be contained in the files.
> [!NOTE]
> If you want to use the value of a field as the path to an existing file, type the following as the **File URL** attribute in **Writer**:
>
> `//#`
>
> This way, if the value of the field used for partitioning is `path/to/my/file/filename.txt`, it will be assigned to the output file as its name. For this reason, the output file will be located in `path/to/my/file` and its name will be `filename.txt`.
