<!-- Development > Component reference > Writers > CloverDataWriter -->

### CloverDataWriter

![CloverDataWriter 64x64](../figures/CloverDataWriter-64x64.png)

| [Short description](cloverwriter.md#short-description) |
| --- |
| [Ports](cloverwriter.md#ports) |
| [Metadata](cloverwriter.md#metadata) |
| [CloverDataWriter attributes](cloverwriter.md#cloverdatawriter-attributes) |
| [Details](cloverwriter.md#details) |
| [Examples](cloverwriter.md#examples) |
| [Compatibility](cloverwriter.md#compatibility) |
| [See also](cloverwriter.md#see-also) |

#### Short description

**CloverDataWriter** writes data to files in our internal binary **CloverDX** data format.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| CloverDX binary file | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For received data records | Any |
| Output | 0 | **⨯** | For port writing. See [Writing to output port](examples-of-file-url-in-writers.md#writing-to-output-port). | `byte` or `cbyte` |

#### Metadata

**CloverDataWriter** does not propagate metadata.

**CloverDataWriter** has no metadata template.

Input metadata can have any metadata type.

Output metadata of **CloverDataWriter** has one field. The field has datatype `byte` or `cbyte`.

#### CloverDataWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | The attribute specifying where received data will be written (**CloverDX** data file, dictionary). See [Supported file URL formats for Writers](examples-of-file-url-in-writers.md). |  |
| Append |  | By default, new records overwrite the older ones. If set to `true`, new records are appended to the older records stored in the output file(s). | false (default) \| true |
| Advanced |  |  |  |
| Create directories |  | By default, non-existing directories are not created. If set to `true`, they are created. | false (default) \| true |
| Compress level |  | Sets the compression level (`0` - no compression, `1` - fastest compression, `9` - best compression). | 1 (default) \| 0-9 |
| Secret key |  | Key to use for encryption of files. Specifying the key enables encryption. Enabling encryption automatically disables compression. |  |
| Number of skipped records |  | The number of records to be skipped. See [Selecting output records](selecting-output-records.md). | 0-N |
| Max number of records |  | The maximum number of records to be written to the output file. See [Selecting output records](selecting-output-records.md). | 0-N |
| Records per file |  | Limits the number of records written to one file. | 0-N |
| Exclude fields |  | A sequence of field names separated by a semicolon that will not be written to the output. | any field(s), e.g. field1;field3 |
| Partition key |  | A sequence of field names separated by a semicolon defining the records distribution into different output files. Records with the same **Partition key** are written to the same output file. According to the selected **Partition file tag**, use the proper placeholder ($ or #) in the file name mask, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). Field(s) to be used in partitioning to several output files. | any field(s), e.g. field1;field3 |
| Partition lookup table |  | An ID of a lookup table serving for selecting records that should be written to output file(s). For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | e.g. MyLookupTable001 |
| Partition file tag |  | By default, output files are numbered. If it is set to `Key file tag`, output files are named according to the values of **Partition key** or **Partition output fields**. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | Number file tag (default) \| Key file tag |
| Partition output fields |  | Fields of **Partition lookup table** whose values serve to name output file(s). For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Partition unassigned file name |  | The name of a file into which the unassigned records should be written if there are any. If not specified, data records whose key values are not contained in **Partition lookup table** are discarded. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). |  |
| Sorted input |  | In case the partitioning into multiple output files is turned on, all output files are opened at once. This could lead to an undesirable memory footprint for many output files (thousands). Moreover, for example unix-based OS usually have a very strict limitation of number of simultaneously open files (1,024) per process. In case you run into one of these limitations, consider sorting the data according to a partition key using one of our standard sorting components and set this attribute to true. The partitioning algorithm does not need to keep all output files open, just the last one is open at one time. For more information, see [Partitioning output into different output files](partitioning-output-into-different-output-files.md). | false (default) \| true |
| Create empty files |  | If set to `false`, prevents the component from creating an empty output file when there are no input records. | true (default) \| false |
| Deprecated |  |  |  |
| Save metadata |  | This attribute is ignored since **CloverETL 4.0**. | false (default) \| true |
| Save index |  | This attribute is ignored since **CloverETL 4.0**. | false (default) \| true |

#### Details

**CloverDataWriter** internally uses compression by default. Additional zipping is redundant. See the **Compress level** attribute.

**CloverDataWriter** can write maps, lists and variants.

With this component, you can write data in this internal format that allows fast access to data. **CloverDataWriter** is faster than **FlatFileWriter**.

#### Examples

| [Writing to CloverDX file](cloverwriter.md#writing-to-cloverdx-file) |
| --- |
| [Appending to existing file](cloverwriter.md#appending-to-existing-file) |
| [Writing to non-existing directories](cloverwriter.md#writing-to-non-existing-directories) |
| [Skipping leading records](cloverwriter.md#skipping-leading-records) |
| [Writing at most N records per file](cloverwriter.md#writing-at-most-n-records-per-file) |
| [Omitting uninteresting fields](cloverwriter.md#omitting-uninteresting-fields) |
| [Parting records into several files according to input field](cloverwriter.md#parting-records-into-several-files-according-to-input-field) |
| [Parting records into several files according to input field using lookup table](cloverwriter.md#parting-records-into-several-files-according-to-input-field-using-lookup-table) |

##### Writing to CloverDX file

Write records to **CloverDX** file.

###### Solution

Set up the **File URL** attribute.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/my-clover-file.cdf |

If the file exists, the data in the file is overwritten.

##### Appending to Existing File

Append records of each graph run to an existing file `my-clover-file.cdf`.

###### Solution

Set up the **File URL** and **Append** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/my-clover-file.cdf |
| Append | true |

##### Writing to non-existing Directories

Write data to file `my-clover-file.cdf` in the `cdrw` directory. The directory may not exist.

###### Solution

Use the **File URL** and **Create directories** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/cdrw/my-clover-file.cdf |
| Create directories | true |

##### Skipping Leading Records

The first 10 records should be omitted. Write the rest of the records.

###### Solution

Use the **File URL** and **Number of skipped records** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/my-clover-file.cdf |
| Number of skipped records | 10 |

##### Writing at most N records per file

Write at most 100 records.

###### Solution

Use the **File URL** and **Max number of records** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/my-clover-file.cdf |
| Max number of records | 100 |

##### Omitting uninteresting fields

Metadata on the input edge of **CloverDataWriter** has fields **ID**, **Firstname**,**Surname** and **Salary**. Save a list containing **Firstname** and **Surname** to **CloverDX** data file `employees.cdf`.

###### Solution

Use the **File URL** and **Exclude fields** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/employees.cdf |
| Exclude fields | ID;Salary |

##### Parting records into several files according to input field

A list of students contains fields **Firstname**, **Lastname** and **Mark**. Categorize records into several files according to the mark. The created files will have names: `students_A.cdf`, …​ `students_F.cdf`.

###### Solution

Use the **File URL**, **Partition key** and **Partition file tag** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/students_#.cdf |
| Partition key | Mark |
| Partition file tag | Key file tag |

Note: Records with students without mark will be saved into the `students_.cdf` file.

##### Parting records into several files according to input field using lookup table

The input data contains a number of active customers for particular countries. The countries are of different regions. Categorize records into the files according to the region.

```
CZ|105
UK|651
US|827
...
```

The input metadata contains fields **CountryCode** and **Customers** but nothing in the record denotes the region directly. You have a list of country codes with corresponding region to be used for partitioning.

```
CZ|Europe
UK|Europe
US|America
...
```

Some country codes may not be present in the list, store records with country codes not present in the list into a separate file `region_missing.cdf`.

###### Solution

Use the attributes **File URL**, **Partition key**, **Partition lookup table**, **Partition file tag**, **Partition output fields**, **Partition unassigned file name**. You need a lookup table **CountryCodeRegion**, too.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/region_#.cdf |
| Partition key | CountryCode |
| Partition lookup table | CountryCodeRegion |
| Partition file tag | Key file tag |
| Partition output fields | Continent |
| Partition unassigned file name | missing |

The files `region_Europe.cdf`, `region_America.cdf`, …​ and `region_missing.cdf` will be created.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 2.9 | **CloverDataWriter** also writes a header to output files with a version number. For this reason, **CloverDataReader** expects that files in **CloverDX** binary format contain such a header with the version number. **CloverDataReader** 2.9 cannot read files written by older versions of **CloverDX** nor these older versions can read data written by **CloverDataWriter** 2.9. |
| 4.0 | The internal structure of zip archive has changed, graphs relying on the structure will stop working. Graphs using a plain file URL without any internal entry specification are not affected.   ``` zip:(${DATAIN_DIR}/customers.zip) - will work zip:(${DATAIN_DIR}/customers.zip)#DATA/customers - won't work ```   As **CloverDX** format can use compression internally, addition of next compression level is redundant.  Values of parameters **Save metadata** and **Save index** are not used since **CloverETL 4.0**. |
| 4.4.0-M2 | **CloverDataWriter** can write to output port just to `byte` or `cbyte` field. |

#### See also

| [CloverDataReader](cloverreader.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
| [Partitioning output into different output files](partitioning-output-into-different-output-files.md) |
