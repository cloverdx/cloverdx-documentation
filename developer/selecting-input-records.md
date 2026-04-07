<!-- Development > Component reference > Readers > Common properties of Readers > Selecting input records -->

#### Selecting input records

Some readers allow you to limit the number of records that should be read. You can set up:

- Maximum number of records to be read
- Number of records to be skipped
- Maximum number of records to be read per source
- Number of records to be skipped per source

The last two constraints can be defined only in readers that allow reading more files at the same time. In these **Readers**, you can define the records that should be read for each input file separately and for all of the input files in total.

##### Per reader configuration

The maximum number of records to be read is defined by the **Max number of record** attribute. The number of records to be skipped is defined by the **Number of skipped records** attribute. The records are skipped and/or read continuously throughout all input files. The records are skipped and/or read independently of the values of per source file attributes.

##### Per source file configuration

In some components, you can also specify how many records should be skipped and/or read from each input file. To do this, set up the following two attributes: **Number of skipped records per source** and/or **Max number of records per source**.

###### Combination of per file and per reader configuration

If you set up both: *per file* and *per reader* limits; firstly, the *per file* limits are applied. Secondly, the *per reader* limits are applied.

For example, there are two files:

```
1 | Alice
2 | Bob
3 | Carolina
4 | Daniel
5 | Eve
```

```
6 | Filip
7 | Gina
8 | Henry
9 | Isac
10| Jane
```

And the reader has the following configuration:

| Attribute | Value |
| --- | --- |
| Number of skipped records | 2 |
| Max number of record | 5 |
| Number of skipped records per source | 1 |
| Max number of records per source | 3 |

The file are read in the following way:

1. From each file, the first record is skipped and the next three records are read.
2. The first two records of the records read in the previous step are skipped. The following records (at most four) are sent to the output.

The record read by the reader are

```
4 | Daniel
7 | Gina
8 | Henry
9 | Isac
```

The example shows that you can read even less records than is the number specified in the **Max number of records** attribute.

The total number of records that are skipped equals to **Number of skipped records per source** multiplied by the number of source files plus **Number of skipped records**.

And total number of records that are read equals to **Max number of records per source** multiplied by the number of source files plus **Max number of records**.

The **Readers** that allow limiting the records for both individual input file and all input files in total are:

- [CloverDataReader](cloverreader.md)
- [DBFDataReader](dbfdatareader.md)
- [FlatFileReader](flatfilereader.md)
- [MultiLevelReader](multilevelreader.md)
- [ParallelReader](parallelreader.md)
- [SpreadsheetDataReader](spreadsheetreader.md)

The following two **Readers** allow you to limit the total number of records by using the **Number of skipped mappings** and/or **Max number of mappings** attributes. What is called **mapping** here, is a subtree which should be mapped and sent out through the output ports.

- [XMLExtract](xmlextract.md); in addition, this component allows to use the `skipRows` and/or `numRecords` attributes of individual XML elements.
- [XMLXPathReader](xmlxpathreader.md); in addition, this component allows to use XPath language to limit the number of mapped XML structures.

The following **Readers** allow limiting the numbers in a different way:

- [JMSReader](jmsreader.md) allows you to limit the number of messages that are received and processed using the **Max msg count** attribute and/or the `false` return value of `endOfInput()` method of the component interface.
- The [QuickBaseRecordReader](quickbaserecordreader.md) component uses the **Records list** attribute to specify the records that should be read.
- The [QuickBaseQueryReader](quickbasequeryreader.md) component can use the **Query** or **Options** attributes to limit the number of records.
- The [DatabaseReader](dbinputtable.md) component can use the **SQL query** or **Query URL** attribute to limit the number of records.

The following **Readers** do not allow limiting the number of records that should be read (they read them all):

- [LDAPReader](ldapreader.md)
- [ParallelReader](parallelreader.md)
