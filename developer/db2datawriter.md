<!-- Development > Component reference > Writers > DB2BulkWriter -->

### DB2BulkWriter

![DB2DataWriter 64x64](../figures/DB2DataWriter-64x64.png)

| [Short description](db2datawriter.md#short-description) |
| --- |
| [Ports](db2datawriter.md#ports) |
| [Metadata](db2datawriter.md#metadata) |
| [DB2BulkWriter attributes](db2datawriter.md#db2bulkwriter-attributes) |
| [Details](db2datawriter.md#details) |
| [Notes and limitations](db2datawriter.md#notes-and-limitations) |
| [Compatibility](db2datawriter.md#compatibility) |
| [See also](db2datawriter.md#see-also) |

#### Short description

**DB2BulkWriter** loads data into DB2 database.
> [!IMPORTANT]
> When to use DB2BulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](db2datawriter.md#db2datawriter-footnote1) | Records to be loaded into the database. | Any |
| Output | 0 | **⨯** | For information about incorrect records | [Error metadata for DB2BulkWriter](db2datawriter.md#db2datawriter-error-metadata) |

| 1 |  If no file containing data for loading (**Loader input file**) is specified, the input port must be connected. |
| --- | --- |

#### Metadata

**DB2BulkWriter** does not propagate metadata.

**Error Metadata** cannot use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 0 | <any_name1> | integer | The incorrect record’s number (records are numbered starting from 1). |
| 1 | <any_name2> | integer | The incorrect field’s number (for delimited records), fields are numbered starting from 1 \| offset of an incorrect field (for fixed-length records). |
| 2 | <any_name3> | string | Error message |

#### DB2BulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File metadata |  | Metadata of an external file.  The metadata must be delimited. Each column, except the last one, is followed by an identical, one char delimiter. The last delimiter following the last column is `\n`. Delimiter must not be a part of any field value. |  |
| Database | yes | The name of the database into which records should be loaded. |  |
| Database table | yes | The name of the database table into which records should be loaded. |  |
| User name | yes | Database user. |  |
| Password | yes | Password for database user. |  |
| Load mode |  | Mode of the action performed when loading data.  For more information, see [Load mode](db2datawriter.md#load-mode). | insert (default) \| replace \| restart \| terminate |
| Field mapping | [[1]](db2datawriter.md#db2datawriter-attributes-fn01) | Sequence of individual mappings (`$CloverField:=DBField`) separated by a semicolon, colon, or pipe. For more information, see [Mapping of Clover fields to DB fields](db2datawriter.md#mapping-of-clover-fields-to-db-fields). |  |
| Clover fields | [[1]](db2datawriter.md#db2datawriter-attributes-fn01) | The sequence of Clover fields separated by a semicolon, colon, or pipe. For more information, see [Mapping of Clover fields to DB fields](db2datawriter.md#mapping-of-clover-fields-to-db-fields). |  |
| DB fields | [[1]](db2datawriter.md#db2datawriter-attributes-fn01) | The sequence of DB fields separated by a semicolon, colon, or pipe. For more information, see [Mapping of Clover fields to DB fields](db2datawriter.md#mapping-of-clover-fields-to-db-fields). |  |
| Advanced |  |  |  |
| Loader input file | [[2]](db2datawriter.md#db2datawriter-footnote3) | Name of input file to be loaded, including path. For more information, see [Loader input file](db2datawriter.md#loader-input-file). |  |
| Parameters |  | All parameters that can be used as parameters by the `load` method. These values are contained in a sequence of pairs of the following form: `key=value`, or `key` only, (if the `key` value is the boolean `true`) separated from each other by a semicolon, colon, or pipe. If the value of any parameter contains the delimiter as its part, such value must be double quoted. |  |
| Rejected records URL (on server) |  | The name of the file, including the path, on a DB2 server where rejected records will be saved. Must be located in the directory owned by the database user. |  |
| Batch file URL |  | The URL of the file where the `connect`, `load` and `disconnect` commands for db2 load utility are stored. Normally, the batch file is automatically generated, stored in the current directory and deleted after the load finishes. If the **Batch file URL** is specified, the component tries to use it as is (generates it only if it does not exist or if its length is 0) and does not delete it after the load finishes.  It is reasonable to use this attribute in connection with the **Loader input file** attribute, because the batch file contains the name of temporary data file which is generated at random, if not provided explicitly.  The path must not contain white spaces. |  |
| DB2 command interpreter |  | Interpreter that should execute script with DB2 commands (`connect`, `load`, `disconnect`). Its form must be the following: `interpreterName [parameters] ${} [parameters]`. This `${}` expression must be replaced with the name of this script file. |  |
| Use pipe transfer |  | By default, data from an input port is written to a temporary file and then it is read by the component. If set to `true` on Unix, data records received through the input port are sent to a pipe instead of a temporary file. | false (default) \| true |
| Column delimiter |  | The first one char field delimiter from **File metadata** or the metadata on the input edge (if **File metadata** is not specified). A character used as a delimiter for each column in data file. The delimiter must not be contained as a part of a field value. The same delimiter can be set by specifying the value of the `coldel` parameter in the **Parameters** attribute. If **Column delimiter** is set, `coldel` in **Parameters** is ignored. |  |
| Number of skipped records |  | The number of records to be skipped. By default, no records are skipped. This attribute is applied only if data is received through the input port; otherwise, it is ignored. | 0 (default) \| 1-N |
| Max number of records |  | The maximum number of records to be loaded into database. The same can be set by specifying the value of the `rowcount` parameter in the **Parameters** attribute.  If `rowcount` is set in **Parameters**, the **Max number of records** attribute is ignored. | all (default) \| 0-N |
| Max error count |  | The Maximum number of records after which the load stops. If the number is set explicitly and when it is reached, the process can continue in RESTART mode. In REPLACE mode, the process continues from the beginning. The same number can be specified with the help of `warningcount` in the **Parameters** attribute. If `warningcount` is specified, **Max error count** is ignored. | all (default) \| 0-N |
| Max warning count |  | The maximum number of printed error messages and/or warnings. | 999 (default) \| 0-N |
| Fail on warnings |  | By default, the component fails on errors. By switching the attribute to `true`, you can make the component fail on warnings. Background: when an underlying bulk-loader utility finishes with a warning, it is just logged to the console. This behavior is sometimes undesirable as warnings from underlying bulk-loaders may seriously impact further processing. For example, `Unable to extend table space` may result in not loading all data records to a database; hence not completing the expected task successfully. | false (default) \| true |

| 1 |  For more information about their relation, see [Mapping of Clover fields to DB fields](db2datawriter.md#mapping-of-clover-fields-to-db-fields). |
| --- | --- |

| 2 |  If the input port is not connected, **Loader input file** must be specified and contain data. For more information, see [Loader input file](db2datawriter.md#loader-input-file). |
| --- | --- |

#### Details

**DB2BulkWriter** loads data into a database using a DB2 database client. It can read data through the input port or from an input file. If the input port is not connected to any other component, data must be contained in an input file that should be specified in the component. If you connect some other component to the optional output port, it can serve to log the information about errors. The DB2 database client must be installed and configured on localhost. The server and database must be cataloged as well.

##### Mapping of Clover fields to DB fields

- **Field mapping is defined**
  If a **Field mapping** is defined, the value of each Clover field specified in this attribute is inserted to such DB field to whose name this Clover field is assigned in the **Field mapping** attribute.
- **Both Clover fields and DB fields are defined**
  If both **Clover fields** and **DB fields** are defined (but **Field mapping** is not), the value of each Clover field specified in the **Clover fields** attribute is inserted to such DB field which lies on the same position in the **DB fields** attribute.
  The number of Clover fields and DB fields in both of these attributes must equal to each other. The number of either part must equal to the number of DB fields that are not defined in any other way (by specifying Clover fields prefixed by dollar sign, db functions or constants in the query).
  Pattern of **Clover fields**:
  `CloverFieldA;…;CloverFieldM`
  Pattern of **DB fields**:
  `DBFieldA;…;DBFieldM`
- **Only Clover fields are defined**
  If only the **Clover fields** attribute is defined (but **Field mapping** and/or **DB fields** are not), the value of each Clover field specified in the **Clover fields** attribute is inserted to such DB field whose position in DB table is equal.
  Number of Clover fields specified in the **Clover fields** attribute must equal to the number of DB fields in DB table that are not defined in any other way (by specifying Clover fields prefixed by a dollar sign, db functions, or constants in the query).
  Pattern of **Clover fields**:
  `CloverFieldA;…;CloverFieldM`
- **Mapping is performed automatically**
  If neither **Field mapping**, **Clover fields**, nor **DB fields** are defined, the whole mapping is performed automatically. The value of each Clover field of Metadata is inserted into the same position in the DB table.
  The number of all Clover fields must equal to the number of DB fields in the DB table that are not defined in any other way (by specifying Clover fields prefixed by a dollar sign, db functions, or constants in the query).

##### Load mode

- `insert`
  Loaded data is added to the database table without deleting or changing existing table content.
- `replace`
  All data existing in the database table is deleted and new loaded data is inserted to the table. Neither the table definition nor the index definition are changed.
- `restart`
  Previously interrupted load operation is restarted. The load operation automatically continues from the last consistency point in the load, build, or delete phase.
- `terminate`
  Previously interrupted load operation is terminated and rolled back to the moment when it started even if consistency points had been passed.

##### Loader input file

**Loader input file** is the name of the input file with data to be loaded, including its path. Normally, this file is a temporary storage for data to be passed to dbload utility unless `named pipe` is used instead.

Remember that a DB2 client must be installed and configured on localhost (see [IBM data server clients and drivers overview](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.swg.im.dbclient.install.doc/doc/c0023452.html?lang=en) and [Installing IBM data server clients (Linux and UNIX)](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.swg.im.dbclient.install.doc/doc/t0007317.html?lang=en)). The server and database must be cataloged as well.

- If it is not set, a loader file is created in **CloverDX** or OS temporary directory (on Windows) or `named pipe` is used instead of a temporary file (on Unix). The file is deleted after the load finishes.
- If it is set, a specified file is created. It is not deleted after data is loaded and it is overwritten on each graph run.
- If the input port is not connected, the file must exist, must be specified and must contain data that should be loaded into the database. It is not deleted nor overwritten.

##### Notes and limitations

**DB2BulkWriter** cannot write maps and fields.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.3.0 | **DB2DataWriter** was renamed to **DB2BulkWriter**. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
