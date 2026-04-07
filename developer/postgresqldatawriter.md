<!-- Development > Component reference > Writers > PostgreSQLBulkWriter -->

### PostgreSQLBulkWriter

![PostgreSQLDataWriter 64x64](../figures/PostgreSQLDataWriter-64x64.png)

| [Short description](postgresqldatawriter.md#short-description) |
| --- |
| [Ports](postgresqldatawriter.md#ports) |
| [Metadata](postgresqldatawriter.md#metadata) |
| [PostgreSQLBulkWriter attributes](postgresqldatawriter.md#postgresqlbulkwriter-attributes) |
| [Details](postgresqldatawriter.md#details) |
| [Examples](postgresqldatawriter.md#examples) |
| [Notes and limitations](postgresqldatawriter.md#notes-and-limitations) |
| [Compatibility](postgresqldatawriter.md#compatibility) |
| [See also](postgresqldatawriter.md#see-also) |

#### Short description

**PostgreSQLBulkWriter** loads data into PostgreSQL database.
> [!IMPORTANT]
> When to use PostgreSQLBulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 0-1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](postgresqldatawriter.md#postgresqldatawriter-footnote1) | Records to be loaded into the database | Any |

| 1 | If no file containing data for loading (**Loader input file**) is specified, the input port must be connected. |
| --- | --- |

#### Metadata

**PostgreSQLBulkWriter** does not propagate metadata.

**PostgreSQLBulkWriter** has no metadata templates.

#### PostgreSQLBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Path to psql utility | yes | The name of the psql utility, including the path. Must be installed and configured on the same machine where **CloverDX** runs. Psql command line tool must be available. |  |
| Host |  | Host where database server is located. | localhost (default) \| other host |
| Database | yes | The name of the database into which the records should be loaded. |  |
| Database table | yes | Name of the database table into which the records should be loaded. |  |
| User name |  | PostgreSQL username to be used when connecting to the server.  If empty, the username of current user is used. |  |
| Advanced |  |  |  |
| Fail on error |  | By default, a graph fails upon each error. If you want to have the standard behavior of PostgreSQL database, you need to switch this attribute to `false`. If set to `false`, a graph will run successfully even with some errors as it happens with PostgreSQL database. | true (default) \| false |
| Path to control script |  | The name of a command file containing the `\copy` statement, including path. For more information, see [Path to Control script](postgresqldatawriter.md#path-to-control-script). |  |
| Column delimiter |  | Delimiter used for each column in data. Field values must not include this delimiter as their part. | tabulator character (default in text mode) \| comma (default in CSV mode) |
| Loader input file |  | The name of the input file to be loaded, including the path. For more information, see [Loader input file](postgresqldatawriter.md#loader-input-file) |  |
| Parameters |  | All parameters that can be used as parameters by the psql utility or the `\copy` statement. These values are contained in a sequence of pairs of the following form: `key=value`, or `key` only (if the `key` value is the boolean `true`) separated from each other by a semicolon, colon, or pipe. If the value of any parameter contains a semicolon, colon, or pipe as its part, such value must be double quoted. |  |

#### Details

**PostgreSQLBulkWriter** loads data into database using PostgreSQL database client.

**PostgreSQLBulkWriter** can read data through the input port or from an input file. If the input port is not connected to any other component, data must be contained in an input file that should be specified in the component.
> [!IMPORTANT]
> PostgreSQL client utility (`psql`) must be installed and configured on the same machine where **CloverDX** runs.

**PostgreSQLBulkWriter** is a bulk loader suitable for uploading many records to database. To insert several records, you can also use [DatabaseWriter](dboutputtable.md), which does not require `psql` utility.

##### Path to Control Script

The name of the command file containing the `\copy` statement, including the path.

- If it is not set, a command file is created in **CloverDX** temporary directory and it is deleted after the load finishes.
- If it is set, but the specified command file does not exist, a temporary file is created with the specified name and path and it is not deleted after the load finishes.
- If it is set and the specified command file exists, this file is used instead of the file created by **CloverDX**. The file is not deleted after the load finishes.

##### Loader Input File

Name of input file to be loaded, including path.

- If the input port is connected and this file is not set, no temporary file is created. Data is read from the edge and loaded into the database directly.
- If it is set, a specified file is created. It is not deleted after data is loaded and it is overwritten on each graph run.
- If the input port is not connected, this file must exist and must contain data that should be loaded into the database. It is not deleted nor overwritten on another graph run.
> [!IMPORTANT]
> Utility psql.exe gets stuck due to asking for password interactively. To avoid the problem, the file `.pgpass` needs to be set up correctly.
>
> On Windows you need to create the file `%APPDATA%\postgresql\pgpass.conf`.
>
> On Unix/Linux you need to create the file `~/.pgpass`. The file has to have permissions `0600`.
>
> The file content is in the following format:
>
> `hostname:port:database:username:password`
>
> for example:
>
> `postgresql.example.com:5432:mydatabase:user1:Pns2kj@Dat`
>
> For more details, see *[corresponding PostgreSQL documentation](http://www.postgresql.org/docs/9.4/static/libpq-pgpass.html)*.

#### Examples

##### Loading data to PostgreSQL database

Load records (productID, amount) to table `products` of PostgreSQL database `postgres` on `postgresql.example.com` with username `smithj`.

###### Solution

Install the 'psql' utility.

Set up the following attributes of **PostgreSQLBulkWriter**.

| Attribute | Value |
| --- | --- |
| Path to psql utility | C:/Program Files/PostgreSQL/9.5/bin/psql.exe |
| Host | postgresql.example.com |
| Database | postgres |
| Database table | products |
| User Name | smithj |

In case the server uses a non-standard port number, specify the **Port** parameter in the **Parameters** attribute.

##### Notes and limitations

You should not write lists and maps.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.3.0 | **PostgreSQLDataWriter** was renamed to **PostgreSQLBulkWriter**. |

#### See also

| [DatabaseWriter](dboutputtable.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
