<!-- Development > Component reference > Writers > UniversalDataWriter -->

### UniversalDataWriter

![UniversalDataWriter 64x64](../figures/UniversalDataWriter-64x64.png)

| [Short description](datawriter.md#short-description) |
| --- |
| [Compatibility](datawriter.md#compatibility) |
| [See also](datawriter.md#see-also) |

#### Short description

**UniversalDataWriter** writes data to flat files. The output flat file can be in a form of CSV (character separated values), fixed-length format or mixed-length format (combination of mixed-length and fixed-length formats).

The component supports partitioning, compression, writing to output port or to remote destination.

**UniversalDataWriter** is an alias for [FlatFileWriter](flatfilewriter.md).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | The last record delimiter in a file can now be skipped. |
| 4.2.0-M1 | **UniversalDataWriter** has been renamed to **FlatFileWriter**. The original name remained as an alias for the **FlatFileWriter** component. |

#### See also

| [FlatFileWriter](flatfilewriter.md) |
| --- |
| [UniversalDataReader](datareader.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
