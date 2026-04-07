<!-- Development > Component reference > Readers > CloverDataReader -->

### CloverDataReader

![CloverDataReader 64x64](../figures/CloverDataReader-64x64.png)

| [Short description](cloverreader.md#short-description) |
| --- |
| [Ports](cloverreader.md#ports) |
| [Metadata](cloverreader.md#metadata) |
| [CloverDataReader attributes](cloverreader.md#cloverdatareader-attributes) |
| [Examples](cloverreader.md#examples) |
| [Compatibility](cloverreader.md#compatibility) |
| [See also](cloverreader.md#see-also) |

#### Short description

**CloverDataReader** reads data stored in our internal binary **CloverDX** data format files. It can also read data from compressed files, or a dictionary.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CloverDX binary file | 1 | 1-n | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For [Input port reading](input-port-reading.md) correct data records | Include specific `byte`/`cbyte` field |
| Output | 0 | **✓** | For correct data records | Any |
| 1-n | **⨯** | For correct data records | Output 0 |  |

#### Metadata

CloverDataReader does not propagate metadata.

CloverDataReader has no metadata template, but it can extract metadata from **CloverDX** file and propagate it forward as it would have a template. (Available since **CloverETL 4.1.0-M1**.)

Metadata on the input port has to include a `byte`, `cbyte` or `string` field.

Metadata on the output port has to be the same as metadata of data from the file.

Metadata can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### CloverDataReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | An attribute specifying what data source(s) will be read (**CloverDX** data file, input port, dictionary). See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| Advanced |  |  |  |
| Secret key |  | Key to use for decryption of encrypted files. |  |
| Number of skipped records |  | Number of records to be skipped. See [Selecting input records](selecting-input-records.md). | 0-N |
| Max number of records |  | Maximum number of records to be read. See [Selecting input records](selecting-input-records.md). | 0-N |
| Number of skipped records per source |  | Skip the first `n` records of each file. | 0-N |
| Max number of records per source |  | Reads maximally `n` records from each file. | 0-N |
| Deprecated |  |  |  |
| Index file URL |  | The name of an index file, including the path. If not specified, all records are read. |  |
| Start record |  | Has exclusive meaning: Last record before the first that is already read. Has lower priority than **Number of skipped records**. | 0 (default) \| 1-n |
| Final record |  | Has inclusive meaning: Last record to be read. Has lower priority than **Max number of records**. | all (default) \| 1-n |

#### Examples

| [Reading a CloverDX data file](cloverreader.md#reading-a-cloverdx-data-file) |
| --- |
| [Omitting leading records](cloverreader.md#omitting-leading-records) |
| [Omitting leading records of each file](cloverreader.md#omitting-leading-records-of-each-file) |
| [Reading at most n records in total](cloverreader.md#reading-at-most-n-records-in-total) |
| [Reading at most n records per file](cloverreader.md#reading-at-most-n-records-per-file) |

##### Reading a CloverDX data file

Read all records from the **CloverDX** data file.

###### Solution

Set up the **File URL** attribute.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/my-clover-file.cdf |

**CloverDataReader** will read all the records from the file(s).

##### Omitting leading records

You have two **CloverDX** data files. First 3 records contain unimportant data and should not be read. The unimportant records are in the first file. (The records have been sorted and partitioned for example.)

`greengrocers1.cdf`

```
bread
honey
raisins
pears
plums
```

`greengrocers2.cdf`

```
carrot
peas
radish
```

###### Solution

Set up the **File URL** and **Number of skipped records** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/greengrocers1.cdf;${DATAIN_DIR}/greengrocers2.cdf |
| Number of skipped records | 3 |

**CloverDataReader** reads the following items:

```
pears
plums
carrot
peas
radish
```

##### Omitting leading records of each file

There are two **CloverDX** data files: `list1.cdf` and `list2.cdf`. Each file starts with one record to be omitted.

`list1.cdf`

```
Goods
cardigan
shirt
trousers
```

`list2.cdf`

```
Goods
shoes
sox
```

###### Solution

Set up the **File URL** and **Number of skipped records per source** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/list1.cdf;${DATAIN_DIR}/list2.cdf |
| Number of skipped records per source | 1 |

**CloverDataReader** sends the following records to the output:

```
cardigan
shirt
trousers
shoes
sox
```

##### Reading at most n records in total

You have three files `stationery1.cdf`, `stationery2.cdf` and `stationery3.cdf` and you need to read six records in total from all files.

`stationery1.cdf`

```
pen
pencil
marker
paintbrush
```

`stationery2.cdf`

```
ink
water colors
oil colors
```

`stationery3.cdf`

```
notebook
coloring book
```

###### Solution

Set up the **File URL** and **Max number of records** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/stationery1.cdf;${DATAIN_DIR}/stationery2.cdf;${DATAIN_DIR}/stationery3.cdf |
| Max number of records | 6 |

**CloverDataReader** sends all 4 records from `stationery1.cdf` and 2 of 3 records from `stationery2.cdf` to the output port. No record from the file `stationery3.cdf` is sent to the output port as the limit has been reached already.

```
pen
pencil
marker
paintbrush
ink
water colors
```

##### Reading at most n records per file

You have three **CloverDX** data files (`stationery[1-3].cdf`) from the previous example. Read at most 3 records from each file.

###### Solution

Set up the **File URL** and **Max number of records per source** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/stationery1.cdf;${DATAIN_DIR}/stationery2.cdf;${DATAIN_DIR}/stationery3.cdf |
| Max number of records per source | 3 |

**CloverDataReader** reads 3 records from `stationery1.cdf`, 3 records from `stationery2.cdf` and 2 of 2 records from `stationery3.cdf`.

```
pen
pencil
marker
ink
water colors
oil colors
notebook
coloring book
```

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 2.9 | **CloverDataWriter** also writes a header to output files with the version number. For this reason, **CloverDataReader** expects that files in **CloverDX** binary format contain such a header with the version number. **CloverDataReader** 2.9 cannot read files written by older versions nor these older versions can read data written by **CloverDataWriter** 2.9. |
| 4.0 | The internal structure of the zip archive has changed. Graphs that rely on the structure will stop working. Graphs that use plain zip file URL without internal entry specification are not affected: **CloverDataReader** with **File URL**`zip:(${DATAOUT_DIR}/employees.zip)#DATA/employees` will need to be fixed to use `zip:(${DATAOUT_DIR}/employees.zip)` instead. |
| 4.1.0-M1 | **CloverDataReader** can extract metadata template from **CloverDX** file. It can be seen as a metadata template corresponding to the file. |
| 4.4.0-M2 | **CloverDataReader** can read from input port just from `byte` or `cbyte` field. |

#### See also

| [CloverDataWriter](cloverwriter.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
