<!-- Development > Component reference > Readers > HadoopReader -->

### HadoopReader

![HDFSReader 64x64](../figures/HDFSReader-64x64.png)

| [Short description](hadoopreader.md#short-description) |
| --- |
| [Ports](hadoopreader.md#ports) |
| [Metadata](hadoopreader.md#metadata) |
| [HadoopReader attributes](hadoopreader.md#hadoopreader-attributes) |
| [Details](hadoopreader.md#details) |
| [Examples](hadoopreader.md#examples) |
| [See also](hadoopreader.md#see-also) |

#### Short description

**HadoopReader** reads Hadoop sequence files.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Hadoop Sequence File | 0–1 | 1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For [Input port reading](input-port-reading.md). Only the `source` mode is supported. | Any |
| Output | 0 | **✓** | For read data records. | Any |

#### Metadata

HadoopReader does not propagate metadata.

HadoopReader has no metadata template.

#### HadoopReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Hadoop connection |  | [Hadoop connections](hadoop-connections.md) with Hadoop libraries containing the Hadoop sequence file parser implementation. If the Hadoop connection ID is specified in a `hdfs://` URL in the **File URL** attribute, the value of this attribute is ignored. | Hadoop connection ID |
| File URL | **✓** | A URL to a file on HDFS or a local file system.  URLs without a protocol (i.e. absolute or relative path) or with the `file://` protocol are considered to be located on the local file system.  If the file to be read is located on the HDFS, use the URL in this form: `hdfs://ConnID/path/to/file`, where `ConnID` is the ID of a *[Hadoop connections](hadoop-connections.md)* (the **Hadoop connection** component attribute will be ignored), and `/path/to/myfile` is the absolute path on corresponding HDFS to the file named `myfile`. |  |
| Key field | **✓** | The name of an output edge record field, where a key of each key-value pair will be stored. |  |
| Value field | **✓** | The name of an output edge record field, where a value of each key-value pair will be stored. |  |

#### Details

**HadoopReader** reads data from a special Hadoop sequence file (`org.apache.hadoop.io.SequenceFile`). These files contain key-value pairs and are used in MapReduce jobs as input/output file formats. The component can read a single file as well as a collection of files which have to be located on HDFS or local file system.

If you connect to local sequence files, there is no need to connect to a Hadoop cluster. However, you still need a valid Hadoop connection (with a correct version of libraries).

The exact version of the file format supported by the **HadoopReader** component depends on Hadoop libraries which you supply in the **Hadoop connection** referenced from the **File URL** attribute. In general, sequence files created by one version of Hadoop may not be readable by a different version.

Hadoop sequence files may contain compressed data. **HadoopReader** automatically detects this and decompresses the data. Remember that supported compression codecs depend on libraries you specify in the **Hadoop connection**.

For technical details about Hadoop sequence files, see [Apache Hadoop Wiki](http://wiki.apache.org/hadoop/SequenceFile).

#### Examples

##### Reading data from local sequence files

Read records from a Hadoop Sequence file `products.dat`. The file has `ProductID` as a key and `ProductName` as a value.

###### Solution

Create a valid Hadoop connection or use existing one. See [Hadoop connections](hadoop-connections.md).

Use the **Hadoop connection**, **File URL**, **Key field** and **Key value** attributes.

| Attribute | Value |
| --- | --- |
| Hadoop connection | MyHadoopConnection |
| File URL | ${DATA_IN}/products.dat |
| Key field | ProductID |
| Value field | ProductName |

#### See also

| [HadoopWriter](hadoopwriter.md) |
| --- |
| [Hadoop connections](hadoop-connections.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
