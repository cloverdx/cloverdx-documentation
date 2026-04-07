<!-- Development > Component reference > Writers > Trash -->

### Trash

![Trash 64x64](../figures/Trash-64x64.png)

| [Short description](trash.md#short-description) |
| --- |
| [Ports](trash.md#ports) |
| [Metadata](trash.md#metadata) |
| [Trash attributes](trash.md#trash-attributes) |
| [Compatibility](trash.md#compatibility) |
| [See also](trash.md#see-also) |

#### Short description

**Trash** discards data. For debugging purpose, it can write its data to a file (local or remote), or **Console** tab. Multiple inputs can be connected for improved graph legibility.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| none | 1–n | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 1-n | **✓** | For received data records | Any |

#### Metadata

**Trash** does not propagate metadata.

It has no metadata templates.

#### Trash attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Debug print |  | By default, all records are discarded. If set to `true`, all records are written to the debug file (if specified), or **Console** tab. You do not need to switch **Log level** from its default value (`INFO`). This mode is only supported when a single input port is connected. | false (default) \| true |
| Debug file URL |  | Attribute specifying debug output file. See [Supported file URL formats for Writers](examples-of-file-url-in-writers.md). If the path is not specified, the file is saved to the `${PROJECT}` directory. You do not need to switch **Log level** from its default value (`INFO`). |  |
| Debug append |  | By default, new records overwrite the older ones. If set to `true`, new records are appended to the older records stored in the output file(s). | false (default) \| true |
| Charset |  | Encoding of debug output. | UTF-8 (default) \| <other encodings> |
| Advanced |  |  |  |
| Print trash ID |  | By default, trash ID is not written to the debug output. If set to `true`, ID of the **Trash** is written to the debug file, or **Console** tab. You do not need to switch **Log level** from its default value (`INFO`). | false (default) \| true |
| Create directories |  | By default, non-existing directories are not created. If set to `true`, they are created. | false (default) \| true |
| Mode |  | Trash can run in either Performance or Validate records modes. In Performance mode, the raw data is discarded; in Validate records, Trash simulates a writer - attempting to deserialize the inputs. | Performance (default) \| Validate records |

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.0.5 | **Trash** can now write lists and maps. |

#### See also

| [DataGenerator](datagenerator.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
