<!-- Development > Component reference > Deprecated > InfobrightBulkWriter -->

### InfobrightBulkWriter

Deprecated Component

![InfobrightDataWriter 64x64](../figures/InfobrightDataWriter-64x64.png)

| [Short Summary](infobrightdatawriter.md#short-summary) |
| --- |
| [Ports](infobrightdatawriter.md#ports) |
| [Metadata](infobrightdatawriter.md#metadata) |
| [InfobrightBulkWriter attributes](infobrightdatawriter.md#infobrightbulkwriter-attributes) |
| [Details](infobrightdatawriter.md#details) |
| [Best practices](infobrightdatawriter.md#best-practices) |
| [Compatibility](infobrightdatawriter.md#compatibility) |
| [See also](infobrightdatawriter.md#see-also) |

#### Short Summary

**InfobrightBulkWriter** loads data into an Infobright database.
> [!IMPORTANT]
> When to use InfobrightBulkWriter
> This component requires installation and configuration of a database native client. The client must be installed on the same machine as **CloverDX Server** (when working in a server project) or **CloverDX Designer** (when working in a local project). Due to this overhead, we recommend using this component only if you require significantly higher loading performance than with [DatabaseWriter](dboutputtable.md) which should be used in typical scenarios.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | Records to be loaded into the database | Any |
| Output | 0 | **⨯** | For records as they were loaded into the database | A corresponding part of metadata on Input 0[[1]](infobrightdatawriter.md#infobrightdatawriter-footnote1) |

| 1 |  Only mapped Clover field values can be sent out through the optional output port. A comma must be set as a delimiter for each field, `System.getProperty("line.separator")` ("\n" for Unix, "\r\n" for Windows) must be set as a record delimiter. Date fields must strictly have the `yyyy-MM-dd` format for dates and the `yyyy-MM-dd HH:mm:ss` format for dates with time. |
| --- | --- |

#### Metadata

**InfobrightBulkWriter** does not propagate metadata.

It has no metadata template.

#### InfobrightBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| DB connection | yes | The ID of the DB connection object to access the database. |  |
| Database table | yes | The name of the DB table where data will be loaded. |  |
| Charset |  | Charset used for encoding string values to VAR, VARCHAR column types.  The default encoding depends on DEFAULT_CHARSET_DECODER in defaultProperties. | UTF-8 \| other encoding |
| Data format |  | `bh_dataformat` supported by Infobright. Options are: `txt_variable` or `binary` (this option is faster, but works with IEE only). | Text (default) \| Binary |
| Advanced |  |  |  |
| Clover fields |  | A sequence of Clover fields separated by a semicolon. Only Clover fields listed in this attribute will be loaded into database columns. The position of both Clover field and database column will be the same. Their number should equal to the number of database columns. |  |
| Log file |  | A file for records loaded into database, including the path. If this attribute is specified, no data goes to the output port even if it is connected. |  |
| Append data to log file |  | By default, new records overwrite the older ones. If set to `true`, new records are appended to the older ones. | false (default) \| true |
| Execution timeout |  | Timeout for the load command (in seconds). Has effect only on the Windows platform. | 15 (default) \| 1-N |
| Check string’s and binary’s sizes |  | By default, sizes are not checked before data is passed to the database. If set to `true`, sizes are checked - should be set to `true` if debugging is supported. | false (default) \| true |
| Remote agent port |  | A port to be used when connecting to the server. | 5555 (default) \| otherportnumber |

#### Details

**InfobrightBulkWriter** loads data into an Infobright database. Only the root user can insert data into the database with this component. To run this component on Windows, `infobright_jni.dll` must be present in the Java library path.

If the hostname is `localhost` or `127.0.0.1`, the load will be done using a local pipe. Otherwise, it will use a remote pipe. The external IP address of the server is not recognized as a local server.

For loading to a remote server, you need to start the Infobright remote load agent on the server where Infobright is running. This should be done by executing the command `java -jar infobright-core-3.0-remote.jar [-p PortNumber] [-l all | debug | error | info]`. The output can be redirected to a log file. By default, the server is listening at port 5555. The `infobright-core-3.0-remote.jar` is distributed with **CloverDX**.

By default, `root` is only allowed to connect from `localhost`. You need to add an additional user `root@%` to connect from other hosts. It is recommended to create a different user (not `root`) for loading data. The user requires the `FILE` privilege in order to be able to load data or use the connector:

```sql
grant FILE on *.* to 'user'@'%';
```

##### Notes and limitations

Writing maps and lists is not supported as database has no lists and maps.

#### Best practices

We recommend users to explicitly specify **Charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.3.0 | **InfobrightDataWriter** was renamed to **InfobrightBulkWriter**. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
