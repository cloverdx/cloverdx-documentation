<!-- Development > Component reference > File Operations > MoveFiles -->

### MoveFiles

![MoveFiles 64x64](../figures/MoveFiles-64x64.png)

| [Short description](movefiles.md#short-description) |
| --- |
| [Ports](movefiles.md#ports) |
| [Metadata](movefiles.md#metadata) |
| [MoveFiles attributes](movefiles.md#movefiles-attributes) |
| [Details](movefiles.md#details) |
| [Examples](movefiles.md#examples) |
| [See also](movefiles.md#see-also) |

#### Short description

**MoveFiles** can be used to move files and directories.

**MoveFiles** can move multiple sources into one destination directory or a regular source file to a target file. Optionally, existing files may be skipped or updated based on the modification date of the files.

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

**MoveFiles** does not propagate metadata form left to right or from right to left.

This component has metadata templates. See [Details](movefiles.md#details). For general details on metadata templates, see [metadata templates](components.md#metadata-templates).

#### MoveFiles attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Source file URL | yes[[1]](movefiles.md#movefiles-attributes-fn01) | Path to the source file or directory (see [Supported URL formats for file operations](fileoperations-url-formats.md)). |  |
| Target file URL | yes[[1]](movefiles.md#movefiles-attributes-fn01) | Path to the destination file or directory (see [Supported URL formats for file operations](fileoperations-url-formats.md)). When it points to a directory, the source will be moved into the directory.  It must be a path to a single file or directory. |  |
| Overwrite | no | Specifies whether existing files shall be overwritten.  In always mode, the target will be overwritten.  In update mode, the target will be overwritten only when the source file is newer than the destination file.  In never mode, the target will not be overwritten. | always (default) \| update \| never |
| Create parent directories | no | Attempt to create non-existing parent directories.  When the **Create parent directories** option is enabled and the **Target file URL** ends with a slash ('/'), it is treated as a parent directory, i.e. the source directory or file is moved *into* the target directory, even if it does not exist. | false (default) \| true |
| Input mapping | [[2]](movefiles.md#movefiles-attributes-fn02) | Defines mapping of input records to component attributes. |  |
| Output mapping | [[2]](movefiles.md#movefiles-attributes-fn02) | Defines mapping of results to the standard output port. |  |
| Error mapping | [[2]](movefiles.md#movefiles-attributes-fn02) | Defines mapping of errors to the error output port. |  |
| Redirect error output | no | If enabled, errors will be sent to the output port instead of the error port. | false (default) \| true |
| Verbose output | no | If enabled, one input record may cause multiple records to be sent to the output, e.g. as a result of wildcard expansion. Otherwise, each input record will yield just one cumulative output record. | false (default) \| true |
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
| sourceURL | Source file URL. | string |  |
| targetURL | Target file URL. | string |  |
| overwrite | Overwrite | string | "always" \| "update" \| "never" |
| makeParentDirs | Create parent directories | boolean | true \| false |

##### Output mapping

The editor allows you to map the results and the input data to the output port.

If the output mapping is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| sourceURL | string | The URL of the source file. |
| targetURL | string | The URL of the destination. |
| resultURL | string | The new URL of the successfully moved file. Only set in **Verbose output** mode. |
| result | boolean | True if the operation has succeeded (can be false when **Redirect error output** is enabled). |
| errorMessage | string | If the operation has failed, the field contains the error message (used when **Redirect error output** is enabled). |
| stackTrace | string | If the operation has failed, the field contains the stack trace of the error (used when **Redirect error output** is enabled). |

##### Error mapping

The editor allows you to map the errors and the input data to the error port.

If the error mapping is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| result | boolean | Will always be set to false. |
| errorMessage | string | The error message. |
| stackTrace | string | The stack trace of the error. |
| sourceURL | string | The URL of the source file. |
| targetURL | string | The URL of the destination. |

This component can be used for renaming files, too.

#### Examples

##### Moving a File

Move file `house.xml` from `${DATATMP_DIR}/dirA` to directory `${DATATMP_DIR}/dirB/`. The target directory may not exist.

###### Solution

Use **Source file URL**, **Target file URL** and **Create parent directories** attributes.

| Attribute | Value |
| --- | --- |
| Source file URL | ${DATATMP_DIR}/dirA/house.xml |
| Target file URL | ${DATATMP_DIR}/dirB/ |
| Create parent directories | true |

If a file with the same name exist in output directory, it is overwritten by default. See **Overwrite** attribute.

#### See also

| [CopyFiles](copyfiles.md) |
| --- |
| [MoveFiles](movefiles.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of File Operations](common-of-file-operations.md) |
| [File Operations comparison](common-of-file-operations.md#file-operations-comparison) |
