<!-- Development > Component reference > Readers > Common properties of Readers -->

### Common properties of Readers

- Readers allow you to *specify the location of input data*.
  See examples of the **File URL** attribute for reading from local and remote files, through proxy, input port and dictionary in [Supported file URL formats for Readers](examples-of-file-url-in-readers.md).
- Readers allow you to *view the source data*. See [Viewing data on Readers](viewing-data-on-readers.md).
- Readers can *read data from the input port*. E.g. you can read URLs of files to be read. See [Input port reading](input-port-reading.md).
- Readers can *read only the new records*. See [Incremental reading](incremental-reading.md).
- Readers can *skip specific number of initial records* or *set limit* on number of records to be read. See [Selecting input records](selecting-input-records.md).
- Readers allow you to configure a policy related to *parsing incomplete or invalid data record*. See [Data policy](data-policy.md).
- Some readers can log information about errors.
- XML-reading components allow you to *configure the parser*. See [XML features](xml-features.md).
- In some **Readers**, a transformation can be or must be defined. For information about transformation templates for transformations written in CTL see:
  [CTL templates for readers](ctl-templates-for-readers.md)
- Similarly, for information about transformation interfaces that must be implemented in transformations written in Java see:
  [Java interfaces for Readers](java-interfaces-for-readers.md)

| Component | Data source | Input ports | Output ports | Each to all outputs[[1]](common-of-readers.md#common-of-readers-footnote1) | Different to different outputs[[2]](common-of-readers.md#common-of-readers-footnote2) | Transformation | Transf. req. | Java | CTL | Auto- propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [CloverDataReader](cloverreader.md) | CloverDX binary file | 0 | 1-n | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [ComplexDataReader](complexdatareader.md) | flat file | 1 | 1-n | **⨯** | **✓** | **✓** | **✓** | **✓** | **✓** | **⨯** |
| [DatabaseReader](dbinputtable.md) | database | 0 | 1-n | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [DataGenerator](datagenerator.md) | none | 0 | 1-n | **⨯** | **✓** | **✓** | **✓** | **✓** | **✓** | **⨯** |
| [DBFDataReader](dbfdatareader.md) | dBase file | 0-1 | 1-n | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [EDIFACTReader](edifactreader.md) | EDIFACT files | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [EmailReader](emailreader.md) | email messages | 0 | 1 | - | - | **✓** | **⨯** | **✓** | **⨯** | **⨯** |
| [FlatFileReader](flatfilereader.md) | flat file | 0-1 | 1-2 | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [HadoopReader](hadoopreader.md) | Hadoop sequence file | 0 | 1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [HL7Reader](hl7reader.md) | HL7v2 files | 0-1 | 1 | **⨯** | **x** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [JavaBeanReader](beanreader.md) | dictionary | 0 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** |  |
| [JMSReader](jmsreader.md) | jms messages | 0 | 1 | - | - | **✓** | **⨯** | **✓** | **⨯** | **⨯** |
| [JSONExtract](jsonextract.md) | JSON file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [JSONReader](jsonreader.md) | JSON file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [KafkaCommit](kafkacommit.md) |  | 0-1 | 0 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |
| [KafkaReader](kafkareader.md) | Kafka cluster | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |
| [LDAPReader](ldapreader.md) | LDAP directory tree | 0 | 1-n | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [MongoDBReader](mongodbreader.md) | database | 0-1 | 1-2 | **⨯** | **⨯** | **✓** | **✓** | **⨯** | **✓** | **✓** |
| [MultiLevelReader](multilevelreader.md) | flat file | 1 | 1-n | **⨯** | **✓** | **✓** | **✓** | **✓** | **⨯** | **⨯** |
| [ParallelReader](parallelreader.md) | flat file | 0 | 1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |
| [ParquetReader](parquetreader.md) | Parquet file | 0-1 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |
| [QuickBaseRecordReader](quickbaserecordreader.md) | QuickBase | 0-1 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [QuickBaseQueryReader](quickbasequeryreader.md) | QuickBase | 0 | 1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [SalesforceBulkReader](salesforcebulkreader.md) | Salesforce | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |
| [SalesforceReader](salesforcereader.md) | Salesforce | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |
| [SpreadsheetDataReader](spreadsheetreader.md) | XLS(X) file | 0-1 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [UniversalDataReader](datareader.md) | flat file | 0-1 | 1-2 | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [X12Reader](x12reader.md) | X12 files | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [XMLExtract](xmlextract.md) | XML file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [XMLReader](xmlreader.md) | XML file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |
| [XMLXPathReader](xmlxpathreader.md) | XML file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

| 1 | The component sends each data record to all of the connected output ports. |
| --- | --- |

| 2 | The component sends different data records to different output ports using return values of the transformation (**DataGenerator** and **MultiLevelReader**). For more information, see [Return values of transformations](transformations.md#return-values-of-transformations). **XMLExtract**, **XMLReader** and **XMLXPathReader** send data to ports as defined in their **Mapping** or **Mapping URL** attribute. |
| --- | --- |
