<!-- Development > Component reference > Writers -->

## 37. Writers

| [Common properties of Writers](common-of-writers.md) |
| --- |
> [!TIP]
> If you’re interested in learning more about this subject, we offer the [Advanced Tips for Using Writer Components course](https://academy.cloverdx.com/courses/advanced-tips-for-using-writer-components) in our CloverDX Academy.

**Writers** can write data to local and remote output files, send it through the connected optional output port, write it to a dictionary, send using JMS connection, insert into database table, send by email, insert into LDAP database or write only for debugging purposes.

### Writers Overview

We can distinguish **Writers** according to their output data format.

#### Writing to File

- Flat files:
  - [FlatFileWriter](flatfilewriter.md) ([UniversalDataWriter](datawriter.md)) writes data to flat files (character-delimited or fixed length).
- Other files:
  - [CloverDataWriter](cloverwriter.md) writes data to files in a **CloverDX** binary format.
  - [StructuredDataWriter](structurewriter.md) writes data to files with a user-defined structure.
  - [TableauWriter](tableauwriter.md) writes data to Tableau files.
  - [XMLWriter](extxmlwriter.md) creates XML files from input data records.
  - [DBFDataWriter](dbfdatawriter.md) writes data to dbase file(s).
  - [HadoopWriter](hadoopwriter.md) writes data into Hadoop sequence file(s).
  - [ParquetWriter](parquetwriter.md) writes data into Apache Parquet files.
  - [EDIFACTWriter](edifactwriter.md) writes data into EDIFACT files.
  - [X12Writer](x12writer.md) writes data into X12 files.

#### Writing to Database

- Database Writers:
  - [DatabaseWriter](dboutputtable.md) loads data into database using JDBC driver.
  - [QuickBaseRecordWriter](quickbaserecordwriter.md) writes data into the a QuickBase online database.
  - [QuickBaseImportCSV](quickbaseimportcsv.md) writes data into a QuickBase online database.
  - [MongoDBWriter](mongodbwriter.md) writes data into a MongoDB NoSQL database.
  - [SalesforceWriter](salesforcewriter.md) writes data into the Salesforce cloud platform.
  - [SalesforceEinsteinWriter](salesforcewavewriter.md) writes data into the Salesforce Einstein (formerly called Salesforce Wave) cloud platform.
- High-Speed Database Specific Writers (Bulk Loaders):
  - [DB2BulkWriter](db2datawriter.md) loads data into a DB2 database using DB2 client.
  - [InformixBulkWriter](informixdatawriter.md) loads data into an Informix database using the Informix client.
  - [MSSQLBulkWriter](mssqldatawriter.md) loads data into an MSSQL database using the MSSQL client.
  - [MySQLBulkWriter](mysqldatawriter.md) loads data into an MYSQL database using the MYSQL client.
  - [OracleBulkWriter](oracledatawriter.md) loads data into an Oracle database using the Oracle client.
  - [PostgreSQLBulkWriter](postgresqldatawriter.md) loads data into a PostgreSQL database using the PostgreSQL client.
  - [SalesforceBulkWriter](salesforcebulkwriter.md) writes data into the Salesforce cloud platform.
  - [SnowflakeBulkWriter](snowflakebulkwriter.md) loads data into Snowflake data warehouse using a Snowflake JDBC connection.

#### Data Set Writers

- [ReferenceDataSetWriter](referencedatasetwriter.md) writes data to reference data set in the Data Manager.
- [TransactionalDataSetWriter](datasetwriter.md) writes data to transactional data set in the Data Manager.
- [TransactionalDataSetCommit](datasetcommit.md) commits approved records in transactional data set in the Data Manager.

#### Other Writers

- Emails:
  - [EmailSender](emailsender.md) converts data records into emails.
- JMS messages:
  - [JMSWriter](jmswriter.md) converts data records into JMS messages.
- Directory structure:
  - [LDAPWriter](ldapwriter.md) converts data records into a directory structure.
- Kafka events:
  - [KafkaWriter](kafkawriter.md) writes events (messages) to a Kafka cluster.
- One component discards data:
  - [Trash](trash.md) discards data or writes data to a debug file.

### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
