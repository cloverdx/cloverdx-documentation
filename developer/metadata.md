<!-- Development > Job elements > Metadata -->

## 25. Metadata

Metadata is data describing the data structure.

Each edge of a graph carries some data. This data must be described using metadata. Metadata describes both the record as a whole and all its fields.

Records can be of different types, each field can have different data type. See [Records and fields](metadata-records-and-fields.md).

- [Date and time format](metadata-records-and-fields.md#date-and-time-format)
- [Numeric format](metadata-records-and-fields.md#numeric-format)
- [Locale](metadata-records-and-fields.md#locale)
- [Time zone](metadata-records-and-fields.md#timezone)
- [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

The metadata can be either internal, or external (shared). metadata can also be created dynamically from an SQL query or read from remote sources. See [Metadata types](metadata-types.md).

- [Internal metadata](metadata-types.md#internal-metadata)
- [External (shared) metadata](metadata-types.md#external-shared-metadata)
- [SQL Query metadata](metadata-types.md#sql-query-metadata)
- [Reading metadata from special sources](metadata-types.md#reading-metadata-from-special-sources)

For details on metadata propagation, see [Auto-propagated metadata](auto-detected-metadata.md).

Metadata can be created from:

- **Flat file**: See [Extracting metadata from a flat file](creating-metadata.md#extracting-metadata-from-a-flat-file).
- **XLS(X) file**: See [Extracting metadata from an XLS(X) File](creating-metadata.md#extracting-metadata-from-an-xlsx-file).
- **DBase file**: See [Extracting metadata from a DBase File](creating-metadata.md#extracting-metadata-from-a-dbase-file).
- **Database**: See [Extracting metadata from a Database](creating-metadata.md#extracting-metadata-from-a-database).
- **SQL query**: See [SQL Query metadata](creating-metadata.md#sql-query-metadata).
- **By user**: See [User defined metadata](creating-metadata.md#user-defined-metadata).
- **Cobol Copybook**
- **Merging existing metadata**: See [Merging existing metadata](metadata-merge.md).

**Metadata Editor** is described in [Metadata Editor](metadata-editor.md).

For detailed information about changing or defining delimiters in `delimited` or `mixed` record types, see [Changing and defining delimiters](changing-and-defining-delimiters.md).

Metadata can serve as a source for creating a database table. See [Create database table from metadata](metadata-merge.md#creating-database-table-from-metadata-and-database-connection).
