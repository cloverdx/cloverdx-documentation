<!-- Development > Component reference > File Operations > CreateFiles -->

### CreateFiles

![CreateFiles 64x64](../figures/CreateFiles-64x64.png)

| [Short description](createfiles.md#short-description) |
| --- |
| [Ports](createfiles.md#ports) |
| [Metadata](createfiles.md#metadata) |
| [CreateFiles attributes](createfiles.md#createfiles-attributes) |
| [Details](createfiles.md#details) |
| [Examples](createfiles.md#examples) |
| [See also](createfiles.md#see-also) |

#### Short description

**CreateFiles** can create files and directories. It is also capable of setting a modification date of both existing and newly created files and directories. Optionally, non-existing parent directories may also be created.

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

**CreateFiles** does not propagate metadata from left to right or from right to left.

This component has metadata template available. The templates of **CreateFiles** are described in [Details](createfiles.md#details). See details on [metadata templates](components.md#metadata-templates).

#### CreateFiles attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes[[1]](createfiles.md#createfiles-footnote1) | Path to the file or directory to be created (see [Supported URL formats for file operations](fileoperations-url-formats.md)). If it ends with a slash ('/'), it denotes that a directory should be created, which can also be specified using the **Create as directory** attribute. |  |
| Create as directory | no | Specifies that directories should be created instead of regular files. | false (default) \| true |
| Create parent directories | no | Attempt to create non-existing parent directories. | false (default) \| true |
| Last modified date | no | Set the last modified date of existing and newly created files to the specified value. Format of the date is defined in the `DEFAULT_DATETIME_FORMAT` property ([Engine configuration](../admin/designer-configuration.md#engine-configuration)). |  |
| Input mapping | [[2]](createfiles.md#createfiles-attributes-fn02) | Defines mapping of input records to the component attributes. |  |
| Output mapping | [[2]](createfiles.md#createfiles-attributes-fn02) | Defines mapping of results to the standard output port. |  |
| Error mapping | [[2]](createfiles.md#createfiles-attributes-fn02) | Defines mapping of errors to the error output port. |  |
| Redirect error output | no | If enabled, errors will be sent to the standard output port instead of the error port. | false (default) \| true |
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
| fileURL | File URL | string |  |
| directory | Create as directory | boolean | true \| false |
| makeParentDirs | Create parent directories | boolean | true \| false |
| modifiedDate | Last modified date | date |  |

##### Output mapping

The editor allows you to map the results and the input data to the output port.

If Output mapping is empty, fields of the input record and result record are mapped to the output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| fileURL | string | URL of the target file or directory. |
| result | boolean | True if the operation has succeeded (can be false when **Redirect error output** is enabled). |
| errorMessage | string | If the operation has failed, the field contains the error message (used when **Redirect error output** is enabled). |
| stackTrace | string | If the operation has failed, the field contains the stack trace of the error (used when **Redirect error output** is enabled). |

##### Error mapping

The editor allows you to map the errors and the input data to the error port.

If Error mapping is empty, fields of the input record and result record are mapped to the output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| result | boolean | Will always be set to false. |
| errorMessage | string | The error message. |
| stackTrace | string | The stack trace of the error. |
| fileURL | string | URL of the target file or directory. |

#### Examples

##### Touching the File with CreateFiles

Create file `touch_me.txt`. If the file exists, update the last modification time.

###### Solution

Use attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATATMP_DIR}/touch_me.txt |
| Input mapping | See the code below |

```ctl
function integer transform() {
    $out.0.modifiedDate = today();

    return ALL;
}
```

You can optionally set **Create parent directories** to true.

#### See also

| [DeleteFiles](deletefiles.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of File Operations](common-of-file-operations.md) |
| [File Operations comparison](common-of-file-operations.md#file-operations-comparison) |
