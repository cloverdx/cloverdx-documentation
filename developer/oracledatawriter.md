<!-- Development > Component reference > Writers > OracleBulkWriter -->

### OracleBulkWriter

![OracleDataWriter 64x64](../figures/OracleDataWriter-64x64.png)

| [Short description](oracledatawriter.md#short-description) |
| --- |
| [Ports](oracledatawriter.md#ports) |
| [Metadata](oracledatawriter.md#metadata) |
| [OracleBulkWriter attributes](oracledatawriter.md#oraclebulkwriter-attributes) |
| [Details](oracledatawriter.md#details) |
| [Example](oracledatawriter.md#example) |
| [Compatibility](oracledatawriter.md#compatibility) |
| [See also](oracledatawriter.md#see-also) |

#### Short description

**OracleBulkWriter** loads data into Oracle database.
> [!IMPORTANT]
> When to use OracleBulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](oracledatawriter.md#oracledatawriter-footnote1) | Records to be loaded into the database. | Any |
| Output | 0 | **⨯** | Rejected records | Input 0 |

| 1 |  If no file containing data for loading (**Loader input file**) is specified, input port must be connected. |
| --- | --- |

#### Metadata

**OracleBulkWriter** does not propagate metadata.

It has no metadata templates.

Both ports must have the same metadata.

Input metadata has to have the same names as database table names. Otherwise, **BD column names** has to be used.

#### OracleBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Path to sqlldr utility | yes | The name of sqlldr utility, including the path. |  |
| TNS name | yes | TNS name identifier. | E.g. db.example.com |
| User name | yes | Username to be used when connecting to the Oracle database. |  |
| Password | yes | Password to be used when connecting to the Oracle database. |  |
| Oracle table | yes | The name of the database table into which the records should be loaded. |  |
| Advanced |  |  |  |
| Control script |  | Control script for the sqlldr utility. For more information, see [Control script](oracledatawriter.md#control-script). |  |
| Append |  | Specifies what should be done with the database table. For more information, see [Append attribute](oracledatawriter.md#append-attribute). | append (default) \| insert \| replace \| truncate |
| Log file name |  | The name of the file where the process is logged. | ${PROJECT}/loaderinputfile.log |
| Bad file name |  | The name of the file where the records causing errors are written. | ${PROJECT}/loaderinputfile.bad |
| Discard file name |  | The name of the file where the records not meeting selection criteria are written. | ${PROJECT}/loaderinputfile.dis |
| DB column names |  | The names of all columns in the database table. | E.g. f1;f2;f3 |
| Loader input file |  | The name of an input file to be loaded, including the path. For more information, see [Loader input file](oracledatawriter.md#loader-input-file). |  |
| Max error count |  | The maximum number of allowed insert errors. When this number is exceeded, the graph fails. If no errors are to be allowed, the attribute should be set to 0. To allow all errors, set this attribute to a very high number. | 50 (default) \| 0-N |
| Max discard count |  | The number of records that can be discarded before the graph stops. If set to 1, even single discarded record stops the graph run. | all (default) \| 1-N |
| Ignore rows |  | The number of rows of the data file that should be skipped when loading data to a database. | 0 (default) \| 1-N |
| Commit interval |  | Conventional path loads only: **Commit interval** specifies the number of rows in the bind array. Direct path loads only: **Commit interval** identifies the number of rows that should be read from the data file before the data is saved. By default, all rows are read and data is all saved at once, at the end of the load. | 64 (default for conventional path) \| all (default for direct path) \| 1-N |
| Use file for exchange |  | On Unix, a pipe transfer is used, by default. If it is set to `true` and **Loader input file** is not set, temporary file is created and used as data source. On Windows, a temporary file is created and used as data source, by default. However, since some clients do not need a temporary data file to be created, this attribute can be set to `false` for such clients. | false (default on Unix) \| true (default on Windows) |
| Parameters |  | All parameters that can be used as parameters by the sqlldr utility. These values are contained in a sequence of pairs of the following form: `key=value`, or `key` only (if the `key` value is the boolean `true`) separated from each other by a semicolon, colon, or pipe. If the value of any parameter contains a semicolon, colon, or pipe as its part, such value must be double quoted. |  |
| Fail on warnings |  | By default, the component fails on errors. By switching the attribute to `true`, you can make the component fail on warnings. Background: when an underlying bulk-loader utility finishes with a warning, it is just logged to the console. This behavior is sometimes undesirable, as warnings from underlying bulk-loaders may seriously impact further processing. For example, 'Unable to extend table space' may result in not loading all data records to a database; hence not completing the expected task successfully. | false (default) \| true |

#### Details

**OracleBulkWriter** loads data into a database using Oracle database client. It can read data through the input port or from an input file. If the input port is not connected to any other component, data must be contained in an input file that should be specified in the component. If you connect some other component to the optional output port, rejected records are sent to it.

**OracleBulkWriter**'s functionality depends on the **sqlldr** utility. Oracle sqlldr database utility must be installed on the computer where **CloverDX** runs.

See details on sqlldr utility: [Loading data into an Oracle database with SQL*Loader](http://docs.oracle.com/cd/B28359_01/server.111/b28319/ldr_concepts.htm)
> [!NOTE]
> One of the common issues with the component functionality is the missing `tnsnames.ora` configuration. For more information about the proper configuration of the file, see [Configuring Tnsnames.ora](http://www.orafaq.com/wiki/Tnsnames.ora).

**OracleBulkWriter** is a bulk loader suitable for uploading many records to a database. To insert several records, you can also use [DatabaseWriter](dboutputtable.md), which does not require the `sqlldr` utility.

##### Control Script

Control script for the sqlldr utility.

- If specified, both the **Oracle table** and the **Append** attributes are ignored. Must be specified if input port is not connected. In such a case, **Loader input file** must also be defined.
- If **Control script** is not set, default control script is used.
Example 394. Example of a Control script

```sql
LOAD DATA
INFILE *
INTO TABLE test
append
(
    name TERMINATED BY ';',
    value TERMINATED BY '\n'
)
```

##### Append attribute

- **Append (default)**
  Specifies that data is simply appended to a table. Existing free space is not used.
- **Insert**
  Adds new rows to the table/view with the `INSERT` statement. The `INSERT` statement in Oracle is used to add rows to a table, the base table of a view, a partition of a partitioned table or a subpartition of a composite-partitioned table, or an object table or the base table of an object view.
  An `INSERT` statement with a `VALUES` clause adds to the table a single row containing the values specified in the `VALUES` clause.
  An `INSERT` statement with a subquery instead of a `VALUES` clause adds to the table all rows returned by the subquery. Oracle processes the subquery and inserts each returned row into the table. If the subquery selects no rows, Oracle inserts no rows into the table. The subquery can refer to any table, view, or snapshot, including the target table of the `INSERT` statement.
- **Update**
  Changes existing values in a table or in a view’s base table.
- **Truncate**
  Removes all rows from a table or cluster and resets the `STORAGE` parameters to the values when the table or cluster was created.

##### Loader input file

Name of input file to be loaded, including path.

- If it is not set, a loader file is created in **CloverDX** or OS temporary directory (on Windows) (unless **Use file for exchange** is set to `false`) or `named pipe` is used instead of temporary file (in Unix). The created file is deleted after the load finishes.
- If it is set, specified file is created. The created file is not deleted after data is loaded and it is overwritten on each graph run.
- If the input port is not connected, this file must be specified, must exist and must contain data that should be loaded into database. At the same time, **Control script** must be specified. The file is not deleted nor overwritten.

##### Notes and limitations

**OracleBulkWriter** does not support writing lists and maps.

#### Example

Load records (fields `username`, `surname`) into database table `users2`. The Oracle database is installed on `bd.example.com` and listens on `1521`. Database login `smithj` and password `MySecretPassword`.

##### Solution

Install `sqlldr` utility, if it is not installed.

Set up the following attributes of the component:

| Attribute | Value |
| --- | --- |
| Path to sqlldr utility | /app/product/12.1.0/client_1/bin/sqlldr |
| TNS name | db.example.com |
| User name | smithj |
| Password | MySecretPassword |
| Oracle table | users2 |

Metadata field names have to match database table field names.

Case 2: database table has columns `user` and `surn`.

Set up attribute **DB Column names** to `user;surn`.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.3.0 | **OracleDataWriter** was renamed to **OracleBulkWriter**. |

#### See also

| [DatabaseWriter](dboutputtable.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
