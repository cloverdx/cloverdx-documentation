<!-- Development > Component reference > File Operations > CopyFiles -->

### CopyFiles

![CopyFiles 64x64](../figures/CopyFiles-64x64.png)

| [Short description](copyfiles.md#short-description) |
| --- |
| [Ports](copyfiles.md#ports) |
| [Metadata](copyfiles.md#metadata) |
| [CopyFiles attributes](copyfiles.md#copyfiles-attributes) |
| [Details](copyfiles.md#details) |
| [Examples](copyfiles.md#examples) |
| [See also](copyfiles.md#see-also) |

#### Short description

**CopyFiles** can be used to copy files and directories.

**CopyFiles** can copy multiple sources into one destination directory, or a regular source file to a target file. Directories can be copied recursively. Optionally, existing files may be skipped or updated based on the modification date of the files.

| Inputs | Outputs | Auto-propagated metadata |
| --- | --- | --- |
| 0-1 | 0-2 | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | Input data records to be mapped to component attributes. | Any |
| Output | 0 | **⨯** | Results | Any |
| 1 | **⨯** | Errors | Any |  |

#### Metadata

**CopyFiles** does not propagate metadata from left to right or from right to left.

This component has metadata template available. See [Details](copyfiles.md#details) for details on template fields of **CopyFiles** or [metadata templates](components.md#metadata-templates) for general details on metadata templates.

#### CopyFiles attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Source file URL | yes [[1]](copyfiles.md#copyfiles-attributes-fn01) | Path to the source file or directory (see [Supported URL formats for file operations](fileoperations-url-formats.md)). |  |
| Target file URL | yes[[1]](copyfiles.md#copyfiles-attributes-fn01) | Path to the destination file or directory (see [Supported URL formats for file operations](fileoperations-url-formats.md)). When it points to a directory, the source will be copied into the directory.  It must be a path to a single file or directory. |  |
| Recursive | no | Copies directories recursively. | false (default) \| true |
| Overwrite | no | Specifies whether existing files shall be overwritten.  In **always mode**, the target will be overwritten.  In **update mode**, the target will be overwritten only when the source file is newer than the destination file.  In **never mode**, the target will not be overwritten. | always (default) \| update \| never |
| Create parent directories | no | Attempts to create non-existing parent directories.  When the **Create parent directories** option is enabled and the **Target file URL** ends with a slash ('/'), it is treated as a parent directory, i.e. the source directory or file is copied *into* the target directory, even if it does not exist. | false (default) \| true |
| Input mapping | [[2]](copyfiles.md#copyfiles-attributes-fn02) | Defines mapping of input records to component attributes. |  |
| Output mapping | [[2]](copyfiles.md#copyfiles-attributes-fn02) | Defines mapping of results to the standard output port. |  |
| Error mapping | [[2]](copyfiles.md#copyfiles-attributes-fn02) | Defines mapping of errors to the error output port. |  |
| Redirect error output | no | If enabled, errors will be sent to the output port instead of the error port. | false (default) \| true |
| Verbose output | no | If enabled, one input record may cause multiple records to be sent to the output (e.g. as a result of wildcard expansion). Otherwise, each input record will yield just one cumulative output record. | false (default) \| true |
| Advanced |  |  |  |
| Stop processing on fail | no | By default, a failure causes the component to skip all subsequent input records and send the information about skipped input records to the error output port. This behavior can be turned off by this attribute. **Note:** this function works only if an edge is connected to the component’s error port. | true (default) \| false |

| 1 |  The attribute is required, unless specified in the **Input mapping**. |
| --- | --- |

| 2 |  Required if the corresponding edge is connected. |
| --- | --- |

#### Details

Editing any of the **Input**, **Output** or **Error mapping** opens the [Transform Editor](transformations.md#transform-editor).

##### Input mapping

The editor allows you to override selected attributes of the component with the values of the input fields.

| Field Name | Attribute | Type | Possible values |
| --- | --- | --- | --- |
| sourceURL | Source file URL | string |  |
| targetURL | Target file URL | string |  |
| recursive | Recursive | boolean | true \| false |
| overwrite | Overwrite | string | "always" \| "update" \| "never" |
| makeParentDirs | Create parent directories | boolean | true \| false |

##### Output mapping

The editor allows you to map the results and the input data to the output port.

If Output mapping is empty, fields of the input record and result record are mapped to the output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| sourceURL | string | URL of the source file. |
| targetURL | string | URL of the destination. |
| resultURL | string | A new URL of the successfully copied file. Only set in **Verbose output** mode. |
| result | boolean | True if the operation has succeeded (can be false when **Redirect error output** is enabled). |
| errorMessage | string | If the operation has failed, the field contains the error message (used when **Redirect error output** is enabled). |
| stackTrace | string | If the operation has failed, the field contains the stack trace of the error (used when **Redirect error output** is enabled). |

##### Error mapping

The editor allows you to map errors and input data to the error port.

If Error mapping is empty, fields of the input record and result record are mapped to the output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| result | boolean | Will always be set to false. |
| errorMessage | string | The error message. |
| stackTrace | string | The stack trace of the error. |
| sourceURL | string | URL of the source file. |
| targetURL | string | URL of the destination. |

##### Stop processing on fail

If you get file URLs from the input port having **Stop processing on fail** set to **true** and an error occurs, the record causing the error and the following ones are skipped.

#### Examples

| [Copying files from one directory to another](copyfiles.md#copying-files-from-one-directory-to-another) |
| --- |
| [Using Stop processing on fail](copyfiles.md#using-stop-processing-on-fail) |
| [Non-recursive copying directory with mixed content](copyfiles.md#non-recursive-copying-directory-with-mixed-content) |

##### Copying files from one directory to another

Copy `.txt` files from `${DATAIN_DIR}/FO/` to `${DATAOUT_DIR}/FO/`. The target directory may not exist. If the files in the target directory exist, they should be overwritten.

###### Solution

Use the attributes **Source file URL**, **Target file URL** and **Create parent directories**.

| Attribute | Value |
| --- | --- |
| Source file URL | ${DATAIN_DIR}/FO/*.txt |
| Target file URL | ${DATAOUT_DIR}/FO/ |
| Create parent directories | true |

##### Using stop processing on fail

Copy files `f1.txt``f2.txt` and `f3.txt`. If you cannot copy a file, continue with the following one.

```
-rw-rw-r--. 1 clover clover 0 Feb 23 18:11 f1.txt
-rw-------. 1 user23 user23 0 Feb 23 18:11 f2.txt
-rw-rw-r--. 1 clover clover 0 Feb 23 18:11 f3.txt
```

###### Solution with Source file URL attribute

The solution without reading file URLs from an input edge is the same as in the previous example. Use the attributes **Source file URL**, **Target file URL** and **Create parent directories**.

Note that only files `f1.txt` and `f2.txt` will be copied. The file `f2.txt` cannot be copied as the user `clover` does not have read access to the file.

###### Solution with input edge

If you read URLs of files from an input edge one by one, use the attributes **Target file URL**, **Create parent directories**, **Input mapping** and **Stop processing on fail**.

| Attribute | Value |
| --- | --- |
| Target file URL | ${DATAOUT_DIR}/FO/ |
| Create parent directories | true |
| Input mapping |  |
| Stop processing on fail | false |

In **Input mapping**, you map **Source URL**.

Note that you need to uncheck the attribute **Stop processing on fail**. Otherwise only the file `f1.txt` would be copied. (Assuming that the files come in ascending order.)

##### Non-recursive copying directory with mixed content

This example shows non-recursive copying of files from one directory to another.

Copy files and directories from `${DATAIN_DIR}/abc` to `${DATAOUT_DIR}/def`. If a directory in `${DATAIN_DIR}/abc` contains a file or a directory, these files and directories should not be copied.

Source directory

```
${DATAIN_DIR}/abc/file.txt
${DATAIN_DIR}/abc/dirA/file2.txt
```

Expected result

```
${DATAIN_DIR}/def/file.txt
${DATAIN_DIR}/def/dirA
```

###### Solution

Use **ListFiles** to list the files and directories to be copied. In **ListFiles**, set the **File URL** attribute to the source directory.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/abc/ |

In **CopyFiles**, copy the files and directories from the list received from an input edge.

| Attribute | Value |
| --- | --- |
| Target file URL | ${DATAIN_DIR}/def/ |
| Create parent directories | true |
| Input mapping | ```ctl function integer transform() {     $out.0.sourceURL = $in.0.URL;      return ALL; } ``` |
> [!NOTE]
> The **ListFiles** component is necessary to list all files and directories. If you non-recursively copy files with **CopyFiles** only, the copying stops when a first subdirectory is reached.

#### See also

| [MoveFiles](movefiles.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of File Operations](common-of-file-operations.md) |
| [File Operations comparison](common-of-file-operations.md#file-operations-comparison) |
