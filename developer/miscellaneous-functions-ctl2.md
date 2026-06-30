<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Miscellaneous functions -->

### Miscellaneous functions

#### List of functions

| [cast](miscellaneous-functions-ctl2.md#cast) |
| --- |
| [currentTimeMillis](miscellaneous-functions-ctl2.md#currenttimemillis) |
| [evalExpression](miscellaneous-functions-ctl2.md#evalexpression) |
| [getEnvironmentVariables](miscellaneous-functions-ctl2.md#getenvironmentvariables) |
| [getJavaProperties](miscellaneous-functions-ctl2.md#getjavaproperties) |
| [getOAuth2Token](miscellaneous-functions-ctl2.md#getoauth2token) |
| [getParamValue](miscellaneous-functions-ctl2.md#getparamvalue) |
| [getParamValues](miscellaneous-functions-ctl2.md#getparamvalues) |
| [getRawParamValue](miscellaneous-functions-ctl2.md#getrawparamvalue) |
| [getRawParamValues](miscellaneous-functions-ctl2.md#getrawparamvalues) |
| [getType](miscellaneous-functions-ctl2.md#gettype) |
| [hashCode](miscellaneous-functions-ctl2.md#hashcode) |
| [iif](miscellaneous-functions-ctl2.md#iif) |
| [isBlank](miscellaneous-functions-ctl2.md#isblank) |
| [isnull](miscellaneous-functions-ctl2.md#isnull) |
| [nvl](miscellaneous-functions-ctl2.md#nvl) |
| [nvl2](miscellaneous-functions-ctl2.md#nvl2) |
| [parseProperties](miscellaneous-functions-ctl2.md#parseproperties) |
| [printErr](miscellaneous-functions-ctl2.md#printerr) |
| [printLog](miscellaneous-functions-ctl2.md#printlog) |
| [raiseError](miscellaneous-functions-ctl2.md#raiseerror) |
| [resolveParams](miscellaneous-functions-ctl2.md#resolveparams) |
| [sleep](miscellaneous-functions-ctl2.md#sleep) |
| [toAbsolutePath](miscellaneous-functions-ctl2.md#toabsolutepath) |

The rest of the functions can be denominated as miscellaneous. These are the functions listed below.
> [!IMPORTANT]
> Remember that the object notation (e.g., `arg.isnull()`) cannot be used for these **Miscellaneous** functions.
>
> For more information about object notation, see [Functions Reference](functions-reference-ctl2.md).

#### cast

```ctl
<type> cast(variant value, <type>, <subtype...>);
```

Returns the value passed as the first argument cast to the type specified as the following arguments.

Returns `null` if the value is null.

Fails with an error if the value is not of the selected type.

Does not check the type of elements of lists and maps, only checks if the value is a `list` or `map`, respectively. E.g. the cast of a list of integers to a list of strings does not fail and will lead to runtime errors later in the code, see the examples below. Use a for loop if you need to check the type of elements.

**Compatibility**

The `cast(variant, type, subtype…)` function is available since **CloverDX 5.6.0**.
Example 307. Usage of cast

```ctl
variant value = "ABC";
string myString = cast(value, string); // myString contains "ABC"
value = 10;
integer myInteger = cast(value, integer); // myInteger contains 10
date myDate = cast(value, date); // error, "value" currently contains an integer

value = [1, 2, 3];
list[integer] intList = cast(value, list, integer); // intList contains [1, 2, 3]

// does not fail, will lead to runtime exceptions later
list[string] stringList = cast(value, list, string);
// avoid this problem by checking the type of elements before casting to list[string]:
for (integer i = 0; i < length(value); i++) {
     variant element = value[i];
     // typeof returns false for null
     if ((element != null) && !(element typeof string)) {
          raiseError(element + " is not a string");
     }
}

variant nullVariant = null;
integer nullInteger = cast(nullVariant, integer); // nullInteger contains null
```

**See also:**[variant](language-reference-ctl2.md#variant), [getType](miscellaneous-functions-ctl2.md#gettype), [typeof](language-reference-ctl2.md#typeof-operator)

#### currentTimeMillis

```ctl
long currentTimeMillis();
```

The `currentTimeMillis()` function returns the current time in milliseconds since the UNIX epoch (January 1, 1970 00:00:00 UTC).

**Compatibility**

The `currentTimeMillis()` function is available since **CloverDX 6.4.0**.
Example 308. Usage of currentTimeMillis()`long millis = currentTimeMillis();`
#### evalExpression

```ctl
variant evalExpression(string expression);
```

The `evalExpression()` function evaluates the result of a given expression and returns it as a `variant` data type. This function is useful for performing dynamic calculations, user-provided expressions, or evaluating conditional statements at runtime. Potential use cases for the evalExpression function include:

- Implementing custom business logic or rules using a more human-readable expression syntax.
- Dynamic calculations based on user input or configuration settings.
- Parsing and evaluating expressions from external sources, such as files or databases.

Basic syntax for using the function:

```ctl
string expression = getParamValue("USER_PROVIDED_CONDITION"); // contains: "$in.0.isValid == true"
variant result = evalExpression(expression);

boolean condition = cast(result, boolean);
```

In this example, the `expression` variable is assigned the value of the `USER_PROVIDED_CONDITION` graph parameter using the `getParamValue` function. This demonstrates a use case where the condition to be evaluated is provided dynamically by the user at runtime. In the example user specifies a condition, which checks input field `isValid` from first input port. The value of `expression` is then passed to the `evalExpression` function, which evaluates the expression and returns the result as a variant data type. Please note, if you need to get the actual value with a proper data type, the `cast` function could be used.

The expression parameter is a string containing the expression to be evaluated. The expression can include arithmetic, logical, or relational operators, as well as functions and constants supported by the CTL engine. The only requirement is the expression should return a value, `for, if` or other statements are not allowed. In addition to simple expressions, the `evalExpression` function can handle more complex logic using custom functions.

To reference external custom functions, make sure the function is defined and accessible within the scope of the `evalExpression` function. The custom function should accept input parameters as needed and return a value that can be used within the expression.
Example 309. Example of using a custom function:

```ctl
import "trans/myCustomFunctions.ctl";

variant result;
integer a = 4;
integer b = 2;

result = evalExpression("doCalculation(a, b)");

$out.0.output = result; // returns 2.0
```

The external file `myCustomFunctions.ctl` is:

```ctl
function number doCalculation(integer a, integer b){
	return a/b;
}
```

**Error handling**

In case the provided expression is invalid or causes a runtime error, the `evalExpression` function generates an exception. To handle these exceptions, use a try-catch block with the `CTLException` exception type.

Error handling is important when using the `evalExpression` function because it is designed for defining external expressions, mainly from users or from dynamic configurations. Therefore, it is necessary to check for syntax and runtime errors. In case the expression is propagated from outside, it is essential to ensure proper error handling to prevent unexpected behavior or crashes in the application.
Example 310. Error handling

```ctl
import "trans/myCustomFunctions.ctl";

variant result;
integer a = 4;
integer b = 0;

result = evalExpression("doCalculation(a, b)");

$out.0.output = result;
```

The external file `myCustomFunctions.ctl` is:

```ctl
function number doCalculation(integer a, integer b){
	return a/b;
}
```

In this example, a runtime exception will occur because `b` is equal to 0, which will cause a division by zero error. The actual source of the exception is in the `doCalculation` function (which is an external). In this example, the issue occurred on line 7 of the transformation, but the actual error is in `myCustomFunctions.ctl` on line 2.
Example 311. Error output

```ctl
Interpreter runtime exception when dynamically evaluating CTL expression on line 12 column 18
    ----------------------- CTL2 snippet -----------------------
    7:          result = evalExpression("doCalculation(a, b)");
                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    ----------------------- CTL2 snippet -----------------------

    *** Caused by executing CTL code:

    Interpreter runtime exception on line 2 column 12 in import trans/myCustomFunctions.ctl
    Caused by: java.lang.ArithmeticException -> / by zero
    ----------------------- CTL2 snippet -----------------------
    2:     return a/b;
```

Example of error handling with the `evalExpression` function:
Example 312. Error handling

```ctl
try {
    variant result = evalExpression("user_input");
} catch (const CTLException e) {
    printLog(warn, "The input expresssion produces an error. Error details: " + e);
}
```

#### getEnvironmentVariables

```ctl
map[string,string] getEnvironmentVariables();
```

The `getEnvironmentVariables()` function returns an unmodifiable map of system environment variables.

An environment variable is a system-dependent external named value. Similar to the Java function `System.getenv()`. Note that the keys are case-sensitive.

**Compatibility**

The `isEmpty()` function is available since **CloverETL 3.3.x**.
Example 313. Usage of getEnvironmentVariables()`string envPath = getEnvironmentVariables()["PATH"];`
**See also:**[getJavaProperties](miscellaneous-functions-ctl2.md#getjavaproperties)

#### getJavaProperties

```ctl
map[string,string] getJavaProperties();
```

The `getJavaProperties()` function returns the map of Java VM system properties.

Similar to the Java function `System.getProperties()`.

**Compatibility**

The `getJavaProperties()` function is available since **CloverETL 3.3.x**.
Example 314. Usage of getJavaProperties()`string operatingSystem = getJavaProperties()["os.name"];`
**See also:**[getEnvironmentVariables](miscellaneous-functions-ctl2.md#getenvironmentvariables)

#### getParamValue

```ctl
string getParamValue(string paramName);
```

The `getParamValue()` function returns the value of the specified graph parameter.

The argument is the name of the graph parameter without the `${ }` characters, e.g. `PROJECT_DIR`. The returned value is resolved, i.e. it does not contain any references to other graph parameters.

The function returns `null` for non-existent parameters.
> [!NOTE]
> Function `getParamValue` decrypts **secure parameters**. Secure parameters are being deciphered with each use. There is a performance penalty associated with this process and therefore, when single secure parameter is used in a single script, it is advisable to cache its value manually to avoid multiple resolutions.

**Compatibility**

The `getParamValue(string)` function is available since **CloverETL 3.3.x**.
Example 315. Usage of getParamValue`string datainDir = getParamValue("DATAIN_DIR"); // will contain "./data-in"`
**See also:**[getParamValues](miscellaneous-functions-ctl2.md#getparamvalues)

#### getParamValues

```ctl
map[string,string] getParamValues();
```

The `getParamValues()` function returns a map of graph parameters and their values.

The keys are the names of the parameters without the `${ }` characters, e.g. `PROJECT_DIR`. The values are resolved, i.e. they do not contain any references to other graph parameters. The map is unmodifiable.

The function returns `null` for non-existent parameters.
> [!NOTE]
> The function `getParamValues` decrypts **secure parameters**. Secure parameters are being deciphered with each use. There is a performance penalty associated with this process and therefore, when single secure parameter is used in a single script, it is advisable to cache its value manually to avoid multiple resolutions.

**Compatibility**

The `getParamValues()` function is available since **CloverETL 3.3.x**.
Example 316. Usage of getParamValues`string datainDir = getParamValues()["DATAIN_DIR"]; // will contain "./data-in"`
**See also:**[getParamValue](miscellaneous-functions-ctl2.md#getparamvalue)

#### getRawParamValue

```ctl
string getRawParamValue(string paramName);
```

The `getRawParamValue()` function returns the value of the specified graph parameter.

The argument is the name of the graph parameter without the `${ }` characters, e.g. `PROJECT_DIR`. In contrast with `getParamValue(string)` function, the returned value is unresolved, so references to other graph parameters are not resolved and secure parameters are not decrypted.

The function returns `null` for non-existent parameters.

**Compatibility**

The `getRawParamValue(string)` function is available since **CloverETL 3.5.0**.
Example 317. Usage of getRawParamValue`string datainDir = getRawParamValue("DATAIN_DIR"); // will contain "${PROJECT}/data-in"`
**See also:**[getRawParamValues](miscellaneous-functions-ctl2.md#getrawparamvalues)

#### getRawParamValues

```ctl
map[string,string] getRawParamValues();
```

The `getRawParamValues()` function returns a map of graph parameters and their values.

The keys are the names of the parameters without the `${ }` characters, e.g. `PROJECT_DIR`. Unlike `getParamValues()` function, the values are unresolved, so references to other graph parameters are not resolved and secure parameters are not decrypted. The map is unmodifiable.

The function returns `null` for non-existent parameters.

**Compatibility**

The `getRawParamValues()` function is available since **CloverETL 3.5.0**.
Example 318. Usage of getRawParamValues`string datainDir = getRawParamValues()["DATAIN_DIR"]; // will contain "${PROJECT}/data-in"`
**See also:**[getRawParamValue](miscellaneous-functions-ctl2.md#getrawparamvalue)

#### getType

```ctl
string getType(variant arg);
```

Returns the actual runtime type of the argument as a `string`.

If the argument is `null`, the function returns the string `"null"`.

**Compatibility**

The `getType(variant)` function is available since **CloverDX 5.6.0**.
Example 319. Usage of getType

```ctl
variant myString = "ABC";
string type1 = getType(myString); // "string"
variant myList = ["a", "b", 7];
string type2 = getType(myList); // "list"
```

**See also:**[variant](language-reference-ctl2.md#variant), [cast](miscellaneous-functions-ctl2.md#cast), [typeof](language-reference-ctl2.md#typeof-operator)

#### hashCode

```ctl
integer hashCode(integer arg);
integer hashCode(long arg);
integer hashCode(number arg);
integer hashCode(decimal arg);
integer hashCode(boolean arg);
integer hashCode(date arg);
integer hashCode(string arg);
integer hashCode(record arg);
integer hashCode(map arg);
integer hashCode(variant arg);
```

Returns java hashCode of parameter.

**Compatibility**

The `hashcode(…)` function is available since **CloverETL 3.5.0-M1**.
Example 320. Usage of hashCode The function `hashCode(5)` returns some number.
#### iif

```ctl
<any type> iif(boolean con, <any type>, <any type>);
```

The `iif()` function returns the second argument if the first argument is `true`, or the third argument if the first argument is `false`.

If the first argument is `null`, the function fails with an error.

**Compatibility**

The `iif(boolean,E,E)` function is available since **CloverETL 3.0.0**.
Example 321. Usage of iif
The function `iif(true, "abc", "def")` returns `abc`.

The function `iif(false, "abc", "def")` returns `def`.

**See also:**[nvl](miscellaneous-functions-ctl2.md#nvl), [nvl2](miscellaneous-functions-ctl2.md#nvl2)

#### isBlank

```ctl
boolean isBlank(boolean arg);
boolean isBlank(byte arg);
boolean isBlank(decimal arg);
boolean isBlank(integer arg);
boolean isBlank(list<E> arg);
boolean isBlank(long arg);
boolean isBlank(map<K, V> arg);
boolean isBlank(number arg);
boolean isBlank(record arg);
boolean isBlank(variant arg);
boolean isBlank(string arg);
```

For `long`, `integer`, `decimal`, `boolean`, `date` and `number` arguments the function returns a `true` if the input is `null` otherwise `false`.

For following structured types: `byte`, `map`, `list` and `variant` it returns `true` if the input is `null` or if the number of elements forming a given structured data type is `0`.

For `string` argument, the `isBlank()` function returns a boolean value depending on whether the string contains only white space characters (true) or not (false), if the input is `null` or an empty string, the function returns `true`.

**Compatibility**

- The `isBlank(string)` function is available since **CloverETL 3.0.0**.
- The overloads for types other than string are available since **CloverDX 7.3.0**.
Example 322. Usage of isBlank

```ctl
// basic data types behave like integer - function returns true for null values
integer intVal1 = 1;
integer intVal2 = null;
isBlank(intVal1); // false
isBlank(intVal2); // true

// list of any type
list[string] listString = null;
isBlank(listString); // true
listString = [];
isBlank(listString); // true
listString[1] = "s";
isBlank(listString); // false

// map of any type
map[string, integer] map1 = null;
isBlank(map1); // true
map1 = {};
isBlank(map1); // true
map1["first"] = 10;
isBlank(map1); // false

// string
isBlank("   "); // true, because there are 3 space chars (char 0x20) between quotes.
isBlank(" "); // true, because there is hard space character (0xA0) has been used between the quotes.
isBlank(" bc"); // false

// record
isBlank($in.0); // false, because there is an input record having 14 fields.
isBlank($out.0); // true, because there is an output record having 0 fields.

// byte
byte b1 = null;
isBlank(b1); // true
isBlank(hex2byte("414243")); // false

// variant
variant v = null;
isBlank(v); // true
v = [];
isBlank(v); // true
v = {};
isBlank(v); // true
v["abc"] = "efg";
isBlank(v); // false
```

**See also:**[removeBlankSpace](string-functions-ctl2.md#removeblankspace), [isBlank(string)](string-functions-ctl2.md#isblank)

#### isnull

```ctl
boolean isnull(<any type> arg);
```

The `isnull()` function returns a boolean value depending on whether the argument is null (true) or not (false). The argument may be of any data type.
> [!IMPORTANT]
> If you set the **Null value** property in metadata for any `string` data field to any non-empty string, the `isnull()` function will return `true` when applied on such string. And return `false` when applied on an empty field.
>
> For example, if `field1` has **Null value** property set to `"<null>"`, `isnull($in.0.field1)` will return `true` on the records in which the value of `field1` is `"<null>"` and `false` on the others, even on those that are empty.
>
> For detailed information, see [Null value](metadata-editor.md#null-value-bridge).

**Compatibility**

The `isnull()` function is available since **CloverETL 3.0.0**.
Example 323. Usage of isnull
The function `isnull(null)` returns `true`.

The function `isnull(123)` returns `false`.

**See also:**[isNull](field-access-functions-ctl2.md#isnull), [nvl](miscellaneous-functions-ctl2.md#nvl), [nvl2](miscellaneous-functions-ctl2.md#nvl2)

#### nvl

```ctl
<any type> nvl(<any type> arg, <any type> default);
```

The `nvl()` function returns the first argument, if its value is not `null`, otherwise the function returns the second argument. Both arguments must be of the same type.

**Compatibility**

The `nvl()` function is available since **CloverETL 3.0.0**.
Example 324. Usage of nvl
The function `nvl(null, "def")` returns `def`.

The function `nvl("abc", "def")` returns `abc`.

**See also:**[iif](miscellaneous-functions-ctl2.md#iif), [isnull](miscellaneous-functions-ctl2.md#isnull), [nvl2](miscellaneous-functions-ctl2.md#nvl2)

#### nvl2

```ctl
<any type> nvl2(<any type> arg, <any type>, <any type>);
```

The `nvl2()` function returns the second argument, if the first argument has not `null` value. If the first argument has a `null` value, the function returns the third argument.

**Compatibility**

The `nvl2(obj,obj,obj)` function is available since **CloverETL 3.0.0**.
Example 325. Usage of nvl2
The function `nvl2(null, "abc", "def")` returns `def`.

The function `nvl2(123, "abc", "def")` returns `abc`.

**See also:**[iif](miscellaneous-functions-ctl2.md#iif), [isnull](miscellaneous-functions-ctl2.md#isnull), [nvl](miscellaneous-functions-ctl2.md#nvl)

#### getOAuth2Token

```ctl
string getOAuth2Token(string connectionName);
string getOAuth2Token(string connectionName, boolean forceRefresh);
```

The `getOAuth2Token` function returns OAuth2 access token from authorized OAuth2 connection linked in graph.

The `connectionName` parameter is a name of the OAuth2 connection linked in graph. If the connection specified does not exist or is of the wrong type, an exception is thrown.

The optional parameter `forceRefresh` can be used to ask the connection to obtain a new OAuth2 access token instead of the currently cached one.

Without `forceRefresh` parameter, returned tokens are valid for at least the next 60 seconds after the call is made. Forcing a refresh ensures maximum possible validity time, but it is slower than using default because new tokens must be obtained from remote OAuth2 provider.

**Compatibility**

The `getOAuth2Token(string)` function is available since **CloverDX 5.12.0**.

#### parseProperties

```ctl
map[string, string] parseProperties(string properties);
```

The `parseProperties()` function converts key-value pairs separated with a new line from a `string` to a `map`.

The order of properties is preserved.

If the input string is `null` or empty, the function returns an empty map.

**Compatibility**

The `parseProperties()` function is available since **CloverETL 4.1.0**.
Example 326. Sample property file

```properties
# lines starting with # are comments
! The exclamation mark can also mark text as comments.

# This is the simplest property
key = value

# A long property may be separated on multiple lines
longvalue = aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa \
            aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

# The key and element characters #, !, =, and : are written with
# a preceding backslash to ensure that they are properly loaded.
website = http\://www.cloverdx.com/

# Add spaces to the key
key\ with\ spaces = This is the value that could be looked up with the key "key with spaces".

# Unicode u-umlaut
uuml : \u00FC
```

Example 327. Usage of parseProperties
The function `parseProperties("key1=value1\nkey2=value2")["key2"]` returns `"value2"`.

Assuming that string variable `input` contains the sample property file from above, `parseProperties(input)` produces the following map: `{key=value, longvalue=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa, website=http://www.cloverdx.com/, key with spaces=This is the value that could be looked up with the key "key with spaces"., uuml=ü}`.

**See also:**[Properties](parameters.md#properties) (as parameter editor type), [java.util.Properties.load(Reader)](http://docs.oracle.com/javase/7/docs/api/java/util/Properties.html#load%28java.io.Reader%29), [https://en.wikipedia.org/wiki/.properties](https://en.wikipedia.org/wiki/.properties)

#### printErr

```ctl
void printErr(<any type> message);
void printErr(<any type> message, boolean printLocation);
```

The `printErr()` function prints out the `message` to the graph execution log with `error` log level. The `printLocation` parameter determines whether the source code location is also printed with the message. If `printLocation` is set to `true`, the location is appended at the end of the message as `(on line: L col: C)` where L is a line number and C is a column number.

**Compatibility**

- The `printErr` is available since **CloverETL 3.0.0**.
- In **CloverETL 4.1**, the functionality was changed and the function no longer writes to stderr but to a graph log. The original behavior with stderr was harder to work with in **CloverDX Server** environment.

```ctl
printErr("My error message");
// Will print something like this to a graph log:
// 2026-02-09 15:00:00,123 ERROR 3904 [MAP_3904] My error message

printErr("My error message", false);
// This is same as if the printLocation parameter was ommitted.
// 2026-02-09 15:00:00,123 ERROR 3904 [MAP_3904] My error message

printErr("My error message", true);
// Will print something like this to a graph log:
// 2026-02-09 15:00:00,123 ERROR 3904 [MAP_3904] My error message (on line: 18 col: 5)
```

**See also:**[printLog](miscellaneous-functions-ctl2.md#printlog), [raiseError](miscellaneous-functions-ctl2.md#raiseerror)

#### printLog

```ctl
void printLog(level loglevel, <any type> message);
void printLog(level loglevel, string logger, <any type> message);
```

The `printLog()` function sends a `message` to a logger.

The log level of the message must be one of the following: `debug`, `info`, `warn`, `error`, or `fatal`. The log level must be specified as a constant, it cannot be a variable reference.

By default, the message is logged to graph’s run log. A custom logger may be chosen by referencing it by the name attribute. If the specified logger doesn’t exist, the function will revert to the default behavior. Custom loggers can be defined in log4j configuration files for both Worker and Core. For more details about custom logging configuration, please see [Logging customization](../operations/logging.md#logging-customization).

**Compatibility**

The `printLog(level,string)` function is available since **CloverETL 3.0.0**.

The `printLog(level loglevel, string logger, <any type> message)` function is available since **CloverDX 6.4.0.**
Example 328. Usage of printLog
The function `printLog(warn, "abc")` prints `abc` into the log.

`printLog(info, $out.0)` prints a string representation of a record to the log.

`printLog(error, "myCustomLogger", "Example error message")` prints a message to a custom logger.

**See also:**[printErr](miscellaneous-functions-ctl2.md#printerr), [raiseError](miscellaneous-functions-ctl2.md#raiseerror)

#### raiseError

```ctl
void raiseError(string message);
```

The `raiseError()` function throws out an error with the `message` specified as the argument.

The execution of the graph is aborted.

**Compatibility**

The `raiseError(string)` function is available since **CloverETL 3.0.0**.
Example 329. Usage of raiseError`raiseError("The error message")`
**See also:**[printErr](miscellaneous-functions-ctl2.md#printerr), [printLog](miscellaneous-functions-ctl2.md#printlog)

#### resolveParams

```ctl
string resolveParams(string text);
string resolveParams(string text, boolean resolveSpecialChars);
```

The `resolveParams()` function substitutes all graph parameter references in the `text` by the values of those parameters. Each occurrence of pattern `${<PARAMETER_NAME>}` which is referencing an existing graph parameter is replaced by the parameter’s value. Undefined parameter references are left without any change - i.e., they will be resolved as `${<PARAMETER_NAME>}`.

The function can also resolve environment variables in similar manner - e.g. `PATH` or `JAVA_HOME`.

Note that parameter names are case sensitive, so `${BATCH_SIZE}` is different than `${batch_size}`.

The second parameter controls whether character escape sequences (like `\n` or `\t` etc.) should be interpreted in the string as well. If `resolveSpecialChars` is `null`, the function fails. Default value is `false` (escape sequences are not resolved).
> [!NOTE]
> Parameter and escape sequence resolution in CTL code is automatic when the graph is parsed if the parameter or sequence is "hard-coded" and there is no need to call `resolveParams`.
>
> For example, code like `printLog(info, "The input directory is ${DATAIN_DIR}")` will print "The input directory is ./data-in" into the graph log.
>
> The `resolveParams` is only needed when the data that includes parameter references is read from a file or computed in the graph.
Example 330. Usage of resolveParams The usage of the function `resolveParams()` is necessary if the string containing a parameter is created at runtime:

```ctl
const string[] FOLDER_TYPES = ["IN", "OUT", "TMP"];
foreach (string type: FOLDER_TYPES) {
    printLog(info, resolveParams(type + " folder is: ${DATA" + type + "_DIR}"));
}
```

This will print output like this into the log:

```ctl
2026-02-09 18:08:54,568 INFO  3915 [MAP_3915] IN folder is: ./data-in
2026-02-09 18:08:54,568 INFO  3915 [MAP_3915] OUT folder is: ./data-out
2026-02-09 18:08:54,568 INFO  3915 [MAP_3915] TMP folder is: ./data-tmp
```

**See also:**[getEnvironmentVariables](miscellaneous-functions-ctl2.md#getenvironmentvariables), [getJavaProperties](miscellaneous-functions-ctl2.md#getjavaproperties), [getParamValues](miscellaneous-functions-ctl2.md#getparamvalues), [getParamValue](miscellaneous-functions-ctl2.md#getparamvalue), [Parameters](parameters.md)

#### sleep

```ctl
void sleep(long duration);
```

The `sleep()` function pauses the execution for specified time in milliseconds.

**Compatibility**

The `sleep(long)` function is available since **CloverETL 3.1.0**.
Example 331. Usage of sleep The function `sleep(5000)` will sleep for 5 seconds.
#### toAbsolutePath

```ctl
string toAbsolutePath(string path);
```

The `toAbsolutePath()` function converts the specified path to an OS-dependent absolute path to the same file. The input may be a path or a URL. If the input path is relative, it is resolved against the context URL of the running graph.

If running on the Server, the function can also handle [sandbox URLs](examples-of-file-url-in-readers.md#sandbox-resource-as-data-source). However, a sandbox URL can only be converted to an absolute path, if the file is locally available on the current server node.

If the conversion fails, the function returns `null`.

If the given parameter is `null`, the function fails with an error.
> [!NOTE]
> The returned path will always use forward slashes as directory separator, even on Microsoft Windows systems.
>
> If you need the path to contain backslashes, use the `translate()`function:
>
>
> ```ctl
> string absolutePath = toAbsolutePath(path).translate('/', '\\');
> ```

**Compatibility**

The `toAbsolutePath(string)` function is available since **CloverETL 3.3.x**.
Example 332. Usage of toAbsolutePath The function `toAbsolutePath("graph")` will return for example `C:/workspace/doc_project/graph`.
**See also:**[translate](string-functions-ctl2.md#translate)
