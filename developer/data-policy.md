<!-- Development > Component reference > Readers > Common properties of Readers > Data policy -->

#### Data policy

**Data policy** affects processing (parsing) of incorrect or incomplete records. This can be specified by the **Data policy** attribute. There are three options:

- **Strict**. This data policy is set by default. It means that data parsing stops if a record field with an incorrect value or format is read. Next processing is aborted.
- **Controlled**. This data policy means that every error is logged, but incorrect records are skipped and data parsing continues. Generally, incorrect records with error information are logged into `stdout`. Only [ParallelReader](parallelreader.md), [FlatFileReader](flatfilereader.md), [JSONReader](jsonreader.md) and [SpreadsheetDataReader](spreadsheetreader.md) enable to sent them out through the optional second port. See error metadata description for particular above mentioned readers.
- **Lenient**. This data policy means that incorrect records are only skipped and data parsing continues.

**Data policy** can be set in the following **Readers**:

| [ComplexDataReader](complexdatareader.md) |
| --- |
| [DBFDataReader](dbfdatareader.md) |
| [DatabaseReader](dbinputtable.md) |
| [FlatFileReader](flatfilereader.md) |
| [JSONReader](jsonreader.md) |
| [MultiLevelReader](multilevelreader.md) |
| [ParallelReader](parallelreader.md) |
| [XMLReader](xmlreader.md) |
| [XMLXPathReader](xmlxpathreader.md) |
