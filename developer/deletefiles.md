<!-- Development > Component reference > File Operations > DeleteFiles -->

### DeleteFiles

![DeleteFiles 64x64](../figures/DeleteFiles-64x64.png)

| [Short description](deletefiles.md#short-description) |
| --- |
| [Ports](deletefiles.md#ports) |
| [Metadata](deletefiles.md#metadata) |
| [DeleteFiles attributes](deletefiles.md#deletefiles-attributes) |
| [Details](deletefiles.md#details) |
| [Examples](deletefiles.md#examples) |
| [See also](deletefiles.md#see-also) |

#### Short description

**DeleteFiles** can be used to delete files and directories (also recursively).

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

**DeleteFiles** does not propagate metadata from left to right or from right to left.

This component has metadata templates. For details on **DeleteFiles** metadata templates, see [Details](deletefiles.md#details) or [metadata templates](components.md#metadata-templates) for general info on metadata templates.

#### DeleteFiles attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes[[1]](deletefiles.md#deletefiles-attributes-fn01) | The path to the file or directory to be deleted (see [Supported URL formats for file operations](fileoperations-url-formats.md)). |  |
| Recursive | no | Delete directories recursively. | false (default) \| true |
| Input mapping | [[2]](deletefiles.md#deletefiles-attributes-fn02) | Defines mapping of input records to component attributes. |  |
| Output mapping | [[2]](deletefiles.md#deletefiles-attributes-fn02) | Defines mapping of results to standard output port. |  |
| Error mapping | [[2]](deletefiles.md#deletefiles-attributes-fn02) | Defines mapping of errors to error output port. |  |
| Redirect error output | no | If enabled, errors will be sent to the standard output port instead of the error port. | false (default) \| true |
| Verbose output | no | If enabled, one input record may cause multiple records to be sent to the output (e.g. as a result of wildcard expansion). Otherwise, each input record will yield just one cumulative output record. | false (default) \| true |
| Advanced |  |  |  |
| Stop processing on fail | no | By default, a failure causes the component to skip all subsequent input records and send the information about skipped input files to the error output port. This behavior can be turned off by this attribute.  False: If an error occurs (e.g. file cannot be found), the component will continue deleting subsequent files.  True: If an error occurs, the component will stop deleting subsequent files and will send the information about skipped operations to the error port. **Note:** this function works only if an edge is connected to the component’s error port. | true (default) \| false |

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
| fileURL | File URL | string |  |
| recursive | Recursive | boolean | true \| false |

##### Output mapping

The editor allows you to map the results and the input data to the output port.

If output mapping is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| fileURL | string | The path to the file or directory that was deleted. |
| result | boolean | True if the operation has succeeded (can be false when **Redirect error output** is enabled). |
| errorMessage | string | If the operation has failed, the field contains the error message (used when **Redirect error output** is enabled). |
| stackTrace | string | If the operation has failed, the field contains the stack trace of the error (used when **Redirect error output** is enabled). |

##### Error mapping

The editor allows you to map the errors and the input data to the error port.

If error mapping is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| result | boolean | Will always be set to false. |
| errorMessage | string | The error message. |
| stackTrace | string | The stack trace of the error. |
| fileURL | string | URL of the deleted file or directory. |

#### Examples

| [Deleting a single file](deletefiles.md#deleting-a-single-file) |
| --- |
| [Deleting directories](deletefiles.md#deleting-directories) |
| [Stop deleting if deleting fails](deletefiles.md#stop-deleting-if-deleting-fails) |

##### Deleting a single file

Delete a file `${DATATMP_DIR}/delete_me.txt`.

###### Solution

Use **File URL** attribute.

| Attribute | Value |
| --- | --- |
| File URL | ${DATATMP_DIR}/delete_me.txt |

##### Deleting directories

Delete directory `${DATATMP_DIR}/old_directory` with all files.

###### Solution

Use **File URL** and **Recursive**.

| Attribute | Value |
| --- | --- |
| File URL | ${DATATMP_DIR}/old_directory |
| Recursive | true |

Note: you need to check the **recursive** attribute also in the case of deleting a single empty directory.

##### Stop deleting if deleting fails

Delete files from the following list. If any of the files cannot be deleted, stop and don’t delete the following items from the list.

```
file1.txt
file2.txt
file3.txt
```

The files `file1.txt` and `file3.txt` exist, the file `file2.txt` does not exist.

###### Solution

Get file URLs from the input port one by one and set **Stop processing on fail** to `true` (default value).

This does not cause jobflow to fail!

#### See also

| [CreateFiles](createfiles.md) |
| --- |
| [MoveFiles](movefiles.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of File Operations](common-of-file-operations.md) |
| [File Operations comparison](common-of-file-operations.md#file-operations-comparison) |
