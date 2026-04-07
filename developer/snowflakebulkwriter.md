<!-- Development > Component reference > Writers > SnowflakeBulkWriter -->

### SnowflakeBulkWriter

![SnowflakeBulkWriter 64x64](../figures/SnowflakeBulkWriter-64x64.png)

| [Short description](snowflakebulkwriter.md#short-description) |
| --- |
| [Ports](snowflakebulkwriter.md#ports) |
| [Metadata](snowflakebulkwriter.md#metadata) |
| [SnowflakeBulkWriter attributes](snowflakebulkwriter.md#snowflakebulkwriter-attributes) |
| [Details](snowflakebulkwriter.md#details) |
| [See also](snowflakebulkwriter.md#see-also) |
> [!NOTE]
> Snowflake has announced plans to [discontinue password-based sign-ons by November 2025](https://docs.snowflake.com/en/user-guide/security-mfa-rollout). If you are currently using password authentication in your Snowflake connections, we recommend migrating to key-pair authentication to ensure uninterrupted access. See [Key-pair authentication](database-connections.md#key-pair-authentication) for more information.

#### Short description

**SnowflakeBulkWriter** loads large volumes of data into Snowflake database. It is faster than [DatabaseWriter](dboutputtable.md), but the target table must have the same structure as the input metadata. If the target table does not exist, the component can create it based on input metadata.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 1 | 1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For data records to be inserted | Any |
| Output | 0 | **⨯** | Load statistics | See below |

#### Metadata

**SnowflakeBulkWriter** does not propagate metadata.

**SnowflakeBulkWriter** has a [metadata template](components.md#metadata-templates) on the output port.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 0 | file | string | Name and relative path of the staged chunk file. See [Chunk files](snowflakebulkwriter.md#chunk-files) for more details. |
| 1 | status | string | Status: LOADED, LOAD_FAILED or PARTIALLY_LOADED. |
| 2 | parsedRows | long | Number of rows in the CSV file. |
| 3 | loadedRows | long | Number of rows that were successfully loaded. |
| 4 | errorLimit | long | If the number of errors reaches this limit, then abort. Either 1 or the same as `parsedRows`, if [Continue on error](snowflakebulkwriter.md#snowflakebulkwriter-continue-on-error). |
| 5 | errorCount | long | Number of rejected rows. Each of these rows could include multiple errors. |
| 6 | firstError | string | First error message in the file. |
| 7 | firstErrorLine | long | Line number of the first error in the file. |
| 8 | firstErrorCharacter | long | Position of the first error character. |
| 9 | firstErrorColumnName | string | Column name and index of the first error, e.g. "TABLE_NAME"["COLUMN_NAME":1] |

#### SnowflakeBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| DB connection | **✓** | A Snowflake connection. | e.g. ${CONN_DIR}/snowflake.cfg (id:JDBC0) |
| DB table | **✓** | Name of the target table. | e.g. Account |
| Create table if not exists |  | Creates the target table if it does not exist. Generates DDL from input port metadata. **CloverDX** must have [CREATE TABLE privilege](https://docs.snowflake.com/en/user-guide/security-access-control-privileges.html#all-privileges-alphabetical) for the target schema. | true (default) \| false |
| Continue on error |  | Prevents the component from failing if an error occurs. | false (default) \| true |
| Advanced |  |  |  |
| Upload threads |  | Max number of concurrent uploads, 5 by default. | e.g. 5 |
| Remove files after import |  | Set to `false` to prevent staged files from being deleted from Snowflake after the import. | true (default) \| false |

#### Details

SnowflakeBulkWriter is a fast writer that can insert records into a Snowflake table at the speed of 25 MB/s or more (about 100 GB per hour). You can expect about 8 times speedup when compared with [DatabaseWriter](dboutputtable.md), depending on settings.

Input fields are mapped to the target columns by position, so the number of input fields and their types must match the target table columns.

The component has full Unicode support. It also allows writing byte fields into BINARY columns and JSON string data into VARIANT columns.

For information about writing **date/time data types** and handling time zones, see [Date/Time data types in Snowflake](database-connections.md#datetime-data-types-in-snowflake).

If the target table does not exist, it is created based on the input metadata by default. See [Create table if not exists](snowflakebulkwriter.md#snowflakebulkwriter-create-if-not-exists) attribute.

**Loading process:**

1. Split the data into chunks.
2. Upload the chunks into Snowflake table stage in parallel.
3. Load data from the stage to the table using the
   [COPY INTO](https://docs.snowflake.com/en/sql-reference/sql/copy-into-table.html) statement.

If the output port is connected, the component produces one output record for every chunk. The output records contain load statistics (e. g. the number of loaded rows, error count and more). If [Continue on error](snowflakebulkwriter.md#snowflakebulkwriter-continue-on-error) is enabled, there may also be error messages.

Staged chunks are deleted when the process finishes, see [Remove files after import](snowflakebulkwriter.md#snowflakebulkwriter-remove-files-after-import).

##### Chunk Files

Incoming data is internally split into gzipped CSV files. These chunks are uploaded and inserted into Snowflake in parallel to improve performance. But due to the parallel loading, there is no guarantee input records will be written in the order they were received by the component.

The staged files are named according to the following pattern:

`CloverDX_[RUN_ID][COMPONENT_ID][RANDOM_NUMBER]/chunk_[CHUNK NUMBER].csv.gz`

When a chunk is successfully loaded, it is deleted automatically.

##### Error Handling

By default, any error causes the component to fail and the transaction is rolled back.

If [Continue on error](snowflakebulkwriter.md#snowflakebulkwriter-continue-on-error) is enabled, the component continues loading data even if an error occurs. The data is internally split into chunks and the component produces one output record for every chunk, regardless of errors. If a chunk contains an error, Snowflake continues loading the file and rejects only the invalid rows. The output record contains the number of errors in the chunk and the first error message and its details. At most one error is reported for each chunk.

The total number of errors is logged to the execution log as a warning.

##### Resource Utilization

The component chunks incoming data into gzipped CSVs and uploads them in parallel to increase throughput. The maximum number of concurrent uploads can be set using the [Upload threads](snowflakebulkwriter.md#snowflakebulkwriter-upload-threads) attribute.

Data is buffered in memory before being uploaded to Snowflake. Memory consumption of the component is approximately 15 MB x [[Upload threads](snowflakebulkwriter.md#snowflakebulkwriter-upload-threads)].

##### Using SnowflakeBulkWriter in Server Core

If you want to use SnowflakeBulkWriter in a graph that runs in Server Core, the server needs to be configured to allow reflective access. See [reflective access](../admin/postinstallation-configuration.md#reflective-access).

##### Notes and limitations

SnowflakeBulkWriter cannot write maps and lists. If you need to write the content of the map or list field, convert the field into string using [Map](reformat.md) first.

The component does not preserve the order of incoming records. The COPY INTO statement loads data in parallel, so the records may appear out of order in Snowflake.

#### See also

| [Snowflake connection](database-connections.md#snowflake-connection) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
