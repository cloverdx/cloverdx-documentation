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
| [map2record](conversion-functions-ctl2.md#map2record) |
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
| [variant2record](conversion-functions-ctl2.md#variant2record) |
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

##### Error states

- The function has no documented error states.

##### Examples
Example 63. Usage of base64byte

```ctl
base64byte("SGVsbG8=");
    // Returns Hello.
```

##### Compatibility

- The `base64byte(string)` overload is available since **CloverETL 3.0.0**.

##### See also

- [byte2base64](conversion-functions-ctl2.md#byte2base64)

---

#### bits2str

```ctl
string bits2str(byte input);
```

The `bits2str()` function converts an array of bytes to a string consisting of two characters: `"0"` or `"1"`.

Each byte is represented by eight characters ("0" or "1"). For each byte, the lowest bit is at the beginning of these eight characters. The counterpart is the function [str2bits](conversion-functions-ctl2.md#str2bits).

If the `input` is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 64. Usage of bits2str

```ctl
bits2str(str2byte("Hi", "utf-8"));
    // Returns 0001001010010110.
```

##### Compatibility

- The `bits2str(byte)` overload is available since **CloverETL 3.0.0**.

##### See also

- [str2bits](conversion-functions-ctl2.md#str2bits)

---

#### bool2num

```ctl
integer bool2num(boolean input);
```

The `bool2num()` function converts the boolean `input` to either integer `1` (if the argument is `true`) or integer `0` (if the argument is `false`).

If the `input` is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 65. Usage of bool2num

```ctl
bool2num(true);
    // Returns 1.

bool2num(false);
    // Returns 0.
```

##### Compatibility

- The `bool2num(boolean)` overload is available since **CloverETL 3.0.0**.

##### See also

- [num2bool](conversion-functions-ctl2.md#num2bool)

---

#### byte2base64

```ctl
string byte2base64(byte input);
string byte2base64(byte input, boolean wrap);
```

The `byte2base64()` function converts an array of bytes to a string in `base64` representation.

The function with one input parameter wraps the encoded lines after 76 characters. The ability of the function with 2 parameters to wrap lines is affected by the second parameter. If the `wrap` parameter is set to `true`, the encoded lines are wrapped after 76 characters.

If the `input` byte array is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 66. Usage of byte2base64

```ctl
byte2base64(str2byte("Clover", "utf-8"));
    // Returns Q2xvdmVy.
    // The function str2byte used in the example is needed for conversion of "Clover" from string to bytes as the function `byte2base64` needs to have bytes as an argument.
```

##### Compatibility

- The `byte2base64(byte)` overload is available since **CloverETL 3.0.0**.
- The `byte2base64(byte, boolean)` overload is available since **CloverETL 3.5.0-M2**.

##### See also

- [base64byte](conversion-functions-ctl2.md#base64byte)
- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [byte2str](conversion-functions-ctl2.md#byte2str)

---

#### byte2hex

```ctl
string byte2hex(byte input);
string byte2hex(byte input, string escapeChars);
```

The `byte2hex()` function converts an array of bytes to a string in `hexadecimal` representation.

If the `input` is `null`, the function returns `null`.

The `escapeChars` are prepended before hexadecimal characters of each byte. If the `escapeChars` is `null`, empty string, or the function has only one argument, nothing is escaped.

##### Error states

- The function has no documented error states.

##### Examples
Example 67. Usage of byte2hex

```ctl
byte2hex(str2byte("Clover", "utf-8"));
    // Returns 436c6f766572.

byte2hex(str2byte("Clover", "utf-8"), null);
    // Returns 436c6f766572.

byte2hex(str2byte("Clover", "utf-8"), "");
    // Returns 436c6f766572.

byte2hex(str2byte("Clover", "utf-8"), "\\");
    // Returns \43\6c\6f\76\65\72.

byte2hex(str2byte("Clover", "utf-8"), "0x");
    // Returns 0x430x6c0x6f0x760x650x72.
```

##### Compatibility

- The `byte2hex(input)` overload is available since **CloverETL 3.0.0**.
- The `byte2hex(input, escapeChars)` overload is available since **CloverETL 4.4.1**.

##### See also

- [byte2base64](conversion-functions-ctl2.md#byte2base64)
- [byte2str](conversion-functions-ctl2.md#byte2str)
- [hex2byte](conversion-functions-ctl2.md#hex2byte)

---

#### byte2str

```ctl
string byte2str(byte payload, string charset);
```

The `byte2str()` function converts an array of bytes to a string using given charset.

If the `payload` is null, the function returns `null`.

##### Error states

- If `charset` is `null`, the function fails with an error.

##### Examples
Example 68. Usage of byte2str

```ctl
byte2str(hex2byte("48656c6c6f"), "utf-8");
    // Returns Hello.
```

##### Compatibility

- The `byte2str(byte, string)` overload is available since **CloverETL 3.2.x**.

##### See also

- [byte2base64](conversion-functions-ctl2.md#byte2base64)
- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### date2long

```ctl
long date2long(date input);
```

The `date2long()` function converts a date argument to the long data type.

The return value is the number of milliseconds elapsed from `January 1, 1970, 00:00:00 GMT` to the date specified as the argument.

If the `input` is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 69. Usage of date2long

```ctl
date2long(str2date("2026-08-25 14:30:00", "yyyy-MM-dd HH:mm:ss", "en.GB", "GMT+0"));
    // Returns 1787668200000.
```

##### Compatibility

- The `date2long(date)` overload is available since **CloverETL 3.0.0**.

##### See also

- [date2num](conversion-functions-ctl2.md#date2num)
- [date2str](conversion-functions-ctl2.md#date2str)
- [long2date](conversion-functions-ctl2.md#long2date)

---

#### date2num

```ctl
integer date2num(date input, unit timeunit);
integer date2num(date input, unit timeunit, string locale);
```

The `date2num()` returns the number of specified time units from the date using system or specified locale.

The `date` parameter is a date to be converted. If the `input` date is `null`, the function returns `null`.

The `timeunit` field accepts one of the following unit constants: `year`, `month`, `week`, `day`, `hour`, `minute`, `second` or `millisec`. The value is supplied as a constant rather than through an edge or variable.

If the function takes two arguments, it returns an integer using the system locale. If the parameter `locale` is used, the function uses the locale from the `locale` parameter instead of the system locale.

If the time unit is contained in the date, it is returned as an integer number. If it is not contained, the function returns `0`.
> [!IMPORTANT]
> Remember that months are numbered starting from `1` unlike in CTL1.

The default time zone is used in the conversion.

##### Error states

- The function has no documented error states.

##### Examples
Example 70. Usage of date2num

```ctl
date2num(2026-08-25, month);
    // Returns 8.

date2num(2026-08-25 14:30:00, hour);
    // Returns 14.

date2num(2026-08-25, year, "en.US");
    // Returns 2026.

date2num(2026-08-25, year, "th.TH");
    // Returns 2569.   (Thai Buddhist calendar: 2026 + 543)
```

##### Compatibility

- The `date2num(date, unit)` overload is available since **CloverETL 3.0.x**.
- The `date2num(date, unit, string)` overload is available since **CloverETL 3.0.x**.

##### See also

- [date2long](conversion-functions-ctl2.md#date2long)
- [date2str](conversion-functions-ctl2.md#date2str)
- [getYear](date-functions-ctl2.md#getyear)
- [getMonth](date-functions-ctl2.md#getmonth)
- [getDay](date-functions-ctl2.md#getday)
- [getHour](date-functions-ctl2.md#gethour)
- [getMinute](date-functions-ctl2.md#getminute)
- [getSecond](date-functions-ctl2.md#getsecond)
- [getMillisecond](date-functions-ctl2.md#getmillisecond)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 71. Usage of date2str

```ctl
date2str(2026-08-25, "dd.MM.yyyy");
    // Returns 25.08.2026.

date2str(2026-08-25, "yyyy-MMM-d", "fr.CA");
    // Returns 2026-août-25.

date2str(2026-08-25 14:30:00, "yyyy-MMM-d HH:mm:ss z", "fr.CA", "GMT-5");
    // Returns 2026-août-25 09:30:00 GMT-05:00.
```

##### Compatibility

- The `date2str(date, string)` overload is available since **CloverETL 3.0.0**.
- The `date2str(date, string, string)` overload is available since **CloverETL 3.0.1**.
- The `date2str(date, string, string, string)` overload is available since **CloverETL 3.5.0-M1**.

##### See also

- [date2long](conversion-functions-ctl2.md#date2long)
- [date2num](conversion-functions-ctl2.md#date2num)
- [str2date](conversion-functions-ctl2.md#str2date)
- [getYear](date-functions-ctl2.md#getyear)
- [getMonth](date-functions-ctl2.md#getmonth)
- [getDay](date-functions-ctl2.md#getday)
- [getHour](date-functions-ctl2.md#gethour)
- [getMinute](date-functions-ctl2.md#getminute)
- [getSecond](date-functions-ctl2.md#getsecond)
- [getMillisecond](date-functions-ctl2.md#getmillisecond)

---

#### decimal2double

```ctl
number decimal2double(decimal arg);
```

The `decimal2double()` function converts a decimal argument to a double value.

On the other hand, any `double` can be converted into `decimal`. Both **Length** and **Scale** of a decimal can be adjusted for it.

If the input is `null`, the function returns `null`.

##### Error states

- If the `decimal` value cannot be converted into `double`, the function fails with an error.

##### Examples
Example 72. Usage of decimal2double

```ctl
decimal2double(9007199254740991D);
    // Returns 9.007199254740991E15. The input decimal number fit into double precisely.

decimal2double(92378352147483647.23D);
    // Returns 9.237835214748365E16.

decimal2double(9007199254740993D);
    // Returns 9.007199254740992E15.
    // The input number is too big to fit into the double data type precisely. Narrowing conversion is used and input decimal number is rounded.
```

##### Compatibility

- The `decimal2double(decimal)` overload is available since **CloverETL 3.0.0**.

##### See also

- [decimal2integer](conversion-functions-ctl2.md#decimal2integer)
- [decimal2long](conversion-functions-ctl2.md#decimal2long)
- [round](mathematical-functions-ctl2.md#round)
- [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

---

#### decimal2integer

```ctl
integer decimal2integer(decimal arg);
```

The `decimal2integer()` function converts a decimal argument to an integer.

On the other hand, any `integer` can be converted into `decimal` without a loss of precision. **Length** of `decimal` can be adjusted for it.

If the input is `null`, the function returns `null`.
> [!NOTE]
> There is no function `decimal2integer(double)`. You can use `double` parameter of the function due to implicit conversion of double to decimal. If you need conversion from `double` to `integer`, use the function [double2integer](conversion-functions-ctl2.md#double2integer).

##### Error states

- If the `decimal` value cannot be converted into `integer`, the function fails with an error.

##### Examples
Example 73. Usage of decimal2integer

```ctl
decimal2integer(352147483647.23D);
    // Fails with an error as the input decimal number is out of range of the integer data type.

decimal2integer(25.95D);
    // Returns 25.

decimal2integer(-123.45D);
    // Returns -123.
```

##### Compatibility

- The `decimal2integer(decimal)` overload is available since **CloverETL 3.0.0**.

##### See also

- [decimal2double](conversion-functions-ctl2.md#decimal2double)
- [decimal2long](conversion-functions-ctl2.md#decimal2long)
- [round](mathematical-functions-ctl2.md#round)
- [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

---

#### decimal2long

```ctl
long decimal2long(decimal arg);
```

The `decimal2long()` function converts a decimal argument to a long value.

On the other hand, any `long` can be converted into `decimal` without loss of precision. **Length** of a `decimal` can be adjusted for it.

If the input is `null`, the function returns `null`.
> [!NOTE]
> There is no function `decimal2long(double)`. You can use `double` parameter of the function due to implicit conversion of double to decimal. If you need conversion from `double` to `long`, use the function [double2long](conversion-functions-ctl2.md#double2long).

##### Error states

- If the `decimal` value cannot be converted into `long`, the function fails with an error.

##### Examples
Example 74. Usage of decimal2long

```ctl
decimal2long(9759223372036854775807.25D);
    // Fails with an error as the input decimal number is out of range of data type long.

decimal2long(72036854775807.79D);
    // Returns 72036854775807.
```

##### Compatibility

- The `decimal2long(decimal)` overload is available since **CloverETL 3.0.0**.

##### See also

- [decimal2double](conversion-functions-ctl2.md#decimal2double)
- [decimal2integer](conversion-functions-ctl2.md#decimal2integer)
- [round](mathematical-functions-ctl2.md#round)
- [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

---

#### double2integer

```ctl
integer double2integer(number arg);
```

The `double2integer()` function converts a number argument to an integer.

On the other hand, any `integer` can be converted into `double` without loss of precision.

If the input is `null`, the function returns `null`.

##### Error states

- If a `double` value cannot be converted into `integer`, the function fails with an error.

##### Examples
Example 75. Usage of double2integer

```ctl
double2integer(352147483647.1);
    // Fails with an error as the input does not fit into integer data type.

double2integer(25.757197);
    // Returns 25.
```

##### Compatibility

- The `double2integer(double)` overload is available since **CloverETL 3.0.0**.

##### See also

- [round](mathematical-functions-ctl2.md#round)
- [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

---

#### double2long

```ctl
long double2long(number arg);
```

The `double2long()` function converts a number argument to `long`.

On the other hand, any `long` can always be converted into `double`; however, the user should take into account that a loss of precision may occur.

If the input argument is `null`, the function returns `null`.

##### Error states

- If a `double` value cannot be converted into `long`, the function fails with an error.

##### Examples
Example 76. Usage of double2long

```ctl
double2long(1.3759739E23);
    // Fails — out of range of long.

double2long(25.8579);
    // Returns 25.
```

##### Compatibility

- The `double2long(double)` overload is available since **CloverETL 3.0.0**.

##### See also

- [double2integer](conversion-functions-ctl2.md#double2integer)
- [round](mathematical-functions-ctl2.md#round)
- [roundHalfToEven](mathematical-functions-ctl2.md#roundhalftoeven)

---

#### getAvroSchema

```ctl
string getAvroSchema(variant object);
```

Converts variant data type to Avro schema. Resulting string contains JSON representation of Avro schema.

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

##### Error states

- The function has no documented error states.

##### Compatibility

- The `getAvroSchema()` function is available since **CloverDX 5.11.0**.

##### See also

- [parseAvro](conversion-functions-ctl2.md#parseavro)
- [writeAvro](conversion-functions-ctl2.md#writeavro)

---

#### hex2byte

```ctl
byte hex2byte(string arg);
```

The `hex2byte()` function converts a string argument in `hexadecimal` representation to an array of bytes. Its counterpart is the [byte2hex](conversion-functions-ctl2.md#byte2hex) function.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 77. Usage of hex2byte

```ctl
hex2byte("436c6f766572");
    // Returns bytes 0x43 0x6c 0x6f 0x76 0x65 0x72 (the string "Clover").
```

##### Compatibility

- The `hex2byte(string)` overload is available since **CloverETL 3.0.0**.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### json2xml

```ctl
string json2xml(string arg);
```

The `json2xml()` function takes one string argument that is `JSON` formatted and converts it to an `XML` formatted string. Its counterpart is the function [xml2json](conversion-functions-ctl2.md#xml2json).

Parsing of an input does not have to result in a valid `XML` structure. For example, if the root element of input JSON contained array, the XML document with more than one root element would be created.

##### Error states

- If the input is an invalid JSON-formatted string or `null`, the function fails with an error.

##### Examples
Example 78. Usage of json2xml

```ctl
json2xml('{ "employee0" : { "id" : "1", "name" : "Alice" }, "employee1" : { "id" : "2", "name" : "Bob" } }');
    // Returns <employee0><name>Alice</name><id>1</id></employee0><employee1><name>Bob</name><id>2</id></employee1>.
```

##### Compatibility

- The `json2xml(string)` overload is available since **CloverETL 3.1.0**.

##### See also

- [xml2json](conversion-functions-ctl2.md#xml2json)

---

#### long2date

```ctl
date long2date(long arg);
```

The `long2date()` function converts a long argument to a date.

It adds the argument number of milliseconds to `January 1, 1970, 00:00:00 GMT` and returns the result as a date. Its counterpart is function [date2long](conversion-functions-ctl2.md#date2long).

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 79. Usage of long2date

```ctl
long2date(1787668200000L);
    // Returns 2026-08-25 14:30:00.
```

##### Compatibility

- The `long2date(long)` overload is available since **CloverETL 3.0.0**.

##### See also

- [date2long](conversion-functions-ctl2.md#date2long)

---

#### long2integer

```ctl
integer long2integer(long arg);
```

The `long2integer()` function converts a long argument to an integer value.

On the other hand, any `integer` value can be converted into a `long` number without a loss of precision.

If the input is `null`, the function returns `null`.

##### Error states

- If the conversion would lose information, the function fails with an error.

##### Examples
Example 80. Usage of long2integer

```ctl
long2integer(352147483647L);
    // Fails — out of range of integer.

long2integer(299792458L);
    // Returns 299792458.
```

##### Compatibility

- The `long2integer(long)` overload is available since **CloverETL 3.0.0**.

##### See also

- [double2integer](conversion-functions-ctl2.md#double2integer)

---

#### long2packDecimal

```ctl
byte long2packDecimal(long arg);
```

The `long2packDecimal()` function converts a long data type argument to the representation of packed decimal number. It is the counterpart of the function [packDecimal2long](conversion-functions-ctl2.md#packdecimal2long).

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 81. Usage of long2packDecimal

```ctl
long2packDecimal(2026L);
    // Returns bytes 0x02 0x02 0x6c ("02026C" in hex — 2026 with sign nibble C).
```

##### Compatibility

- The `long2packDecimal(long)` overload is available since **CloverETL 3.0.0**.

##### See also

- [packDecimal2long](conversion-functions-ctl2.md#packdecimal2long)

---

#### map2record

```ctl
integer map2record(map[string, variant] map, record record);
integer map2record(map[string, variant] map, record record, boolean strict);
```

Copies values from a map into the fields of a record. An entry is copied when its key is the name of a field of `record` and its value can be assigned to that field. Entries which do not meet both conditions are left out.

The function returns the number of fields it has populated, or `-1` if `map` or `record` is `null`.

Values are assigned using the standard CTL assignment compatibility, so a value is widened where necessary but never narrowed. An `integer` value is therefore copied into an `integer`, `long`, `number` or `decimal` field, while a `long` value is not copied into an `integer` field. A `null` value can be copied into a field of any nullable type.

The values `Integer.MIN_VALUE`, `Long.MIN_VALUE` and `NaN` are the internal null indicators of the numeric field types. They cannot be stored, so an entry holding one of them is left out as well.

The `strict` parameter turns the entries which have been left out into errors. In strict mode the function fails when a key does not match any field name, when a value cannot be assigned to its matching field, when a `null` value meets a `not null` field, and when `map` or `record` is `null`. If `strict` is missing, it works in the same way as if it was set to `false` - such entries are left out silently.

The function does not reset `record` first, so fields which are not matched by any entry keep their previous value.
> [!NOTE]
> The first argument has to be a `map[string, variant]`. A map with a more specific value type, e.g. a `map[string, string]`, does not match the signature. Use [variant2record](conversion-functions-ctl2.md#variant2record) if you need to map such a map, or if the map contains nested maps and lists.

**Compatibility**

The `map2record(map, record)` and `map2record(map, record, boolean)` functions are available since **CloverDX 7.6.0**.
Example 82. Usage of map2record

```ctl
// metadata Person contains three fields: string 'Name', integer 'Age' and decimal 'Salary'
Person person;

map[string, variant] values;
values["Name"] = "Joe";
values["Age"] = 17;
values["Salary"] = 2500;      // an integer widened into the decimal field
values["Nickname"] = "Joey";  // there is no such field, the entry is left out

integer count = map2record(values, person); // returns 3

// the same call in strict mode fails on the key 'Nickname'
count = map2record(values, person, true);
```

**See also:**[variant2record](conversion-functions-ctl2.md#variant2record), [record2map](conversion-functions-ctl2.md#record2map)

#### md5

```ctl
byte md5(byte arg);
byte md5(string arg);
```

The `md5()` function calculates an `MD5` hash value of the argument.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of byte manually using the function [str2byte](conversion-functions-ctl2.md#str2byte) to the bytes and then use the function `md5`.

##### Error states

- If the input is `null`, the function fails with an error.

##### Examples
Example 83. Usage of md5

```ctl
byte2hex(md5("Secret"));
    // Returns 1e6947ac7fb3a9529a9726eb692c8cc5.
```

##### Compatibility

- The `md5(byte)` overload is available since **CloverETL 3.0.0**.
- The `md5(string)` overload is available since **CloverETL 3.0.0**.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [sha1](conversion-functions-ctl2.md#sha1)
- [sha256](conversion-functions-ctl2.md#sha256)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### md5HexString

```ctl
string md5HexString(byte arg);
string md5HexString(string arg);
```

The `md5HexString()` function calculates an `MD5` hash value of the argument. Return value is converted to a hexadecimal string.

If the input is `null`, the function returns `null`.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of byte manually using the function [str2byte](conversion-functions-ctl2.md#str2byte) to the bytes and than use the function `md5`.

##### Error states

- The function has no documented error states.

##### Examples
Example 84. Usage of md5HexString

```ctl
md5HexString("CloverDX");
    // Returns 8397159342ce8f9d626809a028afa5a0.
```

##### Compatibility

- The `md5HexString(byte)` overload is available since **CloverETL 6.4.0**.
- The `md5HexString(string)` overload is available since **CloverETL 6.4.0**.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [sha1HexString](conversion-functions-ctl2.md#sha1hexstring)
- [sha256HexString](conversion-functions-ctl2.md#sha256hexstring)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### num2bool

```ctl
boolean num2bool(<numeric type> arg);
```

The `num2bool()` function converts a numeric type to boolean.

The function takes one argument of any numeric data type (`integer`, `long`, `number` or `decimal`) and returns boolean `false` for 0 and `true` for any other value.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 85. Usage of num2bool

```ctl
num2bool(0);
    // Returns false.

num2bool(3.1);
    // Returns true.
```

##### Compatibility

- The `num2bool(integer)` overload is available since **CloverETL 3.0.0**.
- The `num2bool(long)` overload is available since **CloverETL 3.0.0**.
- The `num2bool(double)` overload is available since **CloverETL 3.0.0**.
- The `num2bool(decimal)` overload is available since **CloverETL 3.0.0**.

##### See also

- [bool2num](conversion-functions-ctl2.md#bool2num)

---

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

The `radix` enables to convert the input number to a different radix-based numerical system, e.g., to the octal numerical system. For both `integer` and `long` data types, any integer number can be used as radix. For the data type double (`number`) only 10 or 16 can be used as radix.

The `format` describes format of number. If the parameter is missing, the [numeric format](metadata-records-and-fields.md#numeric-format) is used.

If the `locale` parameter is missing, the locale has system value.

##### Error states

- If a `number` input uses a radix other than 10 or 16, the function fails.

##### Examples
Example 86. Usage of num2str

```ctl
num2str(250000);
    // Returns 250000.

num2str(250000L);
    // Returns 250000.

num2str(1234.56);
    // Returns 1234.56.

num2str(1234.56D);
    // Returns 1234.56.

num2str(493, 8);
    // Returns 755.   (493 decimal = 0755 octal)

num2str(493L, 8);
    // Returns 755.

num2str(123.75, 8);
    // Fails — num2str for a double first argument only supports base 10 and 16.

num2str(4.0, 16);
    // Returns 0x1.0p2.

num2str(1250000, "###,###");
    // Returns 1,250,000.

num2str(1250000L, "###,###");
    // Returns 1,250,000.

num2str(1250000.25, "###,###.#");
    // Returns 1,250,000.2.

num2str(1250000.75D, "###,###.##");
    // Returns 1,250,000.75.

num2str(1250000, "###,###", "fr.FR");
    // Returns 1 250 000.

num2str(1250000L, "###,###", "fr.FR");
    // Returns 1 250 000.

num2str(1250000.75, "###,###.##", "fr.FR");
    // Returns 1 250 000,75.

num2str(1250000.25D, "###,###.##", "fr.FR");
    // Returns 1 250 000,25.
```

##### Compatibility

- The `num2str(integer)` overload is available since **CloverETL 3.0.0**.
- The `num2str(long)` overload is available since **CloverETL 3.0.0**.
- The `num2str(number)` overload is available since **CloverETL 3.0.0**.
- The `num2str(decimal)` overload is available since **CloverETL 3.0.0**.
- The `num2str(integer, integer)` overload is available since **CloverETL 3.0.0**.
- The `num2str(long, integer)` overload is available since **CloverETL 3.0.0**.
- The `num2str(number, integer)` overload is available since **CloverETL 3.0.0**.
- The `num2str(integer, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(long, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(double, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(decimal, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(integer, string, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(long, string, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(double, string, string)` overload is available since **CloverETL 3.0.0**.
- The `num2str(decimal, string, string)` overload is available since **CloverETL 3.0.0**.

##### See also

- [str2double](conversion-functions-ctl2.md#str2double)
- [toString](conversion-functions-ctl2.md#tostring)

---

#### packDecimal2long

```ctl
long packDecimal2long(byte arg);
```

The `packDecimal2long()` function converts an array of bytes whose meaning is the packed decimal representation of a long number to a long number.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 87. Usage of packDecimal2long

```ctl
packDecimal2long(hex2byte("02026C"));
    // Returns 2026.
```

##### Compatibility

- The `packDecimal2long(byte)` overload is available since **CloverETL 3.0.0**.

##### See also

- [long2packDecimal](conversion-functions-ctl2.md#long2packdecimal)

---

#### parseAvro

```ctl
variant parseAvro(byte avroData, string schema);
```

Converts bytes containing Avro data serialized with the [Binary encoding](https://avro.apache.org/docs/current/spec.html#binary_encoding) to a variant using the specified Avro schema in JSON. Avro data have to match Avro schema supplemented as the second parameter. The Avro data bytes are not regular Avro file, but the data only without Avro schema. The Avro data can be received for example from a messaging system (JMS) or events streaming system (Kafka).

If the data input is `null`, the function returns `null`.

Its counterpart is the function [writeAvro](conversion-functions-ctl2.md#writeavro).

| Avro type | Avro logical type | Result CTL type | Note |
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

##### Error states

- If the Avro schema is `null`, the function fails with an error.

##### Compatibility

- The `parseAvro()` function is available since **CloverDX 5.11.0**.

##### See also

- [writeAvro](conversion-functions-ctl2.md#writeavro)
- [getAvroSchema](conversion-functions-ctl2.md#getavroschema)

---

#### parseBson

```ctl
variant parseBson(byte bson);
```

Converts bytes containing [BSON](http://bsonspec.org) serialized data to a tree data structure composed of CTL lists and maps. Note that the return type is always variant, regardless of the actual returned value.

If the input is `null`, the function returns `null`.

Its counterpart is the function [writeBson](conversion-functions-ctl2.md#writebson). The function can also read data written by [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson).

##### Error states

- The function has no documented error states.

##### Examples
Example 88. Usage of parseBson

```ctl
// simulates data from an input port, $in.0.bson
byte bson = hex2byte("30000000106e756d62657200" +
                     "0100000008626f6f6c65616e" +
                     "000102737472696e67000900" +
                     "0000436c6f76657244580000");
variant v = parseBson(bson);
    // Returns map as variant {"number":1,"boolean":true,"string":"CloverDX"}.
```

##### Compatibility

- The `parseBson()` function is available since **CloverDX 5.6.0**.

##### See also

- [writeBson](conversion-functions-ctl2.md#writebson)
- [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson)

---

#### parseJson

```ctl
variant parseJson(string json);
variant parseJson(string json, boolean normalize);
```

Converts a [JSON](https://www.json.org) formatted string to a tree data structure composed of CTL lists and maps. Note that the return type is always variant, regardless of the actual returned value.

If the input is `null`, the function returns `null`.

The `normalize` parameter makes the CTL type of a parsed number depend on how the number is written rather than on how large it is. A whole number becomes a `long` and a number written with a decimal point or an exponent becomes a `decimal`. A whole number too large for a `long` becomes a `decimal` as well. If `normalize` is missing, it works in the same way as if it was set to `false` - the type follows the magnitude of the value, so the same JSON property can arrive as an `integer`, a `long`, a `number` or a `decimal` in different records.

| JSON number | normalize = false | normalize = true |
| --- | --- | --- |
| 25 | integer | long |
| 9223372036854775807 | long | long |
| 92233720368547758071 | decimal | decimal - the value does not fit into a long |
| 25.0 | number | decimal |
| 3.14 | number | decimal |
| 1e400 | number - the value overflows to Infinity | decimal - the value is kept exactly |
| NaN, Infinity, -Infinity | number | number |

Its counterpart is the function [writeJson](conversion-functions-ctl2.md#writejson).
> [!NOTE]
> Normalization is useful when the parsed values are stored into record fields with [variant2record](conversion-functions-ctl2.md#variant2record), because a `decimal` value is never converted into an `integer` or a `long` field. Without normalization the same JSON property can be mapped in one record and skipped in another, depending on how large its value happens to be.

##### Error states

- The function has no documented error states.

##### Examples
Example 89. Usage of parseJson

```ctl
variant var;

var = parseJson('{ "price" : 19.99, "inStock" : true, "name" : "Clover T-Shirt" }');
    // Returns the map {"price":19.99,"inStock":true,"name":"Clover T-Shirt"}.

var = parseJson('[10, 20, 30]');
    // Returns the list [10, 20, 30].

var = parseJson('true');
    // Returns the boolean value true.

var = parseJson('42');
    // Returns the integer 42.
```

With normalization the numeric types no longer depend on the magnitude of the value:

```ctl
// returns the map { "count" -> 25, "price" -> 3.14 },
// where 25 is an integer and 3.14 is a number
variant a = parseJson('{"count":25,"price":3.14}');

// returns the same map, but 25 is a long and 3.14 is a decimal
variant b = parseJson('{"count":25,"price":3.14}', true);
```

##### Compatibility

- The `parseJson(string)` function is available since **CloverDX 5.6.0**.
- The `parseJson(string, boolean)` function is available since **CloverDX 7.6.0**.

##### See also

- [writeJson](conversion-functions-ctl2.md#writejson)
- [parseBson](conversion-functions-ctl2.md#parsebson)
- [variant2record](conversion-functions-ctl2.md#variant2record)

---

#### record2map

```ctl
variant record2map(record record);
```

Converts a data record into a map. Field names and values become the keys and values in the map, respectively.

This can be used to convert records into JSON as there is no direct record2json function.

Returns `null` if the record is null.

##### Error states

- The function has no documented error states.

##### Examples
Example 90. Usage of record2map

```ctl
// metadata Person contains two fields: string 'Name' and integer 'Age':
Person person; // creates a new record with metadata 'Person'
person.Name = "Joe";
person.Age = 17;
variant myMap = record2map(person);
string json = writeJson(myMap);
    // Produces the map {"Name" -> "Joe", "Age" -> 17}; writeJson(myMap) returns the JSON string '{"Name":"Joe","Age":17}'.
```

##### Compatibility

- The `record2map(record)` overload is available since **CloverDX 5.7.0**.

##### See also

- [toMap](container-functions-ctl2.md#tomap)
- [writeJson](conversion-functions-ctl2.md#writejson)
- [map2record](conversion-functions-ctl2.md#map2record)
- [variant2record](conversion-functions-ctl2.md#variant2record)

---

#### sha1

```ctl
string sha1(byte arg);
string sha1(string arg);
```

The `sha1()` function calculates `SHA-1` hash value of a given byte array or for a given string argument.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

##### Error states

- If the input is `null`, the function fails with an error.

##### Examples
Example 91. Usage of sha1

```ctl
sha1("CloverDX");
    // Returns u8lvuZGqk2reZ6FB7K2i3BLQrzc=.
```

##### Compatibility

- The `sha(byte)` and `sha(string)` functions are available since **CloverETL 3.0.0**.
- Since **CloverETL 6.4.0** their names were changed to `sha1(byte)` and `sha1(string)`. Old function names `sha(byte)` and `sha(string)` were deprecated.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [md5](conversion-functions-ctl2.md#md5)
- [sha256](conversion-functions-ctl2.md#sha256)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### sha1HexString

```ctl
string sha1HexString(byte arg);
string sha1HexString(string arg);
```

The `sha1HexString()` function calculates `SHA-1` hash value of a given byte array or for a given string argument. Returns hash value in a form of a hexadecimal string.

If the input is `null`, the function returns `null`.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

##### Error states

- The function has no documented error states.

##### Examples
Example 92. Usage of sha1HexString

```ctl
sha1HexString("CloverDX");
    // Returns bbc96fb991aa936ade67a141ecada2dc12d0af37.
```

##### Compatibility

- The `sha1HexString(byte)` overload is available since **CloverETL 6.4.0**.
- The `sha1HexString(string)` overload is available since **CloverETL 6.4.0**.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [md5HexString](conversion-functions-ctl2.md#md5hexstring)
- [sha256HexString](conversion-functions-ctl2.md#sha256hexstring)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### sha256

```ctl
byte sha256(byte arg);
byte sha256(string arg);
```

The `sha256()` function calculates a `SHA-256` hash value of a given array of bytes or of a given string argument.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

##### Error states

- If the input is `null`, the function fails with an error.

##### Examples
Example 93. Usage of sha256

```ctl
byte2hex(sha256("CloverDX"));
    // Returns 8bf7191703ada9165023ec6873f0d574a80401c1749887798077a29f20c18595.
```

##### Compatibility

- The `sha256(byte)` overload is available since **CloverETL 3.4.x**.
- The `sha256(string)` overload is available since **CloverETL 3.4.x**.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [md5](conversion-functions-ctl2.md#md5)
- [sha1](conversion-functions-ctl2.md#sha1)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### sha256HexString

```ctl
string sha256HexString(byte arg);
string sha256HexString(string arg);
```

The `sha256HexString()` function calculates a `SHA-256` hash value of a given array of bytes or of a given string argument. It returns hash value in a form of a hexadecimal string.

If the input is `null`, the function returns `null`.

If the input string may contain a non-ASCII character, it is recommended to convert the input string to an array of bytes manually using the function [str2byte](conversion-functions-ctl2.md#str2byte).

##### Error states

- The function has no documented error states.

##### Examples
Example 94. Usage of sha256HexString

```ctl
sha256HexString("CloverDX");
    // Returns 8bf7191703ada9165023ec6873f0d574a80401c1749887798077a29f20c18595.
```

##### Compatibility

- The `sha256HexString(byte)` overload is available since **CloverETL 6.4.0**.
- The `sha256HexString(string)` overload is available since **CloverETL 6.4.0**.

##### See also

- [byte2hex](conversion-functions-ctl2.md#byte2hex)
- [md5HexString](conversion-functions-ctl2.md#md5hexstring)
- [sha1HexString](conversion-functions-ctl2.md#sha1hexstring)
- [str2byte](conversion-functions-ctl2.md#str2byte)

---

#### str2bits

```ctl
byte str2bits(string arg);
```

The `str2bits()` function converts a given string argument to an array of bytes.

The string can contain only characters: `"1"` and `"0"`. Each character `"1"` of a string is converted to the bit `1`, each character `"0"` is converted to the bit `0`. If the number of characters in the string is not an integral multiple of eight, the string is completed by "0" characters from the right. Then, the string is converted to an array of bytes as if the number of its characters were integral multiple of eight.

The first character represents the lowest bit.

If the input is `null`, the function returns `null`.

##### Error states

- If the input contains a character other than `0` or `1`, the function fails.

##### Examples
Example 95. Usage of str2bits

```ctl
str2bits("0001001010010110");
    // Returns bytes 0x48 0x69 (the string "Hi")

str2bits("00010012");
    // Fails — invalid character '2' at position 7.
```

##### Compatibility

- The `str2bits(string)` overload is available since **CloverETL 3.0.0**.
- The functionality of `str2bits()` has been changed in **CloverETL 3.5.0**. In the earlier versions, all characters not being `1` have been considered as `0`. The function call `str2bits("A010011001100110")` is correct in **CloverETL 3.4**, but the same function call *fails with an error* in **CloverETL 3.5**.

##### See also

- [bits2str](conversion-functions-ctl2.md#bits2str)

---

#### str2bool

```ctl
boolean str2bool(string arg);
```

The `str2bool()` function converts a given string argument to the corresponding boolean value.

The string can be one of the following: `"TRUE"`, `"true"`, `"T"`, `"t"`, `"YES"`, `"yes"`, `"Y"`, `"y"`, `"1"`, `"FALSE"`, `"false"`, `"F"`, `"f"`, `"NO"`, `"no"`, `"N"`, `"n"`, `"0"`. The strings are converted to boolean `true` or boolean `false`.

If the input is `null`, the function returns `null`.

##### Error states

- If the input is `"True"` (uppercase T with lowercase remaining letters), the function fails.

##### Examples
Example 96. Usage of str2bool

```ctl
str2bool("true");
    // Returns true.

str2bool("True");
    // Fails — "True" (capital T, lowercase rest) is not an accepted token.

str2bool("NO");
    // Returns false.
```

##### Compatibility

- The `str2bool(string)` overload is available since **CloverETL 3.0.0**.

##### See also

- [str2bits](conversion-functions-ctl2.md#str2bits)
- [str2date](conversion-functions-ctl2.md#str2date)
- [str2decimal](conversion-functions-ctl2.md#str2decimal)
- [str2double](conversion-functions-ctl2.md#str2double)
- [str2integer](conversion-functions-ctl2.md#str2integer)
- [str2long](conversion-functions-ctl2.md#str2long)

---

#### str2byte

```ctl
byte str2byte(string payload, string charset);
```

The `str2byte()` function converts a string `payload` to an array of bytes using a given `charset` encoder.

If the `payload` is `null`, the function returns `null`.

##### Error states

- If `charset` is `null`, the function fails with an error.

##### Examples
Example 97. Usage of str2byte

```ctl
str2byte("grep", "utf-8");
    // Returns bytes `0x67`, `0x72`, `0x65` and `0x70`.

str2byte("voilà", "utf-8");
    // Returns bytes `0x76`, `0x6f`, `0x69`, `0x6c`, `c3` and `a0`.
```

##### Compatibility

- The `str2byte(string, string)` overload is available since **CloverETL 3.2.x**.

##### See also

- [byte2str](conversion-functions-ctl2.md#byte2str)
- [hex2byte](conversion-functions-ctl2.md#hex2byte)

---

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

If the `input` is `null`, the function returns `null`.

If the `pattern` is `null` or an empty string, the [default date format](../admin/designer-configuration.md#default-date-format) is used.

If the `locale` is `null` or an empty string, the respective [default value](metadata-records-and-fields.md#locale) is used instead.

If the `timeZone` is `null` or an empty string, the respective [default value](metadata-records-and-fields.md#timezone) is used instead.

If `strict` is `true`, date format is checked using a conversion from string to date, conversion from date to string and subsequent comparison of an input string and result string.

This way you can enforce required number of digits in date.

If `strict` is `null` or the function does not have the argument `strict`, it works in the same way as if it was set to `false` - the format is not checked in the strict way.

##### Error states

- If `input` does not correspond with `pattern`, the function fails.
- If `strict` is `true` and the input string differs from the string produced after parsing and formatting, the function fails.

##### Examples
Example 98. Usage of str2date

```ctl
str2date("27.8.2026", "dd.MM.yyyy");
    // Returns the date 2026-08-27 in a local time zone.

str2date("27.8.2026", "dd.MM.yyyy", "cs.CZ");
    // Returns the date 2026-08-27 in a local time zone.

str2date("27.8.2026 13:55:06", "dd.MM.yyyy HH:mm:ss", "cs.CZ", "GMT+5");
    // Returns 2026-08-27 13:55:06 in GMT+5  (= 2026-08-27 08:55:06 UTC).

str2date("27-August-2026", "dd-MMMM-yyyy", "de.DE");
    // Returns 2026-08-27, interpreting the month name via the German locale.

str2date("27.008.2026", "dd.MM.yyyy", false);
    // Returns 2026-08-27 (lenient parsing accepts "008" as month 8).

str2date("27.008.2026", "dd.MM.yyyy", true);
    // Fails — strict parsing rejects the differently formatted input.

str2date("2026-08-27", "iso-8601:yyyy-MM-dd");
    // Returns 2026-08-27 in a local time zone.

str2date("2026-08-27", "iso-8601:date");
    // Returns 2026-08-27 in a local time zone.

str2date("2026-08-27T06:07:02.123+00:00", "iso-8601:yyyy-MM-dd'T'H:m:sZZZ");
    // Returns 2026-08-27 06:07:02.123 in the time zone +00:00.

str2date("2026-08-27T06:07:02.123+00:00", "iso-8601:dateTime");
    // Returns 2026-08-27 06:07:02.123 in the time zone +00:00.

str2date("2026-08-27T06:07:02.234Z", "iso-8601:yyyy-MM-dd'T'H:m:sZZZ");
    // Returns 2026-08-27 06:07:02.234 in the time zone +00:00.

str2date("2026-08-27 00:00:10 America/New_York", "joda:yyyy-MM-dd HH:mm:ss ZZZ");
    // Returns 2026-08-27 00:00:10 in America/New_York (= 2026-08-27 04:00:10 UTC).
```

##### Compatibility

- The `str2date(string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2date(string, string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2date(string, string, boolean)` overload is available since **CloverETL 4.1.0**.
- The `str2date(string, string, string, boolean)` overload is available since **CloverETL 4.1.0**.
- The `str2date(string, string, string, string, boolean)` overload is available since **CloverETL 4.1.0**.

##### See also

- [date2str](conversion-functions-ctl2.md#date2str)
- [isDate](string-functions-ctl2.md#isdate)

---

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

##### Error states

- Since CloverDX 6.4.0, if any part of the argument does not match `format`, the function fails.

##### Examples
Example 99. Usage of str2decimal

```ctl
str2decimal("42");
    // Returns 42.

str2decimal("19.99");
    // Returns 19.99.

str2decimal("123.456789");
    // Returns 123.456789.

str2decimal("2.147483648e9");
    // Returns 2147483648.

str2decimal("1,250,000.75", "###,###.##");
    // Returns 1250000.75.

str2decimal("1.250.000,75", "#,###.##", "de.DE");
    // Returns 1250000.75.

str2decimal("1.250.000,75", null, "de.DE");
    // Returns 1250000.75.

str2decimal("1.250.000,75", "", "de.DE");
    // Returns 1250000.75.
```

##### Compatibility

- The `str2decimal(string)` overload is available since **CloverETL 3.0.0**.
- The `str2decimal(string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2decimal(string, string, string)` overload is available since **CloverETL 3.0.0**.
- Since **CloverDX 6.4.0** the whole string argument must be successfully parsed according to the `format`. If any part of the argument does not match format, the function fails.

##### See also

- [str2double](conversion-functions-ctl2.md#str2double)
- [str2integer](conversion-functions-ctl2.md#str2integer)
- [str2long](conversion-functions-ctl2.md#str2long)
- [toString](conversion-functions-ctl2.md#tostring)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 100. Usage of str2double

```ctl
str2double("98.6");
    // Returns 98.6.

str2double("1,250,000", "###,###");
    // Returns 1250000.0.

str2double("1.250.000,75", "#,###.##", "de.DE");
    // Returns 1250000.75.

str2double("1.250.000,75", null, "de.DE");
    // Returns 1250000.75.

str2double("1.250.000,75", "", "de.DE");
    // Returns 1250000.75.
```

##### Compatibility

- The `str2double(string)` overload is available since **CloverETL 3.0.0**.
- The `str2double(string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2double(string, string, string)` overload is available since **CloverETL 3.0.0**.

##### See also

- [num2str](conversion-functions-ctl2.md#num2str)
- [toString](conversion-functions-ctl2.md#tostring)

---

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

##### Error states

- If the input is not an integer representation, the function fails.
- If the parsed value does not fit into the `integer` data type, the function fails.

##### Examples
Example 101. Usage of str2integer

```ctl
str2integer("2026");
    // Returns 2026.

str2integer("19.99");
    // Fails — argument is not an integer.

str2integer("12345678901");
    // Fails — value too big for the integer data type.

str2integer("755", 8);
    // Returns 493.   (755 octal = 493 decimal — inverse of num2str(493, 8))

str2integer("1,250,000", "###,###");
    // Returns 1250000.

str2integer("1.250.000", "###,###", "de.DE");
    // Returns 1250000.

str2integer("1.250.000", null, "de.DE");
    // Returns 1250000.

str2integer("1.250.000", "", "de.DE");
    // Returns 1250000.
```

##### Compatibility

- The `str2integer(string)` overload is available since **CloverETL 3.0.0**.
- The `str2integer(string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2integer(string, string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2integer(string, integer)` overload is available since **CloverETL 3.0.0**.

##### See also

- [toString](conversion-functions-ctl2.md#tostring)

---

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

##### Error states

- If the input is not a long-integer representation, the function fails.

##### Examples
Example 102. Usage of str2long

```ctl
str2long("9876543210");
    // Returns 9876543210.

str2long("19.99");
    // Fails — argument is not a long number.

str2long("755", 8);
    // Returns 493.

str2long("123,456,789,012", "###,###");
    // Returns 123456789012.

str2long("9.876.543.210", "###,###", "de.DE");
    // Returns 9876543210.

str2long("9.876.543.210", null, "de.DE");
    // Returns 9876543210.

str2long("9.876.543.210", "", "de.DE");
    // Returns 9876543210.
```

##### Compatibility

- The `str2long(string)` overload is available since **CloverETL 3.0.0**.
- The `str2long(string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2long(string, string, string)` overload is available since **CloverETL 3.0.0**.
- The `str2long(string, integer)` overload is available since **CloverETL 3.0.0**.

##### See also

- [toString](conversion-functions-ctl2.md#tostring)

---

#### str2timeUnit

```ctl
unit str2timeUnit(string arg);
```

The `str2timeUnit(string)` function converts a given input string argument to a time unit value, making it easier to work with different time units in your code. The function is case-insensitive.

This function is useful when you have a time unit represented as a string (e.g., in a graph parameter or field from metadata) and need to obtain its corresponding unit constant.

##### Error states

- The function has no documented error states.

##### Examples
Example 103. Usage of str2timeUnit

```ctl
date myDate = 2026-08-27;

integer y = date2num(myDate, str2timeUnit("year"));
    // Returns the integer 2026 (the year component of myDate).

date tomorrow = dateAdd(today(), 1, str2timeUnit("day"));
    // Returns today + 1 day.
```

##### Compatibility

- The `str2timeUnit(string)` overload is available since **CloverDX 6.4.0**.

##### See also

- [date2num](conversion-functions-ctl2.md#date2num)
- [dateAdd](date-functions-ctl2.md#dateadd)
- [dateDiff](date-functions-ctl2.md#datediff)

---

#### toString

```ctl
string toString(<any type> arg);
```

Converts the given argument to its string representation.

If the input is `null`, the function returns the string "null".

The function should be used for logging or similar purposes, not for application logic. The output format is unspecified and may change in future versions.

##### Error states

- The function has no documented error states.

##### Examples
Example 104. Usage of toString

```ctl
toString(2026);
    // Returns "2026".

toString(9876543210L);
    // Returns "9876543210".

toString(3.14159);
    // Returns "3.14159".

toString(19.99D);
    // Returns "19.99".

toString(true);
    // Returns "true".

toString(["Clover", true, 42, null, {1 -> 2}]);
    // Returns "[Clover, true, 42, null, {1=2}]".
```

##### Compatibility

- The `toString(int|long|double|decimal|map|list)` overload is available since **CloverETL 3.0.0**.
- The `toString(boolean)` overload is available since **CloverETL 4.1.0**.
- The `toString(variant)` overload is available since **CloverDX 5.6.0**.

##### See also

- [str2decimal](conversion-functions-ctl2.md#str2decimal)
- [str2double](conversion-functions-ctl2.md#str2double)
- [str2integer](conversion-functions-ctl2.md#str2integer)
- [str2long](conversion-functions-ctl2.md#str2long)

---

#### variant2record

```ctl
integer variant2record(variant source, record target);
integer variant2record(variant source, record target, boolean strict);
integer variant2record(variant source, list[<metadata name>] target);
integer variant2record(variant source, list[<metadata name>] target, boolean strict);
integer variant2record(variant source, list[<metadata name>] target, <metadata name> template);
integer variant2record(variant source, list[<metadata name>] target, <metadata name> template, boolean strict);
```

Maps a variant tree - typically the result of [parseJson](conversion-functions-ctl2.md#parsejson) - into a flat record.

A variant parsed from JSON is a tree of nested maps and lists, while a record is flat: it has scalar fields and container fields which hold scalars of a single type only. The function bridges the two by searching the whole tree for keys which match a field name of `target` and converting the values it finds. The `target` is either a single record, or a list of records - one new record is then appended to the list for every item of the source list.

The `source` parameter is the variant to read. Any map or list is accepted, including a `map[string, string]` or another map with a specific value type. A scalar has no keys, so it populates nothing.

The tree is searched breadth-first:

- The shallowest match wins. A field populated by this call is never overwritten by a deeper key of the same name; a container under such a key is still searched and can populate the fields which are still empty.
- A key which matches no field name is ignored, and is not an error even in the strict mode.
- A value which fits its matching field is consumed. The keys of a sub-map stored into a `string` or a `variant` field are therefore not searched any more.
- A container which does not fit its matching field is descended into instead. That is a part of the search rather than a failure.

When `target` is a single record, the function returns the number of fields it has populated; when `target` is a list of records, it returns the number of records it has appended. It returns `-1` if `source` or `target` is `null`.

| Target field type | Accepted value | Note |
| --- | --- | --- |
| string | any value | a sub-map or a sub-list is stored as compact JSON, a date in the ISO-8601 UTC format and a byte value in Base64 |
| integer | integer, long | a long value out of the integer range is not converted |
| long | integer, long |  |
| number, decimal | integer, long, number, decimal | a decimal value never goes into an integer or a long field, not even with a zero fractional part |
| boolean, date, byte, cbyte | a value of the very same type | there is no conversion from a string |
| variant | any value | the whole sub-tree is stored as it is |
| list of <type> | a list whose every single element converts to <type> | all or nothing; an empty list gives an empty, non-null field |
| map[string, <type>] | a map with string keys whose every single value converts to <type> | all or nothing |

A `null` value converts into a scalar field of any type, as long as the field is nullable. A `not null` field rejects it, in the very same way as a value of an unfit type. A list or a map field takes a list or a map only, so a `null` is left out of it like any other unfit value, whether the field is nullable or not.

The `strict` parameter turns a failed conversion into an error. In strict mode the function fails when a key matches a field name but its value cannot be converted, when `target` is a list of records but `source` is not a list, and when `source` or `target` is `null`. If `strict` is missing, it works in the same way as if it was set to `false` - such a value is left out silently.

The function does not reset `target` first: fields which are not matched by any key keep their previous value, and a list of records keeps the records it already holds.

When `target` is a list of records, `source` has to be a list too - typically a parsed JSON array. Every single item of the source list is mapped into a new record appended to `target`, by the very same search and conversion rules as for a single record. One item always gives one record, so the records keep the positions of the items; an item which is `null` or a scalar matches nothing and gives an all-null record. A `source` which is not a list appends nothing and returns `0`, and is an error only in the strict mode.

The `template` parameter is a record whose metadata is used for the records being appended. Its metadata has to be the element metadata of `target`, otherwise the list ends up holding records of mixed metadata. The parameter can be left out when `target` already holds at least one record, because the metadata of that record is used instead. Note that `target` may be a list of any type, not only a list of records; a list of a scalar type is rejected where that can be recognized, which is not possible for an empty one.
> [!NOTE]
> The `template` parameter can be left out in the interpreted CTL only. A compiled transformation does not know the element type of a list at runtime, so `template` has to be passed whenever `target` is empty. Without it the function fails with
>
>
> ```ctl
> variant2record - cannot determine the metadata for the records to be appended: the
> target list is empty and no template record was passed. The element type of a list is
> not available at runtime in compiled CTL, so a template record of the list element
> type has to be passed as the third argument.
> ```
>
>
> Passing `template` always works, so pass one unless `target` is known to hold a record already.
> [!NOTE]
> Field names are matched case sensitively, and labels are not taken into account. A JSON key `firstName` does not match a field named `FirstName`.
>
> The values `Integer.MIN_VALUE`, `Long.MIN_VALUE` and `NaN` are the internal null indicators of the numeric field types. They cannot be stored, so such a value is skipped like any other value which does not fit the field, and reported as an error in the strict mode.

**Compatibility**

Available since **CloverDX 7.6.0**.
Example 105. Usage of variant2record
The whole tree is searched, so a field is filled in from a sub-object or from an object inside an array:

```ctl
// metadata Customer contains fields: string 'Name', string 'City',
// integer 'Age' and list[string] 'Tags'
Customer customer;

variant data = parseJson('{"Name":"Joe","address":{"City":"Prague","zip":"11000"},"profile":[{"Age":17}],"Tags":["vip","eu"]}');

// returns 4 - 'City' comes from the sub-object, 'Age' from inside the array,
// 'Tags' fills the whole list field and 'zip' matches no field
integer count = variant2record(data, customer);
```

A value is converted when a safe conversion exists:

```ctl
// metadata Person contains: string 'Name', integer 'Age', decimal 'Salary'
Person person;

variant data = parseJson('{"Name":42,"Age":2500000000,"Salary":1200}');

// returns 2 - 42 becomes the string "42" and 1200 is widened into the decimal
// field, while 2500000000 does not fit into the integer field 'Age'
integer count = variant2record(data, person);

// the same call in strict mode fails on the field 'Age'
count = variant2record(data, person, true);
```

A list of records is filled in from a JSON array, one record per item:

```ctl
// metadata Customer contains fields: string 'Name', string 'City' and integer 'Age'
list[Customer] customers;
Customer template;

variant data = parseJson('[{"Name":"Joe","City":"Prague"},{"Name":"Jane","address":{"City":"Brno"}}]');

// returns 2 - two records are appended to 'customers', the second one taking
// its 'City' from the sub-object
integer count = variant2record(data, customers, template);
```

**Mapping a JSON API response**

A response of this shape:

```ctl
{
  "status": "success",
  "requested_at": "2026-08-29T19:17:00Z",
  "data": {
    "user": {
      "id": "usr_948201",
      "username": "johndoe",
      "profile": {
        "first_name": "John", "last_name": "Doe",
        "email": "john.doe@example.com", "is_active": true
      }
    },
    "shopping_cart": {
      "cart_id": "crt_77102", "currency": "USD",
      "totals": {"subtotal": 128.50, "tax": 10.28, "shipping": 5.00, "grand_total": 143.78},
      "items": [
        {
          "product_id": "prod_001", "sku": "SKU-WIRELESS-MOUSE",
          "name": "Ergonomic Wireless Mouse", "quantity": 1, "price": 45.00,
          "tags": ["electronics", "accessories", "office"],
          "dimensions": {"weight_oz": 4.2, "width_in": 2.8, "height_in": 1.5}
        },
        {
          "product_id": "prod_042", "sku": "SKU-MECH-KEYBOARD",
          "name": "Mechanical Gaming Keyboard", "quantity": 1, "price": 83.50,
          "tags": ["electronics", "gaming"],
          "dimensions": {"weight_oz": 28.4, "width_in": 17.4, "height_in": 1.4}
        }
      ]
    },
    "shipping_address": {
      "street": "123 Innovation Way", "app_suite": "Suite 404",
      "city": "Tech City", "state": "CA", "postal_code": "94016",
      "coordinates": {"latitude": 37.7749, "longitude": -122.4194}
    }
  },
  "metadata": {"server_id": "pod-us-west-3", "execution_time_ms": 42}
}
```

is mapped into three flat structures - a flattened object, a list of records from an array, and a narrowed sub-object. The record types are declared in the script itself, so no metadata has to exist in the graph:

```ctl
record ApiUser {
    string id;
    string username;
    string first_name;
    string last_name;
    string email;
    boolean is_active;
}

record ApiItems {
    string product_id;
    string sku;
    string name;
    integer quantity;
    decimal price;
    string[] tags;          // a list field of a declared record is written '<type>[]'
    decimal weight_oz;
    decimal width_in;
    decimal height_in;
}

record ApiShipTo {
    string street;
    string app_suite;
    string city;
    string state;
    string postal_code;
}

function integer transform() {
    // normalized, so that a whole number is always a long and a decimal always a decimal
    variant parsed = parseJson($in.0.content, true);

    // the whole response is searched, so the nesting does not matter: 'id' and 'username'
    // are found in data.user, the other four one level deeper in data.user.profile
    ApiUser user;
    integer userFields = variant2record(parsed, user);                        // returns 6

    // a list target needs the array itself as the source, plus a template record for
    // the metadata of the records being appended - one item gives one record
    // 'dimensions' matches no field, so it is descended into and weight_oz, width_in
    // and height_in are found inside it; 'tags' fills the string[] field as a whole
    ApiItems[] cartItems;
    ApiItems template;
    integer itemCount = variant2record(parsed["data"]["shopping_cart"]["items"],
                                       cartItems, template);                 // returns 2

    // narrowing the input keeps the search inside one sub-object
    // 'coordinates' drops out on its own - ApiShipTo has no latitude or longitude field
    ApiShipTo shipTo;
    integer shipToFields = variant2record(parsed["data"]["shipping_address"], shipTo); // returns 5

    return 0;
}
```

Note that mapping from the whole response relies on the field names being unique in it. A record with a field `name` would pick up the product name of the first cart item, because that is the shallowest `name` in the tree; narrowing the input, as `ApiShipTo` does, avoids that.

**See also:**[map2record](conversion-functions-ctl2.md#map2record), [record2map](conversion-functions-ctl2.md#record2map), [parseJson](conversion-functions-ctl2.md#parsejson), [resetRecord](field-access-functions-ctl2.md#resetrecord)

#### writeAvro

```ctl
byte writeAvro(variant object, string schema);
```

Converts variant data type to bytes contianing Avro data serialized with the [Binary encoding](https://avro.apache.org/docs/current/spec.html#binary_encoding) using the specified Avro schema in JSON. Converted data have to match Avro schema supplemented as the second parameter. The resulting Avro data bytes are not regular Avro file, but the data only without Avro schema. The resulting Avro data can be used for example for a messaging system (JMS) or events streaming system (Kafka).

If the data input is `null`, the function returns `null`.

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
| string | uuid | string | UUID-formatted value |
| record |  | map {string → any} | keys match field names; apply this table to the value types |
| enum |  | string | value must match enum symbol |
| array |  | list | apply this table to the items type |
| map |  | map | apply this table to the values type |
| union |  | types from union | apply this table to the union types |
| fixed |  | byte, cbyte |  |
| fixed | decimal | byte, cbyte, decimal |  |
| fixed | duration |  | not supported |

##### Error states

- If the Avro schema is `null`, the function fails with an error.

##### Examples
Example 106. Usage of writeAvro

```ctl
variant varMap = {"id" -> 42, "active" -> true, "name" -> "Clover"};
string varSchema = getAvroSchema(varMap);
byte varData = writeAvro(varMap, varSchema);
variant varMapCopy = parseAvro(varData, varSchema);
    // Round-trips: varMapCopy == {"id":42,"active":true,"name":"Clover"}.

integer varInteger = 42;
byte varData2 = writeAvro(varInteger, "\"int\"");
    // Produces Avro bytes 0x54.
```

##### Compatibility

- The `writeAvro()` function is available since **CloverDX 5.11.0**.

##### See also

- [parseAvro](conversion-functions-ctl2.md#parseavro)
- [getAvroSchema](conversion-functions-ctl2.md#getavroschema)

---

#### writeBson

```ctl
byte writeBson(map[<type of key>,<type of value>] object);
byte writeBson(variant object);
```

Converts a map to [BSON](http://bsonspec.org) binary data format.

The top-level object is a map. Lists and primitive values are allowed inside the top-level map. Unlike [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson), top-level lists and single values are not supported.

The advantage over [writeJson](conversion-functions-ctl2.md#writejson) is that BSON preserves data types. For example, dates are written as strings in JSON and you need to convert them manually back to dates.

On the other hand, JSON is a text-based format, so it is human readable. It is also more commonly used than BSON, especially in REST APIs.

To sum it up:

- Use
  [writeJson](conversion-functions-ctl2.md#writejson) to call REST APIs.
- Use
  [writeBson](conversion-functions-ctl2.md#writebson) to communicate with third-party applications that support BSON.

If the input is `null`, the function returns `null`.

Its counterpart is the function [parseBson](conversion-functions-ctl2.md#parsebson).

##### Error states

- If a map key at any level of the argument is not a string, the function fails.
- If the top-level object is not a map, the function fails.

##### Examples
Example 107. Usage of writeBson

```ctl
variant varMap = {"id" -> 42, "active" -> true, "name" -> "Clover"};
byte bson = writeBson(varMap);
variant varMapCopy = parseBson(bson);
    // Round-trips: varMapCopy == {"id":42,"active":true,"name":"Clover"}.

variant varInteger = 42;
bson = writeBson(varInteger);
    // Fails — writeBson only accepts a map at the top level.
```

##### Compatibility

- The `writeBson()` function is available since **CloverDX 5.6.0**.

##### See also

- [parseBson](conversion-functions-ctl2.md#parsebson)
- [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson)
- [writeJson](conversion-functions-ctl2.md#writejson)

---

#### writeExtendedBson

```ctl
byte writeExtendedBson(<element type>[] object);
byte writeExtendedBson(map[<type of key>,<type of value>] object);
byte writeExtendedBson(variant object);
```

Converts lists, maps or primitive values to an extension of [BSON](http://bsonspec.org) binary data format. Use this function to transport structured data internally within CloverDX. Reconstruct the original object using [parseBson](conversion-functions-ctl2.md#parsebson).

Unlike [writeBson](conversion-functions-ctl2.md#writebson), [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson) supports single values, e.g., strings and integers, and top-level lists. The output is not compatible with third-party applications supporting standard BSON.

To sum it up:

- Use
  [writeJson](conversion-functions-ctl2.md#writejson) if you need text-based output.
- Use
  [writeBson](conversion-functions-ctl2.md#writebson) for compatibility with third-party applications supporting BSON.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 108. Usage of writeExtendedBson

```ctl
variant var = {"id" -> 42, "active" -> true, "name" -> "Clover"};
byte bson = writeExtendedBson(var);
variant varCopy = parseBson(bson);
    // Round-trips: varCopy == {"id":42,"active":true,"name":"Clover"}.

bson = writeExtendedBson(42);
    // Produces extended BSON for a simple value; parseBson(bson) returns 42.

bson = writeExtendedBson([10, 20, 30]);
    // Produces extended BSON for a top-level list; parseBson(bson) returns [10, 20, 30].
```

##### Compatibility

- The `writeExtendedBson()` function is available since **CloverDX 5.6.0**.
- Deprecated since **CloverDX 5.11.0**.

##### See also

- [parseBson](conversion-functions-ctl2.md#parsebson)
- [writeBson](conversion-functions-ctl2.md#writebson)
- [writeJson](conversion-functions-ctl2.md#writejson)

---

#### writeJson

```ctl
string writeJson(variant object);
```

Converts CTL lists, maps or primitive values to a [JSON](https://www.json.org) string. Dates are written as strings in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format in UTC time zone, e.g., "2020-03-24T18:45:34.853Z". Keys in all maps at any level of the object are converted to strings.

If the input is `null`, the function returns `null`.

There are two similar functions:

- [writeBson](conversion-functions-ctl2.md#writebson) produces BSON, a binary format that preserves data types better than JSON.
- [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson) is a way of encoding variant into proprietary extension of the BSON format and it is incompatible with third-party applications.

The counterpart of writeJson is the function [parseJson](conversion-functions-ctl2.md#parsejson).

##### Error states

- The function has no documented error states.

##### Examples
Example 109. Usage of writeJson

```ctl
variant varMap = {"id" -> 42, "active" -> true, "name" -> "Clover"};
writeJson(varMap);
    // Returns {"id":42,"active":true,"name":"Clover"}.

variant varList = [10, 20, 30];
writeJson(varList);
    // Returns [10,20,30].

date d = str2date("27.8.2026 13:55:06", "dd.MM.yyyy HH:mm:ss", "en.US", "GMT+5");
writeJson(d);
    // Returns "2026-08-27T08:55:06.000Z" (13:55 at GMT+5 == 08:55 UTC).

writeJson(true);
    // Returns true.

writeJson(42);
    // Returns 42.
```

##### Compatibility

- The `writeJson()` function is available since **CloverDX 5.6.0**.

##### See also

- [parseJson](conversion-functions-ctl2.md#parsejson)
- [record2map](conversion-functions-ctl2.md#record2map)
- [writeBson](conversion-functions-ctl2.md#writebson)
- [writeExtendedBson](conversion-functions-ctl2.md#writeextendedbson)

---

#### xml2json

```ctl
string xml2json(string arg);
```

The `xml2json()` function converts a string `XML` formatted argument to a `JSON` formatted string. Its counterpart is the function [json2xml](conversion-functions-ctl2.md#json2xml).

##### Error states

- If the input is `null`, the function fails with an error.

##### Examples
Example 110. Usage of xml2json

```ctl
xml2json('<employee0><id>1</id><name>Alice</name></employee0><employee1><id>2</id><name>Bob</name></employee1>');
    // Returns {"employee1":{"name":"Bob","id":2},"employee0":{"name":"Alice","id":1}}.
```

##### Compatibility

- The `xml2json(string)` overload is available since **CloverETL 3.1.0**.

##### See also

- [json2xml](conversion-functions-ctl2.md#json2xml)

---
