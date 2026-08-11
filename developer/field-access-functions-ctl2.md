<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Record functions (dynamic field access) -->

### Record functions (dynamic field access)

#### List of Functions

| [compare](field-access-functions-ctl2.md#compare) |
| --- |
| [copyByName](field-access-functions-ctl2.md#copybyname) |
| [copyByPosition](field-access-functions-ctl2.md#copybyposition) |
| [getBoolValue](field-access-functions-ctl2.md#getboolvalue) |
| [getByteValue](field-access-functions-ctl2.md#getbytevalue) |
| [getDateValue](field-access-functions-ctl2.md#getdatevalue) |
| [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue) |
| [getFieldIndex](field-access-functions-ctl2.md#getfieldindex) |
| [getFieldLabel](field-access-functions-ctl2.md#getfieldlabel) |
| [getFieldName](field-access-functions-ctl2.md#getfieldname) |
| [getFieldProperties](field-access-functions-ctl2.md#getfieldproperties) |
| [getFieldType](field-access-functions-ctl2.md#getfieldtype) |
| [getIntValue](field-access-functions-ctl2.md#getintvalue) |
| [getLongValue](field-access-functions-ctl2.md#getlongvalue) |
| [getNumValue](field-access-functions-ctl2.md#getnumvalue) |
| [getRecordProperties](field-access-functions-ctl2.md#getrecordproperties) |
| [getStringValue](field-access-functions-ctl2.md#getstringvalue) |
| [getValue](field-access-functions-ctl2.md#getvalue) |
| [getValueAsString](field-access-functions-ctl2.md#getvalueasstring) |
| [isNull](field-access-functions-ctl2.md#isnull) |
| [length(record)](field-access-functions-ctl2.md#length) |
| [resetRecord](field-access-functions-ctl2.md#resetrecord) |
| [setBoolValue](field-access-functions-ctl2.md#setboolvalue) |
| [setByteValue](field-access-functions-ctl2.md#setbytevalue) |
| [setDateValue](field-access-functions-ctl2.md#setdatevalue) |
| [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue) |
| [setIntValue](field-access-functions-ctl2.md#setintvalue) |
| [setLongValue](field-access-functions-ctl2.md#setlongvalue) |
| [setNumValue](field-access-functions-ctl2.md#setnumvalue) |
| [setStringValue](field-access-functions-ctl2.md#setstringvalue) |
| [setValue](field-access-functions-ctl2.md#setvalue) |

These functions are to be found in the **Functions** tab, section **Dynamic field access library** inside the [Transform Editor](transformations.md#transform-editor).

#### compare

```ctl
integer compare(record record1, integer fieldIndex1, record record2, integer fieldIndex2);
integer compare(record record1, string fieldName1, record record2, string fieldName2);
```

The `compare()` function compares two fields of given records.

The fields are identified by their index (integer - 0 is the first field) or name (string). The function returns an integer value which is either:

1. < 0 …​ `field2` is greater than `field1`
2. > 0 …​ `field2` is lower than `field1`
3. 0 …​ fields are equal

If one of the given record has a `null` reference, the function fails with an error.

If one of the given record fields is of type `list`, `map` or `variant`, the function fails with an error.

**Compatibility**

The `compare(reference,integer,reference,integer)` and `compare(reference,string,reference,string)` functions are available since **CloverETL 3.2.0**.
Example 275. Usage of compare

```ctl
$out.0.field1 = $in.0.field1 + 1;
$out.0.field2 = $in.0.field1;
$out.0.field3 = $in.0.field1 - 1;

$out.0.field5 = compare($in.0, 0, $out.0, 0);  // returns -1
$out.0.field6 = compare($in.0, 0, $out.0, 1);  // returns  0
$out.0.field7 = compare($in.0, 0, $out.0, 2);  // returns  1

$out.0.field8 = compare($in.0, "field1", $out.0, "field1");  // returns -1
$out.0.field9 = compare($in.0, "field1", $out.0, "field2");  // returns  0
$out.0.field10 = compare($in.0, "field1", $out.0, "field3"); // returns  1
```

#### copyByName

```ctl
void copyByName(record to, record from);
```

The `copyByName()` function copies data from the input record to the output record based on field names. Enables mapping of equally named fields only.

If a record specified as a first argument has a `null` reference, the function fails with an error.

**Compatibility**

The `copyByName(reference,reference)` function is available since **CloverETL 3.2.2** or earlier.
Example 276. Usage of copyByName
There are two records. The input record has fields `city`, `countryCode` and `phone`. The output record has fields `countryCode`, `phone` and `email`.

The function `copyByName($out.0, $in.0)` copies fields `countryCode` and `phone`.

**See also:**[copyByPosition](field-access-functions-ctl2.md#copybyposition)

#### copyByPosition

```ctl
void copyByPosition(record to, record from);
```

The `copyByPosition()` function copies data from the input record to the output record based on fields order. The number of fields in output metadata decides which input fields (beginning the first one) are mapped.

If a record specified as a first argument has a `null` reference, the function fails with an error.

**Compatibility**

The `copyByPosition(reference,reference)` function is available since **CloverETL 3.2.2** or earlier.
Example 277. Usage of copyByPosition There are two records. The input record has fields `field1`, `field2` and `field3`. The output record has fields `firstField` and `lastField`. The function `copyByPosition($out.0, $in.0)` copies value from `field1` to `firstField` and from `field2` to `lastField`.
**See also:**[copyByName](field-access-functions-ctl2.md#copybyname)

#### getBoolValue

```ctl
boolean getBoolValue(record record, integer fieldIndex);
boolean getBoolValue(record record, string fieldName);
```

The `getBoolValue()` function returns the value of a boolean field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getBoolValue(reference, integer)` and `getBoolValue(reference,string)` functions are available since **CloverETL 3.2.0**.
Example 278. Usage of getBoolValue
There is a record with with fields `field1`, `field2` and `field3` and values `[true, false, true]`.

The function `getBoolValue($in.0, 1)` returns `false` as second field of record is set to `false`.

The function `getBoolValue($in.0, "field1")` returns `true`.

**See also:**[getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setBoolValue](field-access-functions-ctl2.md#setboolvalue)

#### getByteValue

```ctl
byte getByteValue(record record, integer fieldIndex);
byte getByteValue(record record, string fieldName);
```

The `getByteValue()` function returns the value of a byte field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getByteValue(record,integer)` and `getByteValue(record,string)` functions are available since **CloverETL 3.2.0**.
Example 279. Usage of getByteValue
There is a record with fields `field1`,`field2` and `field3` containing values `oak`, `larch` and `pine`.

The function `getByteValue($in.0, 0)` returns `oak`.

The function `getByteValue($in.0, 1)` returns `larch`.

The function `getByteValue($in.0, "field3")` returns `pine`.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setByteValue](field-access-functions-ctl2.md#setbytevalue)

#### getDateValue

```ctl
date getDateValue(record record, integer fieldIndex);
date getDateValue(record record, string fieldName);
```

The `getDateValue()` function returns the value of a date field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getDateValue(reference,integer)` and `getDateValue(reference,string)` functions are available since **CloverETL 3.2.0**.
Example 280. Usage of getDateValue
There is a record having fields `date1`, `date2`, `date3` and `date4` with values `2010-10-10`, `2011-11-11`, `2012-12-12` and `null`.

The function `getDateValue($in.0, 0)` returns `2010-10-10`.

The function `getDateValue($in.0, 3)` returns `null`.

The function `getDateValue($in.0, 8)` fails with an error.

The function `getByteValue($in.0, "field3")` returns `2012-12-12`.

The function `getByteValue($in.0, "field9")` fails with an error. Field `field9` is not present in the record.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setDateValue](field-access-functions-ctl2.md#setdatevalue)

#### getDecimalValue

```ctl
decimal getDecimalValue(record record, integer fieldIndex);
decimal getDecimalValue(record record, string fieldName);
```

The `getDecimalValue()` function returns the value of a decimal field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getDecimalValue(reference,integer)` and `getDecimalValue(reference,string)` functions are available **CloverETL 3.2.0**.
Example 281. Usage of DecimalValue
There is a record having fields `field1`, `field2` and `field3` with values `1.01D`, `20.52D` and `100.75D`.

The function `getDecimalValue($in.0, 0)` returns `1.01`.

The function `getDecimalValue($in.0, "field3")` returns `100.75`.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue)

#### getFieldIndex

```ctl
integer getFieldIndex(record record, string field);
```

The `getFieldIndex()` function returns the index (zero-based) of a field which is identified by its name. If the field name is not found in the record, the function returns -1.

If a given record has a `null` reference, the function fails with an error.

**Compatibility**

The `getFieldIndex(reference,string)` function is available since **CloverETL 3.2.0**.
Example 282. Usage of getFieldIndex
There is a record having fields `field1`, `field2` and `field3`.

The function `getFieldIndex($in.0, "field1")` returns `0`.

The function `getFieldIndex($in.0, "field123")` returns `-1`.

**See also:**[getFieldLabel](field-access-functions-ctl2.md#getfieldlabel), [getFieldName](field-access-functions-ctl2.md#getfieldname), [getFieldType](field-access-functions-ctl2.md#getfieldtype)

#### getFieldLabel

```ctl
string getFieldLabel(record record, integer field);
```

The `getFieldLabel()` function returns the label of a field which is identified by its index. Please note a label is not a field’s name, see [Field Name vs. Label vs. Description](metadata-editor.md#field-name-vs-label-vs-description).

If a given record has a `null` reference, the function fails with an error.

**Compatibility**

The `getFieldLabel(record,integer)` and `getFieldLabel(record,string)` functions are available since **CloverETL 3.2.0**.
Example 283. Usage of getFieldLabel
There is a record having fields `field1` and `field2` with field labels `The first field` and `The second field`.

The function `getFieldLabel($in.0, "field1")` returns `The first field`.

The function `getFieldLabel($in.0, "field41")` fails with an error.

**See also:**[getFieldIndex](field-access-functions-ctl2.md#getfieldindex), [getFieldName](field-access-functions-ctl2.md#getfieldname), [getFieldType](field-access-functions-ctl2.md#getfieldtype)

#### getFieldName

```ctl
string getFieldName(record argRecord, integer index);
```

The `getFieldName()` function returns the name of the field with the specified index. Fields are numbered starting from 0.
> [!IMPORTANT]
> The `argRecord` may have any of the following forms:
>
> - `$<port number>.*`
>   E.g. `$in.0.*`
> - `$<metadata name>.*`
>   E.g. `$customers.*`
> - `<record variable name>[.*]`
>   E.g. `Customers` or `Customers.*` (both cases, if `Customers` was declared as record in CTL.)
> - `lookup(<lookup table name>).get(<key value>)[.*]`
>   E.g. `lookup(Comp).get("JohnSmith")` or `lookup(Comp).get("JohnSmith").*`
> - `lookup(<lookup table name>).next()[.*]`
>   E.g. `lookup(Comp).next()` or `lookup(Comp).next().*`

If a given record has a `null` reference, the function fails with an error.

**Compatibility**

The `getFieldName(record,integer)` function is available since **CloverETL 3.0.0**.
Example 284. Usage of getFieldName
There is a record having fields `field1` and `field2`.

The function `getFieldName($in.0, 0)` returns `field1`.

The function `getFieldName($in.0, 15)`fails with an error.

**See also:**[getFieldIndex](field-access-functions-ctl2.md#getfieldindex), [getFieldLabel](field-access-functions-ctl2.md#getfieldlabel), [getFieldType](field-access-functions-ctl2.md#getfieldtype)

#### getFieldProperties

```ctl
map[string,string] getFieldProperties(record argRecord, integer index);
map[string,string] getFieldProperties(record argRecord, string fieldName);
```

The `getFieldProperties()` function returns an unmodifiable map of selected properties of the specified data field metadata. Fields are indexed starting from 0.

New properties may be added to the map in future versions.

If a `null` reference is passed to any of the arguments, if the field index is out of range or if the record does not contain a field with the specified name, the function fails with an error.

**Compatibility**

The `getFieldProperties(re)` function is available since **CloverETL 4.1.0-M1**.
Example 285. Usage of getFieldProperties
Assume there is a record with fields `rawValue` of type `string` and `convertedValue` of type `integer` on the first input and first output port.

```ctl
map[string, string] properties = getFieldProperties($out.0, "convertedValue");
// converts $in.0.rawValue to an integer using format and locale from $out.0.convertedValue
$out.0.convertedValue = str2integer($in.0.rawValue, properties["format"], properties["locale"]);
```

**See also:**[getRecordProperties](field-access-functions-ctl2.md#getrecordproperties)

#### getFieldType

```ctl
string getFieldType(record argRecord, integer index);
string getFieldType(record argRecord, string fieldName);
```

The `getFieldType()` function returns the type of a field you specify by its index (i.e. field’s number starting from 0) or name. The returned string is the name of the type (`string`, `integer`, …​), see [Data Types in Metadata](metadata-records-and-fields.md#data-types-in-metadata). Example code:

```ctl
string dataType = getFieldType($in.0, 2);
```

will return the data type of the third field for each incoming record (e.g. `decimal`).
> [!IMPORTANT]
> Records as arguments look like the records for the `getFieldName()` function. See above.

If a given record has a `null` reference, the function fails with an error.

**Compatibility**

The `getFieldType(record,integer)` function is available since **CloverETL 3.0.0**.

The `getFieldType(record,string)` function is available since **CloverETL 4.1**.
Example 286. Usage of getFieldType There is a record having first field of data type `string`. The function `getFieldType($in.0, 0)` returns `string`.
**See also:**[getFieldIndex](field-access-functions-ctl2.md#getfieldindex), [getFieldLabel](field-access-functions-ctl2.md#getfieldlabel), [getFieldName](field-access-functions-ctl2.md#getfieldname)

#### getIntValue

```ctl
integer getIntValue(record record, integer index);
integer getIntValue(record record, string field);
```

The `getIntValue()` function returns the value of an integer field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getIntValue(record,integer)` and `getIntValue(record,string)` functions are available since **CloverETL 3.2.0**.
Example 287. Usage of getIntValue
There is a record having integer fields `field1` and `field2` with values `25` and `22`.

The function `getIntValue($in.0, 1)` returns `22`.

The function `getIntValue($in.0, "field1")` returns `25.`

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setIntValue](field-access-functions-ctl2.md#setintvalue)

#### getLongValue

```ctl
long getLongValue(record record, integer index);
long getLongValue(record record, string field);
```

The `getLongValue()` function returns the value of a long field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getLongValue(record,integer)` and `getLongValue(record,string)` functions are available since **CloverETL 3.2.0**.
Example 288. Usage of getLongValue
There is a record having fields `field1` and `field2` with values `443L` and `509L`.

The function `getLongValue($in.0, 1)` returns `509`.

The function `getLongValue($in.0, "field1")` returns `443`.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setLongValue](field-access-functions-ctl2.md#setlongvalue)

#### getNumValue

```ctl
number getNumValue(record record, integer index);
number getNumValue(record record, string field);
```

The `getNumValue()` function returns the value of a number field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getNumValue(recored,integer)` and `getNumValue(record,string)` functions are available since **CloverETL 3.2.0**.
Example 289. Usage of getNumValue
There is a record having fields `field1` and `field2` with values `1.41` and `1.7`.

The function `getNumValue($in.0, 0)` returns `1.41`.

The function `getNumValue($in.0, "field2")` returns `1.7`.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setNumValue](field-access-functions-ctl2.md#setnumvalue)

#### getRecordProperties

```ctl
map[string,string] getRecordProperties(record argRecord);
```

The `getRecordProperties()` function returns an unmodifiable map of selected properties of the specified record metadata.

New properties may be added to the map in future versions.

If a `null` reference is passed as the argument, the function fails with an error.

**Compatibility**

The `getRecordProperties(record)` function is available since **CloverETL 4.1.0-M1**.
Example 290. Usage of getRecordProperties
Assume there is a record with fields `rawValue` of type `string` on the first input and first output port.

```ctl
map[string, string] properties = getRecordProperties($out.0);
// converts $in.0.rawValue to a date using locale and time zone from $out.0
date convertedValue = str2date($in.0.rawValue, properties["locale"], properties["timeZone"]);
```

**See also:**[getFieldProperties](field-access-functions-ctl2.md#getfieldproperties)

#### getStringValue

```ctl
string getStringValue(record record, integer index);
string getStringValue(record record, string field);
```

The `getStringValue()` function returns the value of a string field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `getStringValue(record, integer)` function is available since **CloverETL 3.2.0**.
Example 291. Usage of getStringValue
There is a record having fields `field1` and `field2` with values `orange` and `yellow`.

The function `getStringValue($in.0, 0)` returns `orange`.

The function `getStringValue($in.0, "field2")` returns `yellow`.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### getValue

```ctl
variant getValue(record record, integer index);
variant getValue(record record, string field);
```

Returns the value of the selected field. The field is identified by its zero-based index (integer) or name (string).

The actual type of the returned value depends on the type of the data field, there is no automatic conversion.

If the record is `null`, the function fails with an error.

**Compatibility**

The function is available since **CloverDX 5.7.0**.
Example 292. Usage of getValue

```ctl
// assumes that the first input port $in.0 has two fields, "field1" and "field2":
variant myVariant1 = getValue($in.0, "field1");
    // returns the value of $in.0.field1
variant myVariant2 = getValue($in.0, 1);
    // returns the value of the 2nd field of $in.0
integer myInt = cast(getValue($in.0, 1), integer);
    // casts the returned value to an integer
```

**See also:**[setValue](field-access-functions-ctl2.md#setvalue), [getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue), [getValueAsString](field-access-functions-ctl2.md#getvalueasstring),

#### getValueAsString

```ctl
string getValueAsString(record record, integer index);
string getValueAsString(record record, string field);
```

The `getValueAsString()` function returns the value of a field (no matter its type) as a common string. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error.

**Compatibility**

The `getValueAsString(record,integer)` and `getValueAsString(record,string)` function is available since **CloverETL 3.2.0**.
Example 293. Usage of getValueAsString
There is a record having fields `field1` and `field2` of `boolean` data type with values `true` and `false`.

The function `getValueAsString($in.0, 0)` returns `true` as string.

The function `getValueAsString($in.0, "field2")` returns `false` as string.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [getByteValue](field-access-functions-ctl2.md#getbytevalue), [getDateValue](field-access-functions-ctl2.md#getdatevalue), [getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [getIntValue](field-access-functions-ctl2.md#getintvalue), [getLongValue](field-access-functions-ctl2.md#getlongvalue), [getNumValue](field-access-functions-ctl2.md#getnumvalue), [getStringValue](field-access-functions-ctl2.md#getstringvalue)

#### isNull

```ctl
boolean isNull(record record, integer index);
boolean isNull(record record, string field);
```

The `isNull()` function checks whether a given field is `null`. The field is identified by its index (integer) or name (string).

**Compatibility**

The `isNull(record,integer)` and `isNull(record,string)` function is available since **CloverETL 3.2.0**.
Example 294. Usage of isNull
There is a record having fields `field1`, `field2`, `field3` and `field4` with values `true`, `false`, `null` and `null`, respectively.

The function `isNull($in.0, 0)` returns `false`.

The function `isNull($in.0, 2)` returns `true`.

The function `isNull($in.0, "field2")` returns `false`.

The function `isNull($in.0, "field4")` returns `true`.

**See also:**[isEmpty(container)](container-functions-ctl2.md#isempty), [isnull](miscellaneous-functions-ctl2.md#isnull)

#### length

```ctl
integer length();
```

The `length()` function returns the number of fields of a record the function is called on.

For a record with `null` reference, the function returns `0`.

**Compatibility**

The `length(record)` function is available since **CloverETL 3.0.0**.
Example 295. Usage of length There is an input record having 14 fields. The function `length($in.0)` returns `14`.
**See also:** String functions: [length(string)](string-functions-ctl2.md#length), Container functions: [length(container)](container-functions-ctl2.md#length)

#### resetRecord

```ctl
void resetRecord(record record);
```

The function `resetRecord()` resets fields of the record to default values.

**Compatibility**

The `resetRecord(record)` function is available since **CloverETL 3.2.2** or earlier.
Example 296. Usage of resetRecord
The output record in the example will contain field `field3` set to `3`. The field `field2` will contain `null`, as the field is reset to the default value.

```ctl
$out.0.field2 = 2;
resetRecord($out.0);
$out.0.field3 = 3;
```

**See also:**[length(record)](field-access-functions-ctl2.md#length)

#### setBoolValue

```ctl
voidsetBoolValue(record record, integer index, boolean value);
voidsetBoolValue(record record, string field, boolean value);
```

The `setBoolValue()` function sets a `boolean` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of the record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setBoolValue(record,integer,boolean)` and `setBoolValue(record,string,boolean)` functions are available since **CloverETL 3.2.0**.
Example 297. Usage of setBoolValue
There is a record of booleans having fields `field1` and `field2`.

The function `setBoolValue($out.0, 0, true)` sets the first field of an output record to `true`.

The function `setBoolValue($out.0, "field2", false)` sets field `field2` of an output record to `false`.

The function `setBoolValue($out.0, "field3456")` fails with an error. The field `field3456` does not exist.

**See also:**[getBoolValue](field-access-functions-ctl2.md#getboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### setByteValue

```ctl
void setByteValue(record record, integer index, byte value);
void setByteValue(record record, string field, byte value);
```

The `setByteValue()` function sets a `byte` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setByteValue(record,integer,byte)`, `setByteValue(record,string,byte)` functions are available since **CloverETL 3.2.0**.
Example 298. Usage of setByteValue
There is a record of booleans having fields `field1` and `field2`.

The function `setByteValue($out.0, 0, str2byte("etc", "utf-8"))` sets the first field to byte value of string `etc` (`0x65`, `0x74`, `0x63`).

The function `setByteValue($out.0, "field2", str2byte("opt"))` sets the second field to byte value of `opt` (`0x6f`, `0x70`, `0x74`).

**See also:**[getByteValue](field-access-functions-ctl2.md#getbytevalue), [hex2byte](conversion-functions-ctl2.md#hex2byte), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue), [str2byte](conversion-functions-ctl2.md#str2byte)

#### setDateValue

```ctl
voidsetDateValue(record record, integer index, date value);
voidsetDateValue(record record, string field, date value);
```

The `setDateValue()` function sets a `date` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setDateValue(record,integer,date)` and `setDateValue(record,string,date)` functions are available since **CloverETL 3.2.0**.
Example 299. Usage of setDateValue
The function `setDateValue($out.0, 0, '2010-10-10')` sets the first field of an output record to `2010-10-10`.

the function `setDateValue($out.0, "field", '2011-11-11')`

**See also:**[getDateValue](field-access-functions-ctl2.md#getdatevalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### setDecimalValue

```ctl
void setDecimalValue(record record, integer index, decimal value);
void setDecimalValue(record record, string field, decimal value);
```

The `setDecimalValue()` function sets a `decimal` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of a record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setDecimalValue(record,integer,decimal)` and `setDecimalValue(record,string,decimal)` functions are available since **CloverETL 3.2.0**.
Example 300. Usage of seDecimalValue
The function `setDecimalValue($out.0, 0, 3.14D)` sets the first field of an output record to `3.14`.

The function `setDecimalValue($out.0, "field3", 2.72D)` sets the first field of an output record to `2.72D`

**See also:**[getDecimalValue](field-access-functions-ctl2.md#getdecimalvalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### setIntValue

```ctl
void setIntValue(record record, integer index, integer value);
void setIntValue(record record, string field, integer value);
```

The `setIntValue()` function sets an `integer` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of a record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setIntValue(record,integer,integer)` and `setIntValue(record,string,integer)` functions are available since **CloverETL 3.2.0**.
Example 301. Usage of setIntValue
The function `setIntValue($out.0, 1, 2718)` sets the second field of an output record to `2718`.

The function `setIntValue($out.0, "field1", 1414)` sets the field `field1` of an output record to `1414`.

**See also:**[getIntValue](field-access-functions-ctl2.md#getintvalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### setLongValue

```ctl
void setLongValue(record record, integer index, long value);
void setLongValue(record record, string field, long value);
```

The `setLongValue()` function sets a `long` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setLongValue(record,integer,long)` and `setLongValue(record,string,long)` functions are available since **CloverETL 3.2.0**.
Example 302. Usage of setLongValue
The function `setLongValue($out.0, 0, 8080L)` sets the first field of a record to `8080`.

The function `setLongValue($out.0, "field3", 127L)` sets the field `field3` of an output record to `127`.

**See also:**[getLongValue](field-access-functions-ctl2.md#getlongvalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### setNumValue

```ctl
void setNumValue(record record, integer index, number value);
void setNumValue(record record, string field, number value);
```

The `setNumValue()` function sets a `number` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of a record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setNumValue(record,integer,number)` and `setNumValue(record,string,number)` functions are available since **CloverETL 3.2.0**.
Example 303. Usage of setNumValue
The function `setNumValue($out.0, 2, 2.718)` sets the third field of an output record to `2.718`.

The function `setNumValue($out.0, "field1", 1.732)` sets the field `field3` of an output record to `1.732`.

**See also:**[getNumValue](field-access-functions-ctl2.md#getnumvalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)

#### setStringValue

```ctl
void setStringValue(record record, integer index, string value);
void setStringValue(record record, string field, string value);
```

The `setStringValue()` function sets a `string` value to a field. The field is identified by its index (integer) or name (string).

If a given record has a `null` reference, the function fails with an error. If the accessed field of a record has a different data type and is not a variant data type, the function fails with an error.

**Compatibility**

The `setStringValue(record,integer,string)` and `setStringValue(record,string,string)` functions are available since **CloverETL 3.2.0**.
Example 304. Usage of setStringValue
The function `setStringValue($out.0, 1, "chocolate cake")` sets the second field of an output record to `chocolate cake`.

The function `setStringValue($out.0, "field1", "donut")` sets the second field `donut` of an output record to `donut`.

**See also:**[getStringValue](field-access-functions-ctl2.md#getstringvalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue)

#### setValue

```ctl
void setValue(record record, integer index, variant value);
void setValue(record record, string field, variant value);
```

Sets a value to a field. The field is identified by its zero-based index (integer) or name (string).

If the field has an incompatible data type, the function fails with a runtime error.

If the given record is `null`, the function fails with an error.

**Compatibility**

The function is available since **CloverDX 5.7.0**.
Example 305. Usage of setValue

```ctl
// assumes that the first output port $out.0 has three fields and one of them is "Name":
$out.0.setValue(5, 90);
    // sets field with index 5 of output record $out.0 to 90
$out.0.setValue("Name", "Zac");
    // sets the field $out.0.Name to "Zac"
```

**See also:**[getValue](field-access-functions-ctl2.md#getvalue), [setBoolValue](field-access-functions-ctl2.md#setboolvalue), [setByteValue](field-access-functions-ctl2.md#setbytevalue), [setDateValue](field-access-functions-ctl2.md#setdatevalue), [setDecimalValue](field-access-functions-ctl2.md#setdecimalvalue), [setIntValue](field-access-functions-ctl2.md#setintvalue), [setLongValue](field-access-functions-ctl2.md#setlongvalue), [setNumValue](field-access-functions-ctl2.md#setnumvalue), [setStringValue](field-access-functions-ctl2.md#setstringvalue)
