<!-- Development > Component reference > Readers > UniversalDataReader -->

### UniversalDataReader

![UniversalDataReader 64x64](../figures/UniversalDataReader-64x64.png)

| [Short description](datareader.md#short-description) |
| --- |
| [Compatibility](datareader.md#compatibility) |
| [See also](datareader.md#see-also) |

#### Short description

**UniversalDataReader** reads data from flat files such as a CSV (comma-separated values) file and delimited, fixed-length or mixed text files.

The component can read a single file as well as a collection of files placed on a local disk or remotely. Remote files are accessible via HTTP, HTTPS, FTP, or SFTP protocols. Using this component, ZIP and TAR archives of flat files can be read. Reading data from an input port, or dictionary is supported, as well.

**UniversalDataReader** is an alias for [FlatFileReader](flatfilereader.md).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.2.0-M1 | **UniversalDataReader** was renamed to [FlatFileReader](flatfilereader.md). Since this version, **UniversalDataReader** is an alias to **FlatFileReader**. |

#### See also

| [FlatFileReader](flatfilereader.md) |
| --- |
| [UniversalDataWriter](datawriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
