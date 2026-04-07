<!-- Development > Job elements > Metadata > Records and fields -->

### Records and fields

#### Record types

Record can be seen as a line of data file or as a row of a database table. The record consists of fields. Each field can have different data type. See [Data types in metadata](metadata-records-and-fields.md#data-types-in-metadata).

Each record is of one of the following three types:

##### Delimited

In a **delimited record**, every two adjacent fields are separated from each other by a delimiter and the whole record is terminated by record delimiter as well.

##### Fixed

In a **fixed record** each field has some specified length (size). The length is counted in number of characters.

##### Mixed

In a **mixed record** each field can be separated from each other by a delimiter and also have some specified length (size). The size is counted in number of characters.

This record type is a mixture of both types above. Each individual field may have different properties. Some fields may only have a delimiter, others may have specified size, the rest of them may have both delimiter and size.

#### Data types in metadata

Each metadata field can be of different data type.

The following types of record fields are used in metadata. If you need to see data types used in CTL, see [Data types in CTL2](language-reference-ctl2.md#data-types-in-ctl2).

| Data type | Size[[1]](metadata-records-and-fields.md#metadata-records-and-fields-footnote1) | Values | Default value |
| --- | --- | --- | --- |
| boolean | Represents 1 bit. Its size is not precisely defined. | `true` \| `false` \| `1` \| `0` | `false` \| `0` |
| byte | Depends on the actual data length. | from -128 to 127 | `null` |
| cbyte | Depends on the actual data length and success of compression. | from -128 to 127 | `null` |
| date | 64 bits[[2]](metadata-records-and-fields.md#metadata-data-types-fn01) | Zero date corresponds to 1st January 1970, 00:00:00 GMT. The precision of this data type is 1 ms. | `1970-01-01, 00:00:00 GMT` |
| decimal | Depends on `Length` and `Scale`. (`Length` is the maximum number of all digits. `Scale` is the maximum number of digits after the decimal dot. Default values are 12 and 2, respectively.)[[3]](metadata-records-and-fields.md#metadata-data-types-fn02)[[4]](metadata-records-and-fields.md#metadata-types-fn03) | Range of values depends on `length` and `scale`. For example, `decimal(6,2)` can have values from `-9999.99` to `9999.99`. | `0.00` |
| integer | 32 bits[[3]](metadata-records-and-fields.md#metadata-data-types-fn02) | From `Integer.MIN_VALUE` to `Integer.MAX_VALUE` (according to the Java integer data type): From -231 to 231-1. `Integer.MIN_VALUE` is interpreted as `null`. | `0` |
| long | 64 bits[[3]](metadata-records-and-fields.md#metadata-data-types-fn02) | From `Long.MIN_VALUE` to `Long.MAX_VALUE` (according to the Java long data type): From -263 to 263-1. `Long.MIN_VALUE` is interpreted as `null`. | `0` |
| number | 64 bits[[3]](metadata-records-and-fields.md#metadata-data-types-fn02) | Negative values are from -(2-2-52).21023 to -2-1074, another value is 0, and positive values are from 2-1074 to (2-2-52).21023. Three special values: `NaN`, `-Infinity`, and `Infinity` are defined. | `0.0` |
| string | Depends on the actual data length. Each character from the basic Unicode plane is stored in 16 bits. Characters from other planes require 32 bits per character. | A string takes (number of characters) * 2 bytes of memory (or 4 bytes if you process characters from other Unicode planes). At the same time, no record can take more than `MAX_RECORD_SIZE` of bytes, see [Engine configuration](../admin/designer-configuration.md#engine-configuration). | `null`[[5]](metadata-records-and-fields.md#metadata-records-and-fields-footnote5) |
| variant | Depends on the actual data length. Variant can contain all other data types. | Any value. Variant field can contain any other data type, including list or map. Lists and maps can be nested, forming arbitrary tree structure. | `null` |

| 1 |  Lets you estimate how much memory your records are going to need. To do that, take a look at how many fields your record has, which data types they are and then compare the result to the `MAX_RECORD_SIZE` property (the maximum size of a record in bytes, see [Engine configuration](../admin/designer-configuration.md#engine-configuration)). If your records are likely to have more bytes than that, simply raise the value (otherwise buffer overflow will occur). |
| --- | --- |

| 2 |  Any date can be parsed and formatted using date and time format pattern. See [Date and time format](metadata-records-and-fields.md#date-and-time-format). Parsing and formatting can also be influenced by locale. See [Locale](metadata-records-and-fields.md#locale). |
| --- | --- |

| 3 |  Any numeric data type can be parsed and formatted using numeric format pattern. See [Numeric format](metadata-records-and-fields.md#numeric-format). Parsing and formatting may also be influenced by locale. See [Locale](metadata-records-and-fields.md#locale). |
| --- | --- |

| 4 |  The default `length` and `scale` of a `decimal` are `12` and `2`, respectively. These default values of DECIMAL_LENGTH and DECIMAL_SCALE are contained in the `org.jetel.data.defaultProperties` file and can be changed to other values. |
| --- | --- |

| 5 |  By default, if the value of any `string` metadata field is an empty string, the value is converted to `null` instead of an empty string (`""`). If you want a specific value to be converted to `null`, use the field’s **Null value** property. |
| --- | --- |

For other information about these data types and other data types used in **CloverDX** Transformation Language (CTL), see [Data types in CTL2](language-reference-ctl2.md#data-types-in-ctl2).

#### Data formats

| [Date and time format](metadata-records-and-fields.md#date-and-time-format) |
| --- |
| [Numeric format](metadata-records-and-fields.md#numeric-format) |
| [Boolean format](metadata-records-and-fields.md#boolean-format) |
| [String format](metadata-records-and-fields.md#string-format) |

Sometimes, a **format** may be defined for parsing and formatting data values.

1. Any date can be parsed and/or formatted using Date and time format pattern. See [Date and time format](metadata-records-and-fields.md#date-and-time-format).
   Parsing and formatting can also be influenced by [Locale](metadata-records-and-fields.md#locale) (names of months, order of day or month information, etc.) and [Time Zone](metadata-records-and-fields.md#timezone).
2. Any numeric data type (`decimal`, `integer`, `long`, `number`) can be parsed and/or formatted using the numeric format pattern. See [Numeric format](metadata-records-and-fields.md#numeric-format).
   Parsing and formatting can also be influenced by locale (e.g. decimal dot or decimal comma, etc.). See [Locale](metadata-records-and-fields.md#locale).
3. Any boolean data type can be parsed and formatted using the boolean format pattern. See [Boolean format](metadata-records-and-fields.md#boolean-format).
4. Any string data type can be parsed using the string format pattern. See [String format](metadata-records-and-fields.md#string-format).
> [!NOTE]
> Remember that both Date and time formats and numeric formats are displayed using the system **Locale** value or the **Locale** specified in the `defaultProperties` file, unless another **Locale** is explicitly specified.
>
> For more information on how **Locale** may be changed in the `defaultProperties` see [Engine configuration](../admin/designer-configuration.md#engine-configuration).

##### Date and time format

A formatting string describes how date/time values should be read and written from/to string representation (flat files, human readable output, etc.). Formatting and parsing of dates is also affected by [Locale](metadata-records-and-fields.md#locale) and [Time zone](metadata-records-and-fields.md#timezone).

A format can also specify an engine which **CloverDX** will use by specifying a prefix (see below). There are two built-in *date engines* available: standard Java and third-party Joda ([https://www.joda.org/joda-time](https://www.joda.org/joda-time/)).

| Date engine | Prefix | Default | Description | Example |
| --- | --- | --- | --- | --- |
| *Java* | `java:` | yes - when no prefix is given | Standard Java date implementation. Provides lenient, error-prone and full-featured parsing and writing. It has moderate speed and is generally a good choice unless you need to work with large quantities of date/time fields. For advanced study, please refer to [Java SimpleDateFormat documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/text/SimpleDateFormat.html). | `java:yyyy-MM-dd HH:mm:ss` |
| *Joda* | `joda:` |  | An improved third-party date library. Joda is more strict on input data accuracy when parsing and does not work well with time zones. Joda provides a 20-30% speed increase compared to standard Java.  Joda may be convenient for AS/400 machines.  On the other hand, Joda is unable to read a time zone expressed with any number of `z` letters and/or at least three `Z` letters in a pattern.  For further reading, please visit the project site at [https://www.joda.org/joda-time](https://www.joda.org/joda-time/)). | `joda:yyyy-MM-dd HH:mm:ss` |
| `iso-8601` |  | This format offers support to parse and print dates and times formatted according to ISO 8601. The standard provides more ways of time expression, but usually the format `YYYY-MM-DDThh:mm:ss±hh:mm` is used - especially in the case of data interchange using XML or JSON documents.  For additional information on the standard, see [Wikipedia article on ISO-8601](http://en.wikipedia.org/wiki/ISO_8601) | There are three possible format values:  - `iso-8601:dateTime` for timestamps - `iso-8601:date` for simple dates without time information - `iso-8601:time` for simple times without date information |  |

Please note that actual format strings for Java and Joda are almost 100% compatible with each other - see tables below.
> [!IMPORTANT]
> The format patterns described in this section are used both in metadata as the **Format** property and in CTL.

At first, we provide the list of pattern syntax, the rules and the examples of its usage for Java:

| Letter | Date or time component | Presentation | Examples |
| --- | --- | --- | --- |
| G | Era designator | Text | AD |
| y | Year | Year | 1996; 96 |
| Y | Week year | Year | 2009; 09 |
| M | Month in year | Month | July; Jul; VII; 07; 7 |
| w | Week in year | Number | 27 |
| W | Week in month | Number | 2 |
| D | Day in year | Number | 189 |
| d | Day in month | Number | 10 |
| F | Day of week in month | Number | 2 |
| E | Day in week | Text | Tuesday; Tue |
| u | Day number of week (1 = Monday, …​, 7 = Sunday) | Number | 1 |
| a | AM/PM marker | Text | PM |
| H | Hour in day (0-23) | Number | 0 |
| k | Hour in day (1-24) | Number | 24 |
| K | Hour in am/pm (0-11) | Number | 0 |
| h | Hour in am/pm (1-12) | Number | 12 |
| m | Minute in hour | Number | 30 |
| s | Second in minute | Number | 55 |
| S | Millisecond | Number | 970 |
| z | Time zone | General time zone | Pacific Standard Time; PST; GMT-08:00 |
| Z | Time zone | RFC 822 time zone | -0800 |
| X | Time zone | ISO 8601 time zone | -08; -0800; -08:00 |
| ' | Escape for text/id | Delimiter | (none) |
| '' | Single quote | Literal | ' |

The number of symbol letters you specify also determines the format. For example, if the "zz" pattern results in "PDT", then the "zzzz" pattern generates "Pacific Daylight Time". The following table summarizes these rules:

| Presentation | Processing | Number of pattern letters | Form |
| --- | --- | --- | --- |
| Text | Formatting | 1 - 3 | Short or abbreviated form, if one exists. |
| Text | Formatting | >= 4 | full form |
| Text | Parsing | >= 1 | both forms |
| Year | Formatting | 2 | truncated to 2 digits |
| Year | Formatting | 1 or >= 3 | interpreted as Number. |
| Year | Parsing | 1 | interpreted literally |
| Year | Parsing | 2 | Interpreted relative to the century within 80 years before or 20 years after the time when the `SimpleDateFormat` instance is created. |
| Year | Parsing | >= 3 | interpreted literally |
| Month | Both | 1-2 | interpreted as a Number |
| Month | Parsing | >= 3 | Interpreted as Text (using Roman numbers, abbreviated month name - if exists, or full month name). |
| Month | Formatting | 3 | Interpreted as Text (using Roman numbers, or abbreviated month name - if exists). |
| Month | Formatting | >= 4 | Interpreted as Text (full month name). |
| Number | Formatting | minimum number of required digits | shorter numbers are padded with zeros |
| Number | Parsing | The number of pattern letters is ignored (unless needed to separate two adjacent fields). | any form |
| General time zone | Both | 1-3 | Short or abbreviated form, if it has a name. Otherwise, GMT offset value (GMT[sign][[0]0-23]:[00-59]). |
| General time zone | Both | >= 4 | Full form, if it has a name; otherwise, GMT offset value (GMT[sign][[0]0-23]:[00-59]). |
| General time zone | Parsing | >= 1 | RFC 822 time zone form is allowed. |
| RFC 822 time zone | Both | >= 1 | RFC 822 4-digit time zone format is used ([sign][0-23][00-59]). |
| RFC 822 time zone | Parsing | >= 1 | General time zone form is allowed. |

Examples of date format patterns and resulting dates follow:

| Date and Time Pattern | Result |
| --- | --- |
| "yyyy.MM.dd G 'at' HH:mm:ss z" | 2001.07.04 AD at 12:08:56 PDT |
| "EEE, MMM d, ''yy" | Wed, Jul 4, '01 |
| "h:mm a" | 12:08 PM |
| "hh 'o''clock' a, zzzz" | 12 o’clock PM, Pacific Daylight Time |
| "K:mm a, z" | 0:08 PM, PDT |
| "yyyyy.MMMMM.dd GGG hh:mm aaa" | 02001.July.04 AD 12:08 PM |
| "EEE, d MMM yyyy HH:mm:ss Z" | Wed, 4 Jul 2001 12:08:56 -0700 |
| "yyMMddHHmmssZ" | 010704120856-0700 |
| "yyyy-MM-dd'T'HH:mm:ss.SSSZ" | 2001-07-04T12:08:56.235-0700 |

The described format patterns are used both in metadata as the **Format** property and in CTL.

Now the list of format pattern syntax for Joda follows:

| Symbol | Meaning | Presentation | Examples |
| --- | --- | --- | --- |
| G | Era designator | Text | AD |
| C | Century of era (>=0) | Number | 20 |
| Y | Year of era (>=0) | Year | 1996 |
| y | Year | Year | 1996 |
| x | Week of weekyear | Year | 1996 |
| M | Month of year | Month | July; Jul; 07 |
| w | Week of year | Number | 27 |
| D | Day of year | Number | 189 |
| d | Day of month | Number | 10 |
| e | Day of week | Number | 2 |
| E | Day of week | Text | Tuesday; Tue |
| a | Halfday of day | Text | PM |
| H | Hour of day (0-23) | Number | 0 |
| k | Clockhour of day (1-24) | Number | 24 |
| K | Hour of halfday (0-11) | Number | 0 |
| h | Clockhour of halfday (1-12) | Number | 12 |
| m | Minute of hour | Number | 30 |
| s | Second of minute | Number | 55 |
| S | Fraction of second | Number | 970 |
| z | Time zone | Text | Pacific Standard Time; PST |
| Z | Time zone offset/id | Zone | -0800; -08:00; America/Los_Angeles |
| ' | Escape for text/id | Delimiter | (none) |
| '' | Single quote | Literal | ' |

The number of symbol letters you specify also determines the format. The following table summarizes these rules:

| Presentation | Processing | Number of Pattern Letters | Form |
| --- | --- | --- | --- |
| Text | Formatting | 1 - 3 | Short or abbreviated form, if one exists. |
| Text | Formatting | >= 4 | full form |
| Text | Parsing | >= 1 | both forms |
| Year | Formatting | 2 | truncated to 2 digits |
| Year | Formatting | 1 or >= 3 | interpreted as Number |
| Year | Parsing | >= 1 | interpreted literally |
| Month | Both | 1-2 | interpreted as Number |
| Month | Parsing | >= 3 | Interpreted as Text (using Roman numbers, abbreviated month name - if exists, or full month name). |
| Month | Formatting | 3 | Interpreted as Text (using Roman numbers, or abbreviated month name - if exists). |
| Month | Formatting | >= 4 | interpreted as Text (full month name) |
| Number | Formatting | The minimum number of required digits. | Shorter numbers are padded with zeros. |
| Number | Parsing | >= 1 | any form |
| Zone name | Formatting | 1-3 | short or abbreviated form |
| Zone name | Formatting | >= 4 | full form |
| Time zone offset/id | Formatting | 1 | Offset without a colon between hours and minutes. |
| Time zone offset/id | Formatting | 2 | Offset with a colon between hours and minutes. |
| Time zone offset/id | Formatting | >= 3 | Full textual form like this: "Continent/City". |
| Time zone offset/id | Parsing | 1 | Offset without a colon between hours and minutes. |
| Time zone offset/id | Parsing | 2 | Offset with a colon between hours and minutes. |
> [!IMPORTANT]
> Remember that parsing with any number of "z" letters, as well as parsing with the number of "Z" letters greater than or equal to 3 is not allowed.

See information about data types in metadata and CTL (CTL2):

- [Data Types in Metadata](metadata-records-and-fields.md#data-types-in-metadata)
- [Data Types in CTL2](language-reference-ctl2.md#data-types-in-ctl2)

They are also used in CTL functions. See:

- [Conversion Functions](conversion-functions-ctl2.md)
- [Date Functions](date-functions-ctl2.md)
- [String Functions](string-functions-ctl2.md)

##### Numeric format

| [Scientific notation](metadata-records-and-fields.md#scientific-notation) |
| --- |
| [Binary formats](metadata-records-and-fields.md#binary-formats) |

When a text is parsed as any numeric data type or any numeric data type should be formatted to a text, format pattern can be specified. If no format pattern is specified, **empty pattern** is used and numbers still get parsed and formatted to text.

There are differences in text parsing and number formatting between cases with an **empty pattern** and specified pattern.

1. **No pattern and default locale**
   - Used when a pattern is empty and no locale is set.
   - Javolution `TypeFormat` is used for parsing
   - Formatting uses Java’s `toString()` function (e.g. `Integer.toString()`)
   - Parsing uses Javolution library. It is typically faster than standard Java library but more strict: parsing "10,00" as number fails, parsing "10.00" as integer fails. The expected format for number type is <decimal>{'.'<fraction>}{'E|e'<exponent>}.
2. **A pattern or locale is set (the format from the documentation is used)**
   - DecimalFormat for formatting and parsing.
   - Parsing depends on pattern, but e.g. 10,00 is parsed as 1000 (with empty pattern and US locale) and 10.00 will be parsed as valid integer (with value 10)

Parsing and formatting are locale sensitive.

In **CloverDX**, Java decimal format is used.

| Symbol | Location | Localized? | Meaning |
| --- | --- | --- | --- |
| # | Number | Yes | Digit, zero shows as absent |
| 0 | Number | Yes | Digit |
| . | Number | Yes | Decimal separator or monetary decimal separator |
| - | Number | Yes | Minus sign |
| , | Number | Yes | Grouping separator |
| E | Number | Yes | Separates mantissa and exponent in scientific notation. *Need not be quoted in prefix or suffix.* |
| ; | Subpattern boundary | Yes | Separates positive and negative subpatterns |
| % | Prefix or suffix | Yes | Multiply by 100 and show as percentage |
| ‰ (\u2030) | Prefix or suffix | Yes | Multiply by 1000 and show as per mille value |
| ¤ (\u00A4) | Prefix or suffix | No | Currency sign, replaced by currency symbol. If doubled, replaced by international currency symbol. If present in a pattern, the monetary decimal separator is used instead of the decimal separator. |
| ' | Prefix or suffix | No | Used to quote special characters in a prefix or suffix; for example, "'#'#" formats 123 to "#123". To create a single quote itself, use two in a row: "# o''clock". |

Both prefix and suffix are Unicode characters from \u0000 to \uFFFD, including the margins, but excluding special characters.

Format pattern composes of subpatterns, prefixes, suffixes, etc. in the way shown in the following table:

| Format | Components |
| --- | --- |
| pattern | subpattern{;subpattern} |
| subpattern | {prefix}integer{.fraction}{suffix} |
| prefix | '\\u0000'..'\\uFFFD' - specialCharacters |
| suffix | '\\u0000'..'\\uFFFD' - specialCharacters |
| integer | '#'* '0'* '0' |
| fraction | '0'* '#'* |

Explanation of these symbols follow:

| Notation | Description |
| --- | --- |
| X* | 0 or more instances of X |
| (X \| Y) | either X or Y |
| X..Y | any character from X up to Y, inclusive |
| S - T | characters in S, except those in T |
| {X} | X is optional |
> [!IMPORTANT]
> The grouping separator is commonly used for thousands, but in some countries it separates ten-thousands. The grouping size is a constant number of digits between the grouping characters, such as 3 for 100,000,000 or 4 for 1,0000,0000. If you supply a pattern with multiple grouping characters, the interval between the last one and the end of the integer is the one that is used. So "#,##,###,####" == "######,####" == "##,####,####".

Remember also that formatting is locale sensitive. See the following table in which results are different for different locales:

| Pattern | Locale | Result |
| --- | --- | --- |
| ###,###.### | en.US | 123,456.789 |
| ###,###.### | de.DE | 123.456,789 |
| ###,###.### | fr.FR | 123 456,789 |
> [!NOTE]
> For a deeper look on handling numbers, consult the official Java documentation of [NumberFormat](http://docs.oracle.com/javase/7/docs/api/java/text/NumberFormat.html), and [DecimalFormat](http://docs.oracle.com/javase/7/docs/api/java/text/DecimalFormat.html).
> [!IMPORTANT]
> Space as group separator
> Depending on the locale, if a space is defined as the *group separator*, the exact space character necessary for parsing will vary (e.g., a hard space, char 160).

###### Scientific notation

Numbers in scientific notation are expressed as the product of a mantissa and a power of ten.

For example, `1234` can be expressed as `1.234 x 103`.

The mantissa is often in the range `1.0 <= x < 10.0`, but it’s not required.

Numeric data types can be instructed to format and parse scientific notation only via a pattern. In a pattern, the exponent character immediately followed by one or more digit characters indicates scientific notation.

**Example:** "0.###E0" formats the number 1234 as "1.234E3".

Examples of numeric pattern and results follow:

| Value | Pattern | Result |
| --- | --- | --- |
| 1234 | 0.###E0 | 1.234E3 |
| 12345 | ##0.#####E0[[1]](metadata-records-and-fields.md#numeric-format-fn01) | 12.345E3 |
| 123456 | ##0.#####E0[[1]](metadata-records-and-fields.md#numeric-format-fn01) | 123.456E3 |
| 1234567 | ##0.#####E0[[1]](metadata-records-and-fields.md#numeric-format-fn01) | 1.234567E6 |
| 12345 | #0.#####E0[[2]](metadata-records-and-fields.md#numeric-format-fn02) | 1.2345E4 |
| 123456 | #0.#####E0[[2]](metadata-records-and-fields.md#numeric-format-fn02) | 12.3456E4 |
| 1234567 | #0.#####E0[[2]](metadata-records-and-fields.md#numeric-format-fn02) | 1.234567E6 |
| 0.00123 | 00.###E0[[3]](metadata-records-and-fields.md#numeric-format-fn03) | 12.3E-4 |
| 123456 | ##0.##E0[[4]](metadata-records-and-fields.md#numeric-format-footnote4) | 12.346E3 |

| 1 | #x00A0;Maximum number of integer digits is 3, minimum number of integer digits is 1, maximum is greater than minimum, thus exponent will be a multiplicate of three (maximum number of integer digits) in each of the cases. |
| --- | --- |

| 2 |  Maximum number of integer digits is 2, minimum number of integer digits is 1, maximum is greater than minimum, thus exponent will be a multiplicate of two (maximum number of integer digits) in each of the cases. |
| --- | --- |

| 3 |  Maximum number of integer digits is 2, minimum number of integer digits is 2, maximum is equal to minimum, minimum number of integer digits will be achieved by adjusting the exponent. |
| --- | --- |

| 4 |  Maximum number of integer digits is 3, maximum number of fraction digits is 2, number of significant digits is sum of maximum number of integer digits and maximum number of fraction digits, thus, the number of significant digits is as shown (5 digits). |
| --- | --- |

###### Binary formats

The table below presents a list of available formats:

| Type | Name | Format | Length |
| --- | --- | --- | --- |
| integer | `BIG_ENDIAN` | two’s-complement, big-endian | variable |
| `LITTLE_ENDIAN` | two’s-complement, little-endian |  |  |
| `PACKED_DECIMAL` | [packed decimal](http://www.simotime.com/datapk01.htm) |  |  |
| floating-point | `DOUBLE_BIG_ENDIAN` | IEEE 754, big-endian | 8 bytes |
| `DOUBLE_LITTLE_ENDIAN` | IEEE 754, little-endian |  |  |
| `FLOAT_BIG_ENDIAN` | IEEE 754, big-endian | 4 bytes |  |
| `FLOAT_LITTLE_ENDIAN` | IEEE 754, little-endian |  |  |

The floating-point formats can be used with `numeric` and `decimal` datatypes. The integer formats can be used with `integer` and `long` datatypes. The exception to the rule is the `decimal` datatype, which also supports integer formats (`BIG_ENDIAN`, `LITTLE_ENDIAN` and `PACKED_DECIMAL`). When an integer format is used with the `decimal` datatype, implicit decimal point is set according to the **Scale** attribute. For example, if the stored value is 123456789 and **Scale** is set to 3, the value of the field will be 123456.789.

To use a binary format, create a metadata field with one of the supported datatypes and set the **Format** attribute to the name of the format prefixed with `"BINARY:"`, e.g. to use the `PACKED_DECIMAL` format, create a decimal field and set its **Format** to `"BINARY:PACKED_DECIMAL"` by choosing it from the list of available formats.

For the fixed-length formats (double and float) also the **Size** attribute must be set accordingly.

Currently, binary data formats can only be handled by [ComplexDataReader](complexdatareader.md) and the deprecated FixLenDataReader.

##### Boolean format

The format for boolean data type specified in **Metadata** consists of up to four parts separated from each other by the same delimiter.

This delimiter must also be at the beginning and the end of the **Format** string. On the other hand, the delimiter must not be contained in the values of the boolean field.
> [!IMPORTANT]
> If you do not use the same character at the beginning and the end of the **Format** string, the whole string will serve as a regular expression for the `true` value. The default values (`false|F|FALSE|NO|N|f|0|no|n`) will be the only ones interpreted as `false`.
>
> Values that match neither the **Format** regular expression (interpreted as `true` only) nor the mentioned default values for `false` will be interpreted as error. In such a case, graph would fail.

If we symbolically display the format as:

`/A/B/C/D/`

the meaning of each part is as follows:

1. If the value of the boolean field matches the pattern of the first part (`A`) and does not match the second part (`B`), it is interpreted as `true`.
2. If the value of the boolean field does not match the pattern of the first part (`A`), but matches the second part (`B`), it is interpreted as `false`.
3. If the value of the boolean field matches both the pattern of the first part (`A`) and, at the same time, the pattern of the second part (`B`), it is interpreted as `true`.
4. If the value of the boolean field matches neither the pattern of the first part (`A`), nor the pattern of the second part (`B`), it is interpreted as error. In such a case, the graph fails.

All parts are optional; however, if any of them is omitted, all of the others that are at its right side must also be omitted.

If the second part (`B`) is omitted, the following default values are the only ones that are parsed as boolean `false`:

`false|F|FALSE|NO|N|f|0|no|n`

If there is not any **Format**, the following default values are the only ones that are parsed as boolean `true`:

`true|T|TRUE|YES|Y|t|1|yes|y`

- The third part (`C`) is a formatting string used to express boolean `true` for all matched strings. If the third part is omitted, either the `true` word is used (if the first part (`A`) is complicated regular expression), or the first substring from the first part is used (if the first part is a serie of simple substrings separated by pipe, e.g.: `Iagree|sure|yes|ok` - all these values are formatted as `Iagree`).
- The fourth part (`D`) is a formatting string used to express boolean `false` for all matched strings. If the fourth part is omitted, either the `false` word is used (if the second part (`B`) is complicated regular expression), or the first substring from the second part is used (if the second part is a serie of simple substrings separated by pipe, e.g.: `Idisagree|nope|no` - all these values are formatted as `Idisagree`).

##### String format

Such string pattern is a [regular expression](language-reference-ctl2.md#regular-expressions) that allows or prohibits parsing of a string.

The combo box offers several pre-filled regular expressions.

The last option (**excel:raw**) serves to read more precise values from `.xlsx` files. See documentation on [SpreadsheetDataReader](spreadsheetreader.md).
Example 8. String format
If an input file contains a string field and a **format** property is `\\w{4}` for this field, only the string whose length is 4 will be parsed.

Thus, when a **format** property is specified for a string, **Data policy** may cause a failure of the graph (if **Data policy** is `Strict`).

If **Data policy** is set to `Controlled` or `Lenient`, the records in which this string value matches the specified **format** property are read and the others are skipped (either sent to **Console** or to the rejected port).

#### Locale and locale sensitivity

Various data types (date and time, any numeric values, strings) can be displayed, parsed, or formatted in different ways according to the **Locale** property. For more information, see [Locale](metadata-records-and-fields.md#locale).

Strings can also be influenced by **Locale sensitivity**. See [Locale sensitivity](metadata-records-and-fields.md#locale-sensitivity).

##### Locale

**Locale** represents a specific geographical, political, or cultural region. An operation that requires a **locale** to perform its task is called locale-sensitive and uses the **locale** to tailor information for the user. For example, displaying a number is a locale-sensitive operation as the number should be formatted according to the customs/conventions of the native country, region, or culture of the user.

Each locale code consists of the language code and country arguments.

The language argument is a valid `ISO Language Code`. These codes are the lower-case, two-letter codes as defined by `ISO-639`.

The country argument is a valid `ISO Country Code`. These codes are the upper-case, two-letter codes as defined by `ISO-3166`.

Instead of specifying the format parameter (or together with it), you can specify the locale parameter.

- In strings, instead of setting a format for the whole date field, specify e.g. the German locale. **CloverDX** will then automatically choose the proper date format used in Germany. If the locale is not specified at all, **CloverDX** will choose the default one which is given by your system. In order to learn how to change the default locale, refer to [Engine configuration](../admin/designer-configuration.md#engine-configuration)
- In numbers, on the other hand, there are cases when both the format and locale parameters are meaningful. In the case of specifying the format of decimal numbers, you define the format/pattern with a decimal separator and the locale determines whether the separator is a comma or a dot. If neither the locale or format is specified, the number is converted to string using a universal technique (without checking defaultProperties). If only the format parameter is given, the default locale is used.

See also *[Class Locale](http://docs.oracle.com/javase/7/docs/api/java/util/Locale.html)* for details about locale in Java.
Example 9. Examples of locale en.US or en.GB
For more examples of formatting affected by changing the locale, see [Locale-Sensitive Formatting](metadata-records-and-fields.md#locale-sensitive-formatting).

Dates, too, can have different formats in different locales (even with different countries of the same language). For instance, `March 2, 2009` (in the USA) vs. `2 March 2009` (in the UK).

###### List of all locale

A complete list of the locales supported by **CloverDX** can be found in a separate table below. The locale format as described above is always "language.COUNTRY".

| Locale code | Meaning |
| --- | --- |
| [system default] | Locale determined by your OS |
| ar | Arabic language |
| ar.AE | Arabic - United Arab Emirates |
| ar.BH | Arabic - Bahrain |
| ar.DZ | Arabic - Algeria |
| ar.EG | Arabic - Egypt |
| ar.IQ | Arabic - Iraq |
| ar.JO | Arabic - Jordan |
| ar.KW | Arabic - Kuwait |
| ar.LB | Arabic - Lebanon |
| ar.LY | Arabic - Libya |
| ar.MA | Arabic - Morocco |
| ar.OM | Arabic - Oman |
| ar.QA | Arabic - Qatar |
| ar.SA | Arabic - Saudi Arabia |
| ar.SD | Arabic - Sudan |
| ar.SY | Arabic - Syrian Arab Republic |
| ar.TN | Arabic - Tunisia |
| ar.YE | Arabic - Yemen |
| be | Belorussian language |
| be.BY | Belorussian - Belarus |
| bg | Bulgarian language |
| bg.BG | Bulgarian - Bulgaria |
| ca | Catalan language |
| ca.ES | Catalan - Spain |
| cs | Czech language |
| cs.CZ | Czech - Czech Republic |
| da | Danish language |
| da.DK | Danish - Denmark |
| de | German language |
| de.AT | German - Austria |
| de.CH | German - Switzerland |
| de.DE | German - Germany |
| de.LU | German - Luxembourg |
| el | Greek language |
| el.CY | Greek - Cyprus |
| el.GR | Greek - Greece |
| en | English language |
| en.AU | English - Australia |
| en.CA | English - Canada |
| en.GB | English - Great Britain |
| en.IE | English - Ireland |
| en.IN | English - India |
| en.MT | English - Malta |
| en.NZ | English - New Zealand |
| en.PH | English - Philippines |
| en.SG | English - Singapore |
| en.US | English - United States |
| en.ZA | English - South Africa |
| es | Spanish language |
| es.AR | Spanish - Argentina |
| es.BO | Spanish - Bolivia |
| es.CL | Spanish - Chile |
| es.CO | Spanish - Colombia |
| es.CR | Spanish - Costa Rica |
| es.DO | Spanish - Dominican Republic |
| es.EC | Spanish - Ecuador |
| es.ES | Spanish - Spain |
| es.GT | Spanish - Guatemala |
| es.HN | Spanish - Honduras |
| es.MX | Spanish - Mexico |
| es.NI | Spanish - Nicaragua |
| es.PA | Spanish - Panama |
| es.PR | Spanish - Puerto Rico |
| es.PY | Spanish - Paraguay |
| es.US | Spanish - United States |
| es.UY | Spanish - Uruguay |
| es.VE | Spanish - Venezuela |
| et | Estonian language |
| et.EE | Estonian - Estonia |
| fi | Finnish language |
| fi.FI | Finnish - Finland |
| fr | French language |
| fr.BE | French - Belgium |
| fr.CA | French - Canada |
| fr.CH | French - Switzerland |
| fr.FR | French - France |
| fr.LU | French - Luxembourg |
| ga | Irish language |
| ga.IE | Irish - Ireland |
| he | Hebrew language |
| he.IL | Hebrew - Israel |
| hi.IN | Hindi - India |
| hr | Croatian language |
| hr.HR | Croatian - Croatia |
| id | Indonesian language |
| id.ID | Indonesian - Indonesia |
| is | Icelandic language |
| is.IS | Icelandic - Iceland |
| it | Italian language |
| it.CH | Italian - Switzerland |
| it.IT | Italian - Italy |
| iw | Hebrew language |
| iw.IL | Hebrew - Israel |
| ja | Japanese language |
| ja.JP | Japanese - Japan |
| ko | Korean language |
| ko.KR | Korean - Republic of Korea |
| lt | Lithuanian language |
| lt.LT | Lithuanian language - Lithuania |
| lv | Latvian language |
| lv.LV | Latvian language - Latvia |
| mk | Macedonian language |
| mk.MK | Macedonian - The Former Yugoslav Republic of Macedonia |
| ms | Malay language |
| ms.MY | Malay - Burmese |
| mt | Maltese language |
| mt.MT | Maltese - Malta |
| nl | Dutch language |
| nl.BE | Dutch - Belgium |
| nl.NL | Dutch - Netherlands |
| no | Norwegian language |
| no.NO | Norwegian - Norway |
| pl | Polish language |
| pl.PL | Polish - Poland |
| pt | Portuguese language |
| pt.BR | Portuguese - Brazil |
| pt.PT | Portuguese - Portugal |
| ro | Romanian language |
| ro.RO | Romanian - Romany |
| ru | Russian language |
| ru.RU | Russian - Russian Federation |
| sk | Slovak language |
| sk.SK | Slovak - Slovakia |
| sl | Slovenian language |
| sl.SI | Slovenian - Slovenia |
| sq | Albanian language |
| sq.AL | Albanian - Albania |
| sr | Serbian language |
| sr.BA | Serbian - Bosnia and Herzegowina |
| sr.CS | Serbian - Serbia and Montenegro |
| sr.ME | Serbian - Serbia (Cyrillic, Montenegro) |
| sr.RS | Serbian - Serbia (Latin, Serbia) |
| sv | Swedish language |
| sv.SE | Swedish - Sweden |
| th | Thai language |
| th.TH | Thai - Thailand |
| tr | Turkish language |
| tr.TR | Turkish - Turkey |
| uk | Ukrainian language |
| uk.UA | Ukrainian - Ukraine |
| vi.VN | Vietnamese - Vietnam |
| zh | Chinese language |
| zh.CN | Chinese - China |
| zh.HK | Chinese - Hong Kong |
| zh.SG | Chinese - Singapore |
| zh.TW | Chinese - Taiwan |

##### Locale sensitivity

**Locale sensitivity** can be applied to the `string` data type only. What is more, the **Locale** has to be specified either for the field or the whole record.

Field settings override the **Locale sensitivity** specified for the whole record.

Values of **Locale sensitivity** are the following:

- `base_letter_sensitivity`
  Does not distinguish different cases of letters nor letters with diacritic marks.
- `accent_sensitivity`
  Does not distinguish different cases of letters. It distinguishes letters with diacritic marks.
- `case_sensitivity`
  Distinguishes different cases of letters and letters with diacritic marks. It does not distinguish the letter encoding ("\u00C0" equals to "A\u0300").
- `identical_sensitivity`
  Distinguishes the letter encoding ("\u00C0" equals to "A\u0300").

#### Time zone

**Time zone** is used to specify the time offset used for parsing dates and writing dates as text.

Time zone can either be specified using a time zone ID, e.g. `"America/Los_Angeles"`, which also takes daylight saving time into account, or using an absolute offset, e.g. `"GMT+10"`.

A time zone usually complements a [Date and time format](metadata-records-and-fields.md#date-and-time-format). In such a case, the time zone specification must match the format, i.e. if the format starts with `"joda:"`, the time zone must also be prefixed `"joda:"`, and vice versa. Both Java and Joda time zone can be selected at the same time using a semicolon-separated list, e.g. `"java:America/Los_Angeles;joda:America/Los_Angeles"`.

Note that if an invalid string is specified as the Java time zone ID, no exception is thrown and Java uses the default "GMT" time zone (unlike Joda, which throws an exception).
> [!NOTE]
> If the **Time zone** is not explicitly specified, **CloverDX** will use the system default time zone.
>
> The default time zone can be changed in the `defaultProperties` file or via the CloverDX Server. For more information, see [Engine configuration](../admin/designer-configuration.md#engine-configuration).

For further reading about time and time zones, see [java.util.TimeZone](http://docs.oracle.com/javase/7/docs/api/java/util/TimeZone.html), [org.joda.time.DateTimeZone](https://www.joda.org/joda-time/apidocs/org/joda/time/DateTimeZone.html) and [http://www.odi.ch/prog/design/datetime.php](http://www.odi.ch/prog/design/datetime.php).

#### Autofilling functions

There is a set of functions you can use to fill records with some special, pre-defined values (e.g. name of the file you are reading, size of the data source etc.). These functions are available in **Metadata Editor** ****Details pane** ****Advanced properties**

The following functions are supported by most **Reader**s, except **ParallelReader**, **QuickBaseRecordReader**, and **QuickBaseQueryReader**. The function fills in the value into the metadata field just on the output port of the **Reader**. The other component that does not read the data source would not know the value to be filled in.

The `ErrCode` and `ErrText` functions can be used only in the following components: **DBExecute** and [DatabaseWriter](dboutputtable.md).

Note a special case of `true` autofilling value in the **MultiLevelReader** component.

- `default_value` - a value of a corresponding data type specified as the **Default** property is set if no value is read by the **Reader**.
- `global_row_count`. This function counts the records of all sources that are read by one **Reader**. It fills the specified field of any numeric data type in the edge(s) with integer numbers sequentially. The records are numbered in the same order they are sent out through the output port(s). The numbering starts at 0. However, if data records are read from more data sources, the numbering goes continuously throughout all data sources. If an edge does not include such a field (in **XMLExtract**, e.g.), corresponding numbers are skipped and the numbering continues.
- `global_row_incl_err_count`. This function is similar to `global_row_count`, but counts error records (if exist) as well.
- `source_row_count`. This function counts the records of each source, read by one **Reader**, separately. It fills the specified field of any numeric data type in the edge(s) with integer numbers sequentially. The records are numbered in the same order they are sent out through the output port(s). The records of each source file are numbered independently on the other sources. The numbering starts at 0 for each data source. If an edge does not include such a field (in **XMLExtract**, e.g.), corresponding numbers are skipped. And the numbering continues.
- `source_row_incl_err_count`. This function is similar to `source_row_count`, but counts error records (if exist) as well.
- `metadata_row_count`. This function counts the records of all sources that are both read by one **Reader** and sent to edges with the same metadata assigned. It fills the specified field of any numeric data type in the edge(s) with integer numbers sequentially. The records are numbered in the same order they are sent out through the output port(s). The numbering starts at 0. However, if data records are read from more data sources, the numbering goes continuously throughout all data sources.
- `metadata_source_row_count`. This function counts the records of each source that are both read by one **Reader** and sent to edges with the same metadata assigned. It fills the specified field of any numeric data type in the edge(s) with integer numbers sequentially. The records are numbered in the same order they are sent out through the output port(s). The records of each source file are numbered independently on the other sources. The numbering starts at 0 for each data source.
- `source_name`. This function fills the specified record fields of string data type with the name of data source from which records are read.
- `source_timestamp`. This function fills the specified record fields of date data type with the timestamp corresponding to the data source from which records are read. Field formatting depends on field "Metadata / Data Formats" settings. This function cannot be used in [DatabaseReader](dbinputtable.md).
- `source_size`. This function fills the specified record fields of any numeric data type with the size of data source from which records are read. This function cannot be used in [DatabaseReader](dbinputtable.md).
- `row_timestamp`. This function fills the specified record fields of date data type with the time when individual records are read. Field formatting depends on field "Metadata / Data Formats" settings.
- `reader_timestamp`. This function fills the specified record fields of date data type with the time when the reader starts reading. The value is the same for all records read by the reader. Field formatting depends on field "Metadata / Data Formats" settings.
- `ErrCode`. This function fills the specified record fields of integer data type with error codes returned by the component. It can be used by [DatabaseWriter](dboutputtable.md) and **DBExecute** components only.
- `ErrText`. This function fills the specified record fields of string data type with error messages returned by component. It can be used by [DatabaseWriter](dboutputtable.md) and **DBExecute** components only.
- `sheet_name`. This function fills the specified record fields of string data type with the name of the sheet of input XLS(X) file from which data records are read. It can be used by the **SpreadsheetDataReader** component only.
