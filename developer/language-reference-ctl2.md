<!-- Development > CTL2 - CloverDX Transformation Language > Language reference -->

## 33. Language reference

This chapter describes the syntax of **CloverDX** Transformation Language - CTL. CTL can be used to define transformations in many components.

This section describes the following areas:

- [Program structure](language-reference-ctl2.md#program-structure)
- [Comments](language-reference-ctl2.md#comments)
- [Import](language-reference-ctl2.md#import)
- [Data types in CTL2](language-reference-ctl2.md#data-types-in-ctl2)
- [Literals](language-reference-ctl2.md#literals)
- [Variables](language-reference-ctl2.md#variables)
- [Dictionary in CTL2](language-reference-ctl2.md#dictionary-in-ctl2)
- [Operators](language-reference-ctl2.md#operators)
- [Simple statement and block of statements](language-reference-ctl2.md#simple-statement-and-block-of-statements)
- [Control statements](language-reference-ctl2.md#control-statements)
- [Functions](language-reference-ctl2.md#functions)
- [Conditional fail expression](language-reference-ctl2.md#conditional-fail-expression)
- [Accessing data records and fields](language-reference-ctl2.md#accessing-data-records-and-fields)
- [Mapping](language-reference-ctl2.md#mapping)
- [Parameters](language-reference-ctl2.md#parameters)

### Program structure

Each program written in CTL must contain the following parts:

```ctl
ImportStatements
VariableDeclarations
FunctionDeclarations
Statements
Mappings
```

All of them may be interspersed; however, there are some principles that are valid for them:

- If an import statement is defined, it must be situated at the beginning of the code.
- Variables and functions must be declared before use.
- Declarations of variables and functions, statements and mappings may also be mutually interspersed.
> [!IMPORTANT]
> In CTL2, variables and functions may be declared in any place of the transformation code and may be preceded by other code. However, remember that each variable and function must always be declared before it is used.
>
> This is one of the differences between the two versions of **CloverDX** Transformation Language.
Example 17. Example of CTL2 syntax (Rollup)

```ctl
//#CTL2

string[] customers;
integer Length;

function void initGroup(VoidMetadata groupAccumulator) {
}

function boolean updateGroup(VoidMetadata groupAccumulator) {
     customers = split($in.0.customers," - ");
     Length = length(customers);

     return true;
}

function boolean finishGroup(VoidMetadata groupAccumulator) {
     return true;
}

function integer updateTransform(integer counter, VoidMetadata groupAccumulator) {
     if (counter >= Length) {
          clear(customers);

          return SKIP;
     }

     $out.0.customers = customers[counter];
     $out.0.EmployeeID = $in.0.EmployeeID;

     return ALL;
}

function integer transform(integer counter, VoidMetadata groupAccumulator) {
     return ALL;
}
```

Note the `//#CTL2` header.

You can enable the CTL compiled mode by changing the header to `//#CTL2:COMPILE`. For more information, see [Compiled mode](ctl-overview.md#ctl-2-compiled-mode).

### Comments

Comments are lines or parts of lines not being processed. They serve to describe what happens within the program or to disable program statements.

The comments are of two types - end of line comments or multiline comments. See the following two options:

```ctl
// This is an end line comment.
// Everything following the slashes until end of line is a comment.

integer count = 0; // Comment can follow the code

/* This is a multiline comment.
   Everything between starting and ending symbol is a comment. */
```

### Import

Import makes accessible functions from other `.ctl` files. It is similar to `import` statement in Java or `include` statement in C/C++. Files to be included must be defined at the beginning before any other declaration(s) and/or statement(s).

- ```ctl
  import 'fileURL';
  ```
- ```ctl
  import "fileURL";
  ```

You must decide whether you want to use single or double quotes. Single quotes do not escape so called escape sequences. For more details see [Literals](language-reference-ctl2.md#literals) below. For these `fileURL`, you must type the URL of some existing source code file.
Example 18. Example of an import of a CTL file

```ctl
//#CTL2

import "trans/filterFunctions.ctl";

function integer transform() {
    $out.0.field1 = filterChars($in.0.field1);

    return ALL;
}
```

You can use graph parameters to define the name of the imported file.
Example 19. Example of importing a CTL file with a graph parameter

```ctl
//#CTL2

import "${FUNCTION_DIR}/filterFunctions.ctl";

function integer transform() {
    $out.0.field1 = filterChars($in.0.field1);

    return ALL;
}
```

#### Metadata import in CTL2

Since CloverDX 5.6, it is also possible to import [metadata](metadata.md) from an external `.fmt` file, similarly to importing external `.ctl` files. Then you can use these metadata definitions in CTL when creating record structures. This enables you to use metadata that are unavailable in the current graph. Note that imported metadata can overlay metadata with the same name that already exist in the current graph.

```ctl
import metadata "<path>";
```

or

```ctl
import metadata "<path>" <new name>;
```

The scope of these new metadata definitions is limited just to the current CTL script, so other components don’t see them.
Example 20. CTL metadata import

```ctl
//#CTL2

import metadata "${META_DIR}/OrderItem.fmt"; // import OrderItem

// import metadata from Person.fmt and rename it to "Customer"
import metadata "${META_DIR}/Person.fmt" Customer;

OrderItem item;
item.productId = 12345;
item.quantity = 5;

Customer c;
c.firstName = "John";
```

### Data types in CTL2

For basic information about data types used in metadata, see [Data types in metadata](metadata-records-and-fields.md#data-types-in-metadata).

In any program, you can use some variables. Data types in CTL are the following:

| [boolean](language-reference-ctl2.md#boolean) |
| --- |
| [byte](language-reference-ctl2.md#byte) |
| [cbyte](language-reference-ctl2.md#cbyte) |
| [date](language-reference-ctl2.md#date) |
| [decimal](language-reference-ctl2.md#decimal) |
| [integer](language-reference-ctl2.md#integer) |
| [long](language-reference-ctl2.md#long) |
| [number (double)](language-reference-ctl2.md#number-double) |
| [string](language-reference-ctl2.md#string) |
| [list](language-reference-ctl2.md#list) |
| [map](language-reference-ctl2.md#map) |
| [variant](language-reference-ctl2.md#variant) |
| [record](language-reference-ctl2.md#record) |

#### boolean

The `boolean` data type contains values of logical expressions.

The default value is `false`.

It can be either `true` or `false`.

Its declaration looks like this: `boolean identifier;`
Example 21. Declaration of boolean variable

```ctl
boolean b;        // declaration
boolean b = true; // declaration with assignment
```

#### byte

This data type stores binary data of a length that can be up to `Integer.MAX_VALUE` as a maximum.

The default value is `null`.

Its declaration looks like this: `byte identifier;`
Example 22. Declaration of byte variable

```ctl
byte b;
// declaration of variable with assignment
byte b = hex2byte("414243");
```

#### cbyte

This data type is a compressed representation of byte data type to reduce runtime memory footprint. Compressed size of the data can be up to `Integer.MAX_VALUE` as a maximum.

The default value is `null`.

Its declaration looks like this: `cbyte identifier;`
Example 23. Declaration of cbyte variable

```ctl
cbyte c1;
cbyte c2 = hex2byte("61"); // declaration with assignment
```

##### date

The `date` data type contains date and time.

The default value is `1970-01-01 00:00:00 GMT`.

Its declaration looks like this: `date identifier;`
Example 24. Declaration of date variable

```ctl
// declaration of variable
date d;
// declaration of variable with assignment from function
date d = str2date("1600-01-31", "yyyy-MM-dd");
```

> [!NOTE]
> If you work with `date`, you should be aware of time zone of the data.

#### decimal

The `decimal` data type serves to store decimal numbers.

Calculations with the `decimal` data type are performed in fixed point arithmetic. It makes `decimal` data type suitable for calculations with money.

The default value is `0`.

Its declaration looks like this: `decimal identifier;`

By default, any decimal may have up to 32 significant digits. If you want to have different **Length** or **Scale**, you need to set these properties of `decimal` field in metadata.
Example 25. Usage of decimal data type in CTL2
If you assign `100.0 / 3` to a decimal variable, its value will be `33.333333333333336`. As `100.0` is double and `3` is integer, the both operands were firstly converted to double, then the value has been calculated and finally the result value has been converted to decimal. Assigning it to a decimal field (with default **Length** and **Scale**, which are 12 and 2, respectively), it will be converted to `33.33D`.

You can cast any float number to the decimal data type by appending the `d` letter to its end.

Any numeric data type (integer, long, number/double) can be converted to `decimal`.
Example 26. Declaration of decimal variable

```ctl
decimal d;
decimal d2 = 4.56D; // declaration of variable with assignment
```

#### integer

The `integer` data type can contain integral values.

CTL2 `integer` can store values from `-2147483648` to `2147483647`.

The `integer` data type can overflow (i.e. adding 1 to the maximum value returns `-2147483648`; similarly, subtracting 1 from the minimum value returns `2147483647`) which may lead to errors and/or incorrect results.

The default value is `0`.

Its declaration looks like this: `integer identifier;`
> [!IMPORTANT]
> The value `-2147483648` can be stored in *CTL2 variable* but cannot be stored in an integer field of record metadata (value of the field would be null). If the value `-2147483648` is expected to arise, consider usage of data type with wider range of values in metadata; e.g. `long`.

If you append the `L` letter to the end of any integer number, you can cast it to the long data type.

`Integer` can be converted to `long`, `double` or `decimal` using automatic conversions.
Example 27. Declaration of integer variable

```ctl
integer i1;
integer i2 = 1241;
```

#### long

`long` is an integral data type allowing to store greater values than the `integer` data type.

CTL2 `long` can store values from `-9223372036854775808` to `9223372036854775807`.

The `long` data type can overflow (i.e. adding 1 to the maximum value returns `-92233720368547758088`; similarly, subtracting 1 from the minimum value returns `9223372036854775807`) which may lead to errors and/or incorrect results.

The default value is `0`.

Its declaration looks like this: `long identifier;`
> [!IMPORTANT]
> The value `-9223372036854775808` can be stored in *CTL2 variable* but the value is used in long field in record metadata for `null` value. If the value `-9223372036854775808` is expected to arise, consider usage of data type with wider range of values in metadata; e.g. `decimal`.

Any integer number can be cast to `long` data type by appending the `l` letter to its end.

`Long` data type can be converted to `number/double` or `decimal` without explicit casting.
Example 28. Declaration of long variable

```ctl
long myLong;
long myLong2 = 2141L;
```

#### number (double)

The `number` data type is used for floating point number.

The default value is `0.0`.

Its declaration looks like this: `number identifier;`

If you need a data type for money amount, we advise using `decimal` instead of `number (double)`.

The `integer` and `long` data types can be converted to `double` using automatic conversions. If `long` is being converted to `number (double)`, lost of precision may occur.

`Number(double)` can be converted to `decimal` without explicit casting.
Example 29. Declaration of number (double) variable

```ctl
double d;
double d2 = 1.5e2;
```

#### string

This data type serves to store sequences of characters.

The default value is *empty string*.

The declaration looks like this: `string identifier;`
Example 30. Declaration of string variable

```ctl
string s;
string s2 = "Hello world!";
```

##### list

Since **CloverDX 5.6**, the type of elements of a list may be any other data type, including nested lists or maps.

The elements of a list are indexed by integers starting from 0.

Its declaration can look like this: `string[] identifier;`

For nested lists or maps, use the following syntax instead: `listtype of elements>] identifier;`

The default list is an empty list.
Example 31. List

```ctl
integer[] myIntegerList;
myIntegerList[5] = 123;

// Customer is metadata record name
Customer JohnSmith;
Customer PeterBrown;
Customer[] CompanyCustomers;
CompanyCustomers[0] = JohnSmith;
CompanyCustomers[1] = PeterBrown;

// Nested lists and maps:
list[list[string]] listOfLists;
list[map[string, integer]] listOfMaps;
```

##### Assignments:

- ```ctl
  myStringList[3] = "abc";
  ```
  The string `"abc"` is put to the fourth position in the string list. The preceding items are filled with `null` as follows:
  `myStringList` is `[null,null,null,"abc"]`
- ```ctl
  myList1 = myList2;
  ```
  Assigns a copy of `myList2` to `myList1`. It means that both lists will contain the same elements.
- ```ctl
  myList1 = myList1 + myList2;
  ```
  Adds all elements of `myList2` to the end of `myList1`.
  Both lists must be based on the same primitive data type.
- ```ctl
  myList = [];
  ```
  Assigns an empty list to `myList`.
- ```ctl
  myList = ["a", "b", "c"];
  ```
  Assigns a list containing three strings to `myList`.
- ```ctl
  myList = null;
  ```
  Discards the previous value of `myList`.

#### map

This data type is a container of pairs of a key and a value.

Its declaration looks like this: `maptype of key>, <type of value>]``identifier``;`

Since **CloverDX 5.6**, the `Value` can be any of the other data types, including records, nested lists or other maps, but the `Key` can only be a primitive data type: `boolean`, `date`, `decimal`, `integer`, `long`, `number` or `string`.

The default map is an empty map.
Example 32. Map

```ctl
map[string, boolean] map1;
map1["abc"] = true;

// Customer is the name of record
Customer JohnSmith;
Customer PeterBrown;

map[integer, Customer] CompanyCustomersMap;
CompanyCustomersMap[JohnSmith.ID] = JohnSmith;
CompanyCustomersMap[PeterBrown.ID] = PeterBrown;

// Nested maps and lists:
map[string, map[string, integer]] mapOfMaps;
map[integer, list[string]] mapOfLists;
```

The assignments are similar to those valid for a list:

- ```ctl
  myMap["abc"] = 7;
  ```
  Puts the value `7` into `myMap` under the key `"abc"`.
- ```ctl
  myMap2 = myMap1;
  ```
  Assigns a copy of `myMap1` to `myMap2`.
- ```ctl
  myMap = {};
  ```
  Assigns an empty map to `myMap`.
- ```ctl
  myMap = { "a" -> 20, "b" -> 10, "c" -> 30 };
  ```
  Assigns a map containing three key-value pairs to `myMap`.
- ```ctl
  myMap = null;
  ```
  Discards the previous value of `myMap`.

#### variant

Variant is a data type added in **CloverDX 5.6**. Variables of this type can be assigned values of any other type - no type checking is performed. In particular, variant can contain nested lists and maps, so it can be used for tree-like data with unknown structure, such as JSON.

Its declaration looks like this: `variant``identifier``;`
> [!IMPORTANT]
> Since **CloverDX 5.11** variant data type is supported in data records too.
>
> `$out.0.myVariantField = myVariantVariable;`

Variant can be used like lists and maps, allowing to access inner values using square brackets `[ ]`. The operation will fail unless the variable contains a list or a map at runtime.

The default value is `null`, so the variable must be initialized to an empty list or map before inserting inner values.

Functions with arguments of type variant can be passed any value. However, they may throw runtime exceptions if the value is not valid for the function. For example, ["append(variant list, variant element)"](container-functions-ctl2.md#append) can be passed any value as the first argument, but it will throw an exception unless the value really is a list.

The type supports only a few basic operations ([== and != comparison](language-reference-ctl2.md#relational-operators), [toString](conversion-functions-ctl2.md#tostring), etc.). In order to perform type-specific operations, the values must be explicitly type-cast to a more specific type. See [*typeof operator*](language-reference-ctl2.md#typeof-operator) and [cast](miscellaneous-functions-ctl2.md#cast) and [getType](miscellaneous-functions-ctl2.md#gettype) functions.
Example 33. Variant

```ctl
variant myVariant = {};
myVariant["one"] = 1;
myVariant["string"] = "not a number";
myVariant["two"] = 2;

// working with unknown structures:
integer sum = 0;
if ( myVariant typeof list ) {
    for  ( integer index = 0; index < length(myVariant); index++) { // iterate through the list
        variant element = myVariant[index]; // get list element by the index
        string type = getType(element); // get the type of the element
        printLog(info, "List element " + index + ": " + element + " " + type);
        if (element typeof integer) { // test the type of the element
            sum += cast(element, integer); // cast to integer and add to the sum
        }
    }
} else if ( myVariant typeof map ) {
    variant keys = getKeys(myVariant); // returns the keys as a list
    for ( integer i = 0; i < length(keys); i++) { // iterate through the list of keys
        variant key = keys[i]; // get the key by the index
        variant value = myVariant[key]; // get the value by the key
        string type = getType(value); // get the type of the value
        printLog(info, "Map entry " + key + " = " + value + " " + type);
        if (value typeof integer) { // test the type of the value
            sum += cast(value, integer); // cast to integer and add to the sum
        }
    }
}
printLog(info, "Sum: " + sum);
```

The assignments are similar to those valid for a list or a map:

- ```ctl
  variant varMap = {};
  ```
  Assigns an empty map to `varMap`.
- ```ctl
  varMap["abc"] = 7;
  ```
  If `varMap` contains a map, puts the value `7` into `varMap` under the key `"abc"`. Throws an exception otherwise.
- ```ctl
  variant varList = [];
  ```
  Assigns an empty list to `varList`.
- ```ctl
  varList[5] = "abc"
  ```
  If `varList` contains a list with at least 6 elements, sets the list element at index `5` to `"abc"`. Unlike with `list` data type, `variant` is not expanded automatically, so if `varList` contains fewer than 6 elements, the assignment fails. Use [append](container-functions-ctl2.md#append) to expand the list. If `varList` is actually a map, puts `"abc"` into the map under the key `5`. Otherwise, throws an exception.
- ```ctl
  var2 = var1;
  ```
  Assigns a copy of `var1` to `var2`.
- ```ctl
  varMap = {
      "name" -> "John Doe",
      "weight" -> 75.3,
      "valid" -> true
  };
  ```
  Assigns a JSON-like map containing three key-value pairs to `varMap`. Note that the values are of mixed types: `string`, `number` and `boolean`, respectively.
- ```ctl
  varMap = null;
  ```
  Discards the previous value of `varMap`.

#### record

Record is a container that can contain different primitive data types.

The structure of record is based on metadata. Any metadata item represents a data type.

Declaration of a record looks like this: `<metadata name> identifier;`

Metadata names must be unique in a graph. Different metadata must have different names.

For more detailed information about possible expressions and records usage, see [Accessing Data Records and Fields](language-reference-ctl2.md#accessing-data-records-and-fields).

Record does not have a default value.

It can be indexed by both integer numbers and strings (field names). If indexed by numbers, fields are indexed starting from 0.

### Literals

Literals serve to write values of any data type.

| Literal | Description | Declaration syntax | Example |
| --- | --- | --- | --- |
| integer | digits representing integer number | [0-9]+ | 95623 |
| long integer | digits representing an integer number with absolute value even greater than 231, but less than 263 | [0-9]+L? | 257L, or 9562307813123123L |
| hexadecimal integer | digits and letters representing an integer number in hexadecimal form | 0x[0-9A-F]+ | 0xA7B0 |
| octal integer | digits representing an integer number in octal form | 0[0-7]* | 0644 |
| number (double) | a floating point number represented by 64bits in double precision format | .[0-9] | 456.123 |
| decimal | digits representing a decimal number | [0-9]+.[0-9]+D | 123.456D |
| double quoted string | string value/literal enclosed in double quotes; escaped characters [\n,\r,\t, \\, \", \b] get translated into corresponding control chars | "…​anything except ["]…​" | "hello\tworld\n\r" |
| single quoted string | string value/literal enclosed in single quotes; only one escaped character [\'] gets translated into corresponding char ['] | '…​anything except [']…​' | 'hello\tworld\n\r' |
| multi-line string | string value/literal enclosed in triple quotes; escaped characters are not translated into corresponding chars | """…​anything …​""" | """ This is multi- line string """ |
| list | list of expressions where all elements are of the same data type | [ <element> (, <element>)* ]  [] for an empty list | [10, 16 + 1, 31] or ['hello', "world" ] |
| map | list of key-value mappings where all keys and all values are expressions of the same data type | { <key> → <value> (, <key> → <value>)* }  {} for an empty map | { "a" → 1, "bb" → 2 } |
| date | date value | this mask is expected: yyyy-MM-dd | 2008-01-01 |
| datetime | datetime value | this mask is expected: yyyy-MM-dd HH:mm:ss | 2008-01-01 18:55:00 |
> [!IMPORTANT]
> You cannot use any literal for the `byte` data type. If you want to write a `byte` value, you must use any of the conversion functions that return `byte` and apply it on an argument value.
>
> For information on these conversion functions, see [Conversion Functions](conversion-functions-ctl2.md).
> [!IMPORTANT]
> Remember that if you need to assign a decimal value to a decimal field, you should use decimal literal. Otherwise, such number would not be decimal, it would be a double number.
>
> For example:
>
> 1. **Decimal value to a decimal field (correct and accurate)**
>    `// correct - assign decimal value to decimal field`
>    `myRecord.decimalField = 123.56d;`
> 2. **Double value to a decimal field (possibly inaccurate)**
>    `// possibly inaccurate - assign double value to decimal field`
>    `myRecord.decimalField = 123.56;`
>
> The latter might produce inaccurate results.

### Variables

To define a variable, type the data type of the variable followed by a white space, the name of the variable and a semicolon.

Such a variable can be initialized later, but it can also be initialized in the declaration itself. Of course, the value of the expression must be of the same data type as the variable.

Both cases of variable declaration and initialization are shown below:

- ```ctl
  dataType variable;
  ...
  variable = expression;
  ```
- ```ctl
  dataType variable = expression;
  ```
Example 34. Variables

```ctl
int a;
a = 27;
int b = 32;
int c = a;
```

#### Constants

Adding `const` modifier to a variable declaration will protect it from being accidentally modified later in the code. CTL validator will report an error on any attempt to assign a value to a constant. Note that modifications via function calls, e.g. `clear()`, are not checked.
Example 35. Constants

```ctl
const integer INT_CONSTANT = 10;
const string MY_ID = "ABC";
const string[] LIST_CONSTANT = ["a", "b", "c"];

INT_CONSTANT = 11; // error
MY_ID = ""; // error
LIST_CONSTANT[0] = "x"; // error
clear(LIST_CONSTANT); // not checked
```

### Dictionary in CTL2

To use a dictionary in your graph, define the dictionary first, see [Dictionary](dictionary.md).

To access the entries from CTL2, use the dot syntax as follows:

`dictionary.<dictionary entry>`

This expression can be used to

- define the value of the entry:
  ```ctl
  dictionary.customer = "John Smith";
  ```
- get the value of the entry:
  ```ctl
  myCustomer = dictionary.customer;
  ```
- map the value of the entry to an output field:
  ```ctl
  $out.0.myCustomerField = dictionary.customer;
  ```
- serve as the argument of a function:
  ```ctl
  myCustomerID = isInteger(dictionary.customer);
  ```

### Operators

The operators serve to perform operations in the same way as functions do, but using operators, your code is more compact and legible.

Operators can be arithmetic, relational and logical. The arithmetic operators can be used in all expressions, not only the logical ones. The relational and logical operators serve to create expressions with resulting boolean value.

All operators can be grouped into four categories:

- [Arithmetic operators](language-reference-ctl2.md#arithmetic-operators) (`\+ - * / % ++ --`)
- [Relational operators](language-reference-ctl2.md#relational-operators) (`> >= == <= < != ~= ?=`)
- [Logical operators](language-reference-ctl2.md#logical-operators) (`&& || ! == !=`)
- [Assignment operator](language-reference-ctl2.md#assignment-operator) (`= += -= *= /= %=`)

#### Arithmetic operators

The arithmetic operators perform basic mathematical operation (addition, subtraction, etc.), concatenate strings or lists or merge content of two maps.

The operators can be used more times in one expression. The result depends on the order of operators within the expressions. In such a case, you can express priority of operations by parentheses.
> [!TIP]
> If you are unsure about priority of operators or associativity, the safest way is to use parentheses.

| [Addition](language-reference-ctl2.md#addition) |
| --- |
| [Subtraction and unitary minus](language-reference-ctl2.md#subtraction-and-unitary-minus) - |
| [Multiplication](language-reference-ctl2.md#multiplication) * |
| [Division](language-reference-ctl2.md#division) / |
| [Modulus](language-reference-ctl2.md#modulus) % |
| [Incrementing](language-reference-ctl2.md#incrementing) ++ |
| [Decrementing](language-reference-ctl2.md#decrementing) —  |

##### Addition

```ctl
+
```

```ctl
numeric type +( numeric type left, numeric type right );
string +( string left, string right );
list +( list left, list right );
map +( map left, map right );
```

The operator `+` serves to sum the values of two expressions, concatenate two string values, concatenate two lists or merge content of two maps.

Nevertheless, if you want to add any data type to a string, the second data type is converted to a string automatically and it is concatenated with the first (string) summand. But remember that the string **must** be on the first place.

Naturally, two strings can be summed in the same way.

Note also that the `concat()` function is faster than `+`. You should use this function instead of adding any summand to a string. See [concat](string-functions-ctl2.md#concat).

The addition of two boolean values or two date data types is not possible. To create a new value from two boolean values, you must use logical operators instead.

```ctl
integer in01 = 1;
integer in02 = 2;
integer in03 = in02 + in01; // 3

// string concatenation
string s1 = "Hello";
string s2 = " World!";
string s3 = s1 + s2; // Hello World!

decimal price = 1.50d;
string order = "turnip " + price; // turnip 1.50

variant mapVar = {1 -> {2 -> 3}, 4 -> {5 -> 6}};
printLog(info, "mapVar = " + mapVar); // prints "mapVar = {1={2=3}, 4={5=6}}"

// concatenation of two lists
integer [] il1 = [2];
integer [] il2 = [3,5];
integer [] il3 = il1 + il2; // [2,3,5]

// merge of two maps
map[string,string] m1;
map[string,string] m2;
map[string,string] m3;
m1["d"] = "Delta";
m1["f"] = "Foxtrot";
m2["e"] = "Echo";
m3 = m1 + m2;
```

> [!TIP]
> If you concatenate several strings, use the following approach instead of the plus sign:
>
>
> ```ctl
> string[] buffer;
>
> buffer.append("<html>\n");
> buffer.append("<head>\n");
> buffer.append("<title>String concatenation example</title>\n");
> buffer.append("</head>\n");
>
> // append multiple strings at once
> buffer.copy(["<body>", "\n", "Sample content", "\n", "</body>", "\n"]);
> buffer.append("</html>");
>
> // concatenates the list into a single string, null list elements are converted to the string "null"
> string result = join("", buffer);
> ```
>
>
> This example is analogous to using a [java.lang.StringBuilder](http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html).
>
> Avoid [Schlemiel the Painter’s algorithm](http://en.wikipedia.org/wiki/Joel_Spolsky#Schlemiel_the_Painter.27s_algorithm) for concatenation of a large number of strings.
>
> You can also use [concat](string-functions-ctl2.md#concat) or [concatWithSeparator](string-functions-ctl2.md#concatwithseparator) to concatenate strings. The difference is that [join](string-functions-ctl2.md#join) allows storing intermediate results in a list of strings, while [concat](string-functions-ctl2.md#concat) requires that all operands are passed as parameters simultaneously.

##### Subtraction and unitary minus

```ctl
-
```

```ctl
numeric type -( numeric type left, numeric type right );
```

The operator `-` subtracts one numeric data type from another.

If the numeric types of operands differ, firstly, automatic conversions are applied and then subtraction is performed.

```ctl
integer i1 = 5 - 3;
```

##### Multiplication

```ctl
*
```

```ctl
numeric type *( numeric type left, numeric type right );
```

The operator `*` multiplies two numbers.

Numbers can be of different data types. If data types of operands differ, automatic conversion is applied.

```ctl
integer i1 = 2 * 3;
decimal d1 = 1.5 * 3.5;
double  d2 = 2.5 * 2;
```

##### Division

```ctl
/
```

```ctl
numeric type /( numeric type left, numeric type right );
```

Operator `/` serves to divide two numeric data types. Remember that you must not divide by zero. Division by zero throws TransformLangExecutorRuntimeException or returns `Infinity` (in the case of `double` (`number`) data type).

```ctl
integer i1 = 7  / 2;      // i1 == 3
long    l2 = 9L / 4L;     // l2 == 2L
decimal d3 = 6.75D / 1.5D // d3 == 4.5D
double d4  = 6.25  / 2.5  // d4 == 2.5
```

##### Modulus

```ctl
%
```

```ctl
numeric type %( numeric type left, numeric type right );
```

Operator `%` returns the remainder of division. The operator can be used for floating-point, fixed-point and integral data types.

```ctl
integer in1 = 7 % 3;         // in1 == 1
long    lo1 = 8 % 5;         // lo1 == 3
decimal de1 = 15.75D % 3.5D  // de1 == 1.75D
double  do1 = 6.25 % 2.5     // do1 == 1.25
```

##### Incrementing

```ctl
++
```

Operator `++` serves to increment numeric data type value by one. The operator can be used for both floating-point data types and integer data types.

If it is used as a prefix, the number is incremented first and then it is used in the expression.

If it is used as a postfix, first, the number is used in the expression and then it is incremented.
> [!IMPORTANT]
> Remember that the incrementing operator cannot be applied on literals, record fields, map, or list values of integer data type.

```ctl
integer i1 = 20;
integer i2 = ++i1; // i1 = i1 + 1; i2 = i1;     i1 == 21 and i2 == 21
integer i3 = i++   // i3 = i1;     i1 = i1 + 1; i1 == 22 and i3 == 21
```

##### Decrementing

```ctl
--
```

Operator `--` serves to decrement numeric data type value by one.

The operator can be used for floating-point, fixed-point and integral data types.

If it is used as a prefix, the number is decremented first and then it is used in the expression.

If it is used as a postfix, first, the number is used in the expression and then it is decremented.
> [!IMPORTANT]
> Remember that the decrementing operator cannot be applied on literals, record fields, map, or list values of integer data type.

```ctl
integer i1 = 20;
integer i2 = --i1; // i1 = i1 - 1; i2 = i1;     i1 == 19 and i2 == 19
integer i3 = i1--; // i3 = i1;     i1 = i1 - 1; i1 == 18 and i3 == 19
```

#### Relational operators

The following operators serve to compare some subexpressions when you want to obtain a boolean value result. Each of the mentioned signs can be used. These signs can be used more times in one expression. In such a case you can express priority of comparisons by parentheses.
> [!IMPORTANT]
> If you choose the `.operator.` syntax, operator must be surrounded by white spaces. Example syntax for the `eq` operator:
>
> | Code | Working? |
> | --- | --- |
> | 5 .eq. 3 | **✓** |
> | 5 == 3 | **✓** |
> | 5 eq 3 | **⨯** |
> | 5.eq(3) | **⨯** |

- Greater than
  Each of the two signs below can be used to compare expressions consisting of numeric, date and string data types. Both data types in the expressions must be comparable. The result can depend on the order of the two expressions if they are of different data types.
  - ```ctl
    >
    ```
  - ```ctl
    .gt.
    ```
  ```ctl
  boolean a = 4 > 3;
  a = "dog" > "cat";
  if ( date1 > date2 ) {}
  ```
- Greater than or equal to
  Each of the three signs below can be used to compare expressions consisting of the numeric, date and string data types. Both data types in the expressions must be comparable. The result can depend on the order of the two expressions if they are of different data types.
  - ```ctl
    >=
    ```
  - ```ctl
    =>
    ```
  - ```ctl
    .ge.
    ```
  ```ctl
  boolean a = 3.5 >= 3.5;
  a = "ls" >= "lsof";
  a = date1 >= date2;
  ```
- Less than
  Each of the two signs below can be used to compare expressions consisting of numeric, date and string data types. Both data types in the expressions must be comparable. The result can depend on the order of the two expressions if they are of different data types.
  - ```ctl
    <
    ```
  - ```ctl
    .lt.
    ```
- Less than or equal to
  Each of the three signs below can be used to compare expressions consisting of the numeric, date and string data types. Both data types in the expressions must be comparable. The result can depend on the order of the two expressions if they are of different data types.
  - ```ctl
    <=
    ```
  - ```ctl
    =<
    ```
  - ```ctl
    .le.
    ```
  ```ctl
  int a = 7L < 8L;
  if ( "awk" < "java" ) {}
  a = date1 < date2;
  ```
- Equal to
  Each of the two signs below can be used to compare expressions of any data type. Both data types in the expressions must be comparable. The result can depend on the order of the two expressions if they are of different data types.
  - ```ctl
    ==
    ```
  - ```ctl
    .eq.
    ```
  ```ctl
  if( 5 == 5 ) {}
  ```
- Not equal to
  Each of the three signs below can be used to compare expressions of any data type. Both data types in the expressions must be comparable. The result can depend on the order of the two expressions if they are of different data types.
  - ```ctl
    !=
    ```
  - ```ctl
    <>
    ```
  - ```ctl
    .ne.
    ```
  ```ctl
  if ( 9 != 8 ) {}
  ```
- Matches regular expression
  The operator serves to compare string and some [*regular expression*](language-reference-ctl2.md#regular-expressions). It returns `true`, if the whole string matches the regular expression, otherwise returns `false`. If the right operand is `null`, operator fails.
  ```ctl
  boolean b = "cat" ~= "[a-z]{3}";
  ```
  - ```ctl
    ~=
    ```
  - ```ctl
    .regex.
    ```
  ```ctl
  boolean b1 = "new bookcase" ~= ".*book.*";  // true
  boolean b2 = "new bookcase" ~= "book";      // false
  boolean b3 = "new bookcase" ~= null;        // fails
  ```
- Contains regular expression
  The operator serves to compare string and some [*regular expression*](language-reference-ctl2.md#regular-expressions). It returns `true`, if the string contains a substring that matches the regular expression, otherwise returns `false`.
  - ```ctl
    ?=
    ```
  ```ctl
  boolean b = "miredo" ?= "redo";
  ```

##### "typeof" Operator

`boolean <value> typeof <type or metadata name>`

Tests if a value (left operand) is of the specified type (right operand).

Returns false if the value is `null`.

For lists and maps, does not check the type of elements.
Example 36. Usage of typeof

```ctl
variant myVariant = 5;
if (myVariant typeof integer) { } // TRUE
if (myVariant typeof number) { } // FALSE
if (myVariant typeof string) { } // FALSE

variant someObject = {"a" -> 1, true -> false};
if (someObject typeof map) { // TRUE
     // handle map
} else if (someObject typeof list) { // FALSE
     // handle list
}

variant nullVariant = null;
if (nullVariant typeof string) { } // null returns FALSE for all types

myMetadata myRecord;
variant recordVariant = myRecord;
if (recordVariant typeof record) { } // TRUE - generic record
if (recordVariant typeof myMetadata) { } // TRUE - specific metadata
if (recordVariant typeof otherMetadata) { } // FALSE - specific metadata
```

**See also:**[variant](language-reference-ctl2.md#variant), [cast](miscellaneous-functions-ctl2.md#cast), [getType](miscellaneous-functions-ctl2.md#gettype)

#### Logical operators

If the expression whose value must be of boolean data type is complex, it can consist of some subexpressions (see above) that are put together by logical conjunctions (AND, OR, NOT, .EQUAL TO, NOT EQUAL TO). If you want to express priority in such an expression, you can use parentheses. From the conjunctions mentioned below, you can choose either form (for example, `&&` or `and`, etc.).

Every sign of the form `.operator.` must be surrounded by a white space.

- Logical AND
  - ```ctl
    &&
    ```
  - ```ctl
    and
    ```
- Logical OR
  - ```ctl
    ||
    ```
  - ```ctl
    or
    ```
- Logical NOT
  - ```ctl
    !
    ```
  - ```ctl
    not
    ```
- Logical EQUAL TO
  - ```ctl
    ==
    ```
  - ```ctl
    .eq.
    ```
- Logical NOT EQUAL TO
  - ```ctl
    !=
    ```
  - ```ctl
    <>
    ```
  - ```ctl
    .ne.
    ```

#### Assignment operator

Assignment operator assigns a value of expression on the right side of the operator to a variable on the left side of the operator.

```ctl
int i = 5;
```

##### Compound operators

Compound operators allow you to use a variable as an accumulator.

Since **CloverETL 4.1.0-M1**, CTL2 supports the following compound assignment operators: `+=` (addition, string concatenation, list concatenation and map union), `-=` (subtraction), `*=` (multiplication), `/=` (division), and `%=` (modulus).

If the original value of the left-hand side variable is `null`, the default value for the target type (0, empty string, empty list, empty map) is used for the evaluation instead. See variables `ns` and `ns2` in the example below.
Example 37. Compound assignment operators

```ctl
integer i = 5;
  i += 4; // i == 9

  integer ni = null;
  ni += 5; // ni == 5

  string s = "hello ";
  s += "world "; // s == "hello world "
  s += 123; // s == "hello world 123"

  string ns = null;
  ns += "hello"; // ns == "hello"

  string ns2 = null;
  ns2 = ns2 + "hello"; // ns2 == "nullhello"

  integer[] list1 = [1, 2, 3];
  integer[] list2 = [4, 5];
  list1 += list2; // list1 == [1, 2, 3, 4, 5]

  map[string, integer] map1;
  map1["1"] = 1;
  map1["2"] = 2;
  map[string, integer] map2;
  map2["2"] = 22;
  map2["3"] = 3;
  map1 += map2; // map1: "1"->1, "2"->22, "3"->3

  long l = 10L;
  l -= 4; // l == 6L;

  decimal d = 12.34D;
  d *= 2; // d == 24.68D;

  number n = 6.15;
  n /= 1.5; // n ~ 4.1

  long r = 27;
  r %= 10; // r == 7L
```

> [!NOTE]
> CTL2 does not perform any counter-intuitive conversion of the right operand of `+=`. If you need to add double to integer, you should convert it explicitly:
>
>
> ```ctl
> integer i = 3;
> i += double2integer(1.0);
> ```
>
>
> It works with `-=`, `*=`, `/=` and `%=` as well.

As of **CloverETL 3.3**, the = operator does not just pass object references, but performs a **deep copy** of values. That is of course more demanding in terms of performance. Deep copy is only performed for mutable data types, i.e. lists, maps, records and dates. Other types are considered immutable, as CTL2 does not provide any means of changing the state of an existing object (even though the object is mutable in Java). Therefore it is safe to pass a reference instead of copying the value. Note that this assumption may not be valid for custom CTL2 function libraries.
Example 38. Modification of a copied list, map and record

```ctl
integer[] list1 = [1, 2, 3];
  integer[] list2;
  list2 = list1;

  list1.clear(); //  only list1 is cleared (older implementation: list2 was cleared, too)

  map[string, integer] map1;
  map1["1"] = 1;
  map1["2"] = 2;
  map[string, integer] map2;
  map2 = map1;

  map1.clear(); //  only map1 is cleared (older implementation: map2 was cleared, too)

  myMetadata record1;
  record1.field1 = "original value";
  myMetadata record2;
  record2 = record1;

  record1.field1 = "updated value"; // only record1 will be updated (older implementation: record2 was updated, too)
```

#### Ternary operator

**Ternary operator** is a compact conditional assignment.

It serves to set a value of a variable depending on a boolean expression or a boolean variable.

```ctl
a = b ? c : d;
```

The expression above is same as:

```ctl
if ( b ) {
    a = c;
} else {
    a = d;
}
```

The `a`, `c` and `d` variables must be of the same data type (or type of `c` and `d` must be convertible to type of `a` using automatic conversion). The `b` variable is `boolean`.

`b`, `c` or `d` do not have to be variables. They may be constants or expressions. `a` has to be a variable.

For example, you can use a ternary operator to assign minimum of `c` and `d` into `a` in a compact way:

```ctl
a = c < d ? c : d;
```

#### Conditional fail expression

The conditional fail expression allows the user to conditionally execute a piece of code depending on a failure occurred in the previous part of the code. `variable = expr1 : expr2 : … : exprN;`

`integer count = getCachedValue() : refreshCacheAndGetCachedValue() : defaultValue;`

Conditional expression is available only in an interpreted mode. It is not available in a compiled mode.

[raiseError](miscellaneous-functions-ctl2.md#raiseerror).

#### Simple statement and block of statements

All statements can be divided into two groups:

- **Simple statement** is an expression terminated by a semicolon.
  For example:
  ```ctl
  integer MyVariable;
  ```
- **Block of statements** is a series of simple statements (each of them is terminated by a semicolon). The statements in a block can follow each other in one line or they can be written in more lines. They are surrounded by curled braces. No semicolon is used after the closing curled brace.
  For example:
  ```ctl
  while (MyInteger<100) {
    Sum = Sum + MyInteger;
    MyInteger++;
  }
  ```

### Control statements

Some statements serve to control the processing flow.

All control statements can be grouped into the following categories:

- [Conditional statements](language-reference-ctl2.md#conditional-statements)
- [Iteration statements](language-reference-ctl2.md#iteration-statements)
- [Jump statements](language-reference-ctl2.md#jump-statements)
- [Try-catch statement](language-reference-ctl2.md#try-catch-statement)

#### Conditional statements

These statements serve to perform different set of statements depending on condition value.

##### If statement

On the basis of the `Condition` value, this statement decides whether the `Statement` should be executed. If the `Condition` is true, the `Statement` is executed. If it is false, the `Statement` is ignored and the process continues next after the `if` statement. The `Statement` is either a simple statement or a block of statements:

- ```ctl
  if (Condition) Statement
  ```

Unlike the previous version of the `if` statement (in which the `Statement`is executed only if the `Condition` is true), other `Statements` that should be executed even if the `Condition` value is false can be added to the `if` statement. Thus, if the `Condition` is true, the `Statement1` is executed, if it is false, the `Statement2` is executed. See below:

- ```ctl
  if (Condition) Statement1 else Statement2
  ```

The `Statement2` can even be another `if` statement, and also with an `else` branch:

- ```ctl
  if (Condition1) Statement1
      else if (Condition2) Statement3
          else Statement4
  ```
Example 39. If statement

```ctl
integer a = 123;
if ( a < 0 ) {
    a = -a;
    }
```

##### Switch statement

Sometimes you would have very complicated statement if you created the statement of more branched out `if` statement. In this case, it is much more convenient to use the `switch` statement.

Now, instead of the `Condition` as in the `if` statement with only two values (true or false), an `Expression` is evaluated and its value is compared with the `Constants` specified in the `switch` statement.

Only the `Constant` that equals to the value of the `Expression` decides which of the `Statements` is executed.

If the `Expression` value is `Constant1`, the `Statement1` will be executed, etc.
> [!IMPORTANT]
> Remember that literals must be unique in the `Switch statement`.

- ```ctl
  switch(Expression) {
      case Constant1 : Statement1 StatementA [break;]
      case Constant2 : Statement2 StatementB [break;]
      ...
      case ConstantN : StatementN StatementW [break;]
  }
  ```

The optional `break;` statements ensure that only the statements corresponding to a constant will be executed. Otherwise, all below them would be executed as well.

In the following case, even if the value of the `Expression` does not equal the values of the `Constant1,…,ConstantN`, the default statement (`StatementN+1`) is executed.

- ```ctl
  switch (Expression) {
      case Constant1 : Statement1 StatementA [break;]
      case Constant2 : Statement2 StatementB [break;]
      ...
      case ConstantN : StatementN StatementW [break;]
      default : StatementN+1 StatementZ
  }
  ```
Example 40. Switch statement

```ctl
integer ok = 0;
switch ( response ) {
    case "yes":
    case "ok":
        a = 1;
        break;
    case "no":
        a = 0;
        break;
    default:
        a = -1;
}
```

#### Iteration statements

Iteration statements repeat some processes during which some inner `Statements` are executed repeatedly until the `Condition` that limits the execution cycle becomes false or they are executed for all values of the same data type.

##### For loop

Firstly, the Initialization is set up. Secondly, the `Condition` is evaluated and if its value is true, the `Statement` is executed. Finally, the `Iteration` is made.

During the next cycle of the loop, the `Condition` is evaluated again and if it is true, `Statement` is executed and `Iteration` is made. This way the process repeats until the `Condition` becomes false. Then the loop is terminated and the process continues with the other part of the program.

If the `Condition` is false at the beginning, the process jumps over the `Statement` out of the loop.

- ```ctl
  for (Initialization;Condition;Iteration)
      Statement
  ```
> [!IMPORTANT]
> Remember that the `Initialization` part of the `For Loop` may also contain the declaration of the variable that is used in the loop.
>
> `Initialization`, `Condition` and `Iteration` are optional.
Example 41. For loop

```ctl
integer result = 1;
integer limit = 5;
for(integer i = 1; i <= limit; ++i) {
    result = result * i;
}
```

##### Do-while loop

Firstly, the `Statement` is executed. Secondly, the value of the `Condition` is evaluated. If its value is true, the `Statement` is executed again and then the `Condition` is evaluated again and the loop either continues (if it is true again) or stops and jumps to the next or higher level subprocesses (if it is false).

Since the `Condition` is at the end of the loop, even if it is false at the beginning of the subprocess, the `Statement` is executed at least once.

- ```ctl
  do Statement while (Condition)
  ```

```ctl
integer a = 5;
integer sum = 0;
do {
    sum = sum + a;
    a--;
} while (a > 3);
```

##### While loop

The processing depends on the value of the `Condition`. If its value is true, the `Statements` is executed and then the `Condition` is evaluated again and the processing either continues (if it is true again) or stops and jumps to the statement following the cycle (if it is false).

Since the `Condition` is at the beginning of the loop, if it is false before entrance to the loop, the `Statements` is not executed at all and the loop is jumped over.

- ```ctl
  while (Condition) Statement
  ```

```ctl
integer a = 5;
integer sum = 0;
while ( a > 3 ) {
    sum = sum + a;
    a--;
```

##### For-each loop

The `foreach` statement is executed on all fields of the same data type within a container. Its syntax is as follows:

- ```ctl
  foreach (<data type> myVariable : iterableVariable) Statement
  ```

All elements of the same data type (data type is declared in this statement) are searched in the `iterableVariable` container. The `iterableVariable` can be a list, map, record or variant. For each variable of the same data type, specified `Statement` is executed. It can be either a simple statement or a block of statements.

Thus, for example, the same `Statement` can be executed for all `string` fields of a record, etc.
> [!NOTE]
> It is possible to iterate over *values* of a map (i.e. not whole `<entries>`). The type of the loop variable has to match the type of map’s values:
>
>
> ```ctl
> map[string, integer] myMap = {'first' -> 1, 'second' -> 2};
> foreach(integer value: myMap) {
>     printErr(value); // prints 1 and 2
> }
> ```
>
>
> To obtain map’s keys as a `list[]`, use the [getKeys()](container-functions-ctl2.md#getkeys) function.
>
> When iterating over a variant (if it contains a list, map or a record), use variant as the loop control variable type: `foreach (variant v: …)`
>
>
> ```ctl
> variant myVariant = [1, 'hello', true, today()];
> foreach(variant value: myVariant ) {
>     printErr(value); // 1, 'hello', true and actual date
> }
> ```

#### Jump statements

Sometimes you need to control the process in a different way than by decision based on the `Condition` value. To do that, you have the following options:

##### Break statement

If you want to jump out of a loop or of a switch, you can use the following statement in the program:

- ```ctl
  break;
  ```

The processing of a loop (or switch) is relinquished and it continues with `Statements` following the loop or switch.

##### Continue statement

If you want to stop processing of some iteration and go to next one, you can use the following statement in the program:

- ```ctl
  continue;
  ```

The processing jumps to the end of a loop, iteration is performed (in for loop) and the processing continues with next iteration step.

##### Return statement

In the functions, you can use the `return` word either alone or along with an `expression`. (See the following two options below.)

The `return` statement can be in any place within the function. There may also be multiple `return` statements among which a specific one is executed depending on a condition, etc.

- ```ctl
  return;
  ```
- ```ctl
  return expression;
  ```

### Error handling

Sometimes the code throws a runtime exception (e.g. unexpected null value, invalid number format, …​). Such exceptions can be handled using one of the following approaches:

- [Try-Catch Statement](language-reference-ctl2.md#try-catch-statement)
  - recommended, available since CloverDX 5.6
- [OnError() Functions](language-reference-ctl2.md#onerror-functions)

#### Try-catch statement

Since CloverDX 5.6, you may use the `try-catch` statement to handle runtime errors.

For every `try` statement, there can be only one `catch` block as there is only one type of exception: `CTLException`. Additionally, there is no `finally` block. In CTL, there are two parts to `try-catch` statement:

- `try` block allows you to define a code to be tested for errors
- `catch` block’s purpose is to handle errors that might occur within the `try` block

Depending on whether the try block encounters an error or not, the execution of the statement may lead to two alternatives:

- If the `try` block executes without errors, the following `catch` block is skipped, and the whole `try-catch` statement completes successfully.
- If the code inside the `try` block is erroneous, the execution jumps to the beginning of the respective `catch` block and executes the code within it.

The implementation of how to handle the error is up to you. For example, you can throw a custom error using the `raiseError()` function, log the exception and have the execution finish successfully, or execute a custom code as a workaround for the exception. You can access some details about the exceptions via the `CTLException` data structure.

`try-catch` statements can be nested.
Example 42. Try-catch statement

```ctl
integer a = 123;
integer b = 0;
integer c;

try {
    c = a / b; // throws ArithmeticException
    printLog(info, c); // skipped
} catch (CTLException ex) {
    c = -1; // workaround: set the variable to -1 to indicate error
    printLog(warn, ex); // log a warning
}
```

`CTLException` is actually a data record with the following fields:
`sourceRow: integer`
the row of the CTL source code where the exception occurred
`sourceColumn: integer`
the column of the CTL source code where the exception occurred
`message: string`
the error message of the innermost exception - the original cause of the failure
`cause: string`
the type of the innermost exception, e.g. `java.lang.ArithmeticException`
`stackTrace: list[string]`
the cascade of function calls that caused the failure
`exceptionTrace: list[string]`
the list of exception types from the outermost to the innermost

#### OnError() functions

Alternatively to the [Try-catch statement](language-reference-ctl2.md#try-catch-statement) introduced in CloverDX 5.6, you can use a set of optional `OnError()` functions that exist to each required transformation function.

For example, for required functions (e.g. `append()`, `transform()`, etc.), there exist following optional functions:

`appendOnError()`, `transformOnError()`, etc.

Each of these required functions may have its (optional) counterpart whose name differs from the original (required) by adding the `OnError` suffix.

Moreover, every `<required ctl template function>OnError()` function returns the same values as the original required function.

This way, any exception that is thrown by the original required function causes call of its `<required ctl template function>OnError()` counterpart (e.g. `transform()` fail may call `transformOnError()`, etc.).

In this `transformOnError()`, any incorrect code can be fixed, an error message can be printed to the Console, etc.
> [!IMPORTANT]
> Remember that these `OnError()` functions are not called when the original required functions return **Error codes** (values less then -1).
>
> If you want some `OnError()` function to be called, you need to use the `raiseError(string arg)` function. Or (as stated before) any exception thrown by original required function calls its `OnError()` counterpart as well.

### Functions

You can define your own functions in the following way:

```ctl
function returnType functionName (type1 arg1, type2 arg2,..., typeN argN) {
        variableDeclarations
        otherFunctionDeclarations
        Statements
        Mappings
        return [expression];
    }
```

You must put the return statement at the end. For more information about the return statement, see [Return Statement](language-reference-ctl2.md#return-statement). Inside some functions, there can be `Mappings`. These may be in any place inside the function.

In addition to any other data type mentioned above, the function can also return `void`.

```ctl
function integer add (integer i1, integer i2) {
    return i1 + i2;
}
```

#### Message function

Since **CloverETL 2.8.0**, you can also define a function for your own error messages.

```ctl
function string getMessage() {
    return message;
}
```

This `message` variable should be declared as a global string variable and defined anywhere in the code so as to be used in the place where the `getMessage()` function is located. The `message` will be written to the console.

### Conditional fail expression

You can also use conditional fail expressions.

They look like this:

```ctl
expression1 : expression2 : expression3 : ... : expressionN;
```

This conditional fail expression may be used for mapping, assignment to a variable and as an argument of a function too.

The expressions are evaluated one by one, starting from the first expression and going from left to right.

1. As soon as one of these expressions is successfully evaluated, it is used and the other expressions are not evaluated.
2. If none of these expressions may be used (assigned to a variable, mapped to the output field, or used as an argument), the graph fails.
> [!TIP]
> This expression may be used in multiple ways: for assigning to a variable, mapping to an output field, or argument of a function.

### Accessing data records and fields

This section describes the way how the record fields should be worked with. As you know, each component can have ports. Both input and output ports are numbered starting from 0.

Metadata of connected edges must be identified by their names. Different metadata must have different names.

#### Working with records and variables
> [!IMPORTANT]
> Since **CloverETL 3.2**, the syntax has changed to:
>
> `$in.portID.fieldID` and `$out.portID.fieldID`
>
> e.g., `$in.0.* = $out.0.*;`
>
> That way, you can clearly distinguish input and output metadata.
>
> Transformations you have written before will be compatible with the old syntax.

Now we suppose that `Customers` is the ID of metadata, their name is `customers`, and their third field (field 2) is `firstname`.

Following expressions represent the value of the third field (field 2) of the specified metadata:

- `$in.<port number>.<field number>`
  Example: `$in.0.2`
  `$in.0.*` means all fields on the first port (port 0).
- `$in.<port number>.<field name>`
  Example: `$in.0.firstname`
- `$<metadata name>.<field number>`
  Example: `$customers.2`
  `$customers.*` means all fields on the first port (port 0).
- `$<metadata name>.<field name>`
  Example: `$customers.firstname`

You can also define records in CTL code. Such definitions can look like these:

- `<metadata name> MyCTLRecord;`
  Example: `customers myCustomers;`
- After that, you can use the following expressions:
  `<record variable name>.<field name>`
  Example: `myCustomers.firstname;`

Mapping of records to variables looks like this:

- `myVariable = $in.<port number>.<field number>;`
  Example: `FirstName = $in.0.2;`
- `myVariable = $in.<port number>.<field name>;`
  Example: `FirstName = $in.0.firstname;`
- `myVariable = $<metadata name>.<field number>;`
  Example: `FirstName = $customers.2;`
- `myVariable = $<metadata name>.<field name>;`
  Example: `FirstName = $customers.firstname;`
- `myVariable = <record variable name>.<field name>;`
  Example: `FirstName = myCustomers.firstname;`
  Mapping of variables to records can look like this:
- `$out.<port number>.<field number> = myVariable;`
  Example: `$out.0.2 = FirstName;`
- `$out.<port number>.<field name> = myVariable;`
  Example: `$out.0.firstname = FirstName;`
- `$<metadata name>.<field number> = myVariable;`
  Example: `$customers.2 = FirstName;`
- `$<metadata name>.<field name> = myVariable;`
  Example: `$customers.firstname = FirstName;`
- `<record variable name>.<field name> = myVariable;`
  Example: `myCustomers.firstname = FirstName;`
> [!IMPORTANT]
> Remember that if the component has a single input port or single output port, you can use the syntax as follows:
>
> `$firstname`
>
> Generally, the syntax is:
>
> `$<field name>`
> [!IMPORTANT]
> You can assign input to an internal CTL record using the following syntax:
>
> `MyCTLRecord.* = $in.0.*;`
>
> Also, you can map values of an internal record to the output using the following syntax:
>
> `$out.0.* = MyCTLRecord.*;`

### Mapping

Mapping is a part of each transformation defined in some of the **CloverDX** components.

Calculated or generated values or values of input fields are assigned (mapped) to output fields.

1. Mapping assigns a value to an output field.
2. Mapping operator is the following:
   `=`
3. Mapping must always be defined inside a function.
4. Mapping may be defined in any place inside a function.
   > [!IMPORTANT]
   > In CTL2, mapping may be in any place of the transformation code and may be followed by any code. This is one of the differences between the two versions of **CloverDX** Transformation Language.
   >
   > (In CTL1, mapping had to be at the end of the function and could only be followed by one `return` statement.)
   >
   > In CTL2, mapping operator is simply the equal sign.
5. Remember that you can also wrap a mapping in a user-defined function which would be subsequently used inside another function.
6. You can also map different input metadata to different output metadata by field names or by field positions. See examples below.

#### Mapping of different metadata (by name)

When you map input to output like this:

`$out.0.* = $in.0.*;`

input metadata may even differ from those on the output.

In the expression above, fields of the input are mapped to the fields of the output that have the same name and type as those of the input. The order in which they are contained in respective metadata and the number of all fields in either metadata is not important.

When you have input metadata in which the first two fields are `firstname` and `lastname`, each of these two fields is mapped to its counterpart on the output. Such output `firstname` field may even be the fifth and `lastname` field be the third, but those two fields of the input will be mapped to these two output fields.

Even if both input metadata and output metadata had more fields, such fields would not be mapped to each other if an output field did not exist with the same name as one of the input (independently on the mutual position of the fields in corresponding metadata).

In addition to the simple mapping as shown above (`$out.0.* = $in.0.*;`), you can also use the following function:

```ctl
void copyByName( record to, record from );
```

Example 43. Mapping of metadata by name (using the copyByName() function)

```ctl
recordName2 myOutputRecord;
copyByName(myOutputRecord.*,$in.0.*);
$in.0.* = myOutputRecord.*;
```

> [!IMPORTANT]
> Metadata fields are mapped from input to output by name and data type independently on their order and on the number of all fields.
>
> Following syntax may also be used: `myOutputRecord.copyByName($in.0.*);`

#### Mapping of different metadata (by position)

Sometimes you need to map input to output, but names of input fields are different from those of output fields. In such a case, you can map input to output by position.

To achieve this, you *must* use the following function:

```ctl
void copyByPosition( record to, record from );
```

Example 44. Mapping of metadata by position

```ctl
recordName2 myOutputRecord;
copyByPosition(myOutputRecord,$in.0.*);
$out.0.* = myOutputRecord.*;
```

> [!IMPORTANT]
> Metadata fields may be mapped from input to output by position (as shown in the example above).
>
> Following syntax may also be used: `myOutputRecord.copyByPosition($in.0.*);`

#### Use Case 1 - one string field to upper case

To show in more details how mapping works, we provide here a few examples of mappings.

We have a graph with the **Map** component. Metadata on its input and output are identical. First two fields (`field1` and `field2`) are of string data type, the third (`field3`) is of integer data type.

1. We want to change the letters of `field1` values to upper case while passing the other two fields unchanged to the output.
2. We also want to distribute records according to the value of `field3`. Those records in which the value of `field3` is less than 5 should be sent to the output port 0, the others to the output port 1.

#### Examples of mapping

As the first possibility, we have the mapping for both ports and all fields defined inside the `transform()` function of CTL template.
Example 45. Example of mapping with individual fields
Note that the mappings will be performed for all records. In other words, even when the record goes to the output port 1, the mapping for output port 0 will be performed, and vice versa.

Moreover, mapping consists of individual fields, which may be complex in case there are many fields in a record. In the next examples, we will see how this can be solved in a better way.

```ctl
function integer transform() {

    // mapping input port records to output port records
    // each field is mapped separately
    $out.0.field1 = upperCase($in.0.field1);
    $out.0.field2 = $in.0.field2;
    $out.0.field3 = $in.0.field3;
    $out.1.field1 = upperCase($in.0.field1);
    $out.1.field2 = $in.0.field2;
    $out.1.field3 = $in.0.field3;

    // output port number returned
    if ($out.0.field3 < 5) return 0; else return 1;
```

> [!NOTE]
> As CTL2 allows to use any code *after* the mapping, here we have used the `if` statement with two `return` statements after the mapping.
>
> In CTL2, mapping may be in any place of the transformation code and may be followed by any code.

As the second possibility, we also have the mapping for both ports and all fields defined inside the `transform()` function of CTL template. But now there are wild cards used in the mapping. These pass the records unchanged to the outputs and, after this wildcard mapping, the fields that should be changed are specified.
Example 46. Example of mapping with wild cards
Note that mappings will be performed for all records. In other words, even when the record goes to the output port 1, the mapping for output port 0 will be performed, and vice versa.

However, now the mapping uses wild cards at first, which passes the records unchanged to the output, but the first field is changed *below* the mapping with wild cards.

This is useful when there are many unchanged fields and a few that will be changed.

```ctl
function integer transform() {

    // mapping input port records to output port records
    // wild cards for mapping unchanged records
     // transformed records mapped additionally
     $out.0.* = $in.0.*;
     $out.0.field1 = upperCase($in.0.field1);
     $out.1.* = $in.0.*;
     $out.1.field1 = upperCase($in.0.field1);

     // return the number of output port
     if ($out.0.field3 < 5) return 0; else return 1;
```

> [!NOTE]
> As CTL2 allows to use any code *after* the mapping, here we have used the `if` statement with two `return` statements after the mapping.
>
> In CTL2, mapping may be in any place of the transformation code and may be followed by any code.

As the third possibility, we have the mapping for both ports and all fields defined outside the `transform()` function of CTL template. Each output port has its own mapping.

Wild cards are used here as well.

The mapping that is defined in a separate function for each output port allows the following improvements:

- Mapping is performed only for a respective output port. In other words, now there is no need to map the record to the port 1 when it will go to the port 0, and vice versa.
Example 47. Example of mapping with wild cards in separate user-defined functions
Moreover, mapping uses wild cards at first, which pass the records unchanged to the output. The first field is changed below the mapping with wild card. This is useful when there are many unchanged fields and a few that will be changed.

```ctl
// mapping input port records to output port records
    // inside separate functions
    // wild cards for mapping unchanged records
    // transformed records mapped additionally
    function void mapToPort0 () {
        $out.0.* = $in.0.*;
        $out.0.field1 = upperCase($in.0.field1);
    }

    function void mapToPort1 () {
        $out.1.* = $in.0.*;
        $out.1.field1 = upperCase($in.0.field1);
    }

    // use mapping functions for all ports in the if statement
    function integer transform() {
        if ($in.0.field3 < 5) {
            mapToPort0();
            return 0;
        }
        else {
            mapToPort1();
            return 1;
        }
```

### Parameters

Parameters are described in [Parameters](parameters.md).

The parameters can be used in **CloverDX** transformation language in the following way: `${nameOfTheParameter}`.

If you want such a parameter to be considered as a string data type, you must surround it by single or double quotes: `'${nameOfTheParameter}'` or `"${nameOfTheParameter}"`.
> [!IMPORTANT]
> 1. Remember that escape sequences are always resolved as soon as they are assigned to parameters. For this reason, if you want them not to be resolved, type double backslashes in these strings instead of single ones.
> 2. Also remember that you can get the values of environment variables using parameters. To learn how to do it, see [Environment variables](parameters.md#environment-variables).

### Regular expressions

*Regular expressions*, often abbreviated as *regex*, are a powerful tool used to search and manipulate text (string) data. They provide a concise way to define patterns within strings, allowing for efficient matching and extraction of specific information. While the underlying syntax might appear complex, understanding the core concepts empowers even non-technical users to leverage this valuable technique.

#### Regex basics

Due to the complexity and variability of regular expressions, it is not possible to cover every single nuance within our documentation. For this reason, this documentation will focus on the most fundamental regex tokens and their core functionalities. This ensures a solid foundation for understanding basic pattern matching and provides a springboard for further exploration of regex’s capabilities.

If you encounter specific use cases beyond the covered tokens, we recommend referring to advanced online regex resources, e.g. [https://regex101.com/](https://regex101.com/). Since our regex implementation is Java-based, make sure to use the Java-based regex flavor to ensure desired results.
> [!NOTE]
> Regex searches are case-sensitive by default. Also, your search might match parts of other words. Bear this in mind and write your search exactly how you want it to match, covering all the needed scenarios. If you don’t care about uppercase or lowercase, you can use the (?i) flag to make the search case insensitive.

| Regex token | Purpose | Description | Example | Explanation |
| --- | --- | --- | --- | --- |
|  | Find exact match | Matches the exact form of the word. | `product` | It will match `product`, `products`, or `productive` but not `Product` or `PRODUCT`. |
| `?` | 0 or 1 | A question mark (`?`) specifies that the preceding element can appear 0 or 1 time. | `colou?r` | It will match both `color` and `colour`. It will not match `coloor` or `colouur`. |
| `*` | 0 or more | An asterisk (`*`) specifies that the preceding element can appear 0 or more times. | `colou*r` | It will match `color`, `colour`, or `colouur`. |
| `+` | 1 or more | A plus sign (`+`) specifies that the preceding element can appear 1 or more times. | `colou+r` | It will match `colour` or `colouur`. |
| `.` | Wildcard dot | A dot (`.`) matches any single character. | `b.t` | It will match `bit`, `bat`, `but`, but also `b-t`, `b t`, or `b*t`. |
| `\|` | Alternative | The pipe (`\|`) functions as the OR operator. | `USA\|UK` | It will match `USA` or `UK`. |
| `()` | Grouping | Parentheses `()` act like brackets in math. They group a set of characters or elements into a single unit. | `col(our\|or)` | `col(our\|or)` will match `colour` or `color`.  Without parentheses, `colour\|or` will match `colour` or `or`. |
| `[]` | Character classes | Square brackets `[]` enclose a group of characters, indicating a match with any character within the set.  Can also be used to exclude a group of characters when preceded by a caret `(^)`. | - `[0-9]` - `[a-z]` - `[A-Z]` - `[a-zA-Z]` - `[aeiou]` - `[^aeiou]` | - `[0-9]` will match any digit. - `[a-z]` and `[A-Z]` will match any lower-case or upper-case letter, respectively. - `[a-zA-Z]` will match any lower-case or upper-case letter. - `[aeiou]` will match any instance of `a, e, i, o, u`. - `[^aeiou]` will match any character except for `a, e, i, o, u`. |
| `{}` | Repeating characters | Curly braces `{}` specify the number of repetitions of the preceding element. Combine it with parentheses to apply to a string of characters.  - `{number}` - exact number of repetitions - `{number,}` - minimum number of repetitions - `{number,number}` - range of repetitions | - `who{1}p` - `who{1,}p` - `who{1,2}p` - `(mur){1,2}` | - `who{1}p` will match `whop` only. - `who{1,}p` will match `whop`, `whoop`, or `whooop`. - `who{1,2}p` will match `whop` or `whoop`, but not `whooop`. - `(mur){1,2}` will match both `mur` and `murmur`. |
| `\s` and `\S` | Whitespace-related tokens | - `\s` - any whitespace character - `\S` - any non-whitespace character | `" Hello "` | - `\s` will match 2 whitespace characters (two spaces). - `\S` will match 5 characters (letters in the word `Hello`). |
| `\d` and `\D` | Digit-related tokens | - `\d` - matches any digit - `\D` - matches any non-digit character, including whitespace characters | `123 Main Street, Anytown, CA 94108` | - `\d` will match 8 characters: `123` and `94108`. - `\D` will match 26 characters, including all whitespace characters and commas: `Main Street, Anytown, CA`. |
| `\w` and `\W` | Word-related tokens | - `\w` - matches any word character (equivalent to `[a-zA-Z0-9_]`). - `\W` - matches any non-word character (equivalent to `[^a-zA-Z0-9_]`). | `123 Main Street, Anytown, CA 94108` | - `\w` will match 27 characters: `123MainStreetAnytownCA94108`. - `\W` will match 7 characters (all whitespace characters and commas). |
| `^` and `$` | Start and end of strings | Caret (`^`) or dollar signs (`$`) can be used to limit your search to the start or end of a string. | - `^SH7890` - `SH7890$` - `^SH7890$` | - `^SH7890` will match product codes begging with `SH7890`, e.g., `SH7890456` or `SH7890BA1`. - `SH7890$` will match product codes ending in `SH7890`, e.g., `415YSH7890` or `464SH7890`. - `^SH7890$` will match `SH7890` only. |

##### Regular expressions use examples
Example 48. Matching dates
Create a basic formula that would find dates in the format `DD/MM/YYYY` (format matching `2 digits/2 digits/4 digits`).
Click to reveal the formula and explanation
The regex formula would be: `\d{2}/\d{2}/\d{4}`.

**Explanation:**

- `\d{2}`: This matches exactly two digits (`\d` represents any single digit, and `{2}` specifies it must occur twice consecutively).
- `/`: This matches a literal forward slash character ("/").
- `\d{2}`: Similar to the first part, this matches exactly two digits again.
- `/`: Another literal forward slash match.
- `\d{4}`: This matches exactly four digits. This captures the year (e.g., `2024`).
Example 50. Validating US postal codes
Postal codes need to be in the format `#####` (basic 5-digit zip code) or `#####-####` (ZIP+4 code).
Click to reveal the formula and explanation
The regex formula would be: `^\d{5}(-\d{4})?$`.

**Explanation:**

- `^`: Matches the beginning of the string.
- `\d{5}`: Matches exactly five digits.
- `(-`: Matches a literal hyphen character (-) but only if it appears after the first five digits.
- `\d{4})?`: Matches an optional group containing four digits (0-9). The question mark `?` makes the entire group optional, allowing the hyphen and four digits to be absent.
- `$`: Matches the end of the string.
Example 52. Validating shipping address format
Create a basic validation that would match the following format: `123 Main Street, Anytown, USA 12345`, i.e., it:

- Starts with a house number (one or more digits).
- Includes a street name containing letters and spaces.
- Has a city name containing letters (and optionally also spaces).
- Specifies the country as "USA" (case-sensitive).
- Ends with a five-digit zip code.
Click to reveal the formula and explanation
The regex formula would be: `^(\d+)\s+([A-Za-z\s]+),\s+([A-Za-z\s]+),\s+USA\s+(\d{5})$`

**Explanation:**

- `^`: Matches the beginning of the string.
- `(\d+)`: Captures one or more digits for the house number.
- `\s+`: Matches one or more whitespace characters (space, tab, etc.).
- `([A-Za-z\s]+)`: Captures the street name, allowing for one or more words separated by spaces.
- `,`: Matches a comma.
- `\s+`: Matches one or more whitespace characters again.
- `([A-Za-z\s]+)`: Captures the city name, allowing for one or more words separated by spaces.
- `,`: Matches another comma.
- `\s+`: Matches one or more whitespace characters again.
- `USA`: Matches the literal string "USA" (case-sensitive).
- `\s+`: Matches one or more whitespace characters again.
- `(\d{5})`: Captures exactly five digits for the ZIP code.
- `$`: Matches the end of the string.
Example 54. Validating email addresses
Identify email addresses that adhere to the following rules:

- The local part can contain letters, numbers, underscores, hyphens, and dots.
- The domain name can have one or more subdomains.
- Subdomains can contain letters, numbers, and hyphens.
- The Top-level domain (TLD) must be 2 to 4 characters long and can contain letters only.
Click to reveal the formula and explanation
The regex formula would be:

`^[\w-\.]+@([a-zA-Z0-9\-]+(?:\.[a-zA-Z0-9\-]+)*)\.[a-zA-Z]{2,4}$`

**Explanation:**

- `^`: Matches the beginning of the string (entire email address).
- `[\w-\.]+`: Matches one or more occurrences of the following characters in the local part:
  - `\w`: Word characters (letters, numbers, and underscores).
  - `-`: Hyphen.
  - `\.`: Dot (period).
- `@`: Matches the "@" symbol, separating the local part from the domain name.
- `([a-zA-Z0-9\-]+(?:\.[a-zA-Z0-9\-]+)*)`: Matches one or more repetitions of the subdomain pattern:
  - `[a-zA-Z0-9\-]+`: Matches one or more letters (a-z, A-Z), numbers (0-9), and hyphens (-) for a subdomain (excluding underscores).
  - `(?:\.[a-zA-Z0-9\-]+)*`: Matches zero or more repetitions of a literal dot (.) followed by another subdomain following the same pattern.
- `\.`: Matches a literal dot (.) separating the subdomains from the TLD.
- `[a-zA-Z]{2,4}`: Matches the Top-Level Domain (TLD) containing:
  - `[a-zA-Z]`: Letters (a-z, A-Z).
  - `{2,4}`: Quantifier specifying a length of 2 to 4 characters.
- `$`: Matches the end of the string (entire email address).

#### Regex for advanced users

Since the implementation of regular expressions comes from the Java standard library, the syntax of expressions is the same as in Java: see [http://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html](http://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html#sum).

For a more detailed explanation of how to use regular expressions, see the Java documentation for `java.util.regex.Pattern`.

The meaning of regular expressions can be modified using embedded flag expressions. The expressions include the following:
`(?i)` – `Pattern.CASE_INSENSITIVE`
Enables case-insensitive matching.
`(?s)` – `Pattern.DOTALL`
In dotall mode, the dot `.` matches any character, including line terminators.
`(?m)` – `Pattern.MULTILINE`
In multiline mode, you can use `^` and `$` to express the beginning and end of the line, respectively (this includes at the beginning and end of the entire expression).

Further reading and description of other flags can be found at [http://docs.oracle.com/javase/tutorial/essential/regex/pattern.html](http://docs.oracle.com/javase/tutorial/essential/regex/pattern.html).
