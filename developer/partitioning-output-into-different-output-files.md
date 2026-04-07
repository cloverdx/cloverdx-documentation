<!-- Development > Component reference > Writers > Common properties of Writers > Partitioning output into different output files -->

#### Partitioning output into different output files

Some **Writers** let you part the incoming data flow and distribute the records among different output files. The components are:

| [CloverDataWriter](cloverwriter.md) |
| --- |
| [DBFDataWriter](dbfdatawriter.md) |
| [EDIFACTWriter](edifactwriter.md) |
| [FlatFileWriter](flatfilewriter.md) |
| [JSONWriter](jsonwriter.md) |
| [SpreadsheetDataWriter](spreadsheetwriter.md) |
| [StructuredDataWriter](structurewriter.md) |
| [X12Writer](x12writer.md) |
| [XMLWriter](extxmlwriter.md) |
|  |

##### Partitioning criteria

You can part data according to the number of records or classified according to values of specified fields.

##### Partitioning by number of records

Partitioning by number of records saves at most `N` records into one file. The other records are saved into another file until the limit is reached and so forth. Use **Records per file** attribute to set up the limit `N`.

**Example:** part 450 record into output files. Each output file has at most 100 record.

**Solution:****File URL** value should contain $ sign(s). The $ signs will be replaced with digits.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/output_$$.txt |
| Records per file | 100 |

##### Partitioning according to data field value

Records can be parted into multiple output files according to a data field value. The field is specified with the **Partition key** attribute.

The placeholder `#` in output file name can be replaced with a field value or with integer. If **Partition file tag** is set to **Number file tag**, the placeholder is replaced with integer. If **Partition file tag** is set to **Key file tag**, the placeholder is replaced with a field value. The default value is **Number file tag**.

The partition key consists of a list of fields forming the partition key. The list has the form of a sequence of incoming record field names separated by a semicolon.

**Example:** part data according to the `field1` field. Use the field value as a part of output file name.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/output_#.txt |
| Partition key | field1 |
| Partition file tag | Key file tag |

If you use two or more fields for partitioning, use the placeholder `#` on one place in the file URL: `${DATAOUT_DIR}/output_#.txt`. Do not use the placeholder for each key field.

##### Partitioning using Lookup table

Partitioning using a lookup table lets you part records using input field values. The values of **Partition key** serve as a key to be looked up in the lookup table. A value corresponding to the key defines a group.

A group can form its name with a number or value from a lookup table.

Each group is written to its own output file.

The difference between partitioning according to a data field value, and partitioning using a lookup table is that in the first case, one unique **Partition key** value creates one group, whereas in the latter one, a single group can correspond to multiple different **Partition key** values.

**Example:** input data contain the field `city` as well as other fields. The lookup table contains `city` and `country`. Part data into files: each file should contain records corresponding to one country. Records with unmatched cities should have `unmatched` instead of the country.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/output_#.txt |
| Partition key | field1 |
| Partition lookup table | TheLookupTable |
| Partition file tag | Key file tag |
| Partition output fields | country |
| Partition unassigned file name | unmatched |

Remember that if all incoming records are assigned to the values of lookup table, the file for unassigned records will be empty (even if it is defined).

##### Filtering records using Lookup table

You can use partitioning using a lookup table to write a subset of input records. For example, you can only write records corresponding to some countries (from previous example). To constrain the records, define values of desired fields in lookup table (key fields) and leave **Partition unassigned file name** blank.

##### Combining of ways of partitioning

You can combine partitioning by number of records and partitioning according to data field value.

**Example:** part data according to the `field1` field. Use the field value as a part of output file name. Write at most 100 records into one file.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAOUT_DIR}/output_#_$.txt |
| Records per file | 100 |
| Partition key | field1 |
| Partition file tag | Key file tag |

The `#` sign is replaced with a `field1` value. The `$` sign is replaced with integer according to number of record with same `field1` value.

##### Limits of partitioning

The partitioning algorithm keeps all output files open at once. This could lead to an undesirable memory footprint for many output files (thousands). Moreover, for example unix-based OS usually have very strict limitation of number of simultaneously open files (1,024) per process.

In case you run into one of these limitations, consider sorting the data according to the partition key using one of our standard sorting components and set the **Sorted input** attribute to true. The partitioning algorithm does not need to keep open all output files, just the last one is open at one time.

##### Name for partitioned file

The **File URL** value only serves as a base name for the output file names. The base name should contain placeholders - dollar sign or hash sign.

The dollar sign is replaced with a number. If you use more dollar signs, each `$` is replaced with one digit. This way, leading zeros can be inserted. Use `$` if you part according to number of records.

The hash sign is replaced with a number, field value, or value from a lookup table. Leading zeros can be created with more hash signs. Use `#` if you part according to field value or using lookup table.

##### Hash sign versus dollar sign
> [!IMPORTANT]
> You should differentiate between hash sign and dollar sign usage.
>
> - **Hash sign**
>   A hash sign should be used when each of multiple output files only contains records corresponding to the value of specified **Partition key**.
> - **Dollar sign**
>   A dollar sign should be used when each of multiple output files contains only a specified number of records based on the **Records per file** attribute.

The hash(es) can be inserted in any place of this file part of **File URL**, even in the middle. For example: `path/output#.xls` (in the case of the output XLS file).

If **Partition file tag** is set to `Number file tag`, output files are numbered and the count of hashes used in **File URL** means the count of digits for these distinguishing numbers. This is the default value of **Partition file tag**. Thus, `###` can go from `000` to `999`.

If **Partition file tag** is set to `Key file tag`, a single hash must be used in **File URL** at most. Distinguishing names are used.

These distinguishing names will be created as follows:

If the **Partition key** attribute (or the **Partition output fields** attribute) is of the following form: `field1;field2;…;fieldN` and the values of these fields are the following: `valueofthefield1`, `valueofthefield2`, …​, `valueofthefieldN`, all the values of the fields are converted to strings and concatenated. The resulting strings will have the following form: `valueofthefield1valueofthefield2…valueofthefieldN`. Such resulting strings are used as distinguishing names and each of them is inserted to the **File URL** into the place marked with hash, or appended to the end of **File URL** if no hash is used in **File URL**.

For example, if `firstname;lastname` is the **Partition key** (or **Partition output fields**), you can have the output files as follows:

- `path/outjohnsmith.xls`, `path/outmarksmith.xls`, `path/outmichaelgordon.xls`, etc. (if **File URL** is `path/out#.xls` and **Partition file tag** is set to `Key file tag`).
- Or `path/out01.xls`, `path/out02.xls`. etc. (if **File URL** is `path/out##.xls` and **Partition file tag** is set to `Number file tag`).
