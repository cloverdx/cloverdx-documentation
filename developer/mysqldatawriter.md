<!-- Development > Component reference > Writers > MySQLBulkWriter -->

### MySQLBulkWriter

![MySQLDataWriter 64x64](../figures/MySQLDataWriter-64x64.png)

| [Short description](mysqldatawriter.md#short-description) |
| --- |
| [Ports](mysqldatawriter.md#ports) |
| [Metadata](mysqldatawriter.md#metadata) |
| [MySQLBulkWriter attributes](mysqldatawriter.md#mysqlbulkwriter-attributes) |
| [Details](mysqldatawriter.md#details) |
| [Notes and limitations](mysqldatawriter.md#notes-and-limitations) |
| [Examples](mysqldatawriter.md#examples) |
| [Compatibility](mysqldatawriter.md#compatibility) |
| [See also](mysqldatawriter.md#see-also) |

#### Short description

**MySQLBulkWriter** is a high-speed MySQL table loader. It uses a MySQL native client.
> [!IMPORTANT]
> When to use MySQLBulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](mysqldatawriter.md#mysqldatawriter-footnote1) | Records to be loaded into the database | Any |
| Output | 0 | **⨯** | For information about incorrect records | [Error metadata for MySQLBulkWriter](mysqldatawriter.md#mysqldatawriter-error-metadata) |

| 1 |  If no file containing data for loading (**Loader input file**)is specified, input port must be connected. |
| --- | --- |

#### Metadata

**MySQLBulkWriter** does not propagate metadata.

**Error metadata** cannot use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 0 | <any_name1> | integer | The number of the incorrect record (records are numbered starting from 1). |
| 1 | <any_name2> | integer | The number of the incorrect column. |
| 2 | <any_name3> | string | Error message |

#### MySQLBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| The path to MySQL utility | yes | The name of the MySQL utility, including the path. Must be installed and configured on the same machine where **CloverDX** runs. The MySQL command line tool must be available. |  |
| Host |  | Host where the database server is located. | localhost (default) \| other host |
| Database | yes | The name of the database into which the records should be loaded. |  |
| Database table | yes | The name of the database table into which the records should be loaded. |  |
| User name | yes | Database user |  |
| Password | yes | The password for a database user. |  |
| Advanced |  |  |  |
| Path to control script |  | The name of the command file containing the `LOAD DATA INFILE` statement, including the path. For more information, see [Path to control script](mysqldatawriter.md#path-to-control-script). |  |
| Lock database table |  | By default, the database is not locked and multiuser access is allowed. If set to `true`, the database table is locked to ensure exclusive access and possibly faster loading. | false (default) \| true |
| Ignore rows |  | The number of rows of a data file that should be skipped. By default, no records are skipped. Valid only for input file with data. | 0 (default) \| 1-N |
| Column delimiter |  | The delimiter used for each column in the data. Field values must not include this delimiter as their part. By default, a tabulator is used. | \t (default) \| other character |
| Loader input file | [[1]](mysqldatawriter.md#mysqldatawriter-footnote2) | The name of an input file to be loaded, including path. For more information, see [Loader input file](mysqldatawriter.md#loader-input-file). |  |
| Control script parameters |  | All parameters that can be used as parameters by the `load` method. These values are contained in a sequence of pairs of the following form: `key=value`, or `key` only (if the `key` value is the boolean `true`) separated from each other by a semicolon, colon, or pipe. If the value of any parameter contains the delimiter as its part, such value must be double quoted. |  |

| 1 |  If the input port is not connected, **Loader input file** must be specified and contain data. For more information, see [Loader input file](mysqldatawriter.md#loader-input-file). |
| --- | --- |

#### Details

**MySQLBulkWriter** loads data into a database table using native MySQL database client.

It reads data either from the input port or from an input file.

You can attach the **optional output port** and read records which have been reported as rejected.

**Reading from input port** (input port connected) dumps the data into a temporary file which is then used by `mysql` utility. You can set the temporary file explicitly by setting the **Loader input file** attribute or leave it blank to use default.

**Reading from a file** (no input connected) uses the **Loader input file** attribute as a path to your data file. The attribute is mandatory in this case. The file needs to be in a format recognized by the `mysql` utility (see *[MySQL LOAD DATA](http://dev.mysql.com/doc/refman/5.1/en/load-data.html)*).

This component executes the MySQL native command-line client (`bin/mysql` or `bin/mysql.exe`). The client must be installed on the same machine as the graph is running on.

**MySQLBulkWriter** is a bulk loader suitable for uploading many records to database. To insert several records, you can also use [DatabaseWriter](dboutputtable.md), which does not require `mysql` utility.

##### Path to Control Script

The name of a command file containing the `LOAD DATA INFILE` statement (See *[MySQL LOAD DATA](http://dev.mysql.com/doc/refman/5.1/en/load-data.html)*), including path.

- If it is not set, the command file is created in **CloverDX** temporary directory and it is deleted after the load finishes.
- If it is set, but the specified command file does not exist, a temporary command file is created with the specified name and path and it is not deleted after the load finishes.
- If it is set and the specified command file exists, this file is used instead of command file created by **CloverDX**.

##### Loader input file

The name of the input file to be loaded, including the path.

- If it is not set, a loader file is created in **CloverDX** or OS temporary directory (on Windows) or stdin is used instead of temporary file (on Unix). The file is deleted after the load finishes.
- If it is set, a specified file is created. It is not deleted after data is loaded and it is overwritten on each graph run.
- If the input port is not connected, this file must be specified, must exist and must contain data that should be loaded into the database. The file is not deleted nor overwritten.

##### Notes and limitations

###### Maps and lists

You should not write maps and lists.

###### MySQL 8.0.2 and newer

When using **MySQLBulkWriter** to write into MySQL 8.0.2 and newer, you must enable the [local_infile](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_local_infile) property. If disabled, **MySQLBulkWriter** fails with the following error:
Mysql utility has failed.
Also, the following error reported by the MySQL database appears in the job log:
The used command is not allowed with this MySQL version
#### Examples

##### Loading data to MySQL database

Load records (productID, amount) to table `products` of MySQL database `dbo` on `mysql.example.com` with username is `smithj` and password `smithy`.

###### Solution

Install the mysql utility.

Set up the following attributes of **MYSQLBulkWriter**.

| Attribute | Value |
| --- | --- |
| Path to mysql utility | C:/Program Files/MySQL/MySQL Server 5.6/bin/mysql.exe |
| Host | mysql.example.com |
| Database | dbo |
| Database table | products |
| User name | smithj |
| Password | smithy |

In case the server uses a non-standard port number, specify the **Port** parameter in the **Control script parameters** attribute.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.3.0 | **MySQLDataWriter** was renamed to **MySQLBulkWriter**. |

#### See also

| [DatabaseWriter](dboutputtable.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
