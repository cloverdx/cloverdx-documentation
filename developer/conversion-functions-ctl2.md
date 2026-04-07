<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Conversion functions -->

### Conversion functions

#### List of functions

| [base64byte](conversion-functions-ctl2.md#base64byte) |
| --- |
| [bits2str](conversion-functions-ctl2.md#bits2str) |
| [bool2num](conversion-functions-ctl2.md#bool2num) |
| [byte2base64](conversion-functions-ctl2.md#byte2base64) |
| [byte2hex](conversion-functions-ctl2.md#byte2hex) |
| [byte2str](conversion-functions-ctl2.md#byte2str) |
| [date2long](conversion-functions-ctl2.md#date2long) |
| [date2num](conversion-functions-ctl2.md#date2num) |
| [date2str](conversion-functions-ctl2.md#date2str) |
| [decimal2double](conversion-functions-ctl2.md#decimal2double) |
| [decimal2integer](conversion-functions-ctl2.md#decimal2integer) |
| [decimal2long](conversion-functions-ctl2.md#decimal2long) |
| [double2integer](conversion-functions-ctl2.md#double2integer) |
| [double2long](conversion-functions-ctl2.md#double2long) |
| [getAvroSchema](conversion-functions-ctl2.md#getavroschema) |
| [hex2byte](conversion-functions-ctl2.md#hex2byte) |
| [json2xml](conversion-functions-ctl2.md#json2xml) |
| [long2date](conversion-functions-ctl2.md#long2date) |
| [long2integer](conversion-functions-ctl2.md#long2integer) |
| [long2packDecimal](conversion-functions-ctl2.md#long2packdecimal) |
| [md5](conversion-functions-ctl2.md#md5) |
| [md5HexString](conversion-functions-ctl2.md#md5hexstring) |
| [num2bool](conversion-functions-ctl2.md#num2bool) |
| [num2str](conversion-functions-ctl2.md#num2str) |
| [packDecimal2long](conversion-functions-ctl2.md#packdecimal2long) |
| [parseAvro](conversion-functions-ctl2.md#parseavro) |
| [parseBson](conversion-functions-ctl2.md#parsebson) |
| [parseJson](conversion-functions-ctl2.md#parsejson) |
| [record2map](conversion-functions-ctl2.md#record2map) |
| [sha1](conversion-functions-ctl2.md#sha1) |
| [sha1HexString](conversion-functions-ctl2.md#sha1hexstring) |
| [sha256](conversion-functions-ctl2.md#sha256) |
| [sha256HexString](conversion-functions-ctl2.md#sha256hexstring) |
| [str2bits](conversion-functions-ctl2.md#str2bits) |
| [str2bool](conversion-functions-ctl2.md#str2bool) |
| [str2byte](conversion-functions-ctl2.md#str2byte) |
| [str2date](conversion-functions-ctl2.md#str2date) |
| [str2decimal](conversion-functions-ctl2.md#str2decimal) |
| [str2double](conversion-functions-ctl2.md#str2double) |
| [str2integer](conversion-functions-ctl2.md#str2integer) |
| [str2long](conversion-functions-ctl2.md#str2long) |
| [str2timeUnit](conversion-functions-ctl2.md#str2timeunit) |
| [toString](conversion-functions-ctl2.md#tostring) |
| [writeAvro](conversion-functions-ctl2.md#writeavro) |
| [writeBson](conversion-functions-ctl2.md#writebson) |
| [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson) |
| [writeJson](conversion-functions-ctl2.md#writejson) |
| [xml2json](conversion-functions-ctl2.md#xml2json) |

Sometimes you need to convert values from one data type to another.

In the functions that convert one data type to another, sometimes a format pattern of a date or any number must be defined. Also locale and time zone can have an influence on their formatting.

- For detailed information about date formatting and/or parsing, see [Date and time format](metadata-records-and-fields.md#date-and-time-format).
- For detailed information about formatting and/or parsing of any numeric data type, see [Numeric format](metadata-records-and-fields.md#numeric-format).
- For detailed information about locale, see [Locale](metadata-records-and-fields.md#locale).
- For detailed information about Time zones, see [Time zone](metadata-records-and-fields.md#timezone).
> [!NOTE]
> Remember that numeric and date formats are displayed using system value **Locale** or **Locale** specified in the `defaultProperties` file, unless other **Locale** is explicitly specified. Similarly for **Time zone**.
>
> For more information on how **Locale** and **Time zone** may be changed in the `defaultProperties`, see [Engine configuration](../admin/designer-configuration.md#engine-configuration).

Here we provide the list of these functions:

#### base64byte

```ctl
byte base64byte(string input);
```

The `base64byte()` function converts the `input` string in `base64` representation to an array of bytes.

Its counterpart is the function [byte2base64](conversion-functions-ctl2.md#byte2base64).

If the `input` is `null`, the function returns `null`.

**Compatibility**

The `base64byte(string)` function is available since **CloverETL 3.0.0**.
Example 56. Usage of base64byte The function `base64byte("YWJj")` returns `abc`.
**See also:**[byte2base64](conversion-functions-ctl2.md#byte2base64)

#### bits2str

```ctl
string bits2str(byte input);
```

The `bits2str()` function converts an array of bytes to a string consisting of two characters: `"0"` or `"1"`.

Each byte is represented by eight characters ("0" or "1"). For each byte, the lowest bit is at the beginning of these eight characters. The counterpart is the function [str2bits](conversion-functions-ctl2.md#str2bits).

If the `input` is `null`, the function returns `null`.

**Compatibility**

The `bits2str(byte)` function is available since **CloverETL 3.0.0**.
Example 57. Usage of bits2str The function `bits2str(str2byte("ab"))` returns `1000011001000110`. Let’s display the result for better legibility as `1000 0110 0100 0110`. The first eight bits are taken from `a` (code `0x61`) and following bits are taken from `b` (code `0x62`).
**See also:**[str2bits](conversion-functions-ctl2.md#str2bits)

#### bool2num

```ctl
integer bool2num(boolean input);
```

The `bool2num()` function converts the boolean `input` to either integer `1` (if the argument is `true`) or integer `0` (if the argument is `false`).

If the `input` is `null`, the function returns `null`.

**Compatibility**

The `bool2num(boolean)` function is available since **CloverETL 3.0.0**.
Example 58. Usage of bool2num
The function `bool2num(true)` returns `1`.

The function `bool2num(false)` returns `0`.

**See also:**[num2bool](conversion-functions-ctl2.md#num2bool)

#### byte2base64

```ctl
string byte2base64(byte input);
string byte2base64(byte input, boolean wrap);
```

The `byte2base64()` function converts an array of bytes to a string in `base64` representation.

The function with one input parameter wraps the encoded lines after 76 characters. The ability of the function with 2 parameters to wrap lines is affected by the second parameter. If the `wrap` parameter is set to `true`, the encoded lines are wrapped after 76 characters.

If the `input` byte array is `null`, the function returns `null`.

**Compatibility**

The `byte2base64(byte)` function is available since **CloverETL 3.0.0**.

The `byte2base64(byte,boolean)` function is available since **CloverETL 3.5.0-M2**.
Example 59. Usage of byte2base64 The function `byte2base64(str2byte("abc", "utf-8"))` returns `YWJj`. The function `str2byte` used in the example is needed for conversion of `abc` from string to bytes as the function `byte2base64` needs to have bytes as an argument.
**See also:**[base64byte](conversion-functions-ctl2.md#base64byte), [byte2hex](conversion-functions-ctl2.md#byte2hex), [byte2str](conversion-functions-ctl2.md#byte2str)

#### byte2hex

```ctl
string byte2hex(byte input);
string byte2hex(byte input, string escapeChars);
```

The `byte2hex()` function converts an array of bytes to a string in `hexadecimal` representation.

If the `input` is `null`, the function returns `null`.

The `escapeChars` are prepended before hexadecimal characters of each byte. If the `escapeChars` is `null`, empty string, or the function has only one argument, nothing is escaped.

**Compatibility**

The `byte2hex(input)` function is available since **CloverETL 3.0.0**.

The `byte2hex(input,escapeChars)` function is available since **CloverETL 4.4.1**.
Example 60. Usage of byte2hex
The function `byte2hex(str2byte("abc", "utf-8"))` returns `616263`.

The function `byte2hex(str2byte("abc", "utf-8"),null)` returns `616263`.

The function `byte2hex(str2byte("abc", "utf-8"),"")` returns `616263`.

The function `byte2hex(str2byte("abc", "utf-8"),"\\")` returns `\61\62\63`.

The function `byte2hex(str2byte("abc", "utf-8"),"hello")` returns `hello61hello62hello63`.

**See also:**[byte2base64](conversion-functions-ctl2.md#byte2base64), [byte2str](conversion-functions-ctl2.md#byte2str), [hex2byte](conversion-functions-ctl2.md#hex2byte)

#### byte2str

```ctl
string byte2str(byte payload, string charset);
```

The `byte2str()` function converts an array of bytes to a string using given charset.

If the `charset` is `null`, the function fails with an error. If the `payload` is null, the function returns `null`.

**Compatibility**

The `byte2str(byte,string)` is available since **CloverETL 3.2.x**.
Example 61. Usage of byte2str The function `byte2str(hex2byte("616263"), "utf-8")` returns string `abc`.
**See also:**[byte2base64](conversion-functions-ctl2.md#byte2base64), [byte2hex](conversion-functions-ctl2.md#byte2hex), [str2byte](conversion-functions-ctl2.md#str2byte)

#### date2long

```ctl
long date2long(date input);
```

The `date2long()` function converts a date argument to the long data type.

The return value is the number of milliseconds elapsed from `January 1, 1970, 00:00:00 GMT` to the date specified as the argument.

If the `input` is `null`, the function returns `null`.

**Compatibility**

The `date2long(date)` function is available since **CloverETL 3.0.0**.
Example 62. Usage of date2long The function `date2long(str2date("2009-02-13 23:31:30", "yyyy-MM-dd HH:mm:ss", "en.GB", "GMT+0"))` returns `1234567890000`.
**See also:**[date2num](conversion-functions-ctl2.md#date2num), [date2str](conversion-functions-ctl2.md#date2str), [long2date](conversion-functions-ctl2.md#long2date)

#### date2num

```ctl
integer date2num(date input, unit timeunit);
integer date2num(date input, unit timeunit, string locale);
```

The `date2num()` returns the number of specified time units from the date using system or specified locale.

The `date` parameter is a date to be converted. If the `input` date is `null`, the function returns `null`.

The unit of field `timeunit` can be one of the following: `year`, `month`, `week`, `day`, `hour`, `minute`, `second` or `millisec`. The unit must be specified as a constant. It can neither be received through an edge nor set as a variable.

If the function takes two arguments, it returns an integer using the system locale. If the parameter `locale` is used, the function uses the locale from the `locale` parameter instead of the system locale.

If the time unit is contained in the date, it is returned as an integer number. If it is not contained, the function returns `0`.
> [!IMPORTANT]
> Remember that months are numbered starting from `1` unlike in CTL1.

The default time zone is used in the conversion.

**Compatibility**

The `date2num(date,unit)` and `date2num(ate,unit,string)` functions are available since **CloverETL 3.0.x**.
Example 63. Usage of date2num
The function `date2num(2008-06-12, month)` returns `6`.

The function `date2num(2008-06-12, hour)` returns `0`.

The function `date2num(long2date(1234567890000L), year, "en.US")` returns `2009`.

The function `date2num(long2date(1234567890000L), year, "th.TH")` returns `2552`.

**See also:**[date2long](conversion-functions-ctl2.md#date2long), [date2str](conversion-functions-ctl2.md#date2str), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond)

#### date2str

```ctl
string date2str(date input, string pattern);
string date2str(date input, string pattern, string locale);
string date2str(date input, string pattern, string locale, string timeZone);
```

The `date2str()` function converts the `input` date to the string data type according to the specified [`pattern`](metadata-records-and-fields.md#date-and-time-format), [`locale`](metadata-records-and-fields.md#locale) and target [`timeZone`](metadata-records-and-fields.md#timezone).

The `input` contains date to be converted to the string. If the `input` date is `null`, the function returns `null`.

The `pattern` describes date and time format. If the `pattern` is `null`, [default value](../admin/designer-configuration.md#default-date-format) is used.

The `locale` parameter defines what date format symbols should be used. If the `locale` is `null`, an empty string, or the function does not have the `locale` parameter, the respective [default value](metadata-records-and-fields.md#locale) is used.

If the `timeZone` parameter is `null`, an empty string, or the function does not have the `locale` parameter, the [default time zone value](metadata-records-and-fields.md#timezone) is used.

**Compatibility**

The `date2str(date,string)` function is available since **CloverETL 3.0.0**.

The `date2str(date,string,string)` function is available since **CloverETL 3.0.1**.

The `date2str(date,string,string,string)` function is available since **CloverETL 3.5.0-M1**.
Example 64. Usage of date2str
The function `date2str(2008-06-12, "dd.MM.yyyy")` returns the following string: `"12.6.2008"`.

The function `date2str(2009-01-04, "yyyy-MMM-d", "fr.CA")` returns `2009-janv.-4`.

The function `date2str(2009-01-04 12:38:06, "yyyy-MMM-d HH:mm:ss z", "fr.CA", "GMT-5")` returns `"2009-janv.-4 06:38:06 GMT-05:00"` (assuming that the default time zone is GMT+1).

**See also:**[date2long](conversion-functions-ctl2.md#date2long), [date2num](conversion-functions-ctl2.md#date2num), [str2date](conversion-functions-ctl2.md#str2date), [getYear](date-functions-ctl2.md#getyear), [getMonth](date-functions-ctl2.md#getmonth), [getDay](date-functions-ctl2.md#getday), [getHour](date-functions-ctl2.md#gethour), [getMinute](date-functions-ctl2.md#getminute), [getSecond](date-functions-ctl2.md#getsecond), [getMillisecond](date-functions-ctl2.md#getmillisecond)

#### decimal2double

```ctl
number decimal2double(decimal arg);
```

The `decimal2double()` function converts a decimal argument to a double value.

The conversion is narrowing, and if the `decimal` value cannot be converted into `double` (as the range of the `double` data type does not cover all `decimal` values), the function fails with an error.

On the other hand, any `double` can be converted into `decimal`. Both **Length** and **Scale** of a decimal can be adjusted for it.

If the input is `null`, the function returns `null`.

**Compatibility**

The `decimal2double(decimal)` function is available since **CloverETL 3.0.0**.
Example 65. Usage of decimal2double
The function `decimal2double(9007199254740991D)` returns `9.007199254740991E15`. The input decimal number fit into double precisely.

The function `decimal2double(92378352147483647.23D)` returns `9.2378352147483648E16`.

The function `decimal2double(9007199254740993D)` returns `9.007199254740992E15`. The input number is too big to fit into the `double` data type precisely. Narrowing conversion is used and input decimal number is rounded.

**See also:**[decimal2integer](conversion-functions-ctl2.md#decimal2integer), [decimal2long](conversion-functions-ctl2.md#decimal2long), [round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### decimal2integer

```ctl
integer decimal2integer(decimal arg);
```

The `decimal2integer()` function converts a decimal argument to an integer.

The conversion is narrowing, and if the `decimal` value cannot be converted into `integer` (as the range of the `integer` data type does not cover the range of `decimal` values), the function fails with an error.

On the other hand, any `integer` can be converted into `decimal` without a loss of precision. **Length** of `decimal` can be adjusted for it.

If the input is `null`, the function returns `null`.
> [!NOTE]
> There is no function `decimal2integer(double)`. You can use `double` parameter of the function due to implicit conversion of double to decimal. If you need conversion from `double` to `integer`, use the function [double2integer](conversion-functions-ctl2.md#double2integer).

**Compatibility**

The `decimal2integer(decimal)` function is available since **CloverETL 3.0.0**.
Example 66. Usage of decimal2integer
The function `decimal2integer(352147483647.23D)` fails with an error as the input decimal number is out of range of the integer data type.

The function `decimal2integer(25.95D)` returns `25`.

The function `decimal2integer(-123.45D)` returns `-123`.

**See also:**[decimal2double](conversion-functions-ctl2.md#decimal2double), [decimal2long](conversion-functions-ctl2.md#decimal2long), [round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### decimal2long

```ctl
long decimal2long(decimal arg);
```

The `decimal2long()` function converts a decimal argument to a long value.

The conversion is narrowing, and if the `decimal` value cannot be converted into `long` (as the range of `long` data type does not cover all `decimal` values), the function fails with an error.

On the other hand, any `long` can be converted into `decimal` without loss of precision. **Length** of a `decimal` can be adjusted for it.

If the input is `null`, the function returns `null`.
> [!NOTE]
> There is no function `decimal2long(double)`. You can use `double` parameter of the function due to implicit conversion of double to decimal. If you need conversion from `double` to `long`, use the function [double2long](conversion-functions-ctl2.md#double2long).

**Compatibility**

The `decimal2long(decimal)` function is available since **CloverETL 3.0.0**.
Example 67. Usage of decimal2long
The function `decimal2long(9759223372036854775807.25D)` fails with an error as the input decimal number is out of range of data type `long`.

The function `decimal2long(72036854775807.79D)` returns `72036854775807`.

**See also:**[decimal2double](conversion-functions-ctl2.md#decimal2double), [decimal2integer](conversion-functions-ctl2.md#decimal2integer), [round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### double2integer

```ctl
integer double2integer(number arg);
```

The `double2integer()` function converts a number argument to an integer.

The conversion is narrowing and if a `double` value cannot be converted into `integer` (as the range of `double` data type does not cover all `integer` values), the function fails with an error.

On the other hand, any `integer` can be converted into `double` without loss of precision.

If the input is `null`, the function returns `null`.

**Compatibility**

The `double2integer(double)` function is available since **CloverETL 3.0.0**.
Example 68. Usage of double2integer
The function `double2integer(352147483647.1)` fails with an error as the input does not fit into integer data type.

The function `double2integer(25.757197)` returns `25`.

**See also:**[round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### double2long

```ctl
long double2long(number arg);
```

The `double2long()` function converts a number argument to `long`.

The conversion is narrowing, and if a `double` value cannot be converted into `long` (as the range of `double` data type does not cover all `long` values), the function fails with an error.

On the other hand, any `long` can always be converted into `double`; however, the user should take into account that a loss of precision may occur.

If the input argument is `null`, the function returns `null`.

**Compatibility**

The `double2long(double)` function is available since **CloverETL 3.0.0**.
Example 69. Usage of double2long
The function `double2long(1.3759739E23)` fails with an error.

The function `double2long(25.8579)` returns `25`.

**See also:**[double2integer](conversion-functions-ctl2.md#double2integer), [round](mathematical-functions-ctl2.md#round), [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

#### getAvroSchema

```ctl
string getAvroSchema(variant object);
```

Converts variant data type to Avro schema. Resulted string contains JSON representation of Avro schema.

This function should be used for one-time operations only. Using it together with [parseAvro](conversion-functions-ctl2.md#parseavro) or [writeAvro](conversion-functions-ctl2.md#writeavro) to generate schema for each processed record would reduce performance.

| CTL | Avro | Note |
| --- | --- | --- |
| null value | null type | null value is considered to be different type than any instance |
| boolean | boolean |  |
| byte, cbyte | bytes |  |
| date | long, logicalType: timestamp-millis |  |
| decimal | bytes, logicalType: decimal | precision: 32, scale: 16 |
| integer | int |  |
| long | long |  |
| number | double |  |
| string | string |  |
| list[type1] | array of type1 | items are of the same type type1 |
| list[type1, type2, …​] | array of union of type1, type2, …​ | items are of different types (like null, string, map, …​) |
| map{string → type1} | map(string) of type1 | keys are of type string; values are of the same type as type1 |
| map{string → type1, type2, …​} | record | keys are of type string, keys become field names; values are of different types (like null, integer, string, list, map, …​) |
| map{noString → type1} | map (string) of type1 | keys become strings; values are of the same type type1 |
| map{noString → type1, type2, …​} | map (string) of union of type1, type2, …​ | keys become strings; values are of different types (like null, string, map, …​) |

**See also:**[parseAvro](conversion-functions-ctl2.md#parseavro), [writeAvro](conversion-functions-ctl2.md#writeavro)

#### hex2byte

```ctl
byte hex2byte(string arg);
```

The `hex2byte()` function converts a string argument in `hexadecimal` representation to an array of bytes. Its counterpart is the [byte2hex](conversion-functions-ctl2.md#byte2hex) function.

If the input is `null`, the function returns `null`.

**Compatibility**

The `hex2byte(string)` function is available since **CloverETL 3.0.0**.
Example 70. Usage of hex2byte The function `hex2byte("616263")` returns bytes `0x61`, `0x62`, `0x63`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [str2byte](conversion-functions-ctl2.md#str2byte)

#### json2xml

```ctl
string json2xml(string arg);
```

The `json2xml()` function takes one string argument that is `JSON` formatted and converts it to an `XML` formatted string. Its counterpart is the function [xml2json](conversion-functions-ctl2.md#xml2json).

Parsing of an input does not have to result in a valid `XML` structure. For example, if the root element of input JSON contained array, the XML document with more than one root element would be created.

If the input is an invalid JSON formatted string or `null`, the function fails with an error.

**Compatibility**

The `json2xml(string)` function is available since **CloverETL 3.1.0**.
Example 71. Usage of json2xml The function `json2xml('{ "element1" : { "id" : "0", "date" : "2011-11-07" }, "element0" : { "id" : "1", "date" : "2012-10-12" }}')` returns `<element0><id>1</id><date>2012-10-12</date></element0><element1><id>0</id><date>2011-11-07</date></element1>`.
**See also:**[xml2json](conversion-functions-ctl2.md#xml2json)

#### long2date

```ctl
date long2date(long arg);
```

The `long2date()` function converts a long argument to a date.

It adds the argument number of milliseconds to `January 1, 1970, 00:00:00 GMT` and returns the result as a date. Its counterpart is function [date2long](conversion-functions-ctl2.md#date2long).

If the input is `null`, the function returns `null`.

**Compatibility**

The `long2date(long)` function is available since **CloverETL 3.0.0**.
Example 72. Usage of long2date The function `long2date(1234567890000L)` returns `2013-02-13 23:31:30`.
**See also:**[date2long](conversion-functions-ctl2.md#date2long)

#### long2integer

```ctl
integer long2integer(long arg);
```

The `long2integer()` function converts a long argument to an integer value.

The conversion is successful only if it is possible without any loss of information, otherwise the function fails with an error.

On the other hand, any `integer` value can be converted into a `long` number without a loss of precision.

If the input is `null`, the function returns `null`.

**Compatibility**

The `long2integer(long)` function is available since **CloverETL 3.0.0**.
Example 73. Usage of long2integer
The function `long2integer(352147483647L)` fails with an error.

The function `long2integer(25)` returns `25`.

#### long2packDecimal

```ctl
byte long2packDecimal(long arg);
```

The `long2packDecimal()` function converts a long data type argument to the representation of packed decimal number. It is the counterpart of the function [packDecimal2long](conversion-functions-ctl2.md#packdecimal2long).

If the input is `null`, the function returns `null`.

**Compatibility**

The `long2packDecimal(long)` function is available since **CloverETL 3.0.0**.
Example 74. Usage of long2packDecimal The function `long2packDecimal(256L)` returns bytes `%l`. The result can be seen as `256C` using hexadecimal notation.
**See also:**[packDecimal2long](conversion-functions-ctl2.md#packdecimal2long)

#### md5

```ctl
byte md5(byte arg);
byte md5(string arg);
```

The `md5()` function calculates an `MD5` hash value of the argument.

If the input is `null`, the function fails with an error.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of byte manually using the function [str2byte](conversion-functions-ctl2.md#str2byte) to the bytes and than use the function `md5`.

**Compatibility**

The `md5(byte)` and `md5(string)` functions are available since **CloverETL 3.0.0**.
Example 75. Usage of md5 Use `byte2hex()` to convert `MD5` hash from a byte array to a usual string representation of 32 hexadecimal digits. For example, `byte2hex(md5sum("abcd"))` returns `e2fc714c4727ee9395f324cd2e7f331f`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [sha1](conversion-functions-ctl2.md#sha1), [sha256](conversion-functions-ctl2.md#sha256), [str2byte](conversion-functions-ctl2.md#str2byte)

#### md5HexString

```ctl
string md5HexString(byte arg);
string md5HexString(string arg);
```

The `md5HexString()` function calculates an `MD5` hash value of the argument. Return value is converted to a hexadecimal string.

If the input is `null`, the function returns `null`.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of byte manually using the function [str2byte](conversion-functions-ctl2.md#str2byte) to the bytes and than use the function `md5`.

**Compatibility**

The `md5HexString(byte)` and `md5HexString(string)` functions are available since **CloverETL 6.4.0**.
Example 76. Usage of md5HexString`md5HexString("abcd")` returns `e2fc714c4727ee9395f324cd2e7f331f`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [sha1HexString](conversion-functions-ctl2.md#sha1hexstring), [sha256HexString](conversion-functions-ctl2.md#sha256hexstring), [str2byte](conversion-functions-ctl2.md#str2byte)

#### num2bool

```ctl
boolean num2bool(<numeric type> arg);
```

The `num2bool()` function converts a numeric type to boolean.

The function takes one argument of any numeric data type (`integer`, `long`, `number` or `decimal`) and returns boolean `false` for 0 and `true` for any other value.

If the input is `null`, the function returns `null`.

**Compatibility**

The `num2bool(integer)`, `num2bool(long)`, `num2bool(double)` and `num2bool(decimal)` functions are available since **CloverETL 3.0.0**.
Example 77. Usage of num2bool
The function `num2bool(0)` returns `false`.

The function `num2bool(3.1)` returns `true`.

**See also:**[bool2num](conversion-functions-ctl2.md#bool2num)

#### num2str

```ctl
string num2str(<numeric type> arg);
string num2str(integer | long | double arg, integer radix);
string num2str(<numeric type> arg, string format);
string num2str(<numeric type> arg, string format, string locale);
```

The `num2str()` converts any numeric type to the string decimal representation.

The function takes one argument of any numeric data type (`integer`, `long`, `number`, or `decimal`) and converts it to a string in decimal representation.

If the input is `null`, the function returns `null`.

The `radix` enables to convert the input number to a different radix-based numerical system, e.g. to the octal numerical system. For both `integer` and `long` data types, any integer number can be used as radix. For the data type double (`number`) only 10 or 16 can be used as radix.

The `format` describes format of number. If the parameter is missing, the [numeric format](metadata-records-and-fields.md#numeric-format) is used.

If the `locale` parameter is missing, the locale has system value.

**Compatibility**

The `num2str(integer)`, `num2str(long)`, `num2str(number)`, `num2str(decimal)`, `num2str(integer,integer)`, `num2str(long,integer)`, `num2str(number,integer)`, `num2str(integer,string)`, `num2str(long,string)`, `num2str(double,string)`, `num2str(decimal,string)`, `num2str(integer,string,string)`, `num2str(long,string,string)`, `num2str(double,string,string)` and `num2str(decimal,string,string)` functions are available since **CloverETL 3.0.0**.
Example 78. Usage of num2str
The function `num2str(123456)` returns `123456`.

The function `num2str(123456L)` returns `123456`.

The function `num2str(123456.45)` returns `123456.45`.

The function `num2str(123456.67D)` returns `123456.67`

The function `num2str(123, 8)` returns `173`.

The function `num2str(123L, 8)` returns `173`

The function `num2str(123.75, 8)` fails. Double as first argument works with base = 10 and base = 16 only.

The function `num2str(4.0, 16)` returns `0x1.0p2`.

The function `num2str(123456, "###,###")` returns `123,456`.

The function `num2str(123456L, "###,###")` returns `123,456`.

The function `num2str(123456.25, "###,###.#")` returns `123,456.2`.

The function `num2str(123456.75D "###,###.##")` returns `123,456.75`.

The function `num2str(123456, "###,###", "fr.FR")` returns `123 456`.

The function `num2str(123456L, "###,###", "fr.FR")` returns `123 456`.

The function `num2str(123456.75, "###,###.##", "fr.FR")` returns `123 456,75`.

The function `num2str(123456.25D, "###,###.##", "fr.FR")` returns `123 456,25`.

**See also:**[str2double](conversion-functions-ctl2.md#str2double), [toString](conversion-functions-ctl2.md#tostring)

#### packDecimal2long

```ctl
long packDecimal2long(byte arg);
```

The `packDecimal2long()` function converts an array of bytes whose meaning is the packed decimal representation of a long number to a long number.

If the input is `null`, the function returns `null`.

**Compatibility**

The `packDecimal2long(byte)` function is available since **CloverETL 3.0.0**.
Example 79. Usage of packDecimal2long The function `packDecimal2long(hex2byte("256C12"))` returns `256`.
**See also:**[long2packDecimal](conversion-functions-ctl2.md#long2packdecimal)

#### parseAvro

```ctl
variant parseAvro(byte avroData, string schema);
```

Converts bytes containing Avro data serialized with the [Binary encoding](https://avro.apache.org/docs/current/spec.html#binary_encoding) to a variant using the specified Avro schema in JSON. Avro data have to match Avro schema supplemented as the second parameter. The Avro data bytes are not regular Avro file, but the data only without Avro schema. The Avro data can be received for example from a messaging system (JMS) or events streaming system (Kafka).

If the data input is `null`, the function returns `null`.

If the Avro schema is `null`, the function fails with an error.

Its counterpart is the function [writeAvro](conversion-functions-ctl2.md#writeavro).

| Avro type | Avro logical type | Resulted CTL type | Note |
| --- | --- | --- | --- |
| null type |  | null value |  |
| boolean |  | boolean |  |
| int |  | integer |  |
| int | date | date | system timezone is used for conversion to Clover date |
| int | time-millis | date | system timezone is used for conversion to Clover date |
| long |  | long |  |
| long | time-micros | date | system timezone is used for conversion to Clover date; micros are truncated |
| long | timestamp-millis | date |  |
| long | timestamp-micros | date | micros are truncated |
| long | local-timestamp-millis | date | system timezone is used for conversion to Clover date |
| long | local-timestamp-micros | date | system timezone is used for conversion to Clover date; micros are truncated |
| float |  | number |  |
| double |  | number |  |
| bytes |  | byte |  |
| bytes | decimal | decimal |  |
| string |  | string |  |
| string | uuid | string |  |
| record |  | map {string → any} | keys match field names; apply this table to the value types |
| enum |  | string |  |
| array |  | list | apply this table to the items type |
| map |  | map | apply this table to the values type |
| union |  | types from union | apply this table to the union types |
| fixed |  | byte |  |
| fixed | decimal | decimal |  |
| fixed | duration |  | not supported |

**See also:**[writeAvro](conversion-functions-ctl2.md#writeavro), [getAvroSchema](conversion-functions-ctl2.md#getavroschema)

#### parseBson

```ctl
variant parseBson(byte bson);
```

Converts bytes containing [BSON](http://bsonspec.org) serialized data to a tree data structure composed of CTL lists and maps. Note that the return type is always variant, regardless of the actual returned value.

If the input is `null`, the function returns `null`.

Its counterpart is the function [writeBson](conversion-functions-ctl2.md#writebson). The function can also read data written by [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson).

**Compatibility**

Available since **CloverDX 5.6.0**.
Example 80. Usage of parseBson

```ctl
// simulates data from an input port, $in.0.bson
byte bson = hex2byte("30000000106e756d62657200" +
                     "0100000008626f6f6c65616e" +
                     "000102737472696e67000900" +
                     "0000436c6f76657244580000");
// returns map as variant {"number" -> 1, "boolean" -> true, "string" -> "CloverDX"}
variant v = parseBson(bson);
```

**See also:**[writeBson](conversion-functions-ctl2.md#writebson), [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson)

#### parseJson

```ctl
variant parseJson(string json);
```

Converts a [JSON](https://www.json.org) formatted string to a tree data structure composed of CTL lists and maps. Note that the return type is always variant, regardless of the actual returned value.

If the input is `null`, the function returns `null`.

Its counterpart is the function [writeJson](conversion-functions-ctl2.md#writejson).

**Compatibility**

Available since **CloverDX 5.6.0**.
Example 81. Usage of parseJson

```ctl
variant var;

// returns the map { "a" -> 1, "b" -> true, "c" -> "d" }
var = parseJson('{ "number" : 1.1, "boolean" : true, "string" : "CloverDX" }');

// returns the list [1, 2, 3];
var = parseJson('[1, 2, 3]');

// returns the boolean value true
var = parseJson('true');

// returns the integer 1
var = parseJson('1');
```

**See also:**[writeJson](conversion-functions-ctl2.md#writejson), [parseBson](conversion-functions-ctl2.md#parsebson)

#### record2map

```ctl
variant record2map(record record);
```

Converts a data record into a map. Field names and values become the keys and values in the map, respectively.

This can be used to convert records into JSON as there is no direct record2json function.

Returns `null` if the record is null.

**Compatibility**

The `record2map(record)` function is available since **CloverDX 5.7.0**.
Example 82. Usage of record2map

```ctl
// metadata Person contains two fields: string 'Name' and integer 'Age':
Person person; // creates a new record with metadata 'Person'
person.Name = "Joe";
person.Age = 17;

variant myMap = record2map(person); // returns the map {"Name" -> "Joe", "Age" -> 17}
string json = writeJson(myMap); // returns the JSON string '{"Name":"Joe","Age":17}'
```

**See also:**[toMap](container-functions-ctl2.md#tomap), [writeJson](conversion-functions-ctl2.md#writejson)

#### sha1

```ctl
string sha1(byte arg);
string sha1(string arg);
```

The `sha1()` function calculates `SHA-1` hash value of a given byte array or for a given string argument.

If the input is `null`, the function fails with an error.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

**Compatibility**

The `sha(byte)` and `sha(string)` functions are available since **CloverETL 3.0.0**. Since **CloverETL 6.4.0** their names were changed to `sha1(byte)` and `sha1(string)`. Old function names `sha(byte)` and `sha(string)` were deprecated.
Example 83. Usage of sha1 Use `byte2hex()` to convert `SHA-1` hash from a byte array to a string representation of 40 hexadecimal digits. For example `byte2hex(sha1("abcd"))` returns `81fe8bfe87576c3ecb22426f8e57847382917acf`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [md5](conversion-functions-ctl2.md#md5), [sha256](conversion-functions-ctl2.md#sha256), [str2byte](conversion-functions-ctl2.md#str2byte)

#### sha1HexString

```ctl
string sha1HexString(byte arg);
string sha1HexString(string arg);
```

The `sha1HexString()` function calculates `SHA-1` hash value of a given byte array or for a given string argument. Returns hash value in a form of a hexadecimal string.

If the input is `null`, the function returns `null`.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

**Compatibility**

The `sha1HexString(byte)` and `sha1HexString(string)` functions are available since **CloverETL 6.4.0**.
Example 84. Usage of sha1HexString`sha1HexString("abcd")` returns `81fe8bfe87576c3ecb22426f8e57847382917acf`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [md5HexString](conversion-functions-ctl2.md#md5hexstring), [sha256HexString](conversion-functions-ctl2.md#sha256hexstring), [str2byte](conversion-functions-ctl2.md#str2byte)

#### sha256

```ctl
byte sha256(byte arg);
byte sha256(string arg);
```

The `sha256()` function calculates a `SHA-256` hash value of a given array of bytes or of a given string argument.

If the input is `null`, the function fails with an error.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

**Compatibility**

The `sha256(byte)` and `sha256(string)` functions are available since **CloverETL 3.4.x**.
Example 85. Usage of sha256 Use the `byte2hex()` function to convert `SHA-256` hash from a byte array to the usual string representation of 64 hexadecimal digits. For example `byte2hex(sha256("abcd"))` returns `88d4266fd4e6338d13b845fcf289579d209c897823b9217da3e161936f031589`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [md5](conversion-functions-ctl2.md#md5), [sha1](conversion-functions-ctl2.md#sha1), [str2byte](conversion-functions-ctl2.md#str2byte)

#### sha256HexString

```ctl
string sha256HexString(byte arg);
string sha256HexString(string arg);
```

The `sha256HexString()` function calculates a `SHA-256` hash value of a given array of bytes or of a given string argument. It returns hash value in a form of a hexadecimal string.

If the input is `null`, the function returns `null`.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

**Compatibility**

The `sha256HexString(byte)` and `sha256HexString(string)` functions are available since **CloverETL 6.4.0**.
Example 86. Usage of sha256`sha256HexString("abcd"))` returns `88d4266fd4e6338d13b845fcf289579d209c897823b9217da3e161936f031589`.
**See also:**[byte2hex](conversion-functions-ctl2.md#byte2hex), [md5HexString](conversion-functions-ctl2.md#md5hexstring), [sha1HexString](conversion-functions-ctl2.md#sha1hexstring), [str2byte](conversion-functions-ctl2.md#str2byte)

#### str2bits

```ctl
byte str2bits(string arg);
```

The `str2bits()` function converts a given string argument to an array of bytes.

The string can contain only characters: `"1"` and `"0"`. Each character `"1"` of a string is converted to the bit `1`, each character `"0"` is converted to the bit `0`. If the number of characters in the string is not an integral multiple of eight, the string is completed by "0" characters from the right. Then, the string is converted to an array of bytes as if the number of its characters were integral multiple of eight.

The first character represents the lowest bit.

If the input is `null`, the function returns `null`.

If the input contains any other character, the function `str2bits()`fails.

**Compatibility**

The `str2bits(string)` function is available since **CloverETL 3.0.0**.

The functionality of `str2bits()` has been changed in **CloverETL 3.5.0**. In the earlier versions, all characters not being `1` have been considered as `0`. The function call `str2bits("A010011001100110")` is correct in **CloverETL 3.4**, but the same function call *fails with an error* in **CloverETL 3.5**.
Example 87. Usage of str2bits
The function `str2bits("0010011001100110")` returns bytes containing `df`.

The function `str2bits("0A10011001100110")` fails with an error. See compatibility notice.

**See also:**[bits2str](conversion-functions-ctl2.md#bits2str)

#### str2bool

```ctl
boolean str2bool(string arg);
```

The `str2bool()` function converts a given string argument to the corresponding boolean value.

The string can be one of the following: `"TRUE"`, `"true"`, `"T"`, `"t"`, `"YES"`, `"yes"`, `"Y"`, `"y"`, `"1"`, `"FALSE"`, `"false"`, `"F"`, `"f"`, `"NO"`, `"no"`, `"N"`, `"n"`, `"0"`. The strings are converted to boolean `true` or boolean `false`.

If the input is `null`, the function returns `null`.

**Compatibility**

The `str2bool(string)` function is available since **CloverETL 3.0.0**.
Example 88. Usage of str2bool
The function `str2bool("true")` returns `true`.

The function `str2bool("True")` fails. The string `True` (with uppercase T and lowercase rest of the letters) is not allowed as a value.

The function `str2bool("NO")` returns `false`.

**See also:**[str2bits](conversion-functions-ctl2.md#str2bits), [str2bool](conversion-functions-ctl2.md#str2bool), [str2date](conversion-functions-ctl2.md#str2date), [str2decimal](conversion-functions-ctl2.md#str2decimal), [str2double](conversion-functions-ctl2.md#str2double), [str2integer](conversion-functions-ctl2.md#str2integer), [str2long](conversion-functions-ctl2.md#str2long)

#### str2byte

```ctl
byte str2byte(string payload, string charset);
```

The `str2byte()` function converts a string `payload` to an array of bytes using a given `charset` encoder.

If the `charset` is `null`, the function fails with an error. If the `payload` is `null`, the function returns `null`.

**Compatibility**

The `str2byte(string,string)` function is available since **CloverETL 3.2.x**.
Example 89. Usage of str2byte
The function `str2byte("grep", "utf-8")` returns bytes `0x67`, `0x72`, `0x65` and `0x70`.

The function `str2byte("voilà", "utf-8")` returns bytes `0x76`, `0x6f`, `0x69`, `0x6c`, `c3` and `a0`.

**See also:**[byte2str](conversion-functions-ctl2.md#byte2str), [hex2byte](conversion-functions-ctl2.md#hex2byte)

#### str2date

```ctl
date str2date(string input, string pattern);
date str2date(string input, string pattern, boolean strict);
date str2date(string input, string pattern, string locale);
date str2date(string input, string pattern, string locale, boolean strict);
date str2date(string input, string pattern, string locale, string timeZone);
date str2date(string input, string pattern, string locale, string timeZone, boolean strict);
```

The `str2date()` function converts the `input` to the date data type using the specified [`pattern`](metadata-records-and-fields.md#date-and-time-format), [`locale`](metadata-records-and-fields.md#locale) and [`timeZone`](metadata-records-and-fields.md#timezone).

The `input` must correspond with the `pattern`. Otherwise the function fails. If the `input` is `null`, the function returns `null`.

If the `pattern` is `null` or an empty string, the [default date format](../admin/designer-configuration.md#default-date-format) is used.

If the `locale` is `null` or an empty string, the respective [default value](metadata-records-and-fields.md#locale) is used instead.

If the `timeZone` is `null` or an empty string, the respective [default value](metadata-records-and-fields.md#timezone) is used instead.

If `strict` is `true`, date format is checked using a conversion from string to date, conversion from date to string and subsequent comparison of an input string and result string. If the input string and result string differ, the function fails. This way you can enforce required number of digits in date.

If `strict` is `null` or the function does not have the argument `strict`, it works in the same way as if it was set to `false` - the format is not checked in the strict way.

**Compatibility**

The `str2date(string,string)` and `str2date(string,string,string)` functions are available since **CloverETL 3.0.0**.

The `str2date(string, string, boolean)`, `str2date(string, string, string, boolean)` and `str2date(string, string, string, string, boolean)` functions are available since **CloverETL 4.1.0**.
Example 90. Usage of str2date
The function `str2date("12.6.2008", "dd.MM.yyyy")` returns the date `2008-06-12` in a local time zone.

The function `str2date("12.6.2008", "dd.MM.yyyy", "cs.CZ")` returns the date `2008-06-12` in a local time zone.

The function `str2date("12.6.2008 13:55:06", "dd.MM.yyyy HH:mm:ss", "cs.CZ", "GMT+5")` returns the date `2008-06-12 13:55:06` in the "GMT+5" time zone.

The function `str2date("15-Dezember-2010","dd-MMMM-yyyy", "de.DE")` returns `15 December 2010` in a local time zone, interpreting the month name using the German locale.

The function `str2date("6.007.2015", "dd.MM.yyyy", false)` returns 6 July 2015 whereas the function `str2date("6.007.2015", "dd.MM.yyyy", true)` fails.

**ISO-8601**

The function `str2date("2015-10-04", "iso-8601:yyyy-MM-dd")` returns `2015-10-04` in a local time zone.

The function `str2date("2015-10-04", "iso-8601:date")` returns `2015-10-04` in a local time zone.

The function `str2date("2015-10-05T06:07:02.123+00:00", "iso-8601:yyyy-MM-dd’T’H:m:sZZZ")` returns `2015-10-05 06:07:02.123` in the time zone `+00:00`.

The function `str2date("2015-10-05T06:07:02.123+00:00", "iso-8601:dateTime")` returns `2015-10-05 06:07:02.123` in the time zone `+00:00`.

The function `str2date("2015-10-05T06:07:02.234Z", "iso-8601:yyyy-MM-dd’T’H:m:sZZZ")` returns `2015-10-05 06:07:02.234` in the time zone `+00.00`.

**Joda**

The function `str2date("2015-06-15 00:00:10 America/New_York","joda:yyyy-MM-dd HH:mm:ss ZZZ")` returns `2015-06-15 00:00:10` in time zone America/New_York that corresponds to `2015-06-15 04:00:10` in UTC.

**See also:**[date2str](conversion-functions-ctl2.md#date2str), [isDate](string-functions-ctl2.md#isdate)

#### str2decimal

```ctl
decimal str2decimal(string arg);
decimal str2decimal(string arg, string format);
decimal str2decimal(string arg, string format, string locale);
```

The `str2decimal()` function converts a given string argument to a decimal value.

The conversion can be determined by the format specified as the second argument and the locale specified as the third argument.

The `arg` is a numeric value to be converted to the decimal. If the argument is `null`, the function returns `null`.

The `format` determines the data conversion. If a locale is specified, you can use `null` or an empty string for the format pattern to apply the default number format of that locale. See [Numeric format](metadata-records-and-fields.md#numeric-format).

The `locale` parameter is described in [Locale](metadata-records-and-fields.md#locale). If the function is called without the locale parameter, the default `locale` is used.

**Compatibility**

The `str2decimal(string)`, `str2decimal(string,string)` and `str2decimal(string,string,string)` functions are available since **CloverETL 3.0.0**.

Since **CloverDX 6.4.0** the whole string argument must be successfully parsed according to the `format`. If any part of the argument does not match format, the function fails.
Example 91. Usage of str2decimal
The function `str2decimal("23")` returns `23`.

The function `str2decimal("23.45")` returns `23.45`.

The function `str2decimal("123.456789")` returns `123.45`.

The function `str2decimal("2.147483648e9")` returns `2147483648.00`.

The function `str2decimal("123,456.78", "###,###.##")` returns `123456.78`.

The function `str2decimal("1.234,56", "#,###.##", "de.DE")` returns `1234.56`.

The function `str2decimal("1.234,56", null, "de.DE")` returns `1234.56`.

The function `str2decimal("1.234,56", "", "de.DE")` returns `1234.56`.

**See also:**[str2double](conversion-functions-ctl2.md#str2double), [str2integer](conversion-functions-ctl2.md#str2integer), [str2long](conversion-functions-ctl2.md#str2long), [toString](conversion-functions-ctl2.md#tostring)

#### str2double

```ctl
number str2double(string arg);
number str2double(string arg, string format);
number str2double(string arg, string format, string locale);
```

The `str2double()` function converts a given string argument to the corresponding double value. The conversion can be determined by a format specified as the second argument and a locale specified as the third argument.

The `arg` is string to be converted to double. If the argument is `null`, the function returns `null`.

The `format` is described in [Data formats](metadata-records-and-fields.md#data-formats). If a locale is specified, you can use `null` or an empty string for the format pattern to apply the default number format of that locale.

The `locale` parameter is described in [Locale](metadata-records-and-fields.md#locale). If the function is called without the `locale` parameter, the default `locale` is used.

**Compatibility**

The `str2double(string)`, `str2double(string,string)` and `str2double(string,string,string)` functions are available since **CloverETL 3.0.0**.
Example 92. Usage of str2double
The function `str2double("123.25")` returns `123.25`.

The function `str2double("123,456", "###,###")` returns `123456.0`

The function `str2double("1.234,56", "#,###.##", "de.DE")` returns `1234.56`.

The function `str2double("1.234,56", null, "de.DE")` returns `1234.56`.

The function `str2double("1.234,56", "", "de.DE")` returns `1234.56`.

**See also:**[num2str](conversion-functions-ctl2.md#num2str), [toString](conversion-functions-ctl2.md#tostring)

#### str2integer

```ctl
integer str2integer(string arg);
integer str2integer(string arg, integer radix);
integer str2integer(string arg, string format);
integer str2integer(string arg, string format, string locale);
```

The `str2integer()` function converts a given string argument to the corresponding integer value. The conversion can be determined by a numeral system, format or locale.

The parameter `arg` is a numeric value to be converted to integer. If the argument is `null`, the function returns `null`.

The parameter `radix` enables to convert a given string argument to integer using specified `radix` based numeric system representation.

The `format` is described in [Numeric format](metadata-records-and-fields.md#numeric-format). If a locale is specified, you can use `null` or an empty string for the format pattern to apply the default number format of that locale.

The `locale` is described in [Locale](metadata-records-and-fields.md#locale).

**Compatibility**

The `str2integer(string)`, `str2integer(string,string)`, `str2integer(string,string,string)` and `str2integer(string,integer)` functions are available since **CloverETL 3.0.0**.
Example 93. Usage of str2integer
The function `str2integer("123")` returns `123`.

The function `str2integer("123.45")` fails as argument in not an integer.

The function `str2integer("12345678901")` fails as argument does not fit into the `integer` data type. The value is too big.

The function `str2integer("101", 8)` returns `65`. Value 101 in the octal numeral system is same as 65 in the decimal numeral system.

The function `str2integer("123,456", "###,###")` returns 123456.

The function `str2integer("123.456", "###,###", "de.DE")` returns 123456.

The function `str2integer("123.456", null, "de.DE")` returns 123456.

The function `str2integer("123.456", "", "de.DE")` returns 123456.

**See also:**[toString](conversion-functions-ctl2.md#tostring)

#### str2long

```ctl
long str2long(string arg);
long str2long(string arg, integer radix);
long str2long(string arg, string format);
long str2long(string arg, string format, string locale);
```

The `str2long()` function converts a given string argument to a long value.

If the value is expressed in the `radix` based numeric system, the representation is specified by the second argument.

The conversion can be affected using a format specified as the second argument and the system locale.

The `arg` is the value to be converted to `long`. If the argument is `null`, the function returns `null`.

The `radix` is radix of numeral system.

The `format` is a format of the number to be converted. If a locale is specified, you can use `null` or an empty string for the format pattern to apply the default number format of that locale. For details, see [Numeric format](metadata-records-and-fields.md#numeric-format).

The `locale` is described in [Locale](metadata-records-and-fields.md#locale).

**Compatibility**

The `str2long(string)`, `str2long(string,string)`, `str2long(string,string,string)` and `str2long(string,integer)` functions are available since **CloverETL 3.0.0**.
Example 94. Usage of str2long
The function `str2long("123456789012")` returns `123456789012`.

The function `str2long("123.45")` fails as argument is not a long number.

The function `str2long("101", 8)` returns `65`.

The function `str2long("123,456,789,012", "###.###")` returns `123456789012`.

The function `str2long("123.456.789.012", "###,###", "de.DE")` returns `123456789012`.

The function `str2long("123.456.789.012", null, "de.DE")` returns `123456789012`.

The function `str2long("123.456.789.012", "", "de.DE")` returns `123456789012`.

**See also:**[toString](conversion-functions-ctl2.md#tostring)

#### str2timeUnit

```ctl
unit str2timeUnit(string arg);
```

The `str2timeUnit(string)` function converts a given input string argument to a time unit value, making it easier to work with different time units in your code. The function is case-insensitive.

This function is useful when you have a time unit represented as a string (e.g. in a graph parameter or field from metadata) and need to obtain its corresponding unit constant.

**Compatibility**

The `str2timeUnit(string)` function is available since **CloverDX 6.4.0**.
Example 95. Usage of str2timeUnit
integer year = date2num(date, str2timeUnit("Year"));

string day = "day";

date tomorrow = dateAdd(today(), 1, str2timeUnit(day))

**See also:**[date2num](conversion-functions-ctl2.md#date2num), [dateAdd](date-functions-ctl2.md#dateadd), [dateDiff](date-functions-ctl2.md#datediff)

#### toString

```ctl
string toString(<any type> arg);
```

Converts the given argument to its string representation.

If the input is `null`, the function returns the string "null".

The function should be used for logging or similar purposes, not for application logic. The output format is unspecified and may change in future versions.

**Compatibility**

The `toString(int|long|double|decimal|map|list)` function is available since **CloverETL 3.0.0**.

The `toString(boolean)` function is available since **CloverETL 4.1.0**.

The `toString(variant)` function is available since **CloverDX 5.6.0**.
Example 96. Usage of toString

```ctl
toString(34); // returns "34"
toString(1234567890123L); // returns "1234567890123"
toString(1234.567); // returns "1234.567"
toString(1234.567D); // returns "1234.567"
toString(true); // returns "true"
toString(["John Doe", true, 5, null, {1 -> 2}]);
     // returns "[John Doe, true, 5, null, {1=2}]"
```

**See also:**[str2decimal](conversion-functions-ctl2.md#str2decimal), [str2double](conversion-functions-ctl2.md#str2double), [str2integer](conversion-functions-ctl2.md#str2integer), [str2long](conversion-functions-ctl2.md#str2long)

#### writeAvro

```ctl
byte writeAvro(variant object, string schema);
```

Converts variant data type to bytes contaning Avro data serialized with the [Binary encoding](https://avro.apache.org/docs/current/spec.html#binary_encoding) using the specified Avro schema in JSON. Converted data have to match Avro schema supplemented as the second parameter. The resulted Avro data bytes are not regular Avro file, but the data only without Avro schema. The resulted Avro data can be used for example for a messaging system (JMS) or events streaming system (Kafka).

If the data input is `null`, the function returns `null`.

If the Avro schema is `null`, the function fails with an error.

Its counterpart is the function [parseAvro](conversion-functions-ctl2.md#parseavro).

| Avro type | Avro logical type | Accepted CTL types | Note |
| --- | --- | --- | --- |
| null type |  | null value |  |
| boolean |  | boolean |  |
| int |  | integer |  |
| int | date | integer, date | system timezone is used for conversion Clover date to Avro date; integer value is written with no conversion |
| int | time-millis | integer, date | system timezone is used for conversion Clover date to Avro time; integer value is written with no conversion |
| long |  | long, integer |  |
| long | time-micros | long, integer, date | system timezone is used for conversion Clover date to Avro time; integer and long values are written with no conversion |
| long | timestamp-millis | long, integer, date |  |
| long | timestamp-micros | long, integer, date |  |
| long | local-timestamp-millis | long, integer, date | system timezone is used for conversion Clover date to Avro timestamp; integer and long values are written with no conversion |
| long | local-timestamp-micros | long, integer, date | system timezone is used for conversion Clover date to Avro timestamp; integer and long values are written with no conversion |
| float |  | number, decimal, long, integer |  |
| double |  | number, decimal, long, integer |  |
| bytes |  | byte, cbyte |  |
| bytes | decimal | byte, cbyte, decimal |  |
| string |  | string |  |
| string | uuid | string | value must be UUID |
| record |  | map {string → any} | keys match field names; apply this table to the value types |
| enum |  | string | value must match enum symbol |
| array |  | list | apply this table to the items type |
| map |  | map | apply this table to the values type |
| union |  | types from union | apply this table to the union types |
| fixed |  | byte, cbyte |  |
| fixed | decimal | byte, cbyte, decimal |  |
| fixed | duration |  | not supported |
Example 97. Usage of writeAvro

```ctl
byte avro;

variant varMap = {"number" -> 1, "boolean" -> true, "string" -> "CloverDX"};
string varSchema = getAvroSchema(varMap);
byte varData = writeAvro(varMap, varSchema);
variant varMapCopy = parseAvro(varData, varSchema);
// varMap == varMapCopy

integer varInteger = 1;
//Avro schema for primitive type
string varSchema = "\"int\"";
byte varData = writeAvro(varInteger, varSchema);
```

**See also:**[parseAvro](conversion-functions-ctl2.md#parseavro), [getAvroSchema](conversion-functions-ctl2.md#getavroschema)

#### writeBson

```ctl
byte writeBson(map[<type of key>,<type of valuey>] object);
byte writeBson(variant object);
```

Converts a map to [BSON](http://bsonspec.org) binary data format. Note that map keys at any level of the argument must be strings, otherwise the function fails.

The top-level object must be a map. Unlike [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson), this function cannot write top-level lists and single values, such as numbers or strings. Lists and primitive values are only allowed inside the top-level map.

The advantage over [writeJson](conversion-functions-ctl2.md#writejson) is that BSON preserves data types. For example, dates are written as strings in JSON and you need to convert them manually back to dates.

On the other hand, JSON is a text-based format, so it is human readable. It is also more commonly used than BSON, especially in REST APIs.

To sum it up:

- Use
  [writeJson](conversion-functions-ctl2.md#writejson) to call REST APIs.
- Use
  [writeBson](conversion-functions-ctl2.md#writebson) to communicate with third-party applications that support BSON.

If the input is `null`, the function returns `null`.

Its counterpart is the function [parseBson](conversion-functions-ctl2.md#parsebson).

**Compatibility**

Available since **CloverDX 5.6.0**.
Example 98. Usage of writeBson

```ctl
byte bson;

variant varMap = {"number" -> 1, "boolean" -> true, "string" -> "CloverDX"};
bson = writeBson(varMap);
variant varMapCopy = parseBson(bson);
// varMap == varMapCopy

variant varInteger = 1;
// fails, writeBson can only handle maps
bson = writeBson(varInteger);
```

**See also:**[parseBson](conversion-functions-ctl2.md#parsebson), [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson), [writeJson](conversion-functions-ctl2.md#writejson)

#### writeExtendedBson
> [!IMPORTANT]
> The function `writeExtendedBson` is **deprecated**. It was used for passing variant values between components. Variant values can be passed on edges directly since **CloverDX 5.11.0**. Using `writeExtendedBson` function is no longer necessary.

```ctl
byte writeExtendedBson(list[<type of element>] object);
byte writeExtendedBson(map[<type of key>,<type of valuey>] object);
byte writeExtendedBson(variant object);
```

Converts lists, maps or primitive values to an extension of [BSON](http://bsonspec.org) binary data format. Use this function to transport structured data internally within CloverDX. Reconstruct the original object using [parseBson](conversion-functions-ctl2.md#parsebson).

A similar function, [writeBson](conversion-functions-ctl2.md#writebson), cannot handle single values, e.g. strings, integers, and top-level lists, because such values are not supported in standard BSON. Function [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson) removes these limitations, but the output is not compatible with third-party applications supporting standard BSON.

To sum it up:

- Use
  [writeJson](conversion-functions-ctl2.md#writejson) if you need text-based output.
- Use
  [writeBson](conversion-functions-ctl2.md#writebson) for compatibility with third-party applications supporting BSON.

If the input is `null`, the function returns `null`.

**Compatibility**

Available since **CloverDX 5.6.0**.

Deprecated since **CloverDX 5.11.0**.
Example 99. Usage of writeExtendedBson

```ctl
byte bson;

variant var = {"number" -> 1, "boolean" -> true, "string" -> "CloverDX"};
bson = writeExtendedBson(var);
variant varCopy = parseBson(bson);
// var == varCopy

// OK, CloverDX Extended BSON can handle simple values
bson = writeExtendedBson(1);

// OK, CloverDX Extended BSON can handle top-level lists
bson = writeExtendedBson([1, 2, 3]);
```

**See also:**[parseBson](conversion-functions-ctl2.md#parsebson), [writeBson](conversion-functions-ctl2.md#writebson), [writeJson](conversion-functions-ctl2.md#writejson)

#### writeJson

```ctl
string writeJson(variant object);
```

Converts CTL lists, maps or primitive values to a [JSON](https://www.json.org) string. Dates are written as strings in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format in UTC time zone, e.g. "2020-03-24T18:45:34.853Z". Keys in all maps at any level of the object are converted to strings.

If the input is `null`, the function returns `null`.

There are two similar functions:

- [writeBson](conversion-functions-ctl2.md#writebson) produces BSON, a binary format that preserves data types better than JSON.
- [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson) is a way of encoding variant into proprietary extension of the BSON format and it is incompatible with third-party applications.

The counterpart of writeJson is the function [parseJson](conversion-functions-ctl2.md#parsejson).

**Compatibility**

Available since **CloverDX 5.6.0**.
Example 100. Usage of writeJson

```ctl
string json;

variant varMap = {"number" -> 1, "boolean" -> true, "string" -> "CloverDX"}; // map
// returns '{"number":1,"number":true,"string":"CloverDX"}'
json = writeJson(varMap);

variant varList = [1, 2, 3]; // list
// returns '[1,2,3]'
json = writeJson(varList);

date d = str2date("12.6.2020 13:55:06", "dd.MM.yyyy HH:mm:ss", "en.US", "UTC+5");
// returns '2020-06-12T13:55:06.000Z'
json = writeJson(d);

boolean b = true;
// returns 'true'
writeJson(b);

// returns '1'
json = writeJson(1);
```

**See also:**[parseJson](conversion-functions-ctl2.md#parsejson), [record2map](conversion-functions-ctl2.md#record2map), [writeBson](conversion-functions-ctl2.md#writebson), [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson)

#### xml2json

```ctl
string xml2json(string arg);
```

The `xml2json()` function converts a string `XML` formatted argument to a `JSON` formatted string. Its counterpart is the function [json2xml](conversion-functions-ctl2.md#json2xml).

If the input is `null`, the function fails with an error.

**Compatibility**

The `xml2json(string)` function is available since **CloverETL 3.1.0**.
Example 101. Usage of xml2json The function `xml2json('<element0><id>1</id><date>2012-10-12</date></element0><element1><id>0</id><date>2011-11-07</date></element1>')` returns `{ "element1" : { "id" : "0", "date" : "2011-11-07" }, "element0" : { "id" : "1", "date" : "2012-10-12" }}`.
**See also:**[json2xml](conversion-functions-ctl2.md#json2xml)
