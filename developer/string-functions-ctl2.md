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
| [decode](string-functions-ctl2.md#decode) |
| [editDistance](string-functions-ctl2.md#editdistance) |
| [endsWith](string-functions-ctl2.md#endswith) |
| [escapeJson](string-functions-ctl2.md#escapejson) |
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
| [unescapeJson](string-functions-ctl2.md#unescapejson) |
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
> Remember that numeric and date formats are displayed using the system value **Locale** or **Locale** specified in the defaultProperties file, unless other **Locale** is explicitly specified.
>
> For more information on how **Locale** may be changed in the defaultProperties, see [Engine configuration](../admin/designer-configuration.md#engine-configuration).

Here we provide the list of the functions:

#### byteAt

```ctl
integer byteAt(byte arg, integer index);
```

The function `byteAt` returns the byte on the specified position.

The `arg` is an input `byte` array.

The `index` defines the position in the `arg`. The first item has `index` equal to `0`.

##### Error states

- If the `index` is out of bound, the function fails.
- If any of the arguments is `null`, the function fails.

##### Examples
Example 165. Usage of byteAt

```ctl
byte b = hex2byte("6d75736b726174");
byteAt(b, 0);
    // Returns 0x6d, which corresponds to 109.
byteAt(b, -1);
    // Fails for this input.
byteAt(b, null);
    // Fails for this input.
byteAt(null, 0);
    // Fails for this input.
```

##### Compatibility

- The `byteAt()` function is available since **CloverETL 4.0.0**.

##### See also

- [bitAnd](mathematical-functions-ctl2.md#bitand)
- [bitIsSet](mathematical-functions-ctl2.md#bitisset)
- [bitSet](mathematical-functions-ctl2.md#bitset)
- [bitLShift](mathematical-functions-ctl2.md#bitlshift)
- [bitNegate](mathematical-functions-ctl2.md#bitnegate)
- [bitOr](mathematical-functions-ctl2.md#bitor)
- [bitRShift](mathematical-functions-ctl2.md#bitrshift)
- [bitXor](mathematical-functions-ctl2.md#bitxor)
- [charAt](string-functions-ctl2.md#charat)

---

#### charAt

```ctl
string charAt(string arg, integer index);
```

The `charAt()` function returns the character from `arg` which is located at the given `index`.

##### Error states

- The function works only for indexes between `0` and `length of input - 1`, otherwise it fails with an error.
- For `null` input and `empty string` input the function fails with an error.

##### Examples
Example 166. Usage of charAt

```ctl
charAt("ABC", 1);
    // Returns B.
charAt("ABC", 0);
    // Returns A.
charAt("ABC", -1);
    // Fails with an error.
charAt("ABC", 3);
    // Fails with an error.
```

##### Compatibility

- The `charAt(string,integer)` function is available since **CloverETL 3.0.0**.

##### See also

- [byteAt](string-functions-ctl2.md#byteat)
- [codePointAt](string-functions-ctl2.md#codepointat)
- [substring](string-functions-ctl2.md#substring)

---

#### chop

```ctl
string chop(string arg);
string chop(string arg, string regexp);
```

The `chop()` function removes the line feed and the carriage return characters or characters corresponding to the provided regular pattern from the string.

If the input is empty string, the function returns empty string.

##### Error states

- For `null` input the function fails with an error.
- If the `regexp` is `null`, the function fails with an error.

##### Examples
Example 167. Usage of chop

```ctl
chop("ab\n z");
    // Returns ab z.
// The \n means line feed (char 0x0A). The character 0x0A can be added to string  either from string read by any of readers, or set up using functions hex2byte and byte2str.
chop("book and pencil", "and");
    // Returns book  pencil.
chop("A quick brown fox jumps.", "[a-y]{5}");
    // Returns A   fox .
```

##### Compatibility

- The `chop(string)` and `chop(string,string)` function is available since **CloverETL 3.0.0**.

##### See also

- [matches](string-functions-ctl2.md#matches)
- [matchGroups](string-functions-ctl2.md#matchgroups)
- [substring](string-functions-ctl2.md#substring)

---

#### codePointAt

```ctl
integer codePointAt(string str, integer index);
```

The function `codePointAt()` returns code of a Unicode character from the given position in the string `str`.

The `str` parameter contains string with Unicode characters.

The `index` parameter specifies a position of the character in the string `str`. The first character has index 0.

##### Error states

- If `str` is `null`, the function fails.
- If the `index` parameter is `null`, the function fails. If the `index` parameter is out of range of the string (*negative* or *greater than or equal to* length of string), the function fails.

##### Examples
Example 168. Usage of codePointAt

```ctl
codePointAt("enseñar", 0);
    // Returns 101.
codePointAt("enseñar", 4);
    // Returns 241.
codePointAt("enseñar", -1);
    // Fails for this input.
codePointAt("enseñar", 10);
    // Fails for this input.
codePointAt("enseñar", null);
    // Fails for this input.
codePointAt(null, 2);
    // Fails for this input.
```

##### Compatibility

- The `codePointAt(string,integer)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [charAt](string-functions-ctl2.md#charat)
- [codePointToChar](string-functions-ctl2.md#codepointtochar)
- [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint)

---

#### codePointLength

```ctl
integer codePointLength(integer code);
```

The function `codePointLength()` returns number of char values needed to encode the Unicode character `code`.

If `code` is *greater than or equal to*`0x10000`, the function returns `2`. Otherwise returns `1`. Invalid codes are not checked. If validation is needed, use the `isValidCodePoint` function.

The parameter `code` is Unicode code point.

##### Error states

- If the `code` is `null`, the function fails.

##### Examples
Example 169. Usage of codePointLength

```ctl
codePointLength(0x41);
    // Returns 1.
codePointLength(0x10300);
    // Returns 2.
```

##### Compatibility

- The `codePointLength(integer)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [codePointAt](string-functions-ctl2.md#codepointat)
- [codePointToChar](string-functions-ctl2.md#codepointtochar)
- [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint)

---

#### codePointToChar

```ctl
string codePointToChar(integer code);
```

The function `codePointToChar()` converts Unicode code to character.

The parameter contains `code` of the character.

##### Error states

- If the `code` is `null`, *negative* or *greater than*`0x10FFFF`, the function fails.

##### Examples
Example 170. Usage of codePointToChar

```ctl
codePointToChar(65);
    // Returns A.
codePointToChar(0x3B1);
    // Returns α.
codePointToChar(0x10300);
    // Returns 𐌀.
codePointToChar(-1);
    // Fails for this input.
codePointToChar(null);
    // Fails for this input.
codePointToChar(0x110000);
    // Fails for this input.
```

##### Compatibility

- The `codePointToChar(integer)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [codePointAt](string-functions-ctl2.md#codepointat)
- [codePointLength](string-functions-ctl2.md#codepointlength)
- [isUnicodeNormalized](string-functions-ctl2.md#isunicodenormalized)

---

#### concat

```ctl
string concat(string arg1, string ..., string argN);
```

The function `concat()` returns concatenation of the strings.

The `concat` function accepts unlimited number of arguments of the string data type. You can also concatenate these arguments using plus signs, but this function is faster for more than two arguments.

`Null` value of arguments are replaced with string 'null' in concatenated string.
> [!NOTE]
> Concatenation of more strings with the `concat()` function is faster than concatenation with `+` operator.

##### Error states

- The function has no documented error states.

##### Examples
Example 171. Usage of concat

```ctl
concat("abc", "def", "ghi");
    // Returns abcdefghi.
concat("abc", null, "ghi");
    // Returns abcnullghi.
```

##### Compatibility

- The `concat(string, …)` function is available since **CloverETL 3.0.0**.

##### See also

- [concatWithSeparator](string-functions-ctl2.md#concatwithseparator)
- [join](string-functions-ctl2.md#join)
- [cut](string-functions-ctl2.md#cut)
- [substring](string-functions-ctl2.md#substring)

---

#### concatWithSeparator

```ctl
string concatWithSeparator(string separator, string arg1, string ..., string argN);
```

The function `concatWithSeparator()` joins parameters `arg1` to `argN` using `separator`.

The `separator` parameter defines a string to be used as a separator in the concatenated string.

The parameters `arg1` to `argN` contain strings to be concatenated. Parameters to be concatenated having `null` values are omitted.
> [!NOTE]
> The `concat()` and `concatWithSeparator()` functions handle `null` strings differently.

##### Error states

- If the `separator` parameter is `null`, the function fails.

##### Examples
Example 172. Usage of concatWithSeparator

```ctl
concatWithSeparator(",", "coffee", "milk", "chocolate");
    // Returns coffee,milk,chocolate.
concatWithSeparator("", "bottle", "neck");
    // Returns bottleneck.
concatWithSeparator("_", "bash", null, "tcsh");
    // Returns bash_tcsh.
concatWithSeparator(null, "");
    // Fails for this input.
concatWithSeparator(" ", "tabular", "itemize");
    // Returns tabular itemize.
concatWithSeparator("-", null);
    // Returns empty string.
```

##### Compatibility

- The `concatWithSeparator(string,string,…)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [concat](string-functions-ctl2.md#concat)
- [join](string-functions-ctl2.md#join)
- [split](string-functions-ctl2.md#split)

---

#### contains

```ctl
boolean contains(string input, string substring);
```

The function `contains()` returns true if the `input` string contains a `substring`. Otherwise the function returns `false`.

If the parameter `input` is `null`, the function returns `false`.

##### Error states

- If the parameter `substring` is `null`, the function fails.

##### Examples
Example 173. Usage of contains

```ctl
contains("woodcutting", "wood");
    // Returns true.
contains("elm", "coffee");
    // Returns false.
contains(null, "pine");
    // Returns false.
contains("oak", "");
    // Returns true.
contains("", "");
    // Returns true.
contains("spruce", null);
    // Fails for this input.
```

##### Compatibility

- The `contains(string,string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [endsWith](string-functions-ctl2.md#endswith)
- [startsWith](string-functions-ctl2.md#startswith)
- [substring](string-functions-ctl2.md#substring)

---

#### countChar

```ctl
integer countChar(string arg, string character);
```

The `countChar()` returns the number of occurrences of the character specified as the second argument in the string specified as the first argument.

##### Error states

- If one of the given arguments is `null` or an empty string, the function fails with an error.

##### Examples
Example 174. Usage of countChar

```ctl
countChar("ALABAMA", "A");
    // Returns 4.
countChar("Alabama", "a");
    // Returns 3.
```

##### Compatibility

- The `countChar(string,string)` function is available since **CloverETL 3.0.0**.

##### See also

- [length](string-functions-ctl2.md#length)

---

#### cut

```ctl
string[] cut(string arg, integer[] indices);
```

The `cut()` function returns a list of strings which are substrings of the original string specified in the first argument.

The second argument (`indices`) specifies rules on how the first argument is cut. The number of elements of the list specified as the second argument must be even. The integers in the list serve as position (each number in the odd position) and length (each number in the even position). Substrings of the specified length are taken from the string specified as the first argument starting from the specified position (excluding the character at the specified position).

##### Error states

- If the first argument is `null` or an empty string, the function fails with an error.

##### Examples
Example 175. Usage of cut

```ctl
cut("somestringasanexample",[2,3,1,5]);
    // Returns ["mes","omest"].
```

##### Compatibility

- The `cut(string,integer[])` function is available since **CloverETL 3.0.0**.

##### See also

- [matchGroups](string-functions-ctl2.md#matchgroups)

---

#### decode

```ctl
string decode(variant expression,
                      variant search1, string result1,
                      variant search2, string result2,
                      variant..., string..., variant defaultResult);
integer decode(variant expression,
                      variant search1, integer result1,
                      variant search2, integer result2,
                      variant..., integer..., integer defaultResult);
```

The `decode()` function creates a small lookup from search-result pairs. It compares the `expression` to each `search` value one by one, and returns the corresponding `result` value. If no match is found, then `defaultResult` is returned. If `defaultResult` is ommitted, then `null` is returned.

If the first argument is `null` or an empty string, the function returns default value.

##### Error states

- The function has no documented error states.

##### Examples
Example 176. Usage of decode

```ctl
decode(1, 1, "value1", "default");
    // Returns "value1".

integer code = 3;
decode(code, 1, 'Southlake',
             2, 'San Francisco',
             3, 'New Jersey',
             4, 'Seattle', 'Non domestic');
    // Returns "New Jersey".
```

##### Compatibility

- The `decode()` function is available since **CloverETL 7.5.0**.

##### See also

- [iif](miscellaneous-functions-ctl2.md#iif)

---

#### editDistance

```ctl
integer editDistance(string arg1, string arg2);
integer editDistance(string arg1, string arg2, string locale);
integer editDistance(string arg1, string arg2, integer strength);
integer editDistance(string arg1, string arg2, integer strength, string locale);
integer editDistance(string arg1, string arg2, integer strength, integer maxDifference);
integer editDistance(string arg1, string arg2, string locale, integer maxDifference);
integer editDistance(string arg1, string arg2, integer strength, string locale, integer maxDifference);
```

The `editDistance()` function compares two string arguments.

##### Error states

- If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.

##### editDistance (arg1, arg2)

```ctl
integer editDistance(string arg1, string arg2);
```

The comparison strength is 4 by default, the locale uses the system value by default, and the maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the two arguments to the other.

However, when the function is being executed, if it counts that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance-arg1-arg2-strength-locale-maxdifference) function below.
Example 177. Usage of editDistance 1

```ctl
editDistance("see", "sea");
    // Returns 1.
editDistance("bike", "bill");
    // Returns 2.
editDistance("age", "get");
    // Returns 2.
editDistance("computer", "preposition");
    // Returns 4.
```

##### editDistance (arg1, arg2, locale)

```ctl
integer editDistance(string arg1, string arg2, string locale);
```

The `editDistance()` function compares two string arguments using the specified locale.

The function accepts two strings to compare and a third argument that specifies the [Locale](metadata-records-and-fields.md#locale) used for comparison.

The default strength of comparison is 4.

The maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other.

However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance-arg1-arg2-strength-locale-maxdifference) function below.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 178. Usage of editDistance 2

```ctl
editDistance("âgé", "âge", "en.US");
    // Returns 1.
editDistance("âgé", "âge", "fr.FR");
    // Returns 1.
```

##### editDistance (arg1, arg2, strength)

```ctl
integer editDistance(string arg1, string arg2, integer strength);
```

The `editDistance()` function compares two strings using the specified strength of comparison.

The function accepts two strings to compare and a third integer argument that specifies the strength of comparison.

The default locale is the system value.

The maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other.

However, when the function is being executed, if it counts that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance-arg1-arg2-strength-locale-maxdifference) function below.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 179. Usage of editDistance 3

```ctl
editDistance("computer", "preposition", 4);
    // Returns 4.
editDistance("computer", "preposition", 7);
    // Fails for this input.
editDistance("âgé", "âge", 2);
    // Returns 0.
editDistance("âgé", "âge", 3);
    // Returns 1.
```

##### editDistance (arg1, arg2, strength, locale)

```ctl
integer editDistance(string arg1, string arg2, integer strength, string locale);
```

The `editDistance()` function compares two strings using the specified strength of comparison and locale.

The function accepts two strings to compare, a third argument that specifies the strength of comparison, and a fourth argument that specifies the [Locale](metadata-records-and-fields.md#locale) used for comparison.

The maximum difference is 3 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other.

However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance-arg1-arg2-strength-locale-maxdifference) function below.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 180. Usage of editDistance 4

```ctl
editDistance("âgé", "âge", 2, "en.US");
    // Returns 1.
editDistance("âgé", "âge", 2, "fr.FR");
    // Returns 0.
```

##### editDistance (arg1, arg2, locale, maxDifference)

```ctl
integer editDistance(string arg1, string arg2, string locale, integer maxDifference);
```

The `editDistance()` function compares two strings using the specified locale and `maxDifference`.

The function accepts two strings to compare, a third argument that specifies the [Locale](metadata-records-and-fields.md#locale) used for comparison, and a fourth argument that specifies the maximum difference.

The strength of comparison is 4 by default.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other.

However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance-arg1-arg2-strength-locale-maxdifference) function below.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 181. Usage of editDistance 5

```ctl
editDistance("bike", "bicycle", "en.US", 2);
    // Returns 2.
```

##### editDistance (arg1, arg2, strength, maxDifference)

```ctl
integer editDistance(string arg1, string arg2, integer strength, integer maxDifference);
```

The `editDistance()` function compares two strings using the specified strength of comparison and maximum difference.

The function accepts two strings to compare and two additional arguments.

The third argument specifies the strength of comparison, and the fourth argument specifies the maximum difference. The locale uses the default system value.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other.

However, when the function is being executed, if it finds that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

For more details, see the ["editDistance (string, string, integer, string, integer)"](string-functions-ctl2.md#editdistance-arg1-arg2-strength-locale-maxdifference) function below.

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 182. Usage of editDistance 6

```ctl
editDistance("OAK", "oak", 3, 1);
    // Returns 0.
editDistance("OAK", "oak", 4, 3);
    // Returns 3.
editDistance("OAK", "oak", 4, 4);
    // Returns 3.
```

##### editDistance (arg1, arg2, strength, locale, maxDifference)

```ctl
integer editDistance(string arg1, string arg2, integer strength, string locale, integer maxDifference);
```

The `editDistance()` function compares two strings using the specified strength of comparison, locale, and maximum difference.

The first two arguments are strings to be compared.

The third integer argument specifies the strength of comparison.

It can have any value from 1 to 4.

At strength 4 (identical comparison), only identical letters are considered equal.

At strength 3 (tertiary comparison), uppercase and lowercase letters are considered equal.

At strength 2 (secondary comparison), letters with diacritical marks are considered equal.

At strength 1 (primary comparison), even letters with some specific signs are considered equal.

In overloads that do not specify the comparison strength, the default is 4.

The fourth argument is a string that specifies the [Locale](metadata-records-and-fields.md#locale) used for comparison.

In overloads that do not specify a locale, the system value is used by default.

The fifth integer argument specifies the maximum difference.

In overloads that do not specify the maximum difference, the default is 3.

The function returns the number of letters that should be changed to transform one of the first two arguments to the other.

However, when the function is being executed, if it counts that the number of letters that should be changed is at least the number specified as the maximum difference, the execution terminates and the function returns `maxDifference + 1` as the return value.

The function is implemented for the following locales: CA, CZ, ES, DA, DE, ET, FI, FR, HR, HU, IS, IT, LT, LV, NL, NO, PL, PT, RO, SK, SL, SQ, SV, TR.

These locales have one thing in common: they all contain language-specific characters.

A complete list of these characters can be examined in [CTL2 Appendix - List of National-specific Characters](ctl2-appendix.md).

If one or both of the input strings to compare are empty strings or `null`, the function fails with an error.
Example 183. Usage of editDistance 7

```ctl
editDistance("OAK", "oak", 4, "en.US", 1);
    // Returns 2.
```

##### Compatibility

- The `editDistance()` function is available since **CloverETL 3.0.0**.

##### See also

- [metaphone](string-functions-ctl2.md#metaphone)
- [NYSIIS](string-functions-ctl2.md#nysiis)
- [soundex](string-functions-ctl2.md#soundex)

---

#### endsWith

```ctl
boolean endsWith(string str, string substr);
```

The function `endsWith()` checks whether the string `str` ends with the `substr` string.

If the parameter `str` is `null`, the function returns `false`.

##### Error states

- If the parameter `substr` is `null`, the function fails.

##### Examples
Example 184. Usage of endsWith

```ctl
endsWith("products.txt", ".txt");
    // Returns true.
endsWith("tree.png", ".ico");
    // Returns false.
endsWith(null, ".pdf");
    // Returns false.
endsWith("dog.ogg", null);
    // Fails for this input.
```

##### Compatibility

- The `endsWith(string,string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [contains](string-functions-ctl2.md#contains)
- [startsWith](string-functions-ctl2.md#startswith)

---

#### escapeJson

```ctl
string escapeJson(string input);
```

The `escapeJson` function converts string to Json value safe string.

##### Error states

- The function has no documented error states.

##### Examples
Example 185. Usage of escapeJson

```ctl
escapeJson('{"msg": "He said "hi""}');
    // Returns {\"msg\": \"He said \"hi\"\"}.
```

##### Compatibility

- The `escapeJson(string)` function is available since **CloverDX 7.5.0**.

##### See also

- [unescapeJson](string-functions-ctl2.md#unescapejson)

---

#### escapeUrl

```ctl
string escapeUrl(string arg);
```

The `escapeUrl()` function escapes illegal characters within components of a specified URL (for the URL component description, see [isUrl](string-functions-ctl2.md#isurl)). Illegal characters must be escaped by a percent (`%`) symbol, followed by the two-digit hexadecimal representation (case-insensitive) of the ISO-Latin code point for the character, e.g., `%20` is the escaped encoding for the US-ASCII space character.

The function accepts a valid URL only.

##### Error states

- For an invalid URL, empty string or `null` input, the function fails with an error.

##### Examples
Example 186. Usage of escapeUrl

```ctl
escapeUrl("http://www.example.com/The URL");
    // Returns \http://www.example.com/The%20URL.
```

##### Compatibility

- The `escapeUrl(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment)
- [isUrl](string-functions-ctl2.md#isurl)
- [unescapeUrl](string-functions-ctl2.md#unescapeurl)
- [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment)

---

#### escapeUrlFragment

```ctl
string escapeUrlFragment(string input);
string escapeUrlFragment(string input, string encoding);
```

The `escapeUrlFragment` function escapes potentially obtrusive characters.

The `input` parameter is a string to be escaped. If the `input` is `null`, the `null` is returned.

The optional parameter `encoding` enables to change encoding of the result string. The default encoding is UTF-8.

##### Error states

- If the encoding is `null` function fails.

##### Examples
Example 187. Usage of escapeUrlFragment

```ctl
escapeUrlFragment("The URL");
    // Returns The+URL.
escapeUrlFragment("Žlutý kůň");
    // Returns %C5%BDlut%C3%BD+k%C5%AF%C5%88.
escapeUrlFragment("1+1=2");
    // Returns 1%2B1%3D2.
escapeUrlFragment(null);
    // Returns null.
escapeUrlFragment("Žlutý kůň", "utf-8");
    // Returns %C5%BDlut%C3%BD+k%C5%AF%C5%88.
escapeUrlFragment("Žlutý kůň", "iso-8859-2");
    // Returns %AElut%FD+k%F9%F2.
escapeUrlFragment("abc", null);
    // Fails with an error.
```

##### Compatibility

- The `escapeUrlFragment(string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [escapeUrl](string-functions-ctl2.md#escapeurl)
- [isUrl](string-functions-ctl2.md#isurl)
- [unescapeUrl](string-functions-ctl2.md#unescapeurl)
- [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment)

---

#### escapeXML

```ctl
string escapeXML(string input);
```

The `escapeXML` function replaces all occurence of XML special entities with their escaped alternatives (XML entities).

By using the **escapeXML** function, you can safely incorporate user-generated content, external data, or any other string values into your XML documents without worrying about invalid XML syntax or potential security issues like XML injection attacks.

List of reserved characters: `' , ", &, <, >`

##### Error states

- The function has no documented error states.

##### Examples
Example 188. Usage of escapeXML

```ctl
escapeXML("<element name=\"&myname;\">");
    // Returns &lt;element name=&quot;&amp;myname;&quot;&gt;.

string nameOfCustomer = "Progress & Prosperity, Co. > Expectations";
string xml = "<company><name>" + escapeXML(nameOfCustomer) + "</name></company>";
    // Returns <company><name>Progress &amp; Prosperity, Co. &gt; Expectations&#39; </name></company>.
```

##### Compatibility

- The `escapeXML(string)` function is available since **CloverDX 6.4.0**.

##### See also

- [unescapeXML](string-functions-ctl2.md#unescapexml)

---

#### find

```ctl
string[] find(string arg, string regex);
string[] find(string arg, string regex, integer group_number);
```

The `find()` function returns a list of substrings corresponding to the [*regular expression*](language-reference-ctl2.md#regular-expressions) pattern that is found in the second argument.

If the second argument is an empty string, the function returns a list of empty strings. The sum of empty strings in the list is same as the length of the original string plus one; e.g., the string 'mark' results in the list of five empty strings.

The third argument specifies which regular expression group to use.

##### Error states

- If one or both of the two arguments are `null` value, the function fails with an error.

##### Examples
Example 189. Usage of find

```ctl
find("A quick brown fox jumps over the lazy dog.", " [a-z]");
    // Returns [ q,  b,  f,  j,  o,  t,  l,  d].
find("A quick brown fox jumps over the lazy dog.", " [a-z]*");
    // Returns [ quick,  brown,  fox,  jumps,  over,  the,  lazy,  dog].
find("A quick brown fox jumps over the lazy dog.", "()([a-z]*)([a-z])", 2);
    // Returns [quic, brow, fo, jump, ove, th, laz, do].
```

##### Compatibility

- The `find(string,string)` function is available since **CloverETL 3.0.0**.
- The `find(string,string,integer)` function is available since **CloverETL 3.4.x**.

##### See also

- [matchGroups](string-functions-ctl2.md#matchgroups)

---

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
3. **format_style** (optional): A string indicating the formatting style for the specified data type. For example, **short, medium, long, full, integer, currency, percent**, or **SubformatPattern**. For more information refer to Oracle’s documentation on the Java java.text.MessageFormat syntax [here](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/text/MessageFormat.html),

Here are some examples of placeholders with different formats:

1. `{0}`: A simple placeholder that references the first parameter.
2. `{1, number, integer}`: A placeholder that formats the second parameter as an integer number.
3. `{2, date, short}`: A placeholder that formats the third parameter as a short date.
4. `{3, time, medium}`: A placeholder that formats the fourth parameter as a medium-style time.

By understanding the [Java java.text.MessageFormat syntax](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/text/MessageFormat.html) and the various formatting options available, you can create more sophisticated and customized message templates for your applications.

The **formatMessage** and **formatMessageWithLocale** functions support using [multi-line strings](language-reference-ctl2.md#multiline-string) strings as the template, which can help improve the readability and formatting of complex templates.

##### Error states

- The function has no documented error states.

##### Examples
Example 190. Usage of `formatMessage()` usage with a multi-line string:

```ctl
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

```ctl
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
Example 191. Usage of `formatMessageWithLocale()` usage with a multi-line string:

```ctl
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

```ctl
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

##### Compatibility

- The `formatMessage(string,variant)` and `formatMessageWithLocale(string,string,variant)` functions are available since **CloverDX 6.4.0**.

##### See also

- Conversion functions: [date2str](conversion-functions-ctl2.md#date2str)
- Conversion functions: [num2str](conversion-functions-ctl2.md#num2str)
- [concat](string-functions-ctl2.md#concat)

#### getAlphanumericChars

```ctl
string getAlphanumericChars(string arg);
string getAlphanumericChars(string arg, boolean takeAlpha, boolean takeNumeric);
```

The `getAlphanumericChars()` function returns only letters and digits contained in a given argument in the order of their appearance in the string. The other characters are removed.

For an empty string input, the function returns an empty string. For `null` input, the function returns `null`.

If the `takeAlpha` is present and set to true and `takeNumeric` is set to false, the function will return letters only.

If the `takeNumeric` is present and set to true and `takeAlpha` is set to false, the function will return numbers only.

##### Error states

- The function has no documented error states.

##### Examples
Example 192. Usage of getAlphanumericChars

```ctl
getAlphanumericChars("34% of books");
    // Returns 34ofbooks.
getAlphanumericChars("(8+4)*2");
    // Returns 842.
getAlphanumericChars("gâteau");
    // Returns gâteau.
getAlphanumericChars("123 books", true, false);
    // Returns books.
getAlphanumericChars("123 books", false, true);
    // Returns 123.
getAlphanumericChars("123 books", false, false);
    // Returns 123 books.
```

##### Compatibility

- The `getAlphanumericChars(string)` and `getAlphanumericChars(string,boolean,boolean)` functions are available since **CloverETL 3.0.0**.

##### See also

- [removeBlankSpace](string-functions-ctl2.md#removeblankspace)
- [removeDiacritic](string-functions-ctl2.md#removediacritic)
- [removeNonAscii](string-functions-ctl2.md#removenonascii)

---

#### getComponentProperty

```ctl
string getComponentProperty(string propertyName);
```

The function `getComponentProperty()` returns value of a component attribute.

The `propertyName` argument is a name of an attribute of a component.

If `propertyName` is `null`, the function `getComponentProperty()` returns `null`.

If `propertyName` does not match the name of any existing attribute, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 193. Usage of getComponentProperty

```ctl
getComponentProperty("type");
    // Returns DATA_GENERATOR in DataGenerator.
getComponentProperty("id");
    // Returns MAP2 in the third Map.
getComponentProperty(null);
    // Returns null.
getComponentProperty("AQuickBrownFoxJumpsOverTheLazyDog");
    // Returns null.
```

##### Compatibility

- The `getComponentProperty()` function is available since **CloverETL 4.0**.

##### See also

- [toProjectUrl](string-functions-ctl2.md#toprojecturl)

---

#### getFileExtension

```ctl
string getFileExtension(string arg);
```

The `getFileExtension()` function extracts a file extension from a specified path or URL.

Returns the textual part of the file name after the last dot. There must be no directory separator after the dot. If extension is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 194. Usage of getFileExtension

```ctl
getFileExtension("theDir/library.src.zip");
    // Returns zip.
getFileExtension("ftp://ftp.example.com/home/user1/my.documents/log");
    // Returns empty string.
```

##### Compatibility

- The `getFileExtension(decimal)` and `log(number)` functions are available since **CloverETL 4.1.0-M1**.

##### See also

- [getFileName](string-functions-ctl2.md#getfilename)
- [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension)
- [getFilePath](string-functions-ctl2.md#getfilepath)
- [normalizePath](string-functions-ctl2.md#normalizepath)

---

#### getFileName

```ctl
string getFileName(string arg);
```

The `getFileName()` function extracts a file name from a specified path or URL.

Returns the text after the last forward or backslash. If the file name is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 195. Usage of getFileName

```ctl
getFileName("http://www.example.com/theDir/theExample.html");
    // Returns theExample.html.
getFileName("C:/Users/Public/Desktop/January");
    // Returns January.
getFileName("file:///home/user1/documents/");
    // Returns empty string.
```

##### Compatibility

- The `getFileName(string)` function is available since **CloverETL 4.1.0-M1**.

##### See also

- [getFileExtension](string-functions-ctl2.md#getfileextension)
- [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension)
- [getFilePath](string-functions-ctl2.md#getfilepath)
- [normalizePath](string-functions-ctl2.md#normalizepath)

---

#### getFileNameWithoutExtension

```ctl
string getFileNameWithoutExtension(string arg);
```

The `getFileNameWithoutExtension()` function extracts a base file name from a specified path or URL.

Returns the text after the last forward or backslash and before the last dot. If the base name is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 196. Usage of getFileNameWithoutExtension

```ctl
getFileNameWithoutExtension("http://www.example.com/theDir/library.src.zip");
    // Returns library.src.
getFileNameWithoutExtension("sandbox://shared/data-in/documents/.index");
    // Returns empty string.
```

##### Compatibility

- The `getFileNameWithoutExtension(string)` function is available since **CloverETL 4.1.0-M1**.

##### See also

- [getFileExtension](string-functions-ctl2.md#getfileextension)
- [getFileName](string-functions-ctl2.md#getfilename)
- [getFilePath](string-functions-ctl2.md#getfilepath)
- [normalizePath](string-functions-ctl2.md#normalizepath)

---

#### getFilePath

```ctl
string getFilePath(string arg);
```

The `getFilePath()` function extracts a file path (without the file name) from a specified full path or URL.

Returns the text before and including the last forward or backslash. Also replaces backslashes with forward slashes. If the path is not present in the argument, returns an empty string.

The function returns `null` value for `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 197. Usage of getFilePath

```ctl
getFilePath("C:\\Program Files\\.\\Java\\src.zip");
    // Returns C:/Program Files/./Java/.
getFilePath("index.html");
    // Returns empty string.
```

##### Compatibility

- The `getFilePath(string)` function is available since **CloverETL 4.1.0-M1**.

##### See also

- [getFileExtension](string-functions-ctl2.md#getfileextension)
- [getFileName](string-functions-ctl2.md#getfilename)
- [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension)
- [normalizePath](string-functions-ctl2.md#normalizepath)

---

#### getUrlHost

```ctl
string getUrlHost(string arg);
```

The `getUrlHost()` function parses out a host name from a specified URL.

If the hostname part is not present in the URL argument, an empty string is returned. If the URL is not valid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for an empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 198. Usage of getUrlHost

```ctl
getUrlHost("http://www.example.com/theDir/theExample.html");
    // Returns www.example.com.
getUrlHost("file:///home/user1/documents/cat.png");
    // Returns empty string.
```

##### Compatibility

- The `getUrlHost(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### getUrlPath

```ctl
string getUrlPath(string arg);
```

The `getUrlPath()` function parses out a path from a specified URL.

If the path part is not present in the URL argument, an empty string is returned. If the URL is not valid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for an empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 199. Usage of getUrlPath

```ctl
getUrlPath("http://www.example.com/theDir/theExample.html");
    // Returns /theDir/theExample.html.
```

##### Compatibility

- The `getUrlPath(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### getUrlPort

```ctl
integer getUrlPort(string arg);
```

The `getUrlPort()` function parses out a port number from a specified URL.

If the port part is not present in the URL argument, `-1` is returned. If the URL has invalid syntax, `-2` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `-2` value for an empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 200. Usage of getUrlPort

```ctl
getUrlPort("http://www.example.com/theDir/theExample.html");
    // Returns -1.
getUrlPort("http://www.example.com:8080/theDir/theExample.html");
    // Returns 8080.
```

##### Compatibility

- The `getUrlPort(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### getUrlProtocol

```ctl
string getUrlProtocol(string arg);
```

The `getUrlProtocol()` function parses out a protocol name from a specified URL.

If the protocol part is not present in the URL argument, an empty string is returned. If the URL is not valid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 201. Usage of getUrlProtocol

```ctl
getUrlProtocol("http://www.example.com/theDir/theExample.html");
    // Returns http.
```

##### Compatibility

- The `getUrlProtocol(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### getUrlQuery

```ctl
string getUrlQuery(string arg);
```

The `getUrlQuery()` function parses out a query (parameters) from a specified URL.

If the query part is not present in the URL argument, an empty string is returned. If the URL syntax is invalid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 202. Usage of getUrlQuery

```ctl
getUrlQuery("http://www.example.com/theDir/theExample.html");
    // Returns empty string.
getUrlQuery("http://www.example.com/theDir/theExample.html?a=file&name=thefile.txt");
    // Returns a=file&name=thefile.txt.
```

##### Compatibility

- The `getUrlQuery(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### getUrlRef

```ctl
string getUrlRef(string arg);
```

The `getUrlRef()` function parses out the fragment after # character, also known as ref, reference or anchor, from a specified URL.

If the fragment part is not present in the URL argument, an empty string is returned. If the URL syntax is invalid, `null` is returned. For the URL scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 203. Usage of getUrlRef

```ctl
getUrlRef("http://www.example.com/index.html");
    // Returns empty string.
getUrlRef("http://www.example.com/Index.html#abc014");
    // Returns abc014.
```

##### Compatibility

- The `getUrlRef(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### getUrlUserInfo

```ctl
string getUrlUserInfo(string arg);
```

The `getUrlUserInfo()` function parses out a username and password from a specified URL.

If the `userinfo` part is not present in the URL argument, an empty string is returned. If the URL syntax is invalid, `null` is returned. For the scheme, see [isUrl](string-functions-ctl2.md#isurl).

The function returns `null` value for the empty string and `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 204. Usage of getUrlUserInfo

```ctl
getUrlUserInfo("http://www.example.com/theDir/theExample.html");
    // Returns empty string.
getUrlUserInfo("http://user1:passwor123@www.example.com/theDir/theExample.html");
    // Returns user1:passwor123.
```

##### Compatibility

- The `getUrlUserInfo(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### indexOf

```ctl
integer indexOf(string arg, string substring);
integer indexOf(string arg, string substring, integer fromIndex);
```

The `indexOf()` function returns the index (zero-based) of the first occurrence of `substring` in the `string`. Returns `-1` if no occurrence is found.

If the parameter `arg` is `null`, the function returns `-1`. See compatibility notice.

If the second argument is an empty string, the function returns `0`.

Start position for search is set up using parameter `fromIndex`.

##### Error states

- If the second argument is `null`, the function fails with an error.

##### Examples
Example 205. Usage of indexOf

```ctl
indexOf("Hello world!", "world");
    // Returns 6.
indexOf("Hello world", "o");
    // Returns 4.
indexOf("Hello world", "o", 6);
    // Returns 7.
indexOf("Hello world", "book");
    // Returns -1.
indexOf("Hello world", "");
    // Returns 0.
indexOf(null, "chair");
    // Returns -1.
```

##### Compatibility

- The `indexOf(string,string)` and `indexOf(string,string,integer)` functions are available since **CloverETL 3.0.0**.
- In **CloverETL 3.5.x** and earlier the function fails with an error if the `arg` argument is `null`.

##### See also

- [matches](string-functions-ctl2.md#matches)

---

#### isAscii

```ctl
boolean isAscii(string arg);
```

The `isAscii()` checks the string for occurrence of non-ASCII characters.

The function takes one string argument and returns a boolean value depending on whether the string can be encoded as an ASCII string (true) or not (false).

If the input is `null` or empty string, the function returns `true`.

##### Error states

- The function has no documented error states.

##### Examples
Example 206. Usage of isAscii

```ctl
isAscii("Hello world! ");
    // Returns true.
isAscii("voilà");
    // Returns false.
```

##### Compatibility

- The `isAscii(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isBlank](miscellaneous-functions-ctl2.md#isblank)
- [isDate](string-functions-ctl2.md#isdate)
- [isInteger](string-functions-ctl2.md#isinteger)
- [isLong](string-functions-ctl2.md#islong)
- [isNumber](string-functions-ctl2.md#isnumber)
- [removeDiacritic](string-functions-ctl2.md#removediacritic)
- [removeNonAscii](string-functions-ctl2.md#removenonascii)
- [removeNonPrintable](string-functions-ctl2.md#removenonprintable)

---

#### isBlank

```ctl
boolean isBlank(string arg);
```

The function returns a boolean value depending on whether the parameter contains only white space characters (true) or not (false), if the input is `null` or an empty string, the function returns `true`.

**Note:** There are many other overloads of the `isBlank` function which work with arguments of other data types. See [isBlank(<not-string>)](miscellaneous-functions-ctl2.md#isblank) for more details.

##### Error states

- The function has no documented error states.

##### Examples
Example 207. Usage of isBlank

```ctl
// Basic data types behave like integer: the function returns true for null values.
isBlank("   ");
    // true, because there are 3 space chars (char 0x20) between quotes.
isBlank(" ");
    // true, because there is hard space character (0xA0) has been used between the quotes.
isBlank(" bc")
    // false
```

##### Compatibility

- The `isBlank(string)` function is available since **CloverETL 3.0.0**.
- The overloads for types other than string are available since **CloverDX 7.3.0**.

##### See also

- [removeBlankSpace](string-functions-ctl2.md#removeblankspace)
- [isBlank(<not-string>)](miscellaneous-functions-ctl2.md#isblank) for other types

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 208. Usage of isDate

```ctl
isDate("2012-06-11", "yyyy-MM-dd");
    // Returns true.
isDate("2012-06-11", "yyyy-MM-dd H:m:s");
    // Returns false.
isDate("2014-03-30 2:30 +1000", "yyyy-MM-dd H:m Z", "en.US");
    // Returns true.
isDate("2014-03-30 2:30", "yyyy-MM-dd H:m", "en.US", "GMT-5");
    // Returns true.
isDate("6.007.2015", "dd.MM.yyyy", false);
    // Returns true.
isDate("6.007.2015", "dd.MM.yyyy", true);
    // Returns false.
```

##### Compatibility

- The `isDate(string,string)` and `isDate(string,string,string)` functions are available since **CloverETL 3.0.0**.
- The `isDate(string,string,string,string)` is available since **CloverETL 3.5.0-M1**.
- The functions `isDate(string, string, boolean)`, `isDate(string, string, string, boolean)` and `isDate(string, string, string, string, boolean)` are available since **CloverETL 4.1.0**.

##### See also

- [isInteger](string-functions-ctl2.md#isinteger)
- [isLong](string-functions-ctl2.md#islong)
- [isNumber](string-functions-ctl2.md#isnumber)
- [str2date](conversion-functions-ctl2.md#str2date)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 209. Usage of isDecimal

```ctl
isDecimal(null);
    // Returns false.
isDecimal("");
    // Returns false.
isDecimal("half");
    // Returns false.
isDecimal("4096");
    // Returns true.
isDecimal("2.71828");
    // Returns true.
isDecimal("2.147483648e9");
    // Returns true.
isDecimal("123,456.78", "###,###.##");
    // Returns true.
isDecimal("123 456,78", "###,###.##", "fr.FR");
    // Returns true. Note that the separator between 3 and 4 is a hard space (character 160).
```

##### Compatibility

- The `isDecimal(string)` function is available since **CloverETL 4.0.0-M1**.
- The `isDecimal(string, format)` and `isDecimal(string, format, locale)` functions are available since **CloverETL 4.9.0**.
- Since **CloverDX 6.4.0** the whole string argument must be successfully parsed according to the `format`. If any part of the argument does not match format, the function returns `false`.

##### See also

- [isDate](string-functions-ctl2.md#isdate)
- [isInteger](string-functions-ctl2.md#isinteger)
- [isLong](string-functions-ctl2.md#islong)
- [isNumber](string-functions-ctl2.md#isnumber)
- [str2decimal](conversion-functions-ctl2.md#str2decimal)

---

#### isEmpty

```ctl
boolean isEmpty(string arg);
boolean isEmpty(<element type>[] arg);
boolean isEmpty(map[<type of key>,<type of value>] arg);
boolean isEmpty(variant arg);
```

The `isEmpty()` function checks whether a given string is `null` or of zero length.

If `arg` is `null`, function returns `true`.

For list, map, and `variant` arguments, the function returns `true` when the specified container is empty.

##### Error states

- For list, map, and `variant` overloads, if the argument is `null`, the function fails with an error.

##### Examples
Example 210. Usage of isEmpty

```ctl
isEmpty("");
    // Returns true.
string s = null;
isEmpty(s);
    // Returns true.
isEmpty("cup of tea");
    // Returns false.
```

##### Compatibility

- The `isEmpty()` function is available since **CloverETL 4.1.0-M1**.
- The `isEmpty(<element type>[])` and `isEmpty(map[<type of key>,<type of value>])` functions are available since **CloverETL 3.0.0**.
- The `isEmpty(variant)` function is available since **CloverDX 5.7.0**.

##### See also

- Container functions: [isEmpty(container)](container-functions-ctl2.md#isempty)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 211. Usage of isInteger

```ctl
isInteger("141592654");
    // Returns true.
isInteger("-718281828");
    // Returns true.
isInteger("999999999");
    // Returns true.
isInteger("12345.6");
    // Returns false.
isInteger("1234567890123");
    // Returns false.
isInteger("spruce");
    // Returns false.
```

##### Compatibility

- The `isInteger(string)` function is available since **CloverETL 3.0.0**.
- The `isInteger(string, format)` and `isInteger(string, format, locale)` functions are available since **CloverDX 6.4.0**.

##### See also

- [isDate](string-functions-ctl2.md#isdate)
- [isDecimal](string-functions-ctl2.md#isdecimal)
- [isLong](string-functions-ctl2.md#islong)
- [isNumber](string-functions-ctl2.md#isnumber)
- [str2integer](conversion-functions-ctl2.md#str2integer)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 212. Usage of isLong

```ctl
isLong("732050807568877293");
    // Returns true.
isLong("-236067977499789696");
    // Returns true.
isLong("999999999999999999");
    // Returns true.
isLong("12345.6");
    // Returns false.
isLong("12345678901234567890");
    // Returns false.
isLong("oak");
    // Returns false.
```

##### Compatibility

- The `isLong(string)` function is available since **CloverETL 3.0.0**.
- The `isLong(string, format)` and `isLong(string, format, locale)` functions are available since **CloverDX 6.4.0**.

##### See also

- [isDate](string-functions-ctl2.md#isdate)
- [isDecimal](string-functions-ctl2.md#isdecimal)
- [isInteger](string-functions-ctl2.md#isinteger)
- [isNumber](string-functions-ctl2.md#isnumber)
- [str2long](conversion-functions-ctl2.md#str2long)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 213. Usage of isNumber

```ctl
isNumber("41421356237");
    // Returns true.
isNumber("-12345.6");
    // Returns true.
isNumber("12345.6e3");
    // Returns true.
isNumber("larch");
    // Returns false.
```

##### Compatibility

- The `isNumber(string)` function is available since **CloverETL 3.0.0**.
- The `isNumber(string, format)` and `isNumber(string, format, locale)` functions are available since **CloverDX 6.4.0**.

##### See also

- [isDate](string-functions-ctl2.md#isdate)
- [isDecimal](string-functions-ctl2.md#isdecimal)
- [isInteger](string-functions-ctl2.md#isinteger)
- [isLong](string-functions-ctl2.md#islong)
- [str2double](conversion-functions-ctl2.md#str2double)

---

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

##### Error states

- If the parameter `form` is `null`, the function fails.

##### Examples
Example 214. Usage of isUnicodeNormalized

```ctl
isUnicodeNormalized("\u0041"+"\u030A", "NFD");
    // Returns true.
isUnicodeNormalized("\u00C5", "NFD");
    // Returns false.
isUnicodeNormalized(null, "NFD");
    // Returns true.
isUnicodeNormalized("seashore", null);
    // Fails for this input.
isUnicodeNormalized("\u0041"+"\u030A", "NFC");
    // Returns false.
isUnicodeNormalized("\u00C5", "NFC");
    // Returns true.
isUnicodeNormalized("\uFB01", "NFKD");
    // Returns false.
isUnicodeNormalized("\u0066\u0069", "NFKD");
    // Returns true.
isUnicodeNormalized("\u0073\u0323\u0307", "NFKC");
    // Returns false.
isUnicodeNormalized("\u1E69", "NFKC");
    // Returns true.
```

##### Compatibility

- The `isUnicodeNormalized(string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [codePointToChar](string-functions-ctl2.md#codepointtochar)
- [isValidCodePoint](string-functions-ctl2.md#isvalidcodepoint)
- [unicodeNormalize](string-functions-ctl2.md#unicodenormalize)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 215. Usage of isUrl

```ctl
isUrl("http://username:passw@host.com:8042/there/index.dtb?type=animal&name=cat#nose");
    // Returns true.
```

##### Compatibility

- The `isUrl()` function is available since **CloverETL 3.1.0**.

##### See also

- [escapeUrl](string-functions-ctl2.md#escapeurl)
- [getUrlHost](string-functions-ctl2.md#geturlhost)
- [getUrlPath](string-functions-ctl2.md#geturlpath)
- [getUrlPort](string-functions-ctl2.md#geturlport)
- [getUrlProtocol](string-functions-ctl2.md#geturlprotocol)
- [getUrlQuery](string-functions-ctl2.md#geturlquery)
- [getUrlUserInfo](string-functions-ctl2.md#geturluserinfo)
- [getUrlRef](string-functions-ctl2.md#geturlref)
- [unescapeUrl](string-functions-ctl2.md#unescapeurl)

---

#### isValidCodePoint

```ctl
boolean isValidCodePoint(integer code);
```

The function `isValidCodePoint()` returns `true` if the code value is valid *Unicode code point*.

If the parameter `code` is `null`, the function returns `false`.

##### Error states

- The function has no documented error states.

##### Examples
Example 216. Usage of isValidCodePoint

```ctl
isValidCodePoint(-1);
    // Returns false.
isValidCodePoint(0);
    // Returns true.
isValidCodePoint(0x03B1);
    // Returns true.
isValidCodePoint(0x10300);
    // Returns true.
isValidCodePoint(0x110000);
    // Returns false.
isValidCodePoint(null);
    // Fails for this input.
```

##### Compatibility

- The `isValidCodePoint(integer)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [codePointAt](string-functions-ctl2.md#codepointat)
- [codePointLength](string-functions-ctl2.md#codepointlength)
- [codePointToChar](string-functions-ctl2.md#codepointtochar)

---

#### join

```ctl
string join(string delimiter, <element type>[] arg);
string join(string delimiter, map[<type of key>,<type of value>] arg);
```

The `join()` converts elements from the list or map of elements to their string representation and puts them together with the first argument as a delimiter.

If the delimiter is `null`, the function joins string representations of elements from the list with the empty string.

##### Error states

- The function has no documented error states.

##### Examples
Example 217. Usage of join

```ctl
list[string] myString = ["a", "b", "c"];
join(":", myString);
    // Returns a:b:c.
join(null, myString);
    // Returns abc.

map[integer, string] theMap = {};
theMap[0] = "cat";
theMap[1] = "grep";
theMap[3] = "head";
join(" ", theMap);
    // Returns 0=cat 1=grep 3=head.
join(null, theMap);
    // Returns 0=cat1=grep3=head.
```

##### Compatibility

- The `join()` function is available since **CloverETL 3.0.0**.

##### See also

- [concat](string-functions-ctl2.md#concat)
- [concatWithSeparator](string-functions-ctl2.md#concatwithseparator)
- [split](string-functions-ctl2.md#split)

---

#### lastIndexOf

```ctl
integer lastIndexOf(string input, string substr);
integer lastIndexOf(string input, string substr, integer index);
```

The function `lastIndexOf` returns an index of the last occurrence of the `substr` substring within the given string `input`, searching backwards from the given position or from the end.

The parameter `input` is a string in which the occurrence of the `substr` string is searched. If `input` is `null`, the function returns `-1`.

The parameter `substr` is a substring to be searched.

The parameter `index` denotes the position in the `input`, where the substring matching process starts. If the parameter is negative, the function returns `-1`.

##### Error states

- If the parameter `substr` is `null`, the function fails.
- If the parameter `index` is `null`, the function fails.

##### Examples
Example 218. Usage of lastIndexOf

```ctl
lastIndexOf(null, "quad");
    // Returns -1.
lastIndexOf(null, "quad", 5);
    // Returns -1.
lastIndexOf("data", "a");
    // Returns 3.
lastIndexOf("fabricable", "ab", 5);
    // Returns 1.
lastIndexOf("fabricable", "ab", 6);
    // Returns 6.
lastIndexOf("fabricable", "ab", -1);
    // Returns -1.
lastIndexOf("fabricable", "ab", 20);
    // Returns 6.
lastIndexOf("fabricable", null, 0);
    // Fails for this input.
lastIndexOf("fabricable", "ab", null);
    // Fails for this input.
```

##### Compatibility

- The `lastIndexOf(string,string)` and `lastIndexOf(string,string,integer)` functions are available since **CloverETL 4.0.0-M1**.

##### See also

- [indexOf](string-functions-ctl2.md#indexof)

---

#### left

```ctl
string left(string input, integer length);
string left(string input, integer length, boolean spacePad);
```

The `left()` function returns a substring of `input` with the specified `length`.

If the `input` is shorter than `length`, the function returns the `input` unmodified. The result may be padded with spaces, based on the value of `spacePad`.

If the `input` is `null`, the function returns `null`.

If `spacePad` is set to `false`, the function behaves the same way as the `left(string, integer)` function. If `spacePad` is set to `true` and the `input` is shorter than `length`, the function pads the `input` with blank spaces from the right side.

##### Error states

- The function has no documented error states.

##### Examples
Example 219. Usage of left

```ctl
left("A very long text", 6);
    // Returns A very.
left("A very long text", 20);
    // Returns A very long text.
left("text", 10, true);
    // Returns `text      `.
        // There are 6 space chars appended after the text.
```

##### Compatibility

- The `left(string,integer)` function is available since **CloverETL 3.0.0**.
- The `left(string,integer,boolean)` function is available since **CloverETL 3.1.0**.

##### See also

- [right](string-functions-ctl2.md#right)
- [substring](string-functions-ctl2.md#substring)

---

#### length

```ctl
integer length(structuredtype arg);
```

The `length()` function accepts a structured data type as its argument: `string`, `<element type>[]`, `map[<type of key>,<type of value>]` or `record`. It takes the argument and returns a number of elements forming the structured data type.

If the argument is `null` or empty string, the function returns `0`.

##### Error states

- The function has no documented error states.

##### Examples
Example 220. Usage of length

```ctl
length("string");
    // Returns 6.
```

##### Compatibility

- The `length(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isEmpty](container-functions-ctl2.md#isempty)

---

#### lowerCase

```ctl
string lowerCase(string input);
```

The `lowerCase()` function returns the `input` string with letters converted to lower case only.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 221. Usage of lowerCase

```ctl
lowerCase("Some string");
    // Returns some string.
```

##### Compatibility

- The `lowerCase(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [upperCase](string-functions-ctl2.md#uppercase)
- [properCase](string-functions-ctl2.md#propercase)

---

#### lpad

```ctl
string lpad(string input, integer length);
string lpad(string input, integer length, string filler);
```

The `lpad()` function pads input string from left using specified characters.

If the parameter `input` is `null` the function returns `null`.

The parameter `length` is minimal length of an output string. If the string length is lower than the parameter `length`, the string is padded from left using space or using `filler`. Otherwise the `input` string is returned.

##### Error states

- If the parameter `length` is *negative* or `null`, the function fails.
- It the `filler` parameter is `null`, *empty string* or longer than one character, function fails.

##### Examples
Example 222. Usage of lpad

```ctl
lpad("256", 0);
    // Returns 256.
lpad("256", 5);
    // Returns "  256".
lpad("256", -1);
    // Fails for this input.
lpad(null, 2);
    // Returns null.
lpad("", 0);
    // Returns "".
lpad("", 2);
    // Returns "  ".
lpad("256", 5, "0");
    // Returns 00256.
lpad("Great Dipper", 20, "");
    // Fails for this input.
lpad("Little Dipper", 20, null);
    // Fails for this input.
lpad("Little Dipper", 17, "The ");
    // Fails for this input.
```

##### Compatibility

- The `lpad(string,integer,string)` and `lpad(string,integer,string)` functions are available since **CloverETL 4.0.0-M1**.

##### See also

- [left](string-functions-ctl2.md#left)
- [right](string-functions-ctl2.md#right)
- [rpad](string-functions-ctl2.md#rpad)

---

#### matches

```ctl
boolean matches(string text, string regex);
```

The `matches()` function checks the string to match the provided regular pattern.

The function returns `true`, if the `text` matches the [*regular expression*](language-reference-ctl2.md#regular-expressions)`regex`. Otherwise it returns `false`.

If the `text` is `null`, the function returns `false`.

##### Error states

- If the `regex` is `null`, the function fails with an error.

##### Examples
Example 223. Usage of matches

```ctl
matches("abc", "[a-c]{3}");
    // Returns true.
matches("abc", "[A-Z]{3}");
    // Returns false.
```

##### Compatibility

- The `matches(string,string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isAscii](string-functions-ctl2.md#isascii)
- [isBlank](miscellaneous-functions-ctl2.md#isblank)
- [isDate](string-functions-ctl2.md#isdate)
- [isDecimal](string-functions-ctl2.md#isdecimal)
- [isInteger](string-functions-ctl2.md#isinteger)
- [isLong](string-functions-ctl2.md#islong)
- [isNumber](string-functions-ctl2.md#isnumber)
- [isUrl](string-functions-ctl2.md#isurl)

---

#### matchGroups

```ctl
string[] matchGroups(string text, string regex);
```

The `matchGroups()` function returns the list of group matches (the substrings matched by the capturing groups of the `regex`) if `text` matches the [*regular expression*](language-reference-ctl2.md#regular-expressions)`regex`.

The list is zero-based and the element with index 0 is the match for the entire expression. The following elements (1, …​) correspond with the capturing groups indexed from left to right, starting at one. The returned list is unmodifiable. If `text` does not match `regex`, `null` is returned.

If the text argument is `null`, the function returns `null`.

##### Error states

- If the `regex` is `null`, the function fails with an error.

##### Examples
Example 224. Usage of matchGroups

```ctl
matchGroups("A fox", "([A-Z]) ([a-z]*)");
    // Returns [A fox, A, fox].
// The first group is a whole pattern, patterns enclosed in parentheses follow.
matchGroups("A quick brown fox jumps", "[A-Z] [a-z]{5} [a-z]{5} ([a-z]*) ([a-z]{5})");
    // Returns [A quick brown fox jumps, fox, jumps].
```

##### Compatibility

- The `matchGroups(string,string)` function is available since **CloverETL 3.4.x**.

##### See also

- [cut](string-functions-ctl2.md#cut)
- [split](string-functions-ctl2.md#split)
- [substring](string-functions-ctl2.md#substring)

---

#### metaphone

```ctl
string metaphone(string arg);
string metaphone(string arg, integer maxLength);
```

The `metaphone()` function returns the metaphone code of the first argument.

For more information, see the following site: [www.lanw.com/java/phonetic/default.htm](http://www.lanw.com/java/phonetic/default.htm).

The default `maximum length` of the metaphone code is 4.

The function returns `null` value for the `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 225. Usage of metaphone

```ctl
metaphone("cheep");
    // Returns XP.
metaphone("sheep");
    // Returns XP.
metaphone("international");
    // Returns INTR.
metaphone("cheep", 1);
    // Returns X.
metaphone("sheep", 2);
    // Returns XP.
metaphone("bookworm", 3);
    // Returns BKW.
metaphone("international", 7);
    // Returns INTRNXN.
```

##### Compatibility

- The `metaphone(string)` and `metaphone(string,integer)` function is available since **CloverETL 3.2.1** or earlier.

##### See also

- [editDistance](string-functions-ctl2.md#editdistance)
- [NYSIIS](string-functions-ctl2.md#nysiis)
- [soundex](string-functions-ctl2.md#soundex)

---

#### normalizeDecimal

```ctl
string normalizeDecimal(string arg);
```

The `normalizeDecimal()` function preprocesses decimal number strings and removes non-numeric characters, standardizes decimal separators, and eliminates thousand separators and currency symbols. By scanning the input string from right to left, it identifies the first occurrence of either a comma or a period, assuming it to be the decimal separator. While this approach offers a basic level of normalization, it’s important to note that it relies on a simple heuristic and may not be suitable for all scenarios, e.g., when your data includes integers with commas used as thousand separators (`1,000`). In such scenarios, more sophisticated parsing techniques may be necessary to accurately identify and handle different number formats.

##### Error states

- The function has no documented error states.

##### Examples
Example 226. Usage of normalizeDecimal

```ctl
normalizeDecimal("1,035");
    // Returns 1.035.
normalizeDecimal("1,035.24");
    // Returns 1035.24.
normalizeDecimal("1,000");
    // Returns 1.000.
normalizeDecimal("EUR451");
    // Returns 451.
normalizeDecimal("€127");
    // Returns 127.
normalizeDecimal("23$56");
    // Returns 2356.
normalizeDecimal("123,456.789");
    // Returns 123456.789.
normalizeDecimal("123 456,789");
    // Returns 123456.789.
normalizeDecimal("123.456,789");
    // Returns 123456.789.
normalizeDecimal(null);
    // Returns null.
```

##### Compatibility

- The `normalizeDecimal(string)` function is available since **CloverDX 6.7.0**.

##### See also

- [normalizeWhitespaces](string-functions-ctl2.md#normalizewhitespaces)

---

#### normalizePath

```ctl
string normalizePath(string arg);
```

The `normalizePath()` function normalizes a specified path or URL to a standard format, removing single and double dot path segments. Also replaces backslashes with forward slashes.

If normalization fails because there is a double dot path segment that is not preceded by a removable parent path segment, the function returns `null`.

The function returns a `null` value for a `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 227. Usage of normalizePath

```ctl
normalizePath("zip:(C:\\Data\\..\\archive.zip)#inner1/../inner2/./data.txt");
    // Returns zip:(C:/archive.zip)#inner2/data.txt.
normalizePath("home/../../data");
    // Returns null.
```

##### Compatibility

- The `normalizePath(string)` function is available since **CloverETL 4.1.0-M1**.

##### See also

- [getFileExtension](string-functions-ctl2.md#getfileextension)
- [getFileName](string-functions-ctl2.md#getfilename)
- [getFileNameWithoutExtension](string-functions-ctl2.md#getfilenamewithoutextension)
- [getFilePath](string-functions-ctl2.md#getfilepath)

---

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

##### Error states

- The function has no documented error states.

##### Examples
Example 228. Usage of normalizeWhitespaces

```ctl
normalizeWhitespaces("   many   spaces   ");
    // Returns many spaces.
normalizeWhitespaces("name:\t\tvalue");
    // Returns name: value.
```

##### Compatibility

- The `normalizeWhitespaces(string)` function is available since **CloverETL 6.1.0**.

##### See also

- [trim](string-functions-ctl2.md#trim)
- [normalizeDecimal](string-functions-ctl2.md#normalizedecimal)

---

#### NYSIIS

```ctl
string NYSIIS(string arg);
```

The `NYSIIS()` function returns the New York State Identification and Intelligence System Phonetic Code of the argument.

For more information, see the following site: [http://en.wikipedia.org/wiki/New_York_State_Identification_and_Intelligence_System](http://en.wikipedia.org/wiki/New_York_State_Identification_and_Intelligence_System). This implementation works with numbers. Input string which contains numbers will result in unchanged string. E.g. input '1234' results in string '1234'.

If the input of function is `null`, the function returns `null`. If the input of function is empty string, the function returns empty string.

##### Error states

- The function has no documented error states.

##### Examples
Example 229. Usage of NYSIIS

```ctl
NYSIIS("cheep");
    // Returns CAP.
NYSIIS("sheep");
    // Returns SAP.
NYSIIS("international");
    // Returns INTARNATANAL.
```

##### Compatibility

- The `NYSIIS(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [editDistance](string-functions-ctl2.md#editdistance)
- [metaphone](string-functions-ctl2.md#metaphone)
- [soundex](string-functions-ctl2.md#soundex)

---

#### properCase

```ctl
string properCase(string arg);
string properCase(string arg, string locale);
```

The `properCase()` function takes one string argument and returns another string with all words converted to proper case. Proper case is text that is written with each of the first letters of every word being capitalized.

Specifying `locale` allows you to apply specifics of any language. For example, in English the proper case of word "iceland" is "Iceland" but in Dutch the proper case of word "ijsland" is "IJsland" because of the "ij" digraph present in the Dutch language.

If the `locale` is `null` or an empty string, the respective [default value](metadata-records-and-fields.md#locale) is used instead.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 230. Usage of properCase

```ctl
properCase("The quick brown fox jumps over the lazy dog");
    // Returns The Quick Brown Fox Jumps Over The Lazy Dog.
properCase("ijsland");
    // Returns Ijsland.
properCase("ijsland", "nl.NL");
    // Returns IJsland.
```

##### Compatibility

- The `properCase(string)` function is available since **CloverETL 6.1.0**.

##### See also

- [lowerCase](string-functions-ctl2.md#lowercase)
- [upperCase](string-functions-ctl2.md#uppercase)

---

#### randomString

```ctl
string randomString(integer minLength, integer maxLength);
```

The `randomString()` function returns a string consisting of lowercase letters.

Its length is between <`minLength`; `maxLength`>. Characters in the generated string always belong to ['a'-'z'] (no special symbols).

##### Error states

- If one of the given arguments is `null`, the function fails with an error.

##### Examples
Example 231. Usage of randomString

```ctl
randomString(3, 5);
    // Can return qjfxq.
```

##### Compatibility

- The `randomString(integer,integer)` function is available since **CloverETL 3.0.0**.

##### See also

- [random](mathematical-functions-ctl2.md#random)
- [randomBoolean](mathematical-functions-ctl2.md#randomboolean)
- [randomDate](date-functions-ctl2.md#randomdate)
- [randomGaussian](mathematical-functions-ctl2.md#randomgaussian)
- [randomInteger](mathematical-functions-ctl2.md#randominteger)
- [randomUUID](string-functions-ctl2.md#randomuuid)
- [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed)
- [addNoise](mathematical-functions-ctl2.md#addnoise)

---

#### randomUUID

```ctl
string randomUUID();
```

The function `randomUUID()` generates a random universally unique identifier (UUID).

The generated string has this format:

`hhhhhhhh-hhhh-hhhh-hhhh-hhhhhhhhhhhh`

where `h` belongs to `[0-9a-f]`. In other words, you generate hexadecimal code of a random 128bit number.

For more details on the algorithm used, see [the Java documentation](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/UUID.html).

##### Error states

- The function has no documented error states.

##### Examples
Example 232. Usage of randomUUID

```ctl
randomUUID();
    // Can return, for example, cee188a3-aa67-4a68-bcd2-52f3ec0329e6.
```

##### Compatibility

- The `randomUUID()` function is available since **CloverETL 3.2.0**.

##### See also

- [random](mathematical-functions-ctl2.md#random)
- [randomBoolean](mathematical-functions-ctl2.md#randomboolean)
- [randomDate](date-functions-ctl2.md#randomdate)
- [randomGaussian](mathematical-functions-ctl2.md#randomgaussian)
- [randomInteger](mathematical-functions-ctl2.md#randominteger)
- [randomString](string-functions-ctl2.md#randomstring)
- [setRandomSeed](mathematical-functions-ctl2.md#setrandomseed)
- [addNoise](mathematical-functions-ctl2.md#addnoise)

---

#### removeBlankSpace

```ctl
string removeBlankSpace(string arg);
```

The `removeBlankSpace()` function takes one string argument and returns another string with white characters removed.

The function removes chars `0x09`, `0x0A`, `0x0B`, `0x0C`, `0x0D`, `0x1C`, `0x1D`, `0x1E` and `0x1F`. The function does *not* remove chars `0x00A0` (hard space), `0x2007` and `0x202F`.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 233. Usage of removeBlankSpace

```ctl
removeBlankSpace("a quick brown fox");
    // Returns aquickbrownfox.
removeBlankSpace("1 000 000");
    // Returns 1 000 000, provided the string contains hard space (char 0xA0).
```

##### Compatibility

- The `removeBlankSpace()` function is available since **CloverETL 3.0.0**.

##### See also

- [isBlank](miscellaneous-functions-ctl2.md#isblank)
- [removeDiacritic](string-functions-ctl2.md#removediacritic)
- [removeNonAscii](string-functions-ctl2.md#removenonascii)
- [removeNonPrintable](string-functions-ctl2.md#removenonprintable)
- [trim](string-functions-ctl2.md#trim)

---

#### removeDiacritic

```ctl
string removeDiacritic(string arg);
```

The `removeDiacritic()` function takes one string argument and returns another string with diacritical marks removed.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 234. Usage of removeDiacritic

```ctl
removeDiacritic("Voyez le brick géant que j'examine.");
    // Returns Voyez le brick geant que j'examine.
removeDiacritic("Küchen");
    // Returns Kuchen.
removeDiacritic("Příšerný žluťoučký kůň úpěl ďábelské ódy.");
    // Returns Priserny zlutoucky kun upel dabelske ody.
```

##### Compatibility

- The `removeDiacritic(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isAscii](string-functions-ctl2.md#isascii)
- [removeBlankSpace](string-functions-ctl2.md#removeblankspace)
- [removeNonAscii](string-functions-ctl2.md#removenonascii)
- [removeNonPrintable](string-functions-ctl2.md#removenonprintable)

---

#### removeNonAscii

```ctl
string removeNonAscii(string arg);
```

The `removeNonAscii()` function returns string with non-ASCII characters removed.

If the input is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 235. Usage of removeNonAscii

```ctl
removeNonAscii("Voyez le brick géant que j'examine.");
    // Returns Voyez le brick gant que j'examine.
removeNonAscii("Příšerný žluťoučký kůň úpěl ďábelské ódy.");
    // Returns Pern luouk k pl belsk dy.
```

##### Compatibility

- The `removeNonAscii(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isAscii](string-functions-ctl2.md#isascii)
- [removeBlankSpace](string-functions-ctl2.md#removeblankspace)
- [removeNonPrintable](string-functions-ctl2.md#removenonprintable)

---

#### removeNonPrintable

```ctl
string removeNonPrintable(string arg);
```

The `removeNonPrintable()` function takes one string argument and returns another string with non-printable characters removed.

If the input is `null`, the function returns `null`.

For the list of characters considered as non-printable, see [www.fileformat.info/controlcharacters](http://www.fileformat.info/info/unicode/category/Cc/list.htm).

The function is not dependent on character encoding.

Note that since **CloverETL 3.5**, the function does not remove non-ASCII characters anymore. If you need to have them removed, please use the `removeNonAscii(string)` function in addition.

##### Error states

- The function has no documented error states.

##### Examples
Example 236. Usage of removeNonPrintable

```ctl
// Let's call a string containing chars A (code 0x41), B (code 0x42), bell (code 0x07) and C (code 0x43) as myString.
string myString = "AB" + codePointToChar(0x07) + "C";
removeNonPrintable(myString);
    // Returns ABC.
```

##### Compatibility

- The `removeNonPrintable(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isAscii](string-functions-ctl2.md#isascii)
- [removeBlankSpace](string-functions-ctl2.md#removeblankspace)
- [removeDiacritic](string-functions-ctl2.md#removediacritic)
- [removeNonAscii](string-functions-ctl2.md#removenonascii)

---

#### replace

```ctl
string replace(string arg, string regex, string replacement);
```

The `replace()` function replaces characters from the input string matching the regexp with the specified replacement string.

The function takes three string arguments - a string, a [*regular expression*](language-reference-ctl2.md#regular-expressions) and a replacement.

All parts of the string that match the regex are replaced. The user can also reference the matched text using a backreference in the replacement string. A backreference to the entire match is indicated as $0. If there are capturing parentheses, specifics groups as $1, $2, $3, etc. can be referenced.

**Important** - please beware of similar syntax of $0, $1, etc. While used inside the replacement string, it refers to matching regular expression parenthesis (in order). If used outside a string, it means a reference to an input field. See the examples.

A modifier can be used at the start of the regular expression: `(?i)` for case-insensitive search, `(?m)` for multiline mode or `(?s)` for "dotall" mode where a dot (".") matches even a newline character.

If the first argument of the function is `null`, the function returns `null`.

##### Error states

- If the regexp pattern is `null`, the function fails with an error. If the third argument is `null`, the function fails with an error, unless the specified regexp does not match the first input.

##### Examples
Example 237. Usage of replace

```ctl
replace("Hello","[Ll]","t");
    // Returns "Hetto".
replace("Hello", "e(l+)", "a$1");
    // Returns "Hallo".
replace("Hello", "e(l+)", $in.0.name);
    // Returns HJohno if input field name on port 0 contains the name John.
replace("Hello", "(?i)L", "t");
    // Returns Hetto.
replace("Hello", "L", "t");
    // Returns Hello.
replace("cornerstone", "(corner)([a-z]*)", "$2 $1");
    // Returns stone corner.
```

##### Compatibility

- The `replace(string,string,string)` function is available since **CloverETL 3.0.0**.

##### See also

- [lowerCase](string-functions-ctl2.md#lowercase)
- [translate](string-functions-ctl2.md#translate)
- [upperCase](string-functions-ctl2.md#uppercase)
- [properCase](string-functions-ctl2.md#propercase)

---

#### reverse

```ctl
string reverse(string arg);
```

The `reverse()` function reverses the order of characters of a given string and returns the reverted string.

If the given string is `null`, the function returns `null`.

##### Error states

- The function 'string' has no documented error states.

##### Examples
Example 238. Usage of reverse

```ctl
reverse("knot");
    // Returns tonk.
```

##### Compatibility

- The `reverse(string)` function is available since **CloverETL 3.0.0**.

##### See also

- Record functions: [reverse(list)](container-functions-ctl2.md#reverse)

---

#### right

```ctl
string right(string arg, integer length);
string right(string arg, integer length, boolean spacePad);
```

The `right()` function returns the substring of the length specified as the second argument counted from the end of the string specified as the first argument.

If the input string is shorter than the `length` parameter, the function returns the original string.

If the input is `null`, the function returns `null`.

If the `spacePad` argument is set to `true`, the new string is padded. Whereas if it is `false` or the function does not have the argument `spacePad`, the input string is returned as the result with no space added.

##### Error states

- The function has no documented error states.

##### Examples
Example 239. Usage of right

```ctl
right("A very long string", 4);
    // Returns ring.
right("A very long string", 20);
    // Returns A very long string.
right("text", 10, true);
    // Returns `      text`.
```

##### Compatibility

- The `right(string,integer)` function is available since **CloverETL 3.0.0**.
- The `right(string,integer,boolean)` function is available since **CloverETL 3.1.0**.

##### See also

- [left](string-functions-ctl2.md#left)
- [substring](string-functions-ctl2.md#substring)

---

#### rpad

```ctl
string rpad(string input, integer length);
string rpad(string input, integer length, string filler);
```

The function `rpad` pads a string from right side to specified length using space or user-defined character.

The parameter `input` contains a string to be padded. If the `input` is shorter than specified in the parameter `length`, the `input` is padded from the right side using `filler`. The `input` with sufficient length is returned unmodified.

If the parameter `input` is `null`, the function returns `null`.

The parameter `length` defines the minimal length of the result string.

The optional parameter `filler` defines the character used for pad. The function `rpad(string, integer)` uses *space character* as a filler.

##### Error states

- If the parameter `length` is *negative*, the function fails.
- If the `filler` is `null`, *empty string* or a string having more than `1` character, the function fails.

##### Examples
Example 240. Usage of rpad

```ctl
rpad("A quick brown fox", 2);
    // Returns "A quick brown fox".
rpad("A quick brown fox", 20);
    // Returns "A quick brown fox   ".
rpad(null, 0);
    // Returns null.
rpad("A quick fox", -1);
    // Fails for this input.
rpad("A quick fox", null);
    // Fails for this input.
rpad("A quick brown fox", 20, ".");
    // Returns "A quick brown fox...".
rpad("A quick brown fox", 20, null);
    // Fails for this input.
rpad("A quick brown fox", 20, "");
    // Fails for this input.
rpad("A quick brown fox", 20, " jumps");
    // Fails for this input.
```

##### Compatibility

- The `rpad(string,integer)` and `rpad(string,integer,string)` functions are available since **CloverETL 4.0.0-M1**.

##### See also

- [left](string-functions-ctl2.md#left)
- [lpad](string-functions-ctl2.md#lpad)
- [right](string-functions-ctl2.md#right)

---

#### soundex

```ctl
string soundex(string arg);
```

The `soundex()` function takes one string argument and converts the string to another.

The resulting string consists of the first letter of the string specified as the argument and three digits. The three digits are based on the consonants contained in the string when similar numbers correspond to similarly sounding consonants.

If the input of the function is `null`, the function returns `null`.

If the input is an empty string, the function returns an empty string.

##### Error states

- The function has no documented error states.

##### Examples
Example 241. Usage of soundex

```ctl
soundex("cheep");
    // Returns C100.
soundex("sheep");
    // Returns S100.
soundex("book");
    // Returns B200.
soundex("bookworm");
    // Returns B265.
soundex("international");
    // Returns I536.
```

##### Compatibility

- The `soundex(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [editDistance](string-functions-ctl2.md#editdistance)
- [metaphone](string-functions-ctl2.md#metaphone)
- [NYSIIS](string-functions-ctl2.md#nysiis)

---

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

The `limit` parameter limits the number of items in the list to be returned. If the limit is *positive*, at most the specified number of items will be returned. The unsplit residue of input string is the last item of the list. If the `limit` is *zero*, the limit is not applied and the function works as without the `limit` parameter: The trailing empty list items are trimmed. If the `limit` parameter is *negative*, the limit is not applied and trailing empty fields are not trimmed. If the function is called without the `limit` parameter, it works in the same way as with `limit` set to `0`.

##### Error states

- If the `regexp` argument is `null`, the function fails with an error.

##### Examples
Example 242. Usage of split

```ctl
split("anaconda", "a");
    // Returns [, n, cond].
split("abcdefg", "[ce]");
    // Returns ["ab", "d", "fg"].
split("cuckoo", "o");
    // Returns [cuck].
// The empty terminating list item is discarded.
split("cuckoos", "o");
    // Returns [cuck, , s].
split("oak,spruce,larch,,", ",");
    // Returns [oak, spruce, larch].
split("oak,spruce,larch,,maple", ",");
    // Returns [oak, spruce, larch, , maple].
// The empty list item has not been discarded as there is non-empty string maple following the empty list item.
split("rabbit", "b{2}[aeiou]");
    // Returns [ra, t].
split("woodcock", "oo");
    // Returns [w, dcock].
split("woodcock", "[oo]");
    // Returns [w, , dc, ck].
split("frog,blowfish,serpent",";");
    // Returns [frog,blowfish,serpent].
// The first string does not contain a semicolon, thus the content of the first list item is frog,blowfish,serpent.
split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", -1);
    // Returns [/bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, , ].
split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", 0);
    // Returns [/bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin].
split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", 1);
    // Returns [/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::].
split("/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin::", ":", 2);
    // Returns [/bin, /sbin:/usr/bin:/usr/sbin:/usr/local/bin::].
split("/bin:/sbin", ":", 5);
    // Returns [/bin, /sbin].
```

##### Compatibility

- The `split(string,string)` function is available since **CloverETL 3.0.0**.
- If the input (`arg`) of the function is `null`, the function returns a list with one `null` string in **CloverETL 3.5.x** and earlier.
- The `split(string,string,integer)` is available since **CloverETL 4.0.0-M1**.

##### See also

- [concat](string-functions-ctl2.md#concat)
- [concatWithSeparator](string-functions-ctl2.md#concatwithseparator)
- [join](string-functions-ctl2.md#join)
- [substring](string-functions-ctl2.md#substring)
- [matchGroups](string-functions-ctl2.md#matchgroups)

---

#### startsWith

```ctl
boolean startsWith(string str, string sub);
```

The `startsWith()` function returns `true` if the parameter `str` starts with string `sub`.

If the parameter `str` is `null`, the function returns `false`.

##### Error states

- If the parameter `sub` is `null`, the function fails.

##### Examples
Example 243. Usage of startsWith

```ctl
startsWith("quadratic", "quad");
    // Returns true.
startsWith("quadratic", "linear");
    // Returns false.
startsWith(null, "a");
    // Returns false.
startsWith("quadratic", null);
    // Fails for this input.
```

##### Compatibility

- The `startsWith(string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [contains](string-functions-ctl2.md#contains)
- [endsWith](string-functions-ctl2.md#endswith)

---

#### substring

```ctl
string substring(string arg, integer fromIndex);
string substring(string arg, integer fromIndex, integer length);
```

The `substring()` function returns a substring of an input string.

The function `substring(arg, fromIndex)` returns a substring of `arg` starting at the position `fromIndex`.

The function `substring(arg, fromIndex, length)` returns a substring of `arg` starting at the position `fromIndex` limited by `length`.

If the original string `arg` is `null`, the function returns `null`. If the `arg` is empty string, the function returns empty string. See the compatibility notice.

The parameter `fromIndex` defines the starting position of the substring.

The parameter `length` is a maximal length of the returned substring.

##### Error states

- If `fromIndex` is negative or `null`, the function fails. See compatibility notice.
- If `length` is negative or `null`, the function fails.

##### Examples
Example 244. Usage of substring

```ctl
substring("elfish", 2);
    // Returns fish.
substring("network", 20);
    // Returns empty string.
substring("network", null);
    // Fails for this input.
substring("minute", 2, 3);
    // Returns nut.
substring("text", 1, 2);
    // Returns "ex".
substring("network", 3, 0);
    // Returns empty string.
substring("network", 20, 2);
    // Returns empty string.
substring("network", 6, 5);
    // Returns k.
substring("network", null, 1);
    // Fails for this input.
substring("network", -2, 1);
    // Fails for this input.
substring("network", 3, null);
    // Fails for this input.
substring("network", 3, -4);
    // Fails for this input.
substring(null, 1, 1);
    // Returns null.
```

##### Compatibility

- The function `substring()` fails, if the input string `arg` is `null` in **CloverETL 3.5.x** and earlier.
- The function `substring()` fails, if any of integer parameters is `null` or out of range of the input string in **CloverETL 3.5.x**. Since **CloverETL 4.0.0.M1**, it fails only with *negative* or `null` values.
- The `substring(string,integer,integer)` function is available since **CloverETL 3.0.0**.
- The `substring(string, integer)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [charAt](string-functions-ctl2.md#charat)
- [cut](string-functions-ctl2.md#cut)
- [left](string-functions-ctl2.md#left)
- [right](string-functions-ctl2.md#right)
- [trim](string-functions-ctl2.md#trim)

---

#### toProjectUrl

```ctl
string toProjectUrl(string path);
```

The `toProjectUrl()` function converts a relative path, e.g., data-in/file.txt to a full URL containing the name of the sandbox: sandbox://mysandbox/data-in/file.txt.

The parameter `path` is a relative path to the file.

If the parameter `path` is `null`, the function `toProjectUrl()` returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 245. Usage of toProjectUrl

```ctl
// Following examples use sandbox called documentation.
// If you use examples in your sandbox, you will see <yourSandboxName> instead of documentation.
toProjectUrl("");
    // Returns sandbox://documentation/.
toProjectUrl(null);
    // Returns null.
toProjectUrl(".");
    // Returns sandbox://documentation/.
toProjectUrl("/");
    // Returns file:/.
```

##### Compatibility

- The `toProjectUrl()` function is available since **CloverETL 4.0**.

##### See also

- [getUrlPath](string-functions-ctl2.md#geturlpath)

---

#### translate

```ctl
string translate(string arg, string searchingSet, string replaceSet);
```

The `translate()` function replaces the characters given in the second string of the first argument with characters from the third string.

If the input of the function is `null`, the function returns `null`.

##### Error states

- If one or both of the second or the third argument is `null`, the function fails with an error.

##### Examples
Example 246. Usage of translate

```ctl
translate('Hello','eo','is');
    // Returns the string Hills.
```

##### Compatibility

- The `translate(string,string,string)` function is available since **CloverETL 3.0.0**.

##### See also

- [replace](string-functions-ctl2.md#replace)
- [toAbsolutePath](miscellaneous-functions-ctl2.md#toabsolutepath)

---

#### trim

```ctl
string trim(string arg);
```

The `trim()` function takes one string argument and returns another string with leading and trailing white spaces removed.

If the input of the function is an empty string, the function returns an empty string.

If the input of the function is `null`, the function returns `null`.

##### Error states

- The function has no documented error states.

##### Examples
Example 247. Usage of trim

```ctl
trim("  Text and space chars  ");
    // Returns Text and space chars.
```

##### Compatibility

- The `trim(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [isBlank](miscellaneous-functions-ctl2.md#isblank)
- [removeBlankSpace](string-functions-ctl2.md#removeblankspace)
- [replace](string-functions-ctl2.md#replace)
- [substring](string-functions-ctl2.md#substring)

#### unescapeJson

```ctl
string unescapeJson(string input);
```

The `unescapeJson` function reverts conversion of `escapeJson`.

##### Error states

- The function has no documented error states.

##### Examples
Example 248. Usage of unescapeJson

```ctl
unescapeJson('{\"msg\": \"He said \"hi\"\"}');
    // Returns {"msg": "He said "hi""}.
```

##### Compatibility

- The `unescapeJson(string)` function is available since **CloverDX 7.5.0**.

##### See also

- [escapeJson](string-functions-ctl2.md#escapejson)

---

#### unescapeUrl

```ctl
string unescapeUrl(string arg);
```

The `unescapeUrl()` function decodes escape sequences of illegal characters within components of a specified URL.

Escape sequences consist of a percent (`%`) symbol, followed by the two-digit hexadecimal representation (case-insensitive) of the ISO-Latin code point for the character, e.g., `%20` is the escaped encoding for the US-ASCII space character. For the URL component description, see [isUrl](string-functions-ctl2.md#isurl).

Function accepts a valid URL only.

##### Error states

- For an invalid URL, empty string or `null` input, the function fails with an error.

##### Examples
Example 249. Usage of unescapeUrl

```ctl
unescapeUrl("http://www.example.com/the%20file.html");
    // Returns \http://www.example.com/the file.html.
```

##### Compatibility

- The `unescapeUrl(string)` function is available since **CloverETL 3.1.0**.

##### See also

- [escapeUrl](string-functions-ctl2.md#escapeurl)
- [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment)
- [isUrl](string-functions-ctl2.md#isurl)
- [unescapeUrlFragment](string-functions-ctl2.md#unescapeurlfragment)

---

#### unescapeUrlFragment

```ctl
string unescapeUrlFragment(string input);
string unescapeUrlFragment(string input, string encoding);
```

The function unescapes a string escaped by [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment).

The parameter `input` is a string to be unescaped. It the parameter is null, the function returns `null`.

The parameter `encoding` is an encoding to be used in conversion.

##### Error states

- If the `encoding` is `null`, the conversion fails.

##### Examples
Example 250. Usage of unescapeUrlFragment

```ctl
unescapeUrlFragment(null);
    // Returns null.
unescapeUrlFragment("");
    // Returns empty string.
unescapeUrlFragment("the+URL");
    // Returns "the URL".
unescapeUrlFragment("cook+book", null);
    // Fails for this input.
```

##### Compatibility

- The `unescapeUrlFragment(string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [escapeUrl](string-functions-ctl2.md#escapeurl)
- [escapeUrlFragment](string-functions-ctl2.md#escapeurlfragment)
- [isUrl](string-functions-ctl2.md#isurl)
- [unescapeUrl](string-functions-ctl2.md#unescapeurl)

---

#### unescapeXML

```ctl
string unescapeXML(string input);
```

The **unescapeXML(string)** function is designed to convert XML-escaped entities back into their original, unescaped characters. This function is useful when you need to extract or display the original content from an XML document that has previously been processed with the [escapeXML](string-functions-ctl2.md#escapexml) function.

List of reserved characters: `' , ", &, <, >`

##### Error states

- The function has no documented error states.

##### Examples
Example 251. Usage of unescapeXML

```ctl
unescapeXML("&lt;element name=&quot;&amp;myname;&quot;&gt;");
    // Returns <element name="&myname;">.
unescapeXML("Peter O&apos;Brian");
    // Returns Peter O'Brian.
// The following source example uses an XML-escaped customer name.
string nameOfCustomer = "Progress &amp; Prosperity, Co. &gt; Expectations";
unescapeXML(nameOfCustomer);
    // Returns Progress & Prosperity, Co. > Expectations.
```

##### Compatibility

- The `unescapeXML(string)` function is available since **CloverDX 6.4.0**.

##### See also

- [escapeXML](string-functions-ctl2.md#escapexml)

---

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

##### Error states

- If the parameter `form` is `null`, the function fails.

##### Examples
Example 252. Usage of unicodeNormalize

```ctl
unicodeNormalize("\u00C5", "NFD");
    // Returns "\u0041\u030A".
unicodeNormalize("\u0041"+"\u030A", "NFD");
    // Returns "\u0041\u030A".
unicodeNormalize("\u00C5", "NFC");
    // Returns "\u00C5".
unicodeNormalize("\u0041"+"\u030A", "NFC");
    // Returns "\u00C5".
unicodeNormalize("\u00C5", null);
    // Fails for this input.
unicodeNormalize(null, "NFD");
    // Returns null.
```

##### Compatibility

- The `unicodeNormalize(string)` function is available since **CloverETL 4.0.0-M1**.

##### See also

- [isUnicodeNormalized](string-functions-ctl2.md#isunicodenormalized)

---

#### upperCase

```ctl
string upperCase(string arg);
```

The `upperCase()` function takes one string argument and returns another string with cases converted to upper cases only.

The function returns `null` for a `null` input.

##### Error states

- The function has no documented error states.

##### Examples
Example 253. Usage of upperCase

```ctl
upperCase("Some string");
    // Returns SOME STRING.
```

##### Compatibility

- The `upperCase(string)` function is available since **CloverETL 3.0.0**.

##### See also

- [lowerCase](string-functions-ctl2.md#lowercase)
- [properCase](string-functions-ctl2.md#propercase)

---

#### validateCreditCard

```ctl
string validateCreditCard(string creditCard, boolean acceptEmpty);
```

The `validateCreditCard()` function takes string argument and uses Luhn algorithm, also known as 'modulus 10', to determine whether the argument is a valid credit card number.

The function returns `null` if the validation passes or an error message if it fails.

If the second parameter is `true` an empty string value is considered to be a valid value.

##### Error states

- The function has no documented error states.

##### Examples
Example 254. Usage of validateCreditCard

```ctl
validateCreditCard("5305-7204-2019-5319", false);
    // Returns null.
validateCreditCard("1234-5678-9012-3456", false);
    // Returns Checksum is not valid.
validateCreditCard(" ", true);
    // Returns null.
validateCreditCard(" ", false);
    // Returns Empty card number is not allowed.
```

##### Compatibility

- The `validateCreditCard()` function is available since **CloverDX 6.5.0**.

##### See also

- [validateEmail](string-functions-ctl2.md#validateemail)
- [validatePhoneNumber](string-functions-ctl2.md#validatephonenumber)

---

#### validateEmail

```ctl
string validateEmail(string email, boolean acceptEmpty);
```

The `validateEmail()` function takes string argument and performs syntactic check according to [RFC822](https://www.w3.org/Protocols/rfc822) standard to determine whether the argument is a valid email address. It does not try to connect or to send any message to the syntactically valid argument.

The function returns `null` if the validation passes or an error message if it fails.

If the second parameter is `true` an empty string value is considered to be a valid value.

##### Error states

- The function has no documented error states.

##### Examples
Example 255. Usage of validateEmail

```ctl
validateEmail("john.doe@example.com", false);
    // Returns null.
validateEmail("john.doeexamplecom", false);
    // Returns Missing final '@domain'.
validateEmail(null, true);
    // Returns null.
validateEmail(null, false);
    // Returns Empty email is not allowed.
```

##### Compatibility

- The `validateEmail()` function is available since **CloverDX 6.5.0**.

##### See also

- [validateCreditCard](string-functions-ctl2.md#validatecreditcard)
- [validatePhoneNumber](string-functions-ctl2.md#validatephonenumber)

---

#### validatePhoneNumber

```ctl
string validatePhoneNumber(string phoneNumber, string phoneRegion, boolean acceptEmpty);
```

The `validatePhoneNumber()` function takes string argument and validates if its a phone number.

The second parameter is phone region in a form of two letters [ISO Alpha 2](https://www.countrycode.org/) code. Its ignored and may be left empty if the phone number is written in international format.

The function returns `null` if the validation passes or an error message if it fails.

If the third parameter is `true` an empty string value is considered to be a valid value.

##### Error states

- The function has no documented error states.

##### Examples
Example 256. Usage of validatePhoneNumber

```ctl
validatePhoneNumber("(800) 555-0111", "US", false);
    // Returns null.
validatePhoneNumber("+18005550111", null, false);
    // Returns null.
validatePhoneNumber("+1 (800) 123-4567", null, false);
    // Returns Invalid phone number.
validatePhoneNumber(null, "US", true);
    // Returns null.
validatePhoneNumber(null, "US", false);
    // Returns Empty phone number is not allowed.
```

##### Compatibility

- The `validatePhoneNumber()` function is available since **CloverDX 6.5.0**.

##### See also

- [validateCreditCard](string-functions-ctl2.md#validatecreditcard)
- [validateEmail](string-functions-ctl2.md#validateemail)

---
