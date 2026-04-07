<!-- Development > Component reference > Readers > Common properties of Readers > Incremental reading -->

#### Incremental reading

**Incremental reading** is a way to read only the new records since the last graph run. This way, you can avoid reading already processed records. Incremental reading allows you to read new records from a single file as well as new records from multiple files. If a file URL possibly matches new files, it can read records from new files.

Incremental reading can be set with the **Incremental file** and **Incremental key** attributes. The **Incremental key** is a string that holds the information about read records/files. This key is stored in the **Incremental file** attribute. This way, the component reads only the records or files that have not been marked in **Incremental file**.

**Readers** with incremental reading are:

| [DBFDataReader](dbfdatareader.md) |
| --- |
| [FlatFileReader](flatfilereader.md) |
| [SpreadsheetDataReader](spreadsheetreader.md) |

The component [DatabaseReader](dbinputtable.md) which reads data from databases performs this incremental reading in a different way.

##### Incremental reading in database components

Unlike other incremental readers, in a database component, more database columns can be evaluated and used as key fields. **Incremental key** is a sequence of the following individual expression separated by a semicolon: `keyname=FUNCTIONNAME(db_field)[!InitialValue]` (e.g. `key01=MAX(EmployeeID);key02=FIRST(CustomerID)!20`). The functions that can be selected are: `FIRST`, `LAST`, `MIN`, `MAX`.

At the same time, when you define an **Incremental key**, you also need to add these key parts to the **Query**. In the query, a part of the `where` sentence will appear; e.g. `where db_field1 > #key01 and db_field2 < #key02`. This way, you can limit which records will be read next time. It depends on the values of `db_field1` and `db_field2`.

Only the records that satisfy the condition specified by the query will be read. These key fields values are stored in the **Incremental file**. To define **Incremental key**, click this attribute row and, by clicking the **Plus** or **Minus** buttons in the **Define incremental key** dialog, add or remove key names and select db field names and function names. Each one of the last two is to be selected from a combo list of possible values.
> [!NOTE]
> Since **CloverETL Designer 2.8.1**, you can also define `Initial value` for each key. This way, non existing **Incremental file** can be created with the specified values.
