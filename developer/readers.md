<!-- Development > Component reference > Readers -->

## 35. Readers

| [Common properties of Readers](common-of-readers.md) |
| --- |
> [!TIP]
> If you’re interested in learning more about this subject, we offer the [Advanced Tips for Using Reader Components course](https://academy.cloverdx.com/courses/advanced-readers-tips) in our CloverDX Academy.

**Readers** can read data from input files (both local and remote), receive it from the connected optional input port, read it from a dictionary, from a database, or from a JMS.

One component only generates data. Since it is also an initial node, we will describe it here.

### Readers overview

We can distinguish **Readers** according to what they can read:

#### Generating data

A [DataGenerator](datagenerator.md) component generates data.

#### Reading flat files

- [FlatFileReader](flatfilereader.md) reads data from flat files (delimited or fixed length).
- [ParallelReader](parallelreader.md) reads data from delimited flat files using more threads.
- [ComplexDataReader](complexdatareader.md) reads data from flat files whose structure is heterogeneous or mutually dependent and it uses a GUI to achieve that.
- [MultiLevelReader](multilevelreader.md) reads data from flat files with a heterogeneous structure.

#### Reading XML files

- [XMLExtract](xmlextract.md) reads data from XML files using SAX technology.
- [XMLReader](xmlreader.md) reads data from XML files using DOM technology.
- [XMLXPathReader](xmlxpathreader.md) reads data from XML files using XPath queries.

Generally, use **XMLExtract**. If you require a more complex XPath queries, use **XMLReader**.

#### Reading JSON files

- [JSONExtract](jsonextract.md) reads data from JSON files. Based on SAX.
- [JSONReader](jsonreader.md) reads data from JSON files using XPath queries. Based on DOM.

#### Reading EDI files

- [EDIFACTReader](edifactreader.md) reads data from EDIFACT files. Based on SAX.
- [X12Reader](x12reader.md) reads data from X12 files. Based on SAX.
- [HL7Reader](hl7reader.md) reads data from HL7v2 files. Based on SAX.

#### Reading other files

- [CloverDataReader](cloverreader.md) reads data from files in **CloverDX** binary format.
- [SpreadsheetDataReader](spreadsheetreader.md) reads data from XLS or XLSX files.
- [DBFDataReader](dbfdatareader.md) reads data from dBase files.
- [HadoopReader](hadoopreader.md) reads data from Hadoop sequence files.
- [ParquetReader](parquetreader.md) reads data from Apache Parquet files.

#### Reading databases

- [DatabaseReader](dbinputtable.md) unloads data from database using a JDBC driver.
- [QuickBaseRecordWriter](quickbaserecordwriter.md) reads data from a **QuickBase** online database.
- [QuickBaseImportCSV](quickbaseimportcsv.md) reads data from a **QuickBase** online database using queries.
- [MongoDBReader](mongodbreader.md) reads data from a **MongoDB** NoSQL database.
- [SalesforceBulkReader](salesforcebulkreader.md) reads data from a **Salesforce** cloud platform using Bulk API.
- [SalesforceReader](salesforcereader.md) reads data from a **Salesforce** cloud platform using SOAP API.

#### Data Set Readers

- [ReferenceDataSetReader](referencedatasetreader.md) reads data from reference data set in the Data Manager.
- [TransactionalDataSetReader](datasetreader.md) reads data from transactional data set in the Data Manager.

#### Reading other resources

- JMS messages:
  - [JMSReader](jmsreader.md) converts JMS messages into data records.
- Directory structure:
  - [LDAPReader](ldapreader.md) converts directory structure into data records.
- Email messages:
  - [EmailReader](emailreader.md) reads email messages.
- Kafka events:
  - [KafkaReader](kafkareader.md) reads events (messages) from a Kafka cluster.
  - [KafkaCommit](kafkacommit.md) commits processed offsets for Kafka topics.

### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
