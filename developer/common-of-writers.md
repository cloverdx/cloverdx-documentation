<!-- Development > Component reference > Writers > Common properties of Writers -->

### Common properties of Writers

**Writers** are the final components of a transformation graph. They serve to write data to files located on disk or to send data using some FTP, LDAP or JMS connection, or insert data into database tables. **Trash** component, which discards all records it receives, is categorized as Writer as it can be set to store records in a debug file.

Each Writer must have at least one input port through which the data flows to this graph component from some of the others.

Writers can either append data to an existing file, sheet or database table, or replace the existing content by new one. For this purpose, Writers writing to files have the **Append** attribute. This attribute is set to false, by default. That means "do not append data, replace it". Replacing database table is available in some bulkloaders, e.g. in [DB2BulkWriter](db2datawriter.md).

You can also write data to one file or one database table by more Writers of the same graph; in such a case you should write data by different Writers in different phases.

Most Writers let you see some part of resulting data. Right-click the Writer and select the **View data** option. You will be prompted with the same View data dialog as when debugging the edges. For more details, see [Viewing debug data](edge.md#viewing-debug-data). This dialog allows you to view the written data. It can only be used after graph has already been run.

Below is a brief overview of links to these options:

- Below are examples of the **File URL** attribute for writing to local and remote files, through proxy, output port and dictionary:
  [Supported file URL formats for Writers](examples-of-file-url-in-writers.md)
- [Viewing data on Writers](viewing-data-on-writers.md)
- [Output port writing](output-port-writing.md)
- [Appending or overwriting](writers-appending-or-overwriting.md)
- [Creating directories](writers-creating-directories.md)
- [Excluding fields](writers-excluding-fields.md)
- [Selecting output records](selecting-output-records.md)
- [Partitioning output into different output files](partitioning-output-into-different-output-files.md)
- As it has been shown in [Defining transformations](transformations.md#defining-transformations), some **Writers** allow you to define a transformation. For information about transformation interfaces that must be implemented in transformations written in Java, see:
  [Java interfaces for Writers](java-interfaces-for-writers.md)

| Component | Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [CloverDataWriter](cloverwriter.md) | CloverDX binary file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [CustomJavaWriter](genericwriter.md) | - | n | n | **✓** | **⨯** | **✓** | **⨯** | **⨯** |
| [DatabaseWriter](dboutputtable.md) | database | 1 | 0-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [DB2BulkWriter](db2datawriter.md) | database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [DBFDataWriter](dbfdatawriter.md) | .dbf file | 1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [EDIFACTWriter](edifactwriter.md) | EDIFACT file | 1-n | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [EmailSender](emailsender.md) | emails | 0-1 | 0-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [FlatFileWriter](flatfilewriter.md) | flat file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [HadoopWriter](hadoopwriter.md) | Hadoop sequence file | 1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [InformixBulkWriter](informixdatawriter.md) | database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [JavaBeanWriter](beanwriter.md) | dictionary | 1-n | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [JavaMapWriter](mapwriter.md) | dictionary | 1-n | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [JMSWriter](jmswriter.md) | jms messages | 1 | 0 | **✓** | **⨯** | **✓** | **⨯** | **⨯** |
| [JSONWriter](jsonwriter.md) | JSON file | 1-n | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [KafkaWriter](kafkawriter.md) | Kafka cluster | 1 | 0-2 | **✓** | **⨯** | **⨯** | **✓** | **✓** |
| [LDAPWriter](ldapwriter.md) | LDAP directory tree | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [MongoDBWriter](mongodbwriter.md) | database | 1 | 0-2 | **✓** | **✓** | **⨯** | **✓** | **✓** |
| [MSSQLBulkWriter](mssqldatawriter.md) | database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [MySQLBulkWriter](mysqldatawriter.md) | database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [OracleBulkWriter](oracledatawriter.md) | database | 0-1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [ParquetWriter](parquetwriter.md) | Parquet file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [PostgreSQLBulkWriter](postgresqldatawriter.md) | database | 0-1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [QuickBaseRecordWriter](quickbaserecordwriter.md) | QuickBase | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [QuickBaseImportCSV](quickbaseimportcsv.md) | QuickBase | 1 | 0-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [SalesforceBulkWriter](salesforcebulkwriter.md) | Salesforce | 1 | 2 | **✓** | **⨯** | **⨯** | **✓** | **✓** |
| [SalesforceWriter](salesforcewriter.md) | Salesforce | 1 | 2 | **✓** | **⨯** | **⨯** | **✓** | **✓** |
| [SalesforceEinsteinWriter](salesforcewavewriter.md) | Salesforce | 1 | 2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [SpreadsheetDataWriter](spreadsheetwriter.md) | XLS(X) file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [SnowflakeBulkWriter](snowflakebulkwriter.md) | Snowflake | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |
| [StructuredDataWriter](structurewriter.md) | structured flat file | 1-3 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [TableauWriter](tableauwriter.md) | .tde file | 1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [Trash](trash.md) | none | 1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [UniversalDataWriter](datawriter.md) | flat file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [X12Writer](x12writer.md) | X12 file | 1-n | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [XMLWriter](extxmlwriter.md) | XML file | 1-n | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
