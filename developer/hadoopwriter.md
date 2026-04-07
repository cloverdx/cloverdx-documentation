<!-- Development > Component reference > Writers > HadoopWriter -->

### HadoopWriter

![HDFSWriter 64x64](../figures/HDFSWriter-64x64.png)

| [Short description](hadoopwriter.md#short-description) |
| --- |
| [Ports](hadoopwriter.md#ports) |
| [Metadata](hadoopwriter.md#metadata) |
| [HadoopWriter attributes](hadoopwriter.md#hadoopwriter-attributes) |
| [Details](hadoopwriter.md#details) |
| [Troubleshooting](hadoopwriter.md#troubleshooting) |
| [See also](hadoopwriter.md#see-also) |

#### Short description

**HadoopWriter** writes data into Hadoop sequence files.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Hadoop sequence file | 1 | 0 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |

#### Metadata

**HadoopWriter** does not propagate metadata.

**HadoopWriter** has no metadata template.

#### HadoopWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Hadoop connection |  | [Hadoop connections](hadoop-connections.md) with Hadoop libraries containing the Hadoop sequence file writer implementation. If the Hadoop connection ID is specified in a `hdfs://` URL in the **File URL** attribute, the value of this attribute is ignored. | Hadoop connection ID |
| File URL | **✓** | A URL to an output file on HDFS or a local file system.  URLs without a protocol (i.e. absolute or relative path) or with the `file://` protocol are considered to be located on the local file system.  If the output file should be located on the HDFS, use the URL in form of `hdfs://ConnID/path/to/file`, where `ConnID` is the ID of a [Hadoop connections](hadoop-connections.md) (the **Hadoop connection** component attribute will be ignored), and `/path/to/myfile` is the absolute path on corresponding HDFS to the file named `myfile`. |  |
| Key field | **✓** | The name of an input record field carrying a key for each written key-value pair. |  |
| Value field | **✓** | The name of an input record field carrying a value for each written key-value pair. |  |
| Advanced |  |  |  |
| Create empty files |  | If set to `false`, prevents the component from creating an empty output file when there are no input records. | true (default) \| false |

#### Details

**HadoopWriter** writes data into a special Hadoop sequence file (`org.apache.hadoop.io.SequenceFile`). These files contain key-value pairs and are used in MapReduce jobs as input/output file formats. The component can write a single file as well as a partitioned file which has to be located on HDFS or a local file system.

The exact version of the file format created by the **HadoopWriter** component depends on Hadoop libraries which you supply in the **Hadoop connection** referenced from the **File URL** attribute. In general, sequence files created by one version of Hadoop may not be readable by different version.

When writing to a local file system, additional `.crc` files are created if the Hadoop connection with default settings is used. That is because, by default, Hadoop interacts with a local file system using `org.apache.hadoop.fs.LocalFileSystem` which creates checksum files for each written file. When reading such files, checksum is verified. You can disable checksum creation/verification by adding this key-value pair in the **Hadoop Parameters** of the [Hadoop connections](hadoop-connections.md): `fs.file.impl=org.apache.hadoop.fs.RawLocalFileSystem`

For technical details about Hadoop sequence files, see [Apache Hadoop Wiki](http://wiki.apache.org/hadoop/SequenceFile).

##### Notes and limitations

Currently, writing compressed data is not supported.

**HadoopWriter** cannot write lists and maps.

#### Troubleshooting

If you write data to a sequence file on a local file system, you may encounter the following error message in the error log:

```
Cannot run program "chmod": CreateProcess error=2, The system cannot find the file specified
```

or

```
Cannot run program "cygpath": CreateProcess error=2, The system cannot find the file specified
```

To solve this problem, disable checksum creation/verification using the `fs.file.impl=org.apache.hadoop.fs.RawLocalFileSystem` Hadoop parameter in Hadoop connection configuration.

This issue is related to non-POSIX operating systems (MS Windows).

#### See also

| [HadoopReader](hadoopreader.md) |
| --- |
| [Hadoop connections](hadoop-connections.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers](writers.md) |
