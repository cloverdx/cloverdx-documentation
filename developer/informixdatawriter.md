<!-- Development > Component reference > Writers > InformixBulkWriter -->

### InformixBulkWriter

![InformixDataWriter 64x64](../figures/InformixDataWriter-64x64.png)

| [Short description](informixdatawriter.md#short-description) |
| --- |
| [Ports](informixdatawriter.md#ports) |
| [Metadata](informixdatawriter.md#metadata) |
| [InformixBulkWriter attributes](informixdatawriter.md#informixbulkwriter-attributes) |
| [Details](informixdatawriter.md#details) |
| [Compatibility](informixdatawriter.md#compatibility) |
| [See also](informixdatawriter.md#see-also) |

#### Short description

**InformixBulkWriter** loads data into an Informix database.
> [!IMPORTANT]
> When to use InformixBulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](informixdatawriter.md#informixdatawriter-footnote1) | Records to be loaded into the database | Any |
| Output | 0 | **⨯** | For information about incorrect records. | Input 0 (plus two [Error fields for InformixBulkWriter](informixdatawriter.md#informixdatawriter-error-fields)[[2]](informixdatawriter.md#informixdatawriter-footnote2)) |

| 1 |  If no file containing data for loading (**Loader input file**) is specified, the input port must be connected. |
| --- | --- |

| 2 |  Metadata on the output port 0 contains two additional fields at their end: `number of row`, `error message`. |
| --- | --- |

#### Metadata

**InformixBulkWriter** does not propagate metadata.

Metadata on the output port 0 contains two additional fields at their end: `number of row`, `error message`.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| LastInputField + 1 | <anyname1> | integer | The number of the row. |
| LastInputField + 2 | <anyname2> | string | The error message. |

#### InformixBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| The path to the dbload utility. | yes | The name of the dbload utility, including the path. The Informix server must be installed and configured on the same machine where **CloverDX** runs and the user must be logged in as root. The dbload command line tool must be available. |  |
| Host |  | The host where the database server is located. |  |
| Database | yes | The name of the database into which the records should be loaded. |  |
| Database table | yes | The name of the database table into which the records should be loaded. |  |
| Advanced |  |  |  |
| Control script |  | The control script to be used by the dbload utility. If it is not set, the default control script is used instead. Is used only if the **Use load utility** attribute is set to `false`. |  |
| Error log URL |  | The name of the error log file, including the path. If not set, the default error log file is used instead. | ./error.log |
| Max error count |  | The maximum number of allowed records. When this number is exceeded, the graph fails. | 10 (default) \| 0-N |
| Ignore rows |  | The number of rows to be skipped. Used only if the **Use load utility** attribute is set to `false`. | 0 (default) \| 1-N |
| Commit interval |  | Commit interval in number of rows. | 100 (default) \| 1-N |
| Column delimiter |  | One character delimiter used for each column in data. Field values must not include this delimiter as their part. Used only if the **Use load utility** attribute is set to `false`. | "\|" (default) \| other character |
| Loader input file |  | The name of the input file to be loaded, including the path. Normally, this file is a temporary storage for data to be passed to the dbload utility unless `named pipe` is used instead. |  |
| Deprecated |  |  |  |
| Use load utility |  | By default, the dbload utility is used to load data to the database. If set to `true`, load2 utility is used instead of dbload. The load2 utility must be available. | false (default) \| true |
| User name |  | The username to be used when connecting to the database. Used only if the **Use load utility** attribute is set to `true`. |  |
| Password |  | The password to be used when connecting to the database. The password is used only if the **Use load utility** attribute is set to `true`. |  |
| Ignore unique key violation |  | By default, unique key violation is not ignored. If key values are not unique, the graph fails. If set to `true`, unique key violation is ignored. The attribute is used only if the **Use load utility** attribute is set to `true`. | false (default) \| true |
| Use insert cursor |  | By default, the insert cursor is used. Using the insert cursor doubles the transfer performance. Used only if the **Use load utility** attribute is set to `true`. Disable it by setting the value to `false`. | true (default) \| false |

#### Details

**InformixBulkWriter** loads data into a database using the Informix database client (`dbload` utility) or the `load2` free library.

It is very important to have the server with the database on the same computer as both the `dbload` database utility and **CloverDX**; furthermore, you must be logged in as the root user. The Informix server must be installed and configured on the same machine where **CloverDX** runs and the user must be logged in as root. The Dbload command line tool must also be available.

**InformixBulkWriter** reads data from the input port or a file. If the input port is not connected to any other component, data must be contained in a file that should be specified in the component.

If you connect a component to the optional output port, rejected records along with information about errors are sent to it.

Another tool is the `load2` free library instead of the `dbload` utility. The `load2` free library can be used even if the server is located on a remote computer.

##### Loader input file

The name of the input file to be loaded, including the path. Normally, this file is a temporary storage for data to be passed to the dbload utility unless `named pipe` is used instead.

- If it is not set, a loader file is created in **CloverDX** or the OS temporary directory. The file is deleted after the load finishes.
- If it is set, a specified file is created. It is not deleted after data is loaded and it is overwritten on each graph run.
- If the input port is not connected, this file must exist, must be specified and must contain data that should be loaded into database. It is not deleted or overwritten.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.7.0-M2 | The attributes *Use load utility*, *User name*, *Password*, *Ignore unique key violation* and *Use insert cursor* were deprecated. |
| 5.3.0 | **InformixDataWriter** was renamed to **InformixBulkWriter**. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
