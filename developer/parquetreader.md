<!-- Development > Component reference > Readers > ParquetReader -->

### ParquetReader

![ParquetReader 64x64](../figures/ParquetReader-64x64.png)

| [Short description](parquetreader.md#short-description) |
| --- |
| [Ports](parquetreader.md#ports) |
| [Metadata](parquetreader.md#metadata) |
| [ParquetReader attributes](parquetreader.md#parquetreader-attributes) |
| [Details](parquetreader.md#details) |
| [Limitations](parquetreader.md#limitations) |
| [Compatibility](parquetreader.md#compatibility) |
| [See also](parquetreader.md#see-also) |

#### Short description

**ParquetReader** reads data stored in Apache Parquet files.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Parquet files | 0-1 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For [Input port reading](input-port-reading.md) |  |
| Output | 0 | **✓** | Successfully read records |  |
| 1 | **⨯** | Read errors |  |  |

When the error port is disconnected, the component fails on first error. When connected, the component provides an error record for every error and continues to run. A common type of error can be, for example, a failure to convert a Parquet data type to a CloverDX data type.

#### Metadata

**ParquetReader** propagates metadata when possible - when using a static local file URL.

Schema is automatically read from the specified Parquet file and converted to CloverDX metadata.

Metadata propagation is not available when using port reading or remote protocols.

Metadata on output port 0 can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### ParquetReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | URL to a Parquet file to be read.  Can be a single static file URL or a wildcard. Port reading is supported. |  |

#### Details

The **ParquetReader** component supports reading from a single Parquet file or multiple Parquet files specified using a file URL wildcard. Supported file URL formats are described in [Supported file URL formats for Readers](examples-of-file-url-in-readers.md).

The component also supports [Input port reading](input-port-reading.md).

The component automatically propagates metadata from the Parquet file schema. If you manually assign metadata, the Parquet columns are mapped to metadata fields by label.
> [!NOTE]
> **ParquetReader** reads only columns (fields) present in the output matadata. Reducing output metadata to contain only the desired fields can have a significant positive impact on read performance (by reducing unnecessary disk or network I/O).

##### Check Config

The component’s check config will report warnings when trying to read a Parquet type to an incompatible CloverDX data type (e.g. Parquet `BINARY` into CloverDX `integer`).

Warnings are also produced when reading types with loss of precision (e.g Parquet `MICROS`, `NANOS` dates).

##### Raw Reading

The **ParquetReader** component also supports "raw reads", i.e. the ability to read a Parquet column not only to its "natural" type based on logical annotation, but also read the underlying "raw" value into a corresponding CloverDX data type.

Examples of such cases are:

- Parquet logical type `TIMESTAMP` uses a primitive type `INT64`.By default, this is read into a `date` type, but it is possible to be read into `long` as well.
- Parquet logical type `DECIMAL` uses primitive types `INT32`, `INT64` or `BYTE_ARRAY` (depending on precision).By default, this is reads into `decimal` type, but it is possible to be read into `integer`, `long`, or `byte`.

This raw reading can be used to avoid loss of precision when reading e.g. `TIMESTAMP` in nanosecond precision. When reading into a CloverDX `date`, there is a precision loss because the `date` has millisecond precision. Reading into `long` gives you full internal value without precision loss.

##### Compression

In addition to uncompressed files, the following types of compression are officially supported:

- gzip
- snappy

#### Limitations

The nested Parquet types (lists and maps) are not supported.

The unsigned `INT` types and the `INT96` primitive type are not supported.

The `UUID` logical type is read as `byte`.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.10.0 | **ParquetReader** is available since **5.10.0**. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |

##### External links

*[https://parquet.apache.org/](https://parquet.apache.org/)*
