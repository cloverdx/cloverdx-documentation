<!-- Development > Component reference > Writers > MSSQLBulkWriter -->

### MSSQLBulkWriter

![MSSQLDataWriter 64x64](../figures/MSSQLDataWriter-64x64.png)

| [Short description](mssqldatawriter.md#short-description) |
| --- |
| [Ports](mssqldatawriter.md#ports) |
| [Metadata](mssqldatawriter.md#metadata) |
| [MSSQLBulkWriter attributes](mssqldatawriter.md#mssqlbulkwriter-attributes) |
| [Details](mssqldatawriter.md#details) |
| [Examples](mssqldatawriter.md#examples) |
| [Compatibility](mssqldatawriter.md#compatibility) |
| [See also](mssqldatawriter.md#see-also) |

#### Short description

**MSSQLBulkWriter** loads data into MSSQL database.
> [!IMPORTANT]
> When to use MSSQLBulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](mssqldatawriter.md#mssqldatawriter-footnote1) | Records to be loaded into the database | Any |
| Output | 0 | **⨯** | For information about incorrect records | Input 0 (plus three [Error Fields for MSSQLBulkWriter](mssqldatawriter.md#mssqldatawriter-error-fields) |

| 1 |  If no file containing data for loading (**Loader input file**) is specified, the input port must be connected. |
| --- | --- |

This component has one optional input port and one optional output port.

#### Metadata

**MSSQLBulkWriter** does not propagate metadata.

Metadata on the output port 0 contains three additional fields at their end: `number of incorrect row`, `number of incorrect column`, `error message`.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| LastInputField + 1 | <anyname1> | integer | The number of the incorrect row. |
| LastInputField + 2 | <anyname2> | integer | The number of the incorrect column. |
| LastInputField + 3 | <anyname3> | string | The error message. |

#### MSSQLBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Path to bcp utility | yes | The name of the bcp utility, including path. SQL Server Client Connectivity Components must be installed and configured on the same machine where **CloverDX** runs. The bcp command line tool must be available. |  |
| Database | yes | The name of the database where the destination table or view resides. |  |
| Server name |  | The name of the server to which bcp utility should connect.  If the bcp utility connects to local named or remote named instance of server, **Server name** should be set to `serverName\instanceName`.  If the bcp utility connects to a local default or remote default instance of server, **Server name** should be set to `serverName`. If it is not set, bcp connects to the local default instance of server on localhost. The same meaning is true for the `serverName` which can be set in **Parameters**. However, if both **Server name** attribute and the `serverName` parameter are set, `serverName` in **Parameters** is ignored. |  |
| Database table | [[1]](mssqldatawriter.md#mssqldatawriter-attributes-fn01) | Name of the destination table. |  |
| Database view | [[1]](mssqldatawriter.md#mssqldatawriter-attributes-fn01) | Name of the destination view. All columns of the view must refer to the same table. |  |
| Database schema |  | Owner of table or view. It does not need to be specified if the user performing the operations is the owner. If it is not set and the user is not the owner, SQL Server returns an error message and the process is cancelled. |  |
| User name | yes | The login ID to be used when connecting to the server. The same can be set by specifying the value of the `userName` parameter in the **Parameters** attribute. If set, `userName` in **Parameters** is ignored. |  |
| Password | yes | The password for the login ID to be used when connecting to the server. The same can be set by specifying the value of the `password` parameter in the **Parameters** attribute. If set, `password` in **Parameters** is ignored. |  |
| Advanced |  |  |  |
| Column delimiter |  | The delimiter used for each column in data. Field values cannot have the delimiter within them. The same can be set by specifying the value of the **fieldTerminator** parameter in the **Parameters** attribute. If set, `fieldTerminator` in **Parameters** is ignored. | \t (default) \| any other character |
| Loader input file | [[2]](mssqldatawriter.md#mssqldatawriter-footnote3) | Name of the input file to be loaded, including path. For more information, see [Loader input file](mssqldatawriter.md#loader-input-file). |  |
| Parameters |  | All parameters that can be used as parameters by the bcp utility. These values are contained in a sequence of pairs of the following form: `key=value`, or `key` only (if the `key` value is the boolean `true`) separated from each other by a semicolon. If the value of any parameter contains a semicolon as its part, such value must be double quoted. For more information, see [Parameters](mssqldatawriter.md#parameters). |  |

| 1 |  One of these must be specified. |
| --- | --- |

| 2 |  If the input port is not connected, **Loader input file** must be specified and contain data. For more information, see [Loader input file](mssqldatawriter.md#loader-input-file). |
| --- | --- |

#### Details

**MSSQLBulkWriter** loads data into a MSSQL database using the MSSQL database client. SQL Server Client Connectivity Components must be installed and configured on the same machine where **CloverDX** runs. The `bcp` command line tool must be available.

**MSSQLBulkWriter** reads data through the input port or from a file. If the input port is not connected to any other component, data must be contained in file that should be specified in the component using **Loader input file** attribute.

If you connect some other component to the optional output port, it can serve to log the rejected records and information about errors. Metadata on this error port must have the same metadata fields as the input records plus three additional fields at its end: `number of incorrect row` (integer), `number of incorrect column` (integer), `error message` (string).

**MSSQLBulkWriter** is a bulk loader suitable for uploading many records to database. To insert several records, you can also use [DatabaseWriter](dboutputtable.md) which does not require the `bcp` utility.

##### Loader input file

Depending on an edge being connected to the input port, you either can or you must specify another attribute (**Loader input file**). It is the name of an input file with data to be loaded, including its path.

- If it is not set, a loader file is created in **CloverDX** or OS temporary directory (on Windows) or `named pipe` is used instead of temporary file (on Unix). The file is deleted after the load finishes.
- If it is set, a specified file is created. It is not deleted after data is loaded and it is overwritten on each graph run.
- If an input port is not connected, the file must exist, must be specified and must contain data that should be loaded. It is not deleted nor overwritten.

##### Parameters

**Parameters** serve to pass additional parameters to the `bcp` utility. All of the parameters must have the form of `key=value` or `key` only (if its value is `true`). Individual parameters must be separated from each other by a colon, semicolon or pipe. Note that a colon, semicolon or pipe can also be a part of some parameter value, but in this case the value must be double quoted.

Among the optional parameters, you can also set `userName`, `password` or `fieldTerminator` for **User name**, **Password** or **Column delimiter** attributes, respectively. If some of the three attributes (**User name**, **Password** and **Column delimiter**) are set, corresponding parameter value will be ignored.

If you also need to specify the server name, you should do it within parameters. The pattern is as follows: `serverName=[msServerHost]:[msServerPort]`. For example, you can specify both server name and user name in the following way: `serverName=msDbServer:1433|userName=msUser`.

##### Notes and limitations

**MSSQLBulkWriter** does not write lists and maps. It converts maps and lists to string and writes the string.

#### Examples

##### Loading data to MSSQL database

Load records (productID, amount) to table `products` of MSSQL database `sales` on `mssql.example.com`. Database schema is `dbo`, username is `smithj` and password is `smithy`.

###### Solution

Install the `bcp` utility.

Set up the following attributes of **MSSQLBulkWriter**.

| Attribute | Value |
| --- | --- |
| Path to bcp utility | C:/Program Files/Microsoft SQL Server/Client SDK/ODBC/170/Tools/Binn/bcp.exe |
| Database | sales |
| Server name | mssql.example.com |
| Database table | products |
| Database schema | dbo |
| User | smithj |
| Password | smithy |

In case the server uses a non-standard port number, append the port number after **Server name**.

```
mssql.example.com,1437
```

The port number is separated by a comma, not by a semicolon.

#### Troubleshooting

To test that the connection to database works, you can read some database table with the `bcp` utility directly:

```bash
bcp [database_name].[database_schema].[tablename] out outputfile -U user -S serverHostName,port -c
```

e.g.

```bash
bcp master.dbo.products out products.txt -U doejohn -S mssql.example.com,1435 -c
```

You can use the utility to check that you can insert records into database table:

```bash
bcp [database_name].[database_schema].[tablename] in inputfile -U user -S serverHostName,port -c
```

e.g.

```bash
bcp master.dbo.products in inputfile.txt -U doejohn -S mssql.example.com,1435 -c
```

The `inputfile.txt` should be a tab-delimited csv file.

See also [documentation on bcp](https://msdn.microsoft.com/en-us/library/ms162802.aspx).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.3.0 | **MSSQLDataWriter** was renamed to **MSSQLBulkWriter**. |
| 6.4.0 | Added support for **-u** (trustServerCertificate) and **-Y** (encryptionMode) options in **Parameters** attribute. |

#### See also

| [DatabaseWriter](dboutputtable.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
