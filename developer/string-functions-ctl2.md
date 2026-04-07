<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > String functions -->

### String functions

#### List of functions

| [byteAt](string-functions-ctl2.md#byteat) |
| --- |
| [charAt](string-functions-ctl2.md#charat) |
| [chop](string-functions-ctl2.md#chop) |
| [codePointAt](string-functions-ctl2.md#codepointat) |
| [codePointLength](string-functions-ctl2.md#codepointlength) |
| [codePointToChar](string-functions-ctl2.md#codepointtochar) |
| [concat](string-functions-ctl2.md#concat) |
| [concatWithSeparator](string-functions-ctl2.md#concatwithseparator) |
| [contains](string-functions-ctl2.md#contains) |
| [countChar](string-functions-ctl2.md#countchar) |
| [cut](string-functions-ctl2.md#cut) |
| [editDistance](string-functions-ctl2.md#editdistance) |
| [endsWith](string-functions-ctl2.md#endswith) |
| [escapeUrl](string-functions-ctl2.md#escapeurl) |
| [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment) |
| [escapeXML](string-functions-ctl2.md#escapexml) |
| [find](string-functions-ctl2.md#find) |
| [formatMessage](string-functions-ctl2.md#formatmessage) |
| [getAlphanumericChars](string-functions-ctl2.md#getalphanumericchars) |
| [getComponentProperty](string-functions-ctl2.md#getcomponentproperty) |
| [getFileExtension](string-functions-ctl2.md#getfileextension) |
| [getFileName](string-functions-ctl2.md#getfilename) |
| [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension) |
| [getFilePath](string-functions-ctl2.md#getfilepath) |
| [getUrlHost](string-functions-ctl2.md#geturlhost) |
| [getUrlPath](string-functions-ctl2.md#geturlpath) |
| [getUrlPort](string-functions-ctl2.md#geturlport) |
| [getUrlProtocol](string-functions-ctl2.md#geturlprotocol) |
| [getUrlQuery](string-functions-ctl2.md#geturlquery) |
| [getUrlRef](string-functions-ctl2.md#geturlref) |
| [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo) |
| [indexOf](string-functions-ctl2.md#indexof) |
| [isAscii](string-functions-ctl2.md#isascii) |
| [isBlank](string-functions-ctl2.md#isblank) |
| [isDate](string-functions-ctl2.md#isdate) |
| [isDecimal](string-functions-ctl2.md#isdecimal) |
| [isEmpty(string)](string-functions-ctl2.md#isempty) |
| [isInteger](string-functions-ctl2.md#isinteger) |
| [isLong](string-functions-ctl2.md#islong) |
| [isNumber](string-functions-ctl2.md#isnumber) |
| [isUnicodeNormalized](string-functions-ctl2.md#isunicodenormalized) |
| [isUrl](string-functions-ctl2.md#isurl) |
| [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint) |
| [join](string-functions-ctl2.md#join) |
| [lastIndexOf](string-functions-ctl2.md#lastindexof) |
| [left](string-functions-ctl2.md#left) |
| [length(string)](string-functions-ctl2.md#length) |
| [lowerCase](string-functions-ctl2.md#lowercase) |
| [lpad](string-functions-ctl2.md#lpad) |
| [matches](string-functions-ctl2.md#matches) |
| [matchGroups](string-functions-ctl2.md#matchgroups) |
| [metaphone](string-functions-ctl2.md#metaphone) |
| [normalizeDecimal](string-functions-ctl2.md#normalizedecimal) |
| [normalizePath](string-functions-ctl2.md#normalizepath) |
| [normalizeWhitespaces](string-functions-ctl2.md#normalizewhitespaces) |
| [NYSIIS](string-functions-ctl2.md#nysiis) |
| [properCase](string-functions-ctl2.md#propercase) |
| [randomString](string-functions-ctl2.md#randomstring) |
| [randomUUID](string-functions-ctl2.md#randomuuid) |
| [removeBlankSpace](string-functions-ctl2.md#removeblankspace) |
| [removeDiacritic](string-functions-ctl2.md#removediacritic) |
| [removeNonAscii](string-functions-ctl2.md#removenonascii) |
| [removeNonPrintable](string-functions-ctl2.md#removenonprintable) |
| [replace](string-functions-ctl2.md#replace) |
| [reverse(string)](string-functions-ctl2.md#reverse) |
| [right](string-functions-ctl2.md#right) |
| [rpad](string-functions-ctl2.md#rpad) |
| [soundex](string-functions-ctl2.md#soundex) |
| [split](string-functions-ctl2.md#split) |
| [startsWith](string-functions-ctl2.md#startswith) |
| [substring](string-functions-ctl2.md#substring) |
| [toProjectUrl](string-functions-ctl2.md#toprojecturl) |
| [translate](string-functions-ctl2.md#translate) |
| [trim](string-functions-ctl2.md#trim) |
| [unescapeUrl](string-functions-ctl2.md#unescapeurl) |
| [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment) |
| [unescapeXML](string-functions-ctl2.md#unescapexml) |
| [unicodeNormalize](string-functions-ctl2.md#unicodenormalize) |
| [upperCase](string-functions-ctl2.md#uppercase) |
| [validateCreditCard](string-functions-ctl2.md#validatecreditcard) |
| [validateEmail](string-functions-ctl2.md#validateemail) |
| [validatePhoneNumber](string-functions-ctl2.md#validatephonenumber) |

Some functions work with strings.

In the functions that work with strings, sometimes a format pattern of a date or any number must be defined.

- For detailed information about date formatting and/or parsing, see [Date and Time Format](metadata-records-and-fields.md#date-and-time-format).
- For detailed information about formatting and/or parsing of any numeric data type see [Numeric Format](metadata-records-and-fields.md#numeric-format).
- For detailed information about locale see [Locale](metadata-records-and-fields.md#locale).
> [!NOTE]
> Remember that numeric and date formats are displayed using the system value **Locale** or **Locale** specified in the `defaultProperties` file, unless other **Locale** is explicitly specified.
>
> For more information on how **Locale** may be changed in the `defaultProperties`, see [Engine configuration](../admin/designer-configuration.md#engine-configuration).

Here we provide the list of the functions:

#### byteAt

```ctl
integer byteAt(byte arg, integer index);
```

The function `byteAt` returns the byte on the specified position.

The `arg` is an input `byte` array.

The `index` defines the position in the `arg`. The first item has `index` equal to `0`.

If the `index` is out of bound, the function fails.

If any of the arguments is `null`, the function fails.

**Compatibility**

The `byteAt()` function is available since **CloverETL 4.0.0**.
Example 156. Usage of byteAt
Let `b = hex2byte("6d75736b726174")`. The function `byteAt(b, 0)` returns `0x6d`, which corresponds to `109`.

The function `byteAt(b, -1)` fails.

The function `byteAt(b, null)` fails.

The function `byteAt(null, 0)` fails.

**See also:**[bitAnd](mathematical-functions-ctl2.md#bitand), [bitIsSet](mathematical-functions-ctl2.md#bitisset), [bitSet](mathematical-functions-ctl2.md#bitset), [bitLShift](mathematical-functions-ctl2.md#bitlshift), [bitNegate](mathematical-functions-ctl2.md#bitnegate), [bitOr](mathematical-functions-ctl2.md#bitor), [bitRShift](mathematical-functions-ctl2.md#bitrshift), [bitSet](mathematical-functions-ctl2.md#bitset), [bitXor](mathematical-functions-ctl2.md#bitxor), [charAt](string-functions-ctl2.md#charat)

#### charAt

```ctl
string charAt(string arg, integer index);
```

The `charAt()` function returns the character from `arg` which is located at the given `index`.

The function works only for indexes between `0` and `length of input - 1`, otherwise it fails with an error.

For `null` input and `empty string` input the function fails with an error.

**Compatibility**

The `charAt(string,integer)` function is available since **CloverETL 3.0.0**.
Example 157. Usage of charAt
The function `charAt("ABC", 1)` returns `B`.

The function `charAt("ABC", 0)` returns `A`.

The function `charAt("ABC", -1)` fails with an error.

The function `charAt("ABC", 3)` fails with an error.

**See also:**[byteAt](string-functions-ctl2.md#byteat), [codePointAt](string-functions-ctl2.md#codepointat), [substring](string-functions-ctl2.md#substring)

#### chop

```ctl
string chop(string arg);
string chop(string arg, string regexp);
```

The `chop()` function removes the line feed and the carriage return characters or characters corresponding to the provided regular pattern from the string.

For `null` input the function fails with an error.

If the input is empty string, the function returns empty string.

If the `regexp` is `null`, the function fails with an error.

**Compatibility**

The `chop(string)` and `chop(string,string)` function is available since **CloverETL 3.0.0**.
Example 158. Usage of chop
The function `chop("ab\n z")` returns `ab z`. The `\n` means line feed (char `0x0A`). The character `0x0A` can be added to string either from string read by any of readers, or set up using functions `hex2byte` and `byte2str`.

The function `chop("book and pencil", "and")` returns `book pencil`.

The function `chop("A quick brown fox jumps.", "[a-y]{5}")` returns `A fox.`

**See also:**[matches](string-functions-ctl2.md#matches), [matchGroups](string-functions-ctl2.md#matchgroups), [substring](string-functions-ctl2.md#substring)

#### codePointAt

```ctl
integer codePointAt(string str, integer index);
```

The function `codePointAt()` returns code of a Unicode character from the given position in the string `str`.

The `str` parameter contains string with Unicode characters. If `str` is `null`, the function fails.

The `index` parameter specifies a position of the character in the string `str`. The first character has index 0.

If the `index` parameter is `null`, the function fails. If the `index` parameter is out of range of the string (*negative* or *greater than or equal to* length of string), the function fails.

**Compatibility**

The `codePointAt(string,integer)` function is available since **CloverETL 4.0.0-M1**.
Example 159. Usage of codePointAt
The function `codePointAt("enseñar", 0)` returns `101`.

The function `codePointAt("enseñar", 4)` returns `241`.

The function `codePointAt("enseñar", -1)` fails.

The function `codePointAt("enseñar", 10)` fails.

The function `codePointAt("enseñar", null)` fails.

The function `codePointAt(null, 2)` fails.

**See also:**[charAt](string-functions-ctl2.md#charat), [codePointToChar](string-functions-ctl2.md#codepointtochar), [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint)

#### codePointLength

```ctl
integer codePointLength(integer code);
```

The function `codePointLength()` returns number of char values needed to encode the Unicode character `code`.

If `code` is *greater than or equal to*`0x10000`, the function returns `2`. Otherwise returns `1`. Invalid codes are not checked. If validation is needed, use the `isValidCodePoint` function.

The parameter `code` is Unicode code point. If the `code` is `null`, the function fails.

**Compatibility**

The `codePointLength(integer)` function is available since **CloverETL 4.0.0-M1**.
Example 160. Usage of codePointLength
The function `codePointLength(0x41)` returns `1`.

The function `codePointLength(0x10300)` returns `2`.

**See also:**[codePointAt](string-functions-ctl2.md#codepointat), [codePointToChar](string-functions-ctl2.md#codepointtochar), [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint)

#### codePointToChar

```ctl
string codePointToChar(integer code);
```

The function `codePointToChar()` converts Unicode code to character.

The parameter contains `code` of the character.

If the `code` is `null`, *negative* or *greater than*`0x10FFFF`, the function fails.

**Compatibility**

The `codePointToChar(integer)` function is available since **CloverETL 4.0.0-M1**.
Example 161. Usage of codePointToChar
The function `codePointToChar(65)` returns `A`.

The function `codePointToChar(0x3B1)` returns `α`.

The function `codePointToChar(0x10300)` returns `𐌀`.

The function `codePointToChar(-1)` fails.

The function `codePointToChar(null)` fails.

The function `codePointToChar(0x110000)` fails.

**See also:**[codePointAt](string-functions-ctl2.md#codepointat), [codePointLength](string-functions-ctl2.md#codepointlength), [isUnicodeNormalized](string-functions-ctl2.md#isunicodenormalized)

#### concat

```ctl
string concat(string arg1, string ..., string argN);
```

The function `concat()` returns concatenation of the strings.

The `concat` function accepts unlimited number of arguments of the string data type. You can also concatenate these arguments using plus signs, but this function is faster for more than two arguments.

`Null` value of arguments are replaced with string 'null' in concatenated string.
> [!NOTE]
> Concatenation of more strings with the `concat()` function is faster than concatenation with `+` operator.

**Compatibility**

The `concat(string, …)` function is available since **CloverETL 3.0.0**.
Example 162. Usage of concat
The function `concat("abc", "def", "ghi")` returns `abcdefghi`.

The function `concat("abc", null, "ghi")` returns `abcnullghi`.

**See also:**[concatWithSeparator](string-functions-ctl2.md#concatwithseparator), [join](string-functions-ctl2.md#join), [cut](string-functions-ctl2.md#cut), [substring](string-functions-ctl2.md#substring)

#### concatWithSeparator

```ctl
string concatWithSeparator(string separator, string arg1, string ..., string argN);
```

The function `concatWithSeparator()` joins parameters `arg1` to `argN` using `separator`.

The `separator` parameter defines a string to be used as a separator in the concatenated string. If the `separator` parameter is `null`, the function fails.

The parameters `arg1` to `argN` contain strings to be concatenated. Parameters to be concatenated having `null` values are omitted.
> [!NOTE]
> The `concat()` and `concatWithSeparator()` functions handle `null` strings differently.

**Compatibility**

The `concatWithSeparator(string,string,…)` function is available since **CloverETL 4.0.0-M1**.
Example 163. Usage of concatWithSeparator
The function `concatWithSeparator(",", "coffee", "milk", "chocolate")` returns `coffee,milk,chocolate`.

The function `concatWithSeparator("", "bottle", "neck")` returns `bottleneck`.

The function `concatWithSeparator("_", "bash", null, "tcsh")` returns `bash_tcsh`.

The function `concatWithSeparator(null, "")` fails.

The function `concatWithSeparator(" ", "tabular", "itemize")`*returns `tabular`*`itemize`.

The function `concatWithSeparator("-", null)` returns *empty string*.

**See also:**[concat](string-functions-ctl2.md#concat), [join](string-functions-ctl2.md#join), [split](string-functions-ctl2.md#split)

#### contains

```ctl
boolean contains(string input, string substring);
```

The function `contains()` returns true if the `input` string contains a `substring`. Otherwise the function returns `false`.

If the parameter `input` is `null`, the function returns `false`.

If the parameter `substring` is `null`, the function fails.

**Compatibility**

The `contains(string,string)` function is available since **CloverETL 4.0.0-M1**.
Example 164. Usage of contains
The function `contains("woodcutting", "wood")` returns `true`.

The function `contains("elm", "coffee")` returns `false`.

The function `contains(null, "pine")` returns `false`.

The function `contains("oak", "")` returns `true`.

The function `contains("", "")` returns `true`.

The function `contains("spruce", null)` fails.

**See also:**[endsWith](string-functions-ctl2.md#endswith), [startsWith](string-functions-ctl2.md#startswith), [substring](string-functions-ctl2.md#substring)

#### countChar

```ctl
integer countChar(string arg, string character);
```

The `countChar()` returns the number of occurrences of the character specified as the second argument in the string specified as the first argument.

If one of the given arguments is `null` or an empty string, the function fails with an error.

**Compatibility**

The `countChar(string,string)` function is available since **CloverETL 3.0.0**.
Example 165. Usage of countChar
The function `countChar("ALABAMA", "A")` returns `4`.

The function `countChar("Alabama", "a")` returns `3`

**See also:**[length(string)](string-functions-ctl2.md#length)

#### cut

```ctl
string[] cut(string arg, integer[] indices);
```

The `cut()` function returns a list of strings which are substrings of the original string specified in the first argument.

The second argument (`indices`) specifies rules on how the first argument is cut. The number of elements of the list specified as the second argument must be even. The integers in the list serve as position (each number in the odd position) and length (each number in the even position). Substrings of the specified length are taken from the string specified as the first argument starting from the specified position (excluding the character at the specified position).

If the first argument is `null` or an empty string, the function fails with an error.

**Compatibility**

The `cut(string,integer[])` function is available since **CloverETL 3.0.0**.
Example 166. Usage of cut The function `cut("somestringasanexample",[2,3,1,5])` returns `["mes","omest"]`.
**See also:**[matchGroups](string-functions-ctl2.md#matchgroups)

#### editDistance

```ctl
integer editDistance(string arg1, string arg2);
integer editDistance(string arg1, string arg2, string locale);
integer editDistance(string arg1, string arg2, integer strength);
integer editDistance(string arg1, string arg2, integer strength, string locale);
integer editDistance(string arg1, string arg2, integer strength, integer maxDifference);
integer editDistance(string arg1, string arg2, integer strength, integer maxDifference);
integer editDistance(string arg1, string arg2, integer strength, string locale, integer maxDifference);
```

The `editDistance()` function compares two string arguments to each other.

```ctl
integer editDistance(string arg1, string arg2);
```

The strength of comparison is 4 by default, the default value of locale for comparison is the system value and the maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the two arguments to the other. However, when the function is being executed, if it counts that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see another version of the `editDistance()` function below - the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance) function.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.

**Compatibility**

The `editDistance()` function is available since **CloverETL 3.0.0**.
Example 167. Usage of editDistance 1
The function `editDistance("see", "sea")` returns `1`.

The function `editDistance("bike", "bill")` returns `2`.

The function `editDistance("age", "get")` returns `2`.

The function `editDistance("computer", "preposition")` returns `4`.

**See also:**[metaphone](string-functions-ctl2.md#metaphone), [NYSIIS](string-functions-ctl2.md#nysiis), [soundex](string-functions-ctl2.md#soundex)

```ctl
integer editDistance(string arg1, string arg2, string locale);
```

The `editDistance()` compares two string arguments to each other using the specified locale.

The function accepts two strings that will be compared to each other and the third argument that is the [Locale](metadata-records-and-fields.md#locale) that will be used for comparison. The default strength of comparison is 4. The maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other. However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see another version of the `editDistance()` function below - the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance) function.

If one or both of the input strings to compare are empty strings or `null` function fails with an error.
Example 168. Usage of editDistance 2
The function `editDistance("âgé", "âge", "en.US")` returns `1`.

The function `editDistance("âgé", "âge", "fr.FR")` returns `1`.

```ctl
integer editDistance(string arg1, string arg2, integer strength);
```

The `editDistance()` compare two string to each other using the specified strength of comparison.

The function accepts two strings that will be compared to each other and the third (integer) that is the strength of comparison. The default locale that will be used for comparison is the system value. The maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other. However, when the function is being executed, if it counts that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see another version of the `editDistance()` function below - the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance) function.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 169. Usage of editDistance 3
The function `editDistance("computer", "preposition", 4)` returns `4`.

The function `editDistance("computer", "preposition", 7)` fails.

The function `editDistance("âgé", "âge", 2)` returns `0`.

The function `editDistance("âgé", "âge", 3)` returns `1`.

```ctl
integer editDistance(string arg1, string arg2, integer strength, string locale);
```

The `editDistance()` function compares two strings to each other using specified strength of comparison and locale.

The function accepts two strings that will be compared to each other, the third argument that is the strength of comparison and the fourth argument that is the [Locale](metadata-records-and-fields.md#locale) that will be used for comparison. The maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other. However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see another version of the `editDistance()` function below - the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance) function.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 170. Usage of editDistance 4
The function `editDistance("âgé", "âge", 2, "en.US")` returns `1`.

The function `editDistance("âgé", "âge", 2, "fr.FR")` returns `0`.

```ctl
integer editDistance(string arg1, string arg2, string locale, integer maxDifference);
```

The `editDistance()` compares two strings to each other using specified locale and maxDifference.

The function accepts two strings that will be compared to each other, the third argument that is the [Locale](metadata-records-and-fields.md#locale) that will be used for comparison and the fourth argument that is the maximum difference. The strength of comparison is 4 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other. However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see another version of the `editDistance()` function below - the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance) function.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 171. Usage of editDistance 5 The function `editDistance("bike", "bicycle", "en.US", 2)` returns `2`.

```ctl
integer editDistance(string arg1, string arg2, integer strength, integer maxDifference);
```

The `editDistance()` compares two strings to each other using specified strength of comparison and maximum difference.

The function accepts two strings that will be compared to each other and two others. These are the strength of comparison (third argument) and the maximum difference (fourth argument). The locale is the default system value.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other. However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see another version of the `editDistance()` function below - the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance) function.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 172. Usage of editDistance 6
`editDistance("OAK", "oak", 3, 1)` returns `0`.

`editDistance("OAK", "oak", 4, 3)` returns `3`.

`editDistance("OAK", "oak", 4, 4)` returns `3`

```ctl
integer editDistance(string arg1, string arg2, integer strength, string locale, integer maxDifference);
```

The `editDistance()` function compares two strings using the specified strength of comparison, locale and maximum difference.

The first two arguments are strings to be compared.

The third argument (integer number) specifies the strength of comparison. It can have any value from 1 to 4.

If it is 4 (identical comparison), it means that only identical letters are considered equal. In the case of 3 (tertiary comparison), it means that upper and lower cases are considered equal. If it is 2 (secondary comparison), it means that letters with diacritical marks are considered equal. Lastly, if the strength of comparison is 1 (primary comparison), it means that even the letters with some specific signs are considered equal. In other versions of the `editDistance()` function where this strength of comparison is not specified, the number 4 is used as the default strength (see above).

The fourth argument is the string data type. It is the [Locale](metadata-records-and-fields.md#locale) that serves for comparison. If no locale is specified in other versions of the `editDistance()` function, its default value is the system value (see above).

The fifth argument (integer number) means the number of letters that should be changed to transform one of the first two arguments to the other. If another version of the `editDistance()` function does not specify this maximum difference, the default maximum difference is number 3 (see above).

The function returns the number of letters that should be changed to transform one of the first two arguments to the other. However, when the function is being executed, if it counts that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

Actually the function is implemented for the following locales: CA, CZ, ES, DA, DE, ET, FI, FR, HR, HU, IS, IT, LT, LV, NL, NO, PL, PT, RO, SK, SL, SQ, SV, TR. These locales have one thing in common: they all contain language-specific characters. A complete list of these characters can be examined in [CTL2 Appendix - List of National-specific Characters](ctl2-appendix.md).

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 173. Usage of editDistance 7 The function `editDistance("OAK", "oak", 4, "en.US", 1)` returns `2`.
#### endsWith

```ctl
boolean endsWith(string str, string substr);
```

The function `endsWith()` checks whether the string `str` ends with the `substr` string.

If the parameter `str` is `null`, the function returns `false`.

If the parameter `substr` is `null`, the function fails.

**Compatibility**

The `endsWith(string,string)` function is available since **CloverETL 4.0.0-M1**.
Example 174. Usage of endsWith
The function `endsWith("products.txt", ".txt")` returns `true`.

The function `endsWith("tree.png", ".ico")` returns `false`.

The function `endsWith(null, ".pdf")` returns `false`.

The function `endsWith("dog.ogg", null)` fails.

**See also:**[contains](string-functions-ctl2.md#contains), [startsWith](string-functions-ctl2.md#startswith)

#### escapeUrl

```ctl
string escapeUrl(string arg);
```

The `escapeUrl()` function escapes illegal characters within components of a specified URL (for the URL component description, see [isUrl](string-functions-ctl2.md#isurl)). Illegal characters must be escaped by a percent (`%`) symbol, followed by the two-digit hexadecimal representation (case-insensitive) of the ISO-Latin code point for the character, e.g. `%20` is the escaped encoding for the US-ASCII space character.

The function accepts a valid URL only. For an invalid URL, empty string or `null` input, the function fails with an error.

**Compatibility**

The `escapeUrl(string)` function is available since **CloverETL 3.1.0**.
Example 175. Usage of escapeUrl The function `escapeUrl("http://www.example.com/The URL")` returns `http://www.example.com/The%20URL`
**See also:**[escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment), [isUrl](string-functions-ctl2.md#isurl), [unescapeUrl](string-functions-ctl2.md#unescapeurl), [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment)

#### escapeUrlFragment

```ctl
string escapeUrlFragment(string input);
string escapeUrlFragment(string input, string encoding);
```

The `escapeUrlFragment` function escapes potentially obtrusive characters.

The `input` parameter is a string to be escaped. If the `input` is `null`, the `null` is returned.

The optional parameter `encoding` enables to change encoding of the result string. The default encoding is UTF-8. If the encoding is `null` function fails.

**Compatibility**

The `escapeUrlFragment(string)` function is available since **CloverETL 4.0.0-M1**.
Example 176. Usage of escapeUrlFragment
The function `escapeUrlFragment("The URL")` returns `The+URL`.

The function `escapeUrlFragment("Žlutý kůň")` returns `%C5%BDlut%C3%BD+k%C5%AF%C5%88`.

The function `escapeUrlFragment("1+1=2")` returns `1%2B1%3D2`.

The function `escapeUrlFragment(null)` returns `null`.

The function `escapeUrlFragment("Žlutý kůň", "utf-8")` returns `%C5%BDlut%C3%BD+k%C5%AF%C5%88`.

The function `escapeUrlFragment("Žlutý kůň", "iso-8859-2")` returns `%AElut%FD+k%F9%F2`.

The function `escapeUrlFragment("abc", null)` fails with an error.

**See also:**[escapeUrl](string-functions-ctl2.md#escapeurl), [isUrl](string-functions-ctl2.md#isurl), [unescapeUrl](string-functions-ctl2.md#unescapeurl), [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment)

#### escapeXML

```ctl
string escapeXML(string input);
```

The `escapeXML` function replaces all occurence of XML special entities with their escaped alternatives (XML entities).

By using the **escapeXML** function, you can safely incorporate user-generated content, external data, or any other string values into your XML documents without worrying about invalid XML syntax or potential security issues like XML injection attacks.

List of reserved characters: `' , ", &, <, >`

**Compatibility**

The `escapeXML(string)` function is available since **CloverDX 6.4.0**.
Example 177. Usage of escapeXML
The function `escapeXML(<element name="&myname;">)` returns `&lt;element name=&quot;&amp;myname;&quot;&gt;`.

The following example:

```
string nameOfCustomer = "Progress & Prosperity, Co. > Expectations";

  string xml = "<company><name>"+escapeXML(nameOfCustomer)+"</name></company>"
```

returns:

```
<company><name>Progress &amp; Prosperity, Co. &gt; Expectations&#39; </name></company>
```

**See also:**[unescapeXML](string-functions-ctl2.md#unescapexml)

#### find

```ctl
string[] find(string arg, string regex);
string[] find(string arg, string regex, integer group_number);
```

The `find()` function returns a list of substrings corresponding to the [*regular expression*](language-reference-ctl2.md#regular-expressions) pattern that is found in the second argument.

If the second argument is an empty string, the function returns a list of empty strings. The sum of empty strings in the list is same as the length of the original string plus one; e.g. the string 'mark' results in the list of five empty strings.

If one or both of the two arguments are `null` value, the function fails with an error.

The third argument specifies which regular expression group to use.

**Compatibility**

The `find(string,string)` function is available since **CloverETL 3.0.0**.

The `find(string,string,integer)` function is available since **CloverETL 3.4.x**.
Example 178. Usage of find
The function `find("A quick brown fox jumps over the lazy dog.", " [a-z]")` returns `[ q, b, f, j, o, t, l, d]`.

The function `find("A quick brown fox jumps over the lazy dog.", " [a-z]*")` returns `[ quick, brown, fox, jumps, over, the, lazy, dog]`.

The function `find("A quick brown fox jumps over the lazy dog.", "()([a-z]*)([a-z])", 2)` returns `[quic, brow, fo, jump, ove, th, laz, do]`.

**See also:**[matchGroups](string-functions-ctl2.md#matchgroups)

#### formatMessage

```ctl
string formatMessage(string template, variant param1, variant ..., variant paramN);
string formatMessageWithLocale(string locale, string template, variant param1, variant ..., variant paramN);
```

The `formatMessage(string template, variant param1, variant …, variant paramN)` function returns a formatted message where the parameters referenced in the input template are replaced with their corresponding values. This function is useful for constructing messages with dynamic content in a structured and readable manner. The template argument can also incorporate [multi-line strings](language-reference-ctl2.md#multiline-string). This allows for the creation of more complex message formats that span multiple lines.

A basic example:

`formatMessage("Name of the applicant is {0}. He is {1} years old.", "John Doe", 32)` returns `"Name of the applicant is John Doe. He is 32 years old."`

Where `{0}` references the first input parameter and `{1}` the second.

The parameters can be of any type supported by the **variant** data type.

In the message template string, placeholders are enclosed in curly braces **{}**. The format of a placeholder can be as simple as a number indicating the position of the parameter, like **{0}, {1}**, etc. However, the placeholders can also include additional formatting information, such as data type, style, or custom patterns.

Here’s a breakdown of the placeholder format:

`{argument_index[,format_type[,format_style]]}`

1. **argument_index**: A non-negative integer indicating the position of the parameter in the input parameters. The index is 0-based, so the first parameter is referenced as **{0}**, the second as **{1}**, and so on.
2. **format_type** (optional): A string indicating the data type of the parameter. Supported types include **number, date, time**, and **choice**. If not specified, the parameter is treated as a plain string.
3. **format_style** (optional): A string indicating the formatting style for the specified data type. For example, **short, medium, long, full, integer, currency, percent**, or **SubformatPattern**. For more information refer to Oracle’s documentation on the Java java.text.MessageFormat syntax [here](https://docs.oracle.com/javase/8/docs/api/java/text/MessageFormat.html),

Here are some examples of placeholders with different formats:

1. `{0}`: A simple placeholder that references the first parameter.
2. `{1, number, integer}`: A placeholder that formats the second parameter as an integer number.
3. `{2, date, short}`: A placeholder that formats the third parameter as a short date.
4. `{3, time, medium}`: A placeholder that formats the fourth parameter as a medium-style time.
5. `{4, number,$'#',##}`: A placeholder that formats the fifth parameter with the pound sign quoted.

By understanding the [Java java.text.MessageFormat syntax](https://docs.oracle.com/javase/8/docs/api/java/text/MessageFormat.html) and the various formatting options available, you can create more sophisticated and customized message templates for your applications.

The **formatMessage** and **formatMessageWithLocale** functions support using [multi-line strings](language-reference-ctl2.md#multiline-string) strings as the template, which can help improve the readability and formatting of complex templates.
Example 179. Usage of `formatMessage()` usage with a multi-line string:

```
formatMessage("""
<html>
<body>
  <h1>Order Summary</h1>
  <p>Order ID: {0}</p>
  <p>Date: {1, date, long}</p>
  <p>Account Type: {2, choice, 0#Free|1#Premium|2#Enterprise}</p>
  <p>Total Amount: {3, number, currency}</p>
</body>
</html>
""", 1234L, today(), 1, 154.52D)
```

It produces the following result:

```
<html>
<body>
  <h1>Order Summary</h1>
  <p>Order ID: 1,234</p>
  <p>Date: March 12, 2024</p>
  <p>Account Type: Premium</p>
  <p>Total Amount: $154.52</p>
</body>
</html>
```

The `formatMessageWithLocale(locale, template, parameters)` function extends the functionality of the `formatMessage` function by allowing you to specify a locale for the formatting process. This is particularly useful when you need to format messages according to specific language or regional settings, such as date, time, or number formatting.
Example 180. Usage of `formatMessageWithLocale()` usage with a multi-line string:

```
formatMessageWithLocale(“es.ES”, """
<html>
<body>
  <h1>Order Summary</h1>
  <p>Order ID: {0}</p>
  <p>Date: {1, date, long}</p>
  <p>Account Type: {2, choice, 0#Free|1#Premium|2#Enterprise}</p>
  <p>Total Amount: {3, number, currency}</p>
</body>
</html>
""", 1234L, today(), 1, 154.52D)
```

It produces the following result:

```
<html>
<body>
  <h1>Order Summary</h1>
  <p>Order ID: 1.234</p>
  <p>Date: 12 de marzo de 2024</p>
  <p>Account Type: Premium</p>
  <p>Total Amount: 154,52 €</p>
</body>
</html>
```

**Compatibility**

The `formatMessage(string,variant)` and `formatMessageWithLocale(string,string,variant)` functions are available since **CloverDX 6.4.0**.

#### getAlphanumericChars

```ctl
string getAlphanumericChars(string arg);
string getAlphanumericChars(string arg, boolean takeAlpha, boolean takeNumeric);
```

The `getAlphanumericChars()` function returns only letters and digits contained in a given argument in the order of their appearance in the string. The other characters are removed.

For an empty string input, the function returns an empty string. For `null` input, the function returns `null`.

If the `takeAlpha` is present and set to true and `takeNumeric` is set to false, the function will return letters only.

If the `takeNumeric` is present and set to true and `takeAlpha` is set to false, the function will return numbers only.

**Compatibility**

The `getAlphanumericChars(string)` and `getAlphanumericChars(string,boolean,boolean)` functions are available since **CloverETL 3.0.0**.
Example 181. Usage of getAlphanumericChars
The function `getAlphanumericChars("34% of books")`returns `34ofbooks`.

The function `getAlphanumericChars("(8+4)*2")`returns `842`.

The function `getAlphanumericChars("gâteau")` returns `gâteau`.

The function `getAlphanumericChars("123 books", true, false)` returns `books`.

The function `getAlphanumericChars("123 books", false, true)` returns `123`.

The function `getAlphanumericChars("123 books", false, false)` returns `123 books`.

**See also:**[removeBlankSpace](string-functions-ctl2.md#removeblankspace), [removeDiacritic](string-functions-ctl2.md#removediacritic), [removeNonAscii](string-functions-ctl2.md#removenonascii)

#### getComponentProperty

```ctl
string getComponentProperty(string propertyName);
```

The function `getComponentProperty()` returns value of a component attribute.

The `propertyName` argument is a name of an attribute of a component.

If `propertyName` is `null`, the function `getComponentProperty()` returns `null`.

If `propertyName` does not match the name of any existing attribute, the function returns `null`.

**Compatibility**

The `getComponentProperty()` function is available since **CloverETL 4.0**.
Example 182. Usage of getComponentProperty
The function `getComponentProperty("type")` returns `DATA_GENERATOR` in **DataGenerator**.

The function `getComponentProperty("id")` returns `MAP2` in the third **Map**.

The function `getComponentProperty(null)` returns `null`.

The function `getComponentProperty("AQuickBrownFoxJumpsOverTheLazyDog")` returns `null`.

**See also:**[toProjectUrl](string-functions-ctl2.md#toprojecturl)

#### getFileExtension

```ctl
string getFileExtension(string arg);
```

The `getFileExtension()` function extracts a file extension from a specified path or URL.

Returns the textual part of the file name after the last dot. There must be no directory separator after the dot. If extension is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

**Compatibility**

The `getFileExtension(decimal)` and `log(number)` functions are available since **CloverETL 4.1.0-M1**.
Example 183. Usage of getFileExtension
The function `getFileExtension("theDir/library.src.zip")` returns `zip`.

The function `getFileExtension("ftp://ftp.example.com/home/user1/my.documents/log")` returns `empty string`.

**See also:**[getFileName](string-functions-ctl2.md#getfilename), [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension), [getFilePath](string-functions-ctl2.md#getfilepath), [normalizePath](string-functions-ctl2.md#normalizepath),

#### getFileName

```ctl
string getFileName(string arg);
```

The `getFileName()` function extracts a file name from a specified path or URL.

Returns the text after the last forward or backslash. If the file name is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

**Compatibility**

The `getFileName(string)` function is available since **CloverETL 4.1.0-M1**.
Example 184. Usage of getFileName
The function `getFileName("http://www.example.com/theDir/theExample.html")` returns `theExample.html`.

The function `getFileName("C:/Users/Public/Desktop/January")` returns `January`.

The function `getFileName("file:///home/user1/documents/")` returns *empty string*.

**See also:**[getFileExtension](string-functions-ctl2.md#getfileextension), [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension), [getFilePath](string-functions-ctl2.md#getfilepath), [normalizePath](string-functions-ctl2.md#normalizepath),

#### getFileNameWithoutExtension

```ctl
string getFileNameWithoutExtension(string arg);
```

The `getFileNameWithoutExtension()` function extracts a base file name from a specified path or URL.

Returns the text after the last forward or backslash and before the last dot. If the base name is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

**Compatibility**

The `getFileNameWithoutExtension(string)` function is available since **CloverETL 4.1.0-M1**.
Example 185. Usage of getFileNameWithoutExtension
The function `getFileNameWithoutExtension("http://www.example.com/theDir/library.src.zip")` returns `library.src`.

The function `getFileNameWithoutExtension("sandbox://shared/data-in/documents/.index")` returns *empty string*.

**See also:**[getFileExtension](string-functions-ctl2.md#getfileextension), [getFileName](string-functions-ctl2.md#getfilename), [getFilePath](string-functions-ctl2.md#getfilepath), [normalizePath](string-functions-ctl2.md#normalizepath),

#### getFilePath

```ctl
string getFilePath(string arg);
```

The `getFilePath()` function extracts a file path (without the file name) from a specified full path or URL.

Returns the text before and including the last forward or backslash. Also replaces backslashes with forward slashes. If the path is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

**Compatibility**

The `getFilePath(string)` function is available since **CloverETL 4.1.0-M1**.
Example 186. Usage of getFilePath
The function `getFilePath("C:\\Program Files\\.\\Java\\src.zip")` returns `C:/Program Files/./Java/`.

The function `getFilePath("index.html")` returns *empty string*.

**See also:**[getFileExtension](string-functions-ctl2.md#getfileextension), [getFileName](string-functions-ctl2.md#getfilename), [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension), [normalizePath](string-functions-ctl2.md#normalizepath),

#### getUrlHost

```ctl
string getUrlHost(string arg);
```

The `getUrlHost()` function parses out a host name from a specified URL.

If the hostname part is not present in the URL argument, an empty string is returned. If the URL is not valid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for an empty string and `null` input.

**Compatibility**

The `getUrlHost(string)` function is available since **CloverETL 3.1.0**.
Example 187. Usage of getUrlHost
The function `getUrlHost("http://www.example.com/theDir/theExample.html")` returns `www.example.com`.

The function `getUrlHost("file:///home/user1/documents/cat.png")` returns *empty string*.

**See also:**[getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [getUrlRef](string-functions-ctl2.md#geturlref), [isUrl](string-functions-ctl2.md#isurl)

#### getUrlPath

```ctl
string getUrlPath(string arg);
```

The `getUrlPath()` function parses out a path from a specified URL.

If the path part is not present in the URL argument, an empty string is returned. If the URL is not valid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for an empty string and `null` input.

**Compatibility**

The `getUrlPath(string)` function is available since **CloverETL 3.1.0**.
Example 188. Usage of getUrlPath The function `getUrlPath("http://www.example.com/theDir/theExample.html")` returns `/theDir/theExample.html`
**See also:**[getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [getUrlRef](string-functions-ctl2.md#geturlref), [isUrl](string-functions-ctl2.md#isurl)

#### getUrlPort

```ctl
integer getUrlPort(string arg);
```

The `getUrlPort()` function parses out a port number from a specified URL.

If the port part is not present in the URL argument, `-1` is returned. If the URL has invalid syntax, `-2` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `-2` value for an empty string and `null` input.

**Compatibility**

The `getUrlPort(string)` function is available since **CloverETL 3.1.0**.
Example 189. Usage of getUrlPort
The function `getUrlPort("http://www.example.com/theDir/theExample.html")` returns `-1`.

The function `getUrlPort("http://www.example.com:8080/theDir/theExample.html")` returns `8080`.

**See also:**[getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [getUrlRef](string-functions-ctl2.md#geturlref), [isUrl](string-functions-ctl2.md#isurl)

#### getUrlProtocol

```ctl
string getUrlProtocol(string arg);
```

The `getUrlProtocol()` function parses out a protocol name from a specified URL.

If the protocol part is not present in the URL argument, an empty string is returned. If the URL is not valid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

**Compatibility**

The `getUrlProtocol(string)` function is available since **CloverETL 3.1.0**.
Example 190. Usage of getUrlProtocol The function `getUrlProtocol("http://www.example.com/theDir/theExample.html")` returns `http`.
**See also:**[getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [getUrlRef](string-functions-ctl2.md#geturlref), [isUrl](string-functions-ctl2.md#isurl)

#### getUrlQuery

```ctl
string getUrlQuery(string arg);
```

The `getUrlQuery()` function parses out a query (parameters) from a specified URL.

If the query part is not present in the URL argument, an empty string is returned. If the URL syntax is invalid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

**Compatibility**

The `getUrlQuery(string)` function is available since **CloverETL 3.1.0**.
Example 191. Usage of getUrlQuery
The function `getUrlQuery("http://www.example.com/theDir/theExample.html")` returns *empty string*.

The function `getUrlQuery("http://www.example.com/theDir/theExample.html?a=file&name=thefile.txt")` returns `a=file&name=thefile.txt`.

**See also:**[getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [getUrlRef](string-functions-ctl2.md#geturlref), [isUrl](string-functions-ctl2.md#isurl)

#### getUrlRef

```ctl
string getUrlRef(string arg);
```

The `getUrlRef()` function parses out the fragment after # character, also known as ref, reference or anchor, from a specified URL.

If the fragment part is not present in the URL argument, an empty string is returned. If the URL syntax is invalid, `null` is returned. For the URL scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

**Compatibility**

The `getUrlRef(string)` function is available since **CloverETL 3.1.0**.
Example 192. Usage of getUrlRef
The function `getUrlRef("http://www.example.com/index.html")` returns *empty string*.

The function `getUrlRef("http://www.example.com/Index.html#abc014")` returns `abc014`.

**See also:**[getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [isUrl](string-functions-ctl2.md#isurl)

#### getUrlUserInfo

```ctl
string getUrlUserInfo(string arg);
```

The `getUrlUserInfo()` function parses out a username and password from a specified URL.

If the `userinfo` part is not present in the URL argument, an empty string is returned. If the URL syntax is invalid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

**Compatibility**

The `getUrlUserInfo(string)` function is available since **CloverETL 3.1.0**.
Example 193. Usage of getUrlUserInfo
The function `getUrlUserInfo("http://www.example.com/theDir/theExample.html")` returns *empty string*.

The function `getUrlUserInfo("http://user1:passwor123@www.example.com/theDir/theExample.html")` returns `user1:passwor123`.

**See also:**[getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlRef](string-functions-ctl2.md#geturlref), [isUrl](string-functions-ctl2.md#isurl)

#### indexOf

```ctl
integer indexOf(string arg, string substring);
integer indexOf(string arg, string substring, integer fromIndex);
```

The `indexOf()` function returns the index (zero-based) of the first occurrence of `substring` in the `string`. Returns `-1` if no occurrence is found.

If the parameter `arg` is `null`, the function returns `-1`. See compatibility notice.

If the second argument is `null`, the function fails with an error. If the second argument is an empty string, the function returns `0`.

Start position for search is set up using parameter `fromIndex`.

**Compatibility**

The `indexOf(string,string)` and `indexOf(string,string,integer)` functions are available since **CloverETL 3.0.0**.

In **CloverETL 3.5.x** and earlier the function fails with an error if the `arg` argument is `null`.

For example `indexOf(null, "chair")` in **CloverETL 3.5.x** and earlier fails.
Example 194. Usage of indexOf
The function `indexOf("Hello world!", "world")` returns `6`.

The function `indexOf("Hello world", "o")` returns `4`.

The function `indexOf("Hello world", "o", 6)` returns `7`

The function `indexOf("Hello world", "book")` returns `-1`.

The function `indexOf("Hello world", "")` returns `0`.

The function `indexOf(null, "chair")` returns -1. See compatibility notice.

**See also:**[indexOf](string-functions-ctl2.md#indexof), [matches](string-functions-ctl2.md#matches)

#### isAscii

```ctl
boolean isAscii(string arg);
```

The `isAscii()` checks the string for occurrence of non-ASCII characters.

The function takes one string argument and returns a boolean value depending on whether the string can be encoded as an ASCII string (true) or not (false).

If the input is `null` or empty string, the function returns `true`.

**Compatibility**

The `isAscii(string)` function is available since **CloverETL 3.0.0**.
Example 195. Usage of isAscii
The function `isAscii("Hello world! ")` returns `true`.

The function `isAscii("voilà")` returns `false`.

**See also:**[isBlank](miscellaneous-functions-ctl2.md#isblank), [isDate](string-functions-ctl2.md#isdate), [isInteger](string-functions-ctl2.md#isinteger), [isLong](string-functions-ctl2.md#islong), [isNumber](string-functions-ctl2.md#isnumber), [removeDiacritic](string-functions-ctl2.md#removediacritic), [removeNonAscii](string-functions-ctl2.md#removenonascii), [removeNonPrintable](string-functions-ctl2.md#removenonprintable)

#### isBlank

```ctl
boolean isBlank(string arg);
```

The function returns a boolean value depending on whether the parameter contains only white space characters (true) or not (false), if the input is `null` or an empty string, the function returns `true`.

**Note:** There are many other overloads of the `isBlank` function which work with arguments of other data types. See [isBlank(<not-string>)](miscellaneous-functions-ctl2.md#isblank) for more details.

**Compatibility**

- The `isBlank(string)` function is available since **CloverETL 3.0.0**.
- The overloads for types other than string are available since **CloverDX 7.3.0**.
Example 196. Usage of isBlank

```ctl
// string
isBlank("   "); // true, because there are 3 space chars (char 0x20) between quotes.
isBlank(" "); // true, because there is hard space character (0xA0) has been used between the quotes.
isBlank(" bc") // false
```

**See also:**[removeBlankSpace](string-functions-ctl2.md#removeblankspace), [isBlank(<not-string>)](miscellaneous-functions-ctl2.md#isblank) for other types

#### isDate

```ctl
boolean isDate(string input, string pattern);
boolean isDate(string input, string pattern, boolean strict);
boolean isDate(string input, string pattern, string locale);
boolean isDate(string input, string pattern, string locale, boolean strict);
boolean isDate(string input, string pattern, string locale, string timeZone);
boolean isDate(string input, string pattern, string locale, string timeZone, boolean strict);
```

The `isDate()` function returns `true` if the `input` matches the date [`pattern`](metadata-records-and-fields.md#date-and-time-format). Returns `false` otherwise.

If the `input` is `null`, the function returns `false`.

If the `pattern` is `null` or an empty string, the [default date format](../admin/designer-configuration.md#default-date-format) is used.

If the parameter `locale` is missing, default [Locale](metadata-records-and-fields.md#locale) is used.

If the parameter `timeZone` is missing, default [Time Zone](metadata-records-and-fields.md#timezone) is used.

If `strict` is `true`, the date format is checked using a conversion from string to date, conversion from date to string and subsequent comparison of the input string and result string. If the input string and result string differ, the function returns `false`. This way you can enforce a required number of digits in the date.

If `strict` is `null` or the function does not have the argument `strict`, it works the same way as if set to `false` - the format is not checked in the strict way.

**Compatibility**

The `isDate(string,string)` and `isDate(string,string,string)` functions are available since **CloverETL 3.0.0**.

The `isDate(string,string,string,string)` is available since **CloverETL 3.5.0-M1**.

The functions `isDate(string, string, boolean)`, `isDate(string, string, string, boolean)` and `isDate(string, string, string, string, boolean)` are available since **CloverETL 4.1.0**.
Example 197. Usage of isDate
The function `isDate("2012-06-11", "yyyy-MM-dd")` returns `true`.

The function `isDate("2012-06-11", "yyyy-MM-dd H:m:s")` returns `false`.

The function `isDate("2014-03-30 2:30 +1000", "yyyy-MM-dd H:m Z", "en.US")` returns `true`.

The function `isDate("2014-03-30 2:30", "yyyy-MM-dd H:m", "en.US", "GMT-5")` returns `true`.

The function `isDate("6.007.2015", "dd.MM.yyyy", false)` returns `true` whereas the function `isDate("6.007.2015", "dd.MM.yyyy", true)` returns `false`.

**See also:**[isInteger](string-functions-ctl2.md#isinteger), [isLong](string-functions-ctl2.md#islong), [isNumber](string-functions-ctl2.md#isnumber), [str2date](conversion-functions-ctl2.md#str2date)

#### isDecimal

```ctl
boolean isDecimal(string arg);
boolean isDecimal(string arg, string format);
boolean isDecimal(string arg, string format, string locale);
```

The `isDecimal` function checks a possibility to convert a string to a decimal data type.

The `format` determines the data conversion. See [Numeric Format](metadata-records-and-fields.md#numeric-format). If `format` is not used, the function checks that `arg` is compatible with java BigDecimal.

The `locale` parameter is described in [Locale](metadata-records-and-fields.md#locale). If the function is called without the locale parameter, the default `locale` is used.

The parameter `arg` is the string to be checked. If the parameter `arg` can be converted to decimal, the function returns `true`, otherwise it returns `false`. It the parameter is `null`, the function returns `false`.

**Compatibility**

The `isDecimal(string)` function is available since **CloverETL 4.0.0-M1**.

The `isDecimal(string, format)` and `isDecimal(string, format, locale)` functions are available since **CloverETL 4.9.0**.

Since **CloverDX 6.4.0** the whole string argument must be successfully parsed according to the `format`. If any part of the argument does not match format, the function returns `false`.
Example 198. Usage of isDecimal
The function `isDecimal(null)` returns `false`.

The function `isDecimal("")` returns `false`.

The function `isDecimal("half")` returns `false`.

The function `isDecimal("4096")` returns `true`.

The function `isDecimal("2.71828")` returns `true`.

The function `isDecimal("2.147483648e9")` returns `true`.

The function `isDecimal("123,456.78", "###,###.##")` returns `true`.

The function `isDecimal("123 456,78", "###,###.##", "fr.FR")` returns `true`. There should be a hard space (character 160) between `3` and `4`.

**See also:**[isDate](string-functions-ctl2.md#isdate), [isInteger](string-functions-ctl2.md#isinteger), [isLong](string-functions-ctl2.md#islong), [isNumber](string-functions-ctl2.md#isnumber), [str2decimal](conversion-functions-ctl2.md#str2decimal)

#### isEmpty

```ctl
boolean isEmpty(string arg);
```

The `isEmpty()` function checks whether a given string is `null` or of zero length.

If `arg` is `null`, function returns `true`.

**Compatibility**

The `isEmpty()` function is available since **CloverETL 4.1.0-M1**.
Example 199. Usage of isEmpty
`isEmpty("")` returns `true`.

`string s = null; isEmpty(s);` returns `true`.

`isEmpty("cup of tea")` returns `false`.

**See also:** Container functions: [isEmpty(container)](container-functions-ctl2.md#isempty)

#### isInteger

```ctl
boolean isInteger(string arg);
boolean isInteger(string arg, string format);
boolean isInteger(string arg, string format, string locale);
```

The `isInteger()` function checks a possibility to convert a string to an integer.

The parameter `arg` is the string to be checked. The function returns a boolean value depending on whether the string can be converted to an integer number `(true)` or not `(false)`. If the parameter is an empty string or `null`, the function returns `false`.

The `format` parameter is described in [Numeric Format](metadata-records-and-fields.md#numeric-format).

The `locale` parameter is described in [Locale](metadata-records-and-fields.md#locale). If the function is called without the `locale` parameter, the default `locale` is used.

**Compatibility**

The `isInteger(string)` function is available since **CloverETL 3.0.0**.

The `isInteger(string, format)` and `isInteger(string, format, locale)` functions are available since **CloverDX 6.4.0**.
Example 200. Usage of isInteger
The function `isInteger("141592654")` returns `true`.

The function `isInteger("-718281828")` returns `true`.

The function `isInteger("999999999")` returns `true`.

The function `isInteger("12345.6")` returns `false`.

The function `isInteger("1234567890123")` returns `false`.

The function `isInteger("spruce")` returns `false`.

**See also:**[isDate](string-functions-ctl2.md#isdate), [isDecimal](string-functions-ctl2.md#isdecimal), [isLong](string-functions-ctl2.md#islong), [isNumber](string-functions-ctl2.md#isnumber), [str2integer](conversion-functions-ctl2.md#str2integer)

#### isLong

```ctl
boolean isLong(string arg);
boolean isLong(string arg, string format);
boolean isLong(string arg, string format, string locale);
```

The `isLong()` function checks a possibility to convert a string to a `long` number.

The parameter `arg` is the string to be checked. The function returns a boolean value depending on whether the string can be converted to a long number `(true)` or not `(false)`. If the parameter is an empty string or `null`, the function returns `false`.

The `format` parameter is described in [Numeric Format](metadata-records-and-fields.md#numeric-format).

The `locale` parameter is described in [Locale](metadata-records-and-fields.md#locale). If the function is called without the `locale` parameter, the default `locale` is used.

**Compatibility**

The `isLong(string)` function is available since **CloverETL 3.0.0**.

The `isLong(string, format)` and `isLong(string, format, locale)` functions are available since **CloverDX 6.4.0**.
Example 201. Usage of isLong
The function `isLong("732050807568877293")` returns `true`.

The function `isLong("-236067977499789696")` returns `true`.

The function `isLong("999999999999999999")` returns `true`.

The function `isLong("12345.6")` returns `false`.

The function `isLong("12345678901234567890")` returns `false`.

The function `isLong("oak")` returns `false`.

**See also:**[isDate](string-functions-ctl2.md#isdate), [isDecimal](string-functions-ctl2.md#isdecimal), [isInteger](string-functions-ctl2.md#isinteger), [isNumber](string-functions-ctl2.md#isnumber), [str2long](conversion-functions-ctl2.md#str2long)

#### isNumber

```ctl
boolean isNumber(string arg);
boolean isNumber(string arg, string format);
boolean isNumber(string arg, string format, string locale);
```

The `isNumber()` function checks the possibility to convert a string to a number (double).

The parameter `arg` is the string to be checked. The function returns a boolean value depending on whether the string can be converted to a double `(true)` or not `(false)`. If the parameter is an empty string or `null`, the function returns `false`.

The `format` parameter is described in [Numeric Format](metadata-records-and-fields.md#numeric-format).

The `locale` parameter is described in [Locale](metadata-records-and-fields.md#locale). If the function is called without the `locale` parameter, the default `locale` is used.

**Compatibility**

The `isNumber(string)` function is available since **CloverETL 3.0.0**.

The `isNumber(string, format)` and `isNumber(string, format, locale)` functions are available since **CloverDX 6.4.0**.
Example 202. Usage of isNumber
The function `isNumber("41421356237")` returns `true`.

The function `isNumber("-12345.6")` returns `true`.

The function `isNumber("12345.6e3")` returns `true`.

The function `isNumber("larch")` returns `false`.

**See also:**[isDate](string-functions-ctl2.md#isdate), [isDecimal](string-functions-ctl2.md#isdecimal), [isInteger](string-functions-ctl2.md#isinteger), [isLong](string-functions-ctl2.md#islong), [str2double](conversion-functions-ctl2.md#str2double),

#### isUnicodeNormalized

```ctl
boolean isUnicodeNormalized(string str, string form);
```

Determine whether the `str` input string is Unicode normalized according to the given form.

The parameter `str` is a string to be checked for accordance with the normalized form. If the parameter `str` is `null`, the function returns `true`.

The parameter `form` contains identification of the Unicode normalization form. Following normalization forms are available:

- NFD: Canonical Decomposition
- NFC: Canonical Decomposition followed by Canonical Composition
- NFKD: Compatibility Decomposition
- NFKC: Compatibility Decomposition followed by Canonical Composition

If the parameter `form` is `null`, the function fails.

**Compatibility**

The `isUnicodeNormalized(string)` function is available since **CloverETL 4.0.0-M1**.
Example 203. Usage of isUnicodeNormalized
The function `isUnicodeNormalized("\u0041"+"\u030A", "NFD")` returns `true`.

The function `isUnicodeNormalized("\u00C5", "NFD")` returns `false`.

The function `isUnicodeNormalized(null, "NFD")` returns `true`.

The function `isUnicodeNormalized("seashore", null)` fails.

The function `isUnicodeNormalized("\u0041"+"\u030A", "NFC")` returns `false`.

The function `isUnicodeNormalized("\u00C5", "NFC")` returns `true`.

The function `isUnicodeNormalized("\uFB01", "NFKD")` returns `false`.

The function `isUnicodeNormalized("\u0066\u0069", "NFKD")` returns `true`.

The function `isUnicodeNormalized("\u0073\u0323\u0307", "NFKC")` returns `false`.

The function `isUnicodeNormalized("\u1E69", "NFKC")` returns `true`.

**See also:**[codePointToChar](string-functions-ctl2.md#codepointtochar), [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint), [unicodeNormalize](string-functions-ctl2.md#unicodenormalize)

#### isUrl

```ctl
boolean isUrl(string arg);
```

The `isUrl()` function checks whether a specified string is a valid URL of the following syntax

```ctl
foo://username:passw@host.com:8042/there/index.dtb?type=animal;name=cat#nose
\_/   \____________/ \______/ \__/\______________/ \__________________/ \__/
 |           |          |      |         |                  |             |
protocol  userinfo     host   port      path               query         ref
```

For more information about the URI standards, see [http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt).

If the input is empty string or `null`, the function returns `false`.

**Compatibility**

The `isUrl()` function is available since **CloverETL 3.1.0**.
Example 204. Usage of isUrl The function `isUrl("http://username:passw@host.com:8042/there/index.dtb?type=animal&name=cat#nose")` returns `true`.
**See also:**[escapeUrl](string-functions-ctl2.md#escapeurl), [getUrlHost](string-functions-ctl2.md#geturlhost), [getUrlPath](string-functions-ctl2.md#geturlpath), [getUrlPort](string-functions-ctl2.md#geturlport), [getUrlProtocol](string-functions-ctl2.md#geturlprotocol), [getUrlQuery](string-functions-ctl2.md#geturlquery), [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo), [getUrlRef](string-functions-ctl2.md#geturlref), [unescapeUrl](string-functions-ctl2.md#unescapeurl)

#### isValidCodePoint

```ctl
boolean isValidCodePoint(integer code);
```

The function `isValidCodePoint()` returns `true` if the code value is valid *Unicode code point*.

If the parameter `code` is `null`, the function returns `false`.

**Compatibility**

The `isValidCodePoint(integer)` function is available since **CloverETL** 4.0.0-M1.
Example 205. Usage of isValidCodePoint
The function `isValidCodePoint(-1)` returns `false`.

The function `isValidCodePoint(0)` returns `true`.

The function `isValidCodePoint(0x03B1)` returns `true`.

The function `isValidCodePoint(0x10300)` returns `true`.

The function `isValidCodePoint(0x110000)` returns `false`.

The function `isValidCodePoint(null)` fails.

**See also:**[codePointAt](string-functions-ctl2.md#codepointat), [codePointLength](string-functions-ctl2.md#codepointlength), [codePointToChar](string-functions-ctl2.md#codepointtochar)

#### join

```ctl
string join(string delimiter, <element type>[] arg);
string join(string delimiter, map[<type of key>,<type of value>] arg);
```

The `join()` converts elements from the list or map of elements to their string representation and puts them together with the first argument as a delimiter.

If the delimiter is `null`, the function joins string representations of elements from the list with the empty string.

**Compatibility**

The `join()` function is available since **CloverETL Designer 3.0.0**.
Example 206. Usage of join
Let’s call a list containing values `a`, `b` and `c` as `myString`. The function `join(":", myString)` returns `a:b:c`.

The function `join(null, myString)` using the list from previous example returns `abc`.

Let’s call `map[integer, string]` as `theMap` and insert values into the map `theMap[0] = "cat"`, `theMap[1] = "grep"` and `theMap[3] = "head"`. The function `join(" ", theMap)` returns `0=cat 1=grep 3=head`.

The function `join(null, theMap)` using the `theMap` from previous example returns `0=cat 1=grep 3=head`.

**See also:**[concat](string-functions-ctl2.md#concat), [concatWithSeparator](string-functions-ctl2.md#concatwithseparator), [split](string-functions-ctl2.md#split)

#### lastIndexOf

```ctl
integer lastIndexOf(string input, string substr);
integer lastIndexOf(string input, string substr, integer index);
```

The function `lastIndexOf` returns an index of the last occurrence of the `substr` substring within the given string `input`, searching backwards from the given position or from the end.

The parameter `input` is a string in which the occurrence of the `substr` string is searched. If `input` is `null`, the function returns `-1`.

The parameter `substr` is a substring to be searched. If the parameter `substr` is `null`, the function fails.

The parameter `index` denotes the position in the `input`, where the substring matching process starts. If the parameter is negative, the function returns `-1`. If the parameter is `null`, the function fails.

**Compatibility**

The `lastIndexOf(string,string)` and `lastIndexOf(string,string,integer)` functions are available since **CloverETL 4.0.0-M1**.
Example 207. Usage of lastIndexOf
The function `lastIndexOf(null, "quad")` returns `-1`.

The function `lastIndexOf(null, "quad", 5)` returns `-1`.

The function `lastIndexOf("data", "a")` returns `3`.

The function `lastIndexOf("fabricable", "ab", 5)` returns `1`.

The function `lastIndexOf("fabricable", "ab", 6)` returns `6`.

The function `lastIndexOf("fabricable", "ab", -1)` returns `-1`.

The function `lastIndexOf("fabricable", "ab", 20)` returns `6`.

The function `lastIndexOf("fabricable", null, 0)` fails.

The function `lastIndexOf("fabricable", "ab", null)` fails.

**See also:**[indexOf](string-functions-ctl2.md#indexof)

#### left

```ctl
string left(string input, integer length);
string left(string input, integer length, boolean spacePad);
```

The `left()` function returns a substring of `input` with the specified `length`.

If the `input` is shorter than `length`, the function returns the `input` unmodified. The result may be padded with spaces, based on the value of `spacePad`.

If the `input` is `null`, the function returns `null`.

If `spacePad` is set to `false`, the function behaves the same way as the `left(string, integer)` function. If `spacePad` is set to `true` and the `input` is shorter than `length`, the function pads the `input` with blank spaces from the right side.

**Compatibility**

The `left(string,integer)` function is available since **CloverETL 3.0.0**.

The `left(string,integer,boolean)` function is available since **CloverETL 3.1.0**.
Example 208. Usage of left
The function `left("A very long text", 6)` returns `A very`.

The function `left("A very long text", 20)` returns `A very long text`.

The function `left("text", 10, true)` returns `text`. There are 6 space chars appended after the `text`.

**See also:**[right](string-functions-ctl2.md#right), [substring](string-functions-ctl2.md#substring)

#### length

```ctl
integer length(structuredtype arg);
```

The `length()` function accepts a structured data type as its argument: `string`, `<element type>[]`, `map[<type of key>,<type of value>]` or `record`. It takes the argument and returns a number of elements forming the structured data type.

If the argument is `null` or empty string, the function returns `0`.

**Compatibility**

The `length(string)` function is available since **CloverETL 3.0.0**.
Example 209. Usage of length
The function `length("string")` returns `6`.

Let’s call a list containing values `ab`, `bc` and `cd` as `myString`. The function `length(myString)` returns `3`.

**See also:** Container functions: [length(container)](container-functions-ctl2.md#length), Record functions: [length(record)](field-access-functions-ctl2.md#length)

#### lowerCase

```ctl
string lowerCase(string input);
```

The `lowerCase()` function returns the `input` string with letters converted to lower case only.

If the input is `null`, the function returns `null`.

**Compatibility**

The `lowerCase(string)` function is available since **CloverETL 3.0.0**.
Example 210. Usage of lowerCase The function `lowerCase("Some string")` returns `some string`.
**See also:**[upperCase](string-functions-ctl2.md#uppercase), [properCase](string-functions-ctl2.md#propercase)

#### lpad

```ctl
string lpad(string input, integer length);
string lpad(string input, integer length, string filler);
```

The `lpad()` function pads input string from left using specified characters.

If the parameter `input` is `null` the function returns `null`.

The parameter `length` is minimal length of an output string. If the string length is lower than the parameter `length`, the string is padded from left using space or using `filler`. Otherwise the `input` string is returned.

If the parameter `length` is *negative* or `null`, the function fails.

It the `filler` parameter is `null`, *empty string* or longer than one character, function fails.

**Compatibility**

The `lpad(string,integer,string)` and `lpad(string,integer,string)` functions are available since **CloverETL 4.0.0-M1**.
Example 211. Usage of lpad
The function `lpad("256", 0)` returns `256`.

The function `lpad("256", 5)` returns `" 256"`.

The function `lpad("256", -1)` fails.

The function `lpad(null, 2)` returns `null`.

The function `lpad("", 0)` returns `""`.

The function `lpad("", 2)` returns `" "`.

The function `lpad("256", 5, "0")` returns `00256`.

The function `lpad("Great Dipper", 20, "")` fails.

The function `lpad("Little Dipper", 20, null)` fails.

The function `lpad("Little Dipper", 17, "The ")` fails.

**See also:**[left](string-functions-ctl2.md#left), [right](string-functions-ctl2.md#right), [rpad](string-functions-ctl2.md#rpad)

#### matches

```ctl
boolean matches(string text, string regex);
```

The `matches()` function checks the string to match the provided regular pattern.

The function returns `true`, if the `text` matches the [*regular expression*](language-reference-ctl2.md#regular-expressions)`regex`. Otherwise it returns `false`.

If the `text` is `null`, the function returns `false`. If the `regex` is `null`, the function fails with an error.

**Compatibility**

The `matches(string,string)` function is available since **CloverETL 3.0.0**.
Example 212. Usage of matches
The function `matches("abc", "[a-c]{3}")` returns `true`.

The function `matches("abc", "[A-Z]{3}")` returns `false`.

**See also:**[isAscii](string-functions-ctl2.md#isascii), [isBlank](miscellaneous-functions-ctl2.md#isblank), [isDate](string-functions-ctl2.md#isdate), [isDecimal](string-functions-ctl2.md#isdecimal), [isInteger](string-functions-ctl2.md#isinteger), [isLong](string-functions-ctl2.md#islong), [isNumber](string-functions-ctl2.md#isnumber), [isUrl](string-functions-ctl2.md#isurl)

#### matchGroups

```ctl
string[] matchGroups(string text, string regex);
```

The `matchGroups()` function returns the list of group matches (the substrings matched by the capturing groups of the `regex`) if `text` matches the [*regular expression*](language-reference-ctl2.md#regular-expressions)`regex`.

The list is zero-based and the element with index 0 is the match for the entire expression. The following elements (1, …​) correspond with the capturing groups indexed from left to right, starting at one. The returned list is unmodifiable. If `text` does not match `regex`, `null` is returned.

If the text argument is `null`, the function returns `null`. If the `regex` is `null`, the function fails with an error.

**Compatibility**

The `matchGroups(string,string)` function is available since **CloverETL 3.4.x**.
Example 213. Usage of matchGroups
The function `matchGroups("A fox", "([A-Z]) ([a-z]*)")` returns `[A fox, A, fox]`. The first group is a whole pattern, patterns enclosed in parentheses follow.

The function `matchGroups("A quick brown fox jumps", "[A-Z] [a-z]{5} [a-z]{5} ([a-z]*) ([a-z]{5})")` returns `[A quick brown fox jumps, fox, jumps]`.

**See also:**[cut](string-functions-ctl2.md#cut), [split](string-functions-ctl2.md#split), [substring](string-functions-ctl2.md#substring)

#### metaphone

```ctl
string metaphone(string arg);
string metaphone(string arg, integer maxLength);
```

The `metaphone()` function returns the metaphone code of the first argument.

For more information, see the following site: [www.lanw.com/java/phonetic/default.htm](http://www.lanw.com/java/phonetic/default.htm).

The default `maximum length` of the metaphone code is 4.

The function returns `null` value for the `null` input.

**Compatibility**

The `metaphone(string)` and `metaphone(string,integer)` function is available since **CloverETL 3.2.1** or earlier.
Example 214. Usage of metaphone
The function `metaphone("cheep")` returns `XP`.

The function `metaphone("sheep")` returns `XP`.

The function `metaphone("international")` returns `INTR`.

The function `metaphone("cheep", 1)` returns `X`.

The function `metaphone("sheep", 2)` returns `XP`.

The function `metaphone("bookworm", 3)` returns `BKW`.

The function `metaphone("international", 7)` returns `INTRNXN`.

**See also:**[editDistance](string-functions-ctl2.md#editdistance), [NYSIIS](string-functions-ctl2.md#nysiis), [soundex](string-functions-ctl2.md#soundex)

#### normalizeDecimal

```ctl
string normalizeDecimal(string arg);
```

The `normalizeDecimal()` function preprocesses decimal number strings and removes non-numeric characters, standardizes decimal separators, and eliminates thousand separators and currency symbols. By scanning the input string from right to left, it identifies the first occurrence of either a comma or a period, assuming it to be the decimal separator. While this approach offers a basic level of normalization, it’s important to note that it relies on a simple heuristic and may not be suitable for all scenarios, e.g., when your data includes integers with commas used as thousand separators (`1,000`). In such scenarios, more sophisticated parsing techniques may be necessary to accurately identify and handle different number formats.

**Compatibility**

The normalizeDecimal(string) function is available since **CloverDX 6.7.0**.
Example 215. Usage of normalizeDecimal
The function `normalizeDecimal("1,035")` returns `1.035`.

The function `normalizeDecimal("1,035.24")` returns `1035.24`.

The function `normalizeDecimal("1,000")` returns `1.000`.

The function `normalizeDecimal("EUR451")` returns `451`.

The function `normalizeDecimal("€127")` returns `127`.

The function `normalizeDecimal("23$56")` returns `2356`.

The function `normalizeDecimal("123,456.789")` returns `123456.789`.

The function `normalizeDecimal("123 456,789")` returns `123456.789`.

The function `normalizeDecimal("123.456,789")` returns `123456.789`.

The function `normalizeDecimal(null)` returns `null`.

**See also:**[normalizeWhitespaces](string-functions-ctl2.md#normalizewhitespaces)

#### normalizePath

```ctl
string normalizePath(string arg);
```

The `normalizePath()` function normalizes a specified path or URL to a standard format, removing single and double dot path segments. Also replaces backslashes with forward slashes.

If normalization fails because there is a double dot path segment that is not preceded by a removable parent path segment, the function returns `null`.

The function returns a `null` value for a `null` input.

**Compatibility**

The `normalizePath(string)` function is available since **CloverETL 4.1.0-M1**.
Example 216. Usage of normalizePath
The function `normalizePath("zip:(C:\\Data\\..\\archive.zip)#inner1/../inner2/./data.txt")` returns `zip:(C:/archive.zip)#inner2/data.txt`.

The function `normalizePath("home/../../data")` returns `null`.

**See also:**[getFileExtension](string-functions-ctl2.md#getfileextension), [getFileName](string-functions-ctl2.md#getfilename), [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension), [getFilePath](string-functions-ctl2.md#getfilepath),

#### normalizeWhitespaces

```ctl
string normalizeWhitespaces(string arg);
```

The `normalizeWhitespaces()` function takes one string argument and returns another string with all white space characters replaced with a single space. Leading and trailing white spaces are removed altogether (trimmed).

Following Unicode character categories are considered as white space by the function:

- ['Other, Control' Category](https://www.fileformat.info/info/unicode/category/Cc/list.htm)
- ['Separator, Space' Category](https://www.fileformat.info/info/unicode/category/Zs/list.htm)
- ['Separator, Paragraph' Category](https://www.fileformat.info/info/unicode/category/Zp/list.htm)
- ['Separator, Line' Category](https://www.fileformat.info/info/unicode/category/Zl/list.htm)

The function returns a `null` value for a `null` input.

**Compatibility**

The `normalizeWhitespaces(string)` function is available since **CloverETL 6.1.0**.
Example 217. Usage of normalizeWhitespaces
The function `normalizeWhitespaces(" many spaces ")` returns `many spaces`.

The function `normalizeWhitespaces("name:\t\tvalue")` returns `name: value`.

**See also:**[trim](string-functions-ctl2.md#trim), [normalizeDecimal](string-functions-ctl2.md#normalizedecimal)

#### NYSIIS

```ctl
string NYSIIS(string arg);
```

The `NYSIIS()` function returns the New York State Identification and Intelligence System Phonetic Code of the argument.

For more information, see the following site: [http://en.wikipedia.org/wiki/New_York_State_Identification_and_Intelligence_System](http://en.wikipedia.org/wiki/New_York_State_Identification_and_Intelligence_System). This implementation works with numbers. Input string which contains numbers will result in unchanged string. E.g. input '1234' results in string '1234'.

If the input of function is `null`, the function returns `null`. If the input of function is empty string, the function returns empty string.

**Compatibility**

The `NYSIIS(string)` function is available since **CloverETL 3.0.0**.
Example 218. Usage of NYSIIS
The function `NYSIIS("cheep")` returns `CAP`.

The function `NYSIIS("sheep")` returns `SAP`.

The function `NYSIIS("international")` returns `INTARNATANAL`.

**See also:**[editDistance](string-functions-ctl2.md#editdistance), [metaphone](string-functions-ctl2.md#metaphone), [soundex](string-functions-ctl2.md#soundex)

#### properCase

```ctl
string properCase(string arg);
string properCase(string arg, string locale);
```

The `properCase()` function takes one string argument and returns another string with all words converted to proper case. Proper case is text that is written with each of the first letters of every word being capitalized.

Specifying `locale` allows you to apply specifics of any language. For example, in English the proper case of word "iceland" is "Iceland" but in Dutch the proper case of word "ijsland" is "IJsland" because of the "ij" digraph present in the Dutch language.

If the `locale` is `null` or an empty string, the respective [default value](metadata-records-and-fields.md#locale) is used instead.

If the input is `null`, the function returns `null`.

**Compatibility**

The `properCase(string)` function is available since **CloverETL 6.1.0**.
Example 219. Usage of properCase
The function `properCase("The quick brown fox jumps over the lazy dog")` returns `The Quick Brown Fox Jumps Over The Lazy Dog`.

The function `properCase("ijsland")` returns `Ijsland`.

The function `properCase("ijsland", "nl.NL")` returns `IJsland`.

**See also:**[lowerCase](string-functions-ctl2.md#lowercase), [upperCase](string-functions-ctl2.md#uppercase)

#### randomString

```ctl
string randomString(integer minLength, integer maxLength);
```

The `randomString()` function returns a string consisting of lowercase letters.

Its length is between <`minLength`; `maxLength`>. Characters in the generated string always belong to ['a'-'z'] (no special symbols).

If one of the given arguments is `null`, the function fails with an error.

**Compatibility**

The `randomString(integer,integer)` function is available since **CloverETL 3.0.0**.
Example 220. Usage of randomString The function `randomString(3, 5)` returns for example `qjfxq`.
**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomUUID](string-functions-ctl2.md#randomuuid), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### randomUUID

```ctl
string randomUUID();
```

The function `randomUUID()` generates a random universally unique identifier (UUID).

The generated string has this format:

`hhhhhhhh-hhhh-hhhh-hhhh-hhhhhhhhhhhh`

where `h` belongs to `[0-9a-f]`. In other words, you generate hexadecimal code of a random 128bit number.

For more details on the algorithm used, see [the Java documentation](http://docs.oracle.com/javase/1.5.0/docs/api/java/util/UUID.html).

**Compatibility**

The `randomUUID()` function is available since **CloverETL 3.2.0**.
Example 221. Usage of randomUUID The function `randomUUID` returns, for example, `cee188a3-aa67-4a68-bcd2-52f3ec0329e6`.
**See also:**[random](mathematical-functions-ctl2.md#random), [randomBoolean](mathematical-functions-ctl2.md#randomboolean), [randomDate](date-functions-ctl2.md#randomdate), [randomGaussian](mathematical-functions-ctl2.md#randomgaussian), [randomInteger](mathematical-functions-ctl2.md#randominteger), [randomString](string-functions-ctl2.md#randomstring), [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed), [addNoise](mathematical-functions-ctl2.md#addnoise)

#### removeBlankSpace

```ctl
string removeBlankSpace(string arg);
```

The `removeBlankSpace()` function takes one string argument and returns another string with white characters removed.

The function removes chars `0x09`, `0x0A`, `0x0B`, `0x0C`, `0x0D`, `0x1C`, `0x1D`, `0x1E` and `0x1F`. The function does *not* remove chars `0x00A0` (hard space), `0x2007` and `0x202F`.

If the input is `null`, the function returns `null`.

**Compatibility**

The `removeBlankSpace()` function is available since **CloverETL 3.0.0**.
Example 222. Usage of removeBlankSpace
The function `removeBlankSpace("a quick brown fox")` returns `aquickbrownfox`.

The function `removeBlankSpace("1 000 000")` returns `1 000 000`, provided the string contains hard space (char 0xA0).

**See also:**[isBlank](miscellaneous-functions-ctl2.md#isblank), [removeDiacritic](string-functions-ctl2.md#removediacritic), [removeNonAscii](string-functions-ctl2.md#removenonascii), [removeNonPrintable](string-functions-ctl2.md#removenonprintable), [trim](string-functions-ctl2.md#trim)

#### removeDiacritic

```ctl
string removeDiacritic(string arg);
```

The `removeDiacritic()` function takes one string argument and returns another string with diacritical marks removed.

If the input is `null`, the function returns `null`.

**Compatibility**

The `removeDiacritic(string)` function is available since **CloverETL 3.0.0**.
Example 223. Usage of removeDiacritic
The function `removeDiacritic("Voyez le brick géant que j’examine.")` returns `Voyez le brick geant que j’examine.`

The function `removeDiacritic("Küchen")` returns `Kuchen`.

The function `removeDiacritic("Příšerný žluťoučký kůň úpěl ďábelské ódy.")` returns `Priserny zlutoucky kun upel dabelske ody.`

**See also:**[isAscii](string-functions-ctl2.md#isascii), [removeBlankSpace](string-functions-ctl2.md#removeblankspace), [removeNonAscii](string-functions-ctl2.md#removenonascii), [removeNonPrintable](string-functions-ctl2.md#removenonprintable)

#### removeNonAscii

```ctl
string removeNonAscii(string arg);
```

The `removeNonAscii()` function returns string with non-ASCII characters removed.

If the input is `null`, the function returns `null`.

**Compatibility**

The `removeNonAscii(string)` function is available since **CloverETL 3.0.0**.
Example 224. Usage of removeNonAscii
The function `removeNonAscii("Voyez le brick géant que j’examine.")` returns `Voyez le brick gant que j’examine`.

The function `removeNonAscii("Příšerný žluťoučký kůň úpěl ďábelské ódy.")` returns `Pern luouk k pl belsk dy.`

**See also:**[isAscii](string-functions-ctl2.md#isascii), [removeBlankSpace](string-functions-ctl2.md#removeblankspace), [removeNonAscii](string-functions-ctl2.md#removenonascii), [removeNonPrintable](string-functions-ctl2.md#removenonprintable)

#### removeNonPrintable

```ctl
string removeNonPrintable(string arg);
```

The `removeNonPrintable()` function takes one string argument and returns another string with non-printable characters removed.

If the input is `null`, the function returns `null`.

For the list of characters considered as non-printable, see [www.fileformat.info/controlcharacters](http://www.fileformat.info/info/unicode/category/Cc/list.htm).

The function is not dependent on character encoding.

Note that since **CloverETL 3.5**, the function does not remove non-ASCII characters anymore. If you need to have them removed, please use the `removeNonAscii(string)` function in addition.

**Compatibility**

The `removeNonPrintable(string)` function is available since **CloverETL 3.0.0**.
Example 225. Usage of removeNonPrintable Let’s call a string containing chars `A` (code 0x41), `B` (code 0x42), `bell` (code 0x07) and `C` (code 0x43) as `myString`. The function `removeNonPrintable(myString)` returns `ABC`.
**See also:**[isAscii](string-functions-ctl2.md#isascii), [removeBlankSpace](string-functions-ctl2.md#removeblankspace), [removeDiacritic](string-functions-ctl2.md#removediacritic), [removeNonAscii](string-functions-ctl2.md#removenonascii)

#### replace

```ctl
string replace(string arg, string regex, string replacement);
```

The `replace()` function replaces characters from the input string matching the regexp with the specified replacement string.

The function takes three string arguments - a string, a [*regular expression*](language-reference-ctl2.md#regular-expressions) and a replacement.

All parts of the string that match the regex are replaced. The user can also reference the matched text using a backreference in the replacement string. A backreference to the entire match is indicated as $0. If there are capturing parentheses, specifics groups as $1, $2, $3, etc. can be referenced.

**Important** - please beware of similar syntax of $0, $1, etc. While used inside the replacement string, it refers to matching regular expression parenthesis (in order). If used outside a string, it means a reference to an input field. See the examples.

A modifier can be used at the start of the regular expression: `(?i)` for case-insensitive search, `(?m)` for multiline mode or `(?s)` for "dotall" mode where a dot (".") matches even a newline character.

If the first argument of the function is `null`, the function returns `null`. If the regexp pattern is `null`, the function fails with an error. If the third argument is `null`, the function fails with an error, unless the specified regexp does not match the first input.

**Compatibility**

The `replace(string,string,string)` function is available since **CloverETL 3.0.0**.
Example 226. Usage of replace
The function `replace("Hello","[Ll]","t")` returns `"Hetto"`.

The function `replace("Hello", "e(l+)", "a$1")` returns `"Hallo"`.

The function `replace("Hello", "e(l+)", $in.0.name)` returns `HJohno` if input field `name` on port 0 contains the name `John`.

The function `replace("Hello", "(?i)L", "t")` will produce `Hetto` while `replace("Hello", "L", "t")` will just produce `Hello`.

The function `replace("cornerstone", "(corner)([a-z]*)", "$2 $1")` returns `stone corner`.

**See also:**[lowerCase](string-functions-ctl2.md#lowercase), [translate](string-functions-ctl2.md#translate), [upperCase](string-functions-ctl2.md#uppercase), [properCase](string-functions-ctl2.md#propercase)

#### reverse

```ctl
string reverse(string arg);
```

The `reverse()` function reverses the order of characters of a given string and returns the reverted string.

If the given string is `null`, the function returns `null`.

**Compatibility**

The `reverse(string)` function is available since **CloverETL 3.0.0**.
Example 227. Usage of reverse Function `reverse("knot")` returns `tonk`.
**See also:** Record functions: [reverse(list)](container-functions-ctl2.md#reverse)

#### right

```ctl
string right(string arg, integer length);
string right(string arg, integer length, boolean spacePad);
```

The `right()` function returns the substring of the length specified as the second argument counted from the end of the string specified as the first argument.

If the input string is shorter than the `length` parameter, the function returns the original string.

If the input is `null`, the function returns `null`.

If the `spacePad` argument is set to `true`, the new string is padded. Whereas if it is `false` or the function does not have the argument `spacePad`, the input string is returned as the result with no space added.

**Compatibility**

The `right(string,integer)` function is available since **CloverETL 3.0.0**.

The `right(string,integer,boolean)` function is available since **CloverETL 3.1.0**.
Example 228. Usage of right
The function `right("A very long string", 4)` returns `ring`.

The function `right("A very long string", 20)` returns `A very long string`.

The function `right("text", 10, true)` returns `text`.

**See also:**[left](string-functions-ctl2.md#left), [substring](string-functions-ctl2.md#substring)

#### rpad

```ctl
string rpad(string input, integer length);
string rpad(string input, integer length, string filler);
```

The function `rpad` pads a string from right side to specified length using space or user-defined character.

The parameter `input` contains a string to be padded. If the `input` is shorter than specified in the parameter `length`, the `input` is padded from the right side using `filler`. The `input` with sufficient length is returned unmodified.

If the parameter `input` is `null`, the function returns `null`.

The parameter `length` defines the minimal length of the result string. If the parameter `length` is *negative*, the function fails.

The optional parameter `filler` defines the character used for pad. The function `rpad(string, integer)` uses *space character* as a filler. If the `filler` is `null`, *empty string* or a string having more than `1` character, the function fails.

**Compatibility**

The `rpad(string,integer)` and `rpad(string,integer,string)` functions are available since **CloverETL 4.0.0-M1**.
Example 229. Usage of rpad
The function `rpad("A quick brown fox", 2)`returns `"A quick brown fox"`.

The function `rpad("A quick brown fox", 20)` returns `"A quick brown fox "`.

The function `rpad(null, 0)` returns `null`.

The function `rpad("A quick fox", -1)` fails.

The function `rpad("A quick fox", null)` fails.

The function `rpad("A quick brown fox", 20, ".")` returns `"A quick brown fox…"`.

The function `rpad("A quick brown fox", 20, null)` fails.

The function `rpad("A quick brown fox", 20, "")` fails.

The function `rpad("A quick brown fox", 20, " jumps")` fails.

**See also:**[left](string-functions-ctl2.md#left), [lpad](string-functions-ctl2.md#lpad), [right](string-functions-ctl2.md#right)

#### soundex

```ctl
string soundex(string arg);
```

The `soundex()` function takes one string argument and converts the string to another.

The resulting string consists of the first letter of the string specified as the argument and three digits. The three digits are based on the consonants contained in the string when similar numbers correspond to similarly sounding consonants.

If the input of the function is `null`, the function returns `null`.

If the input is an empty string, the function returns an empty string.

**Compatibility**

The `soundex(string)` function is available since **CloverETL 3.0.0**.
Example 230. Usage of soundex
The function `soundex("cheep")` returns `C100`.

The function `soundex("sheep")` returns `S100`.

The function `soundex("book")` returns `B200`.

The function `soundex("bookworm")` returns `B265`.

The function `soundex("international")` returns `I536`.

**See also:**[editDistance](string-functions-ctl2.md#editdistance), [metaphone](string-functions-ctl2.md#metaphone), [NYSIIS](string-functions-ctl2.md#nysiis)

#### split

```ctl
string[] split(string arg, string regex);
string[] split(string arg, string regex, integer limit);
```

The `split()` function splits a string from the first argument, based on a [*regular expression*](language-reference-ctl2.md#regular-expressions) given as the second argument.

The function searches in the first argument for substrings matching the `regexp`. If any substring matching the `regexp` exists, it is used as a delimiter and the `arg` is split up using the delimiter. The resulting parts of the string are returned as a list of strings. If the regular pattern does not match any character in the string `arg`, a list containing one item (the string `arg`) is returned.

The function `split()` removes terminating empty list items from the result. See the function `split("cuckoo","o")` in examples.

If the input parameter `arg` is an empty string, the function returns a list with one empty string.

If the input `arg` is `null`, the function returns an empty list.

If the `regexp` argument is `null`, the function fails with an error.

The `limit` parameter limits the number of items in the list to be returned. If the limit is *positive*, at most the specified number of items will be returned. The unsplit residue of input string is the last item of the list. If the `limit` is *zero*, the limit is not applied and the function works as without the `limit` parameter: The trailing empty list items are trimmed. If the `limit` parameter is *negative*, the limit is not applied and trailing empty fields are not trimmed. If the function is called without the `limit` parameter, it works in the same way as with `limit` set to `0`.

**Compatibility**

The `split(string,string)` function is available since **CloverETL 3.0.0**.

If the input (`arg`) of the function is `null`, the function returns a list with one `null` string in **CloverETL 3.5.x** and earlier.

The `split(string,string,integer)` is available since **CloverETL 4.0.0-M1**.
Example 231. Usage of split
The function `split("anaconda", "a")` returns `[, n, cond]`.

The function `split("abcdefg", "[ce]")` returns `["ab", "d", "fg"]`.

The function `split("cuckoo", "o")` returns `[cuck]`. The empty terminating list item is discarded.

The function `split("cuckoos", "o")` returns `[cuck, , s]`

The function `split("oak,spruce,larch,,", ",")` returns `[oak, spruce, larch]`.

The function `split("oak,spruce,larch,,maple", ",")` returns `[oak, spruce, larch, , maple]`. The empty list item has not been discarded as there is non-empty string `maple` following the empty list item.

The function `split("rabbit", "b{2}[aeiou]")` returns `[ra, t]`.

The function `split("woodcock", "oo")` returns `[w, dcock]`.

The function `split("woodcock", "[oo]")` returns `[w, , dc, ck]`.

The function `split("frog,blowfish,serpent",";")` returns `[frog,blowfish,serpent]`. The first string does not contain a semicolon, thus the content of the first list item is `frog,blowfish,serpent`.

The function `split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", -1)` returns `[/bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, , ]`.

The function `split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", 0)` returns `[/bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin]`.

The function `split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", 1)` returns `[/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::]`.

The function `split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", 2)` returns `[/bin, /sbin:/usr/bin:/usr/sbin:/usr/local/bin::]`.

The function `split("/bin:/sbin", ":", 5)` returns `[/bin, /sbin]`.

**See also:**[concat](string-functions-ctl2.md#concat), [concatWithSeparator](string-functions-ctl2.md#concatwithseparator), [join](string-functions-ctl2.md#join), [substring](string-functions-ctl2.md#substring), [matchGroups](string-functions-ctl2.md#matchgroups)

#### startsWith

```ctl
boolean startsWith(string str, string sub);
```

The `startsWith()` function returns `true` if the parameter `str` starts with string `sub`.

If the parameter `str` is `null`, the function returns `false`.

If the parameter `sub` is `null`, the function fails.

**Compatibility**

The `startsWith(string)` function is available since **CloverETL 4.0.0-M1**.
Example 232. Usage of startsWith
The function `startsWith("quadratic", "quad")` returns `true`.

The function `startsWith("quadratic", "linear")` returns `false`.

The function `startsWith(null, "a")` returns `false`.

The function `startsWith("quadratic", null)` fails.

**See also:**[contains](string-functions-ctl2.md#contains), [endsWith](string-functions-ctl2.md#endswith)

#### substring

```ctl
string substring(string arg, integer fromIndex);
string substring(string arg, integer fromIndex, integer length);
```

The `substring()` function returns a substring of an input string.

The function `substring(arg, fromIndex)` returns a substring of `arg` starting at the position `fromIndex`.

The function `substring(arg, fromIndex, length)` returns a substring of `arg` starting at the position `fromIndex` limited by `length`.

If the original string `arg` is `null`, the function returns `null`. If the `arg` is *empty string*, the function returns *empty string*. See the compatibility notice.

The parameter `fromIndex` defines the starting position of the substring. If `fromIndex` is negative or `null`, the function fails. See compatibility notice.

The parameter `length` is a maximal length of the returned substring. If `length` is negative or `null`, the function fails.

**Compatibility**

The function `substring()` works differently in **CloverETL 3.5.x** and earlier.

The function `substring()` fails, if the input string `arg` is `null` in **CloverETL 3.5.x** and earlier.

The function `substring()` fails, if any of integer parameters is `null` or out of range of the input string in **CloverETL 3.5.x**. Since **CloverETL 4.0.0.M1**, it fails only with *negative* or `null` values.

The `substring(string,integer,integer)` function is available since **CloverETL 3.0.0**.

The `substring(string, integer)` function is available since **CloverETL 4.0.0-M1**.
Example 233. Usage of substring
The function `substring("elfish", 2)` returns `fish`.

The function `substring("network", 20)` returns *empty string*.

The function `substring("network", null)` fails.

The function `substring("minute", 2, 3)` returns `nut`.

The function `substring("text", 1, 2)` returns `"ex"`.

The function `substring("network", 3, 0)` returns *empty string*.

The function `substring("network", 20, 2)` returns *empty string*. This fails in **CloverETL 3.5.x**, see compatibility notice.

The function `substring("network", 6, 5)` returns `k`. This fails in **CloverETL 3.5.x**, see compatibility notice.

The function `substring("network", null, 1)`fails.

The function `substring("network", -2, 1)`fails.

The function `substring("network", 3, null)`fails.

The function `substring("network", 3, -4)` fails.

The function `substring(null, 1, 1)` returns `null`. This fails in **CloverETL 3.5.x**, see compatibility notice.

**See also:**[charAt](string-functions-ctl2.md#charat), [cut](string-functions-ctl2.md#cut), [left](string-functions-ctl2.md#left), [right](string-functions-ctl2.md#right), [trim](string-functions-ctl2.md#trim)

#### toProjectUrl

```ctl
string toProjectUrl(string path);
```

The `toProjectUrl()` function converts a relative path, e.g. `data-in/file.txt` to a full URL containing the name of the sandbox: `sandbox://mysandbox/data-in/file.txt`.

The parameter `path` is a relative path to the file.

If the parameter `path` is `null`, the function `toProjectUrl()` returns `null`.

**Compatibility**

The `toProjectUrl()` function is available since **CloverETL 4.0**.
Example 234. Usage of toProjectURL
Following examples use sandbox called `documentation`. If you use examples in your sandbox, you will see `yourSandboxName` instead of `documentation`.

The function `toProjectUrl("")` returns `sandbox://documentation/`.

The function `toProjectUrl(null)` returns `null`.

The function `toProjectUrl(".")` returns `sandbox://documentation/`.

The function `toProjectUrl("/")` returns `file:/`.

#### translate

```ctl
string translate(string arg, string searchingSet, string replaceSet);
```

The `translate()` function replaces the characters given in the second string of the first argument with characters from the third string.

If one or both of the second or the third argument is `null`, the function fails with an error.

If the input of the function is `null`, the function returns `null`.

**Compatibility**

The `translate(string,string,string)` function is available since **CloverETL 3.0.0**.
Example 235. Usage of translate The function call `translate('Hello','eo','is')` results in the string `Hills`.
**See also:**[replace](string-functions-ctl2.md#replace)[toAbsolutePath](miscellaneous-functions-ctl2.md#toabsolutepath)

#### trim

```ctl
string trim(string arg);
```

The `trim()` function takes one string argument and returns another string with leading and trailing white spaces removed.

If the input of the function is an empty string, the function returns an empty string.

If the input of the function is `null`, the function returns `null`.

**Compatibility**

The `trim(string)` function is available since **CloverETL 3.0.0**.
Example 236. Usage of trim The function `trim(" Text and space chars ")` returns `Text and space chars`.
**See also:**[isBlank](miscellaneous-functions-ctl2.md#isblank), [removeBlankSpace](string-functions-ctl2.md#removeblankspace), [replace](string-functions-ctl2.md#replace), [substring](string-functions-ctl2.md#substring)

#### unescapeUrl

```ctl
string unescapeUrl(string arg);
```

The `unescapeUrl()` function decodes escape sequences of illegal characters within components of a specified URL.

Escape sequences consist of a percent (`%`) symbol, followed by the two-digit hexadecimal representation (case-insensitive) of the ISO-Latin code point for the character, e.g. `%20` is the escaped encoding for the US-ASCII space character. For the URL component description, see [isUrl](string-functions-ctl2.md#isurl).

Function accepts a valid URL only. For an invalid URL, empty string or `null` input, the function fails with an error.

**Compatibility**

The `unescapeUrl(string)` function is available since **CloverETL 3.1.0**.
Example 237. Usage of unescapeUrl The function `unescapeUrl("http://www.example.com/the%20file.html")` returns `http://www.example.com/the file.html`
**See also:**[escapeUrl](string-functions-ctl2.md#escapeurl), [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment), [isUrl](string-functions-ctl2.md#isurl), [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment)

#### unescapeUrlFragment

```ctl
string unescapeUrlFragment(string  input);
string unescapeUrlfragment(string input, string encoding);
```

The function unescapes a string escaped by [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment).

The parameter `input` is a string to be unescaped. It the parameter is null, the function returns `null`.

The parameter `encoding` is an encoding to be used in conversion. If the `encoding` is `null`, the conversion fails.

**Compatibility**

The `unescapeUrlFragment(string)` function is available since **CloverETL 4.0.0-M1**.
Example 238. Usage of unescapeUrlFragment
The function `unescapeUrlFragment(null)` returns `null`.

The function `unescapeUrlFragment("")` returns *empty string*.

The function `unescapeUrlFragment("the+URL")` returns `"the URL"`.

The function `unescapeUrlFragment("cook+book", null)` fails.

**See also:**[escapeUrl](string-functions-ctl2.md#escapeurl), [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment), [isUrl](string-functions-ctl2.md#isurl), [unescapeUrl](string-functions-ctl2.md#unescapeurl)

#### unescapeXML

```ctl
string unescapeXML(string input);
```

The **unescapeXML(string)** function is designed to convert XML-escaped entities back into their original, unescaped characters. This function is useful when you need to extract or display the original content from an XML document that has previously been processed with the [escapeXML](string-functions-ctl2.md#escapexml) function.

List of reserved characters: `' , ", &, <, >`

**Compatibility**

The `unescapeXML(string)` function is available since **CloverDX 6.4.0**.
Example 239. Usage of unescapeXML
The function unescapeXML("&lt;element name=&quot;&amp;myname;&quot;&gt;") returns `<element name="&myname;">`.

The function `unescapeXML("Peter O&apos;Brian")` returns `Peter O’Brian`.

The following example:

```
string nameOfCustomer = "Progress &amp; Prosperity, Co. &gt; Expectations";
  unescapeXML(nameOfCustomer)
```

Returns the following:

```
Progress & Prosperity, Co. > Expectations
```

**See also:**[escapeXML](string-functions-ctl2.md#escapexml)

#### unicodeNormalize

```ctl
string unicodeNormalize(string input, string form);
```

The `unicodeNormalize()` normalizes an input string using a specified *normalization form*.

The parameter `input` contains the string to be normalized. If the parameter `input` is `null`, the function returns `null`.

The parameter `form` defines the *normalization form* to be used. Following normalization forms are available:

- NFD: Canonical Decomposition
- NFC: Canonical Decomposition followed by Canonical Composition
- NFKD: Compatibility Decomposition
- NFKC: Compatibility Decomposition followed by Canonical Composition

If the parameter `form` is `null`, the function fails.

**Compatibility**

The `unicodeNormalize(string)` function is available since **CloverETL 4.0.0-M1**.
Example 240. Usage of unicodeNormalize
The function `unicodeNormalize("\u00C5", "NFD")` returns `"\u0065\u030A"`.

The function `unicodeNormalize("\u0041"+"\u030A", "NFD")` returns `"\u0065\u030A"`.

The function `unicodeNormalize("\u00C5", "NFC")` returns `"\u00C5"`.

The function `unicodeNormalize("\u0041"+"\u030A", "NFC")` returns `"\u00C5"`.

The function `unicodeNormalize("\u00C5", null)` fails.

The function `unicodeNormalize(null, "NFD")` returns `null`.

**See also:**[isUnicodeNormalized](string-functions-ctl2.md#isunicodenormalized)

#### upperCase

```ctl
string upperCase(string arg);
```

The `upperCase()` function takes one string argument and returns another string with cases converted to upper cases only.

The function returns `null` for a `null` input.

**Compatibility**

The `upperCase(string)` function is available since **CloverETL 3.0.0**.
Example 241. Usage of upperCase The function `upperCase("Some string")` returns `SOME STRING`.
**See also:**[lowerCase](string-functions-ctl2.md#lowercase), [properCase](string-functions-ctl2.md#propercase)

#### validateCreditCard

```ctl
string validateCreditCard(string creditCard, boolean acceptEmpty);
```

The `validateCreditCard()` function takes string argument and uses Luhn algorithm, also known as 'modulus 10', to determine whether the argument is a valid credit card number.

The function returns `null` if the validation passes or an error message if it fails.

If the second parameter is `true` an empty string value is considered to be a valid value.
Example 242. Usage of validateCreditCard
The function `validateCreditCard("5305-7204-2019-5319", false)` returns `null`.

The function `validateCreditCard("1234-5678-9012-3456", false)` returns `Checksum is not valid`.

The function `validateCreditCard(" ", true)` returns `null`.

The function `validateCreditCard(" ", false)` returns `Empty card number is not allowed`.

**See also:**[validateEmail](string-functions-ctl2.md#validateemail), [validatePhoneNumber](string-functions-ctl2.md#validatephonenumber)

#### validateEmail

```ctl
string validateEmail(string email, boolean acceptEmpty);
```

The `validateEmail()` function takes string argument and performs syntactic check according to [RFC822](https://www.w3.org/Protocols/rfc822) standard to determine whether the argument is a valid email address. It does not try to connect or to send any message to the syntactically valid argument.

The function returns `null` if the validation passes or an error message if it fails.

If the second parameter is `true` an empty string value is considered to be a valid value.
Example 243. Usage of validateEmail
The function `validateEmail("john.doe@example.com", false)` returns `null`.

The function `validateEmail("john.doeexamplecom", false)` returns `Missing final '@domain'`.

The function `validateEmail(null, true)` returns `null`.

The function `validateEmail(null, false)` returns `Empty email is not allowed`.

**See also:**[validateCreditCard](string-functions-ctl2.md#validatecreditcard), [validatePhoneNumber](string-functions-ctl2.md#validatephonenumber)

#### validatePhoneNumber

```ctl
string validatePhoneNumber(string email, string phoneRegion, boolean acceptEmpty);
```

The `validatePhoneNumber()` function takes string argument and validates if its a phone number.

The second parameter is phone region in a form of two letters [ISO Alpha 2](https://www.countrycode.org/) code. Its ignored and may be left empty if the phone number is written in international format.

The function returns `null` if the validation passes or an error message if it fails.

If the third parameter is `true` an empty string value is considered to be a valid value.
Example 244. Usage of validatePhoneNumber
The function `validatePhoneNumber("(800) 555-0111", null, false)` returns `null`.

The function `validatePhoneNumber("8005550111", null, false)` returns `null`.

The function `validatePhoneNumber("+1 (800) 123-4567", null, false)` returns `Invalid phone number`.

The function `validatePhoneNumber(null, "US", true)` returns `null`.

The function `validatePhoneNumber(null, "US", false)` returns `Empty phone number is not allowed`.

**See also:**[validateCreditCard](string-functions-ctl2.md#validatecreditcard), [validateEmail](string-functions-ctl2.md#validateemail)
