<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Container functions -->

### Container functions

Container functions allow you to work with various container types - lists, maps and variant. These functions all operate on containers of various types - like lists of integers (`integer[]`), maps (e.g., `map[long, string]`), etc. To make the text easier to read, we use the following syntax to represent containers of various types:

- `element_type[]` means a list of any type, e.g., `integer[]`, `string[]`, or even `MyRecordType[]`. Alternative way of writing this is `list[element_type]` (e.g., `list[string]`).
- `map[key_type, value_type]` means a map that maps from given type of keys to given type of values. For example, `map[date, string]`, `map[long, MyRecordType]`, etc.

In many cases, you can see something like this: `element_type[] append(element_type[] target, element_type item)`. This means that `item` and must be the same type as type of elements in the `target` list.

#### List of functions

| [append](container-functions-ctl2.md#append) |
| --- |
| [appendAll](container-functions-ctl2.md#appendall) |
| [binarySearch](container-functions-ctl2.md#binarysearch) |
| [clear](container-functions-ctl2.md#clear) |
| [containsAll](container-functions-ctl2.md#containsall) |
| [containsKey](container-functions-ctl2.md#containskey) |
| [containsValue](container-functions-ctl2.md#containsvalue) |
| [copy](container-functions-ctl2.md#copy) |
| [findAllValues](container-functions-ctl2.md#findallvalues) |
| [getKeys](container-functions-ctl2.md#getkeys) |
| [getValues](container-functions-ctl2.md#getvalues) |
| [in](container-functions-ctl2.md#in) |
| [insert](container-functions-ctl2.md#insert) |
| [isEmpty(container)](container-functions-ctl2.md#isempty) |
| [length(container)](container-functions-ctl2.md#length) |
| [poll](container-functions-ctl2.md#poll) |
| [pop](container-functions-ctl2.md#pop) |
| [push](container-functions-ctl2.md#push) |
| [remove](container-functions-ctl2.md#remove) |
| [reverse(list)](container-functions-ctl2.md#reverse) |
| [sort](container-functions-ctl2.md#sort) |
| [toMap](container-functions-ctl2.md#tomap) |

#### append

```ctl
element_type[] append(element_type[] target, element_type item);
variant append(variant target, variant item);
```

Appends the `item` to the end of the `target` list. The function modifies `target` and then returns the modified list (i.e., it does not create a copy of the list before appending).

This function is an alias of the `push` function.

##### Error states

- If the given list is `null`, the function fails with an error.
- The variant version fails if the first argument is not a list.

##### Examples
Example 261. Usage of append

```ctl
string[] files = ["orders.csv", "customers.csv", "products.csv"];
string[] filesWithPayments = append(files, "payments.csv");
// returns list ["orders.csv", "customers.csv", "products.csv", "payments.csv"], also updates files to the same value.
```

##### Compatibility

- The `append(element_type[], element_type)` function is available since **CloverETL 3.0.0**.
- The `append(variant, variant)` function is available since **CloverDX 5.6.0**.

##### See also

- [insert](container-functions-ctl2.md#insert)
- [pop](container-functions-ctl2.md#pop)
- [push](container-functions-ctl2.md#push)

---

#### appendAll

```ctl
element_type[] appendAll(element_type[] target, element_type source);
map[key_type, value_type] appendAll(map[key_type, value_type] target, map[key_type, value_type] source);
variant appendAll(variant target, variant source);
```

Adds all elements from the `source` list or map to the end of the `target` list or map. The function modifies the `target` and then returns the modified version.

When appending a map with conflicting keys the original values are preserved (i.e., the function does not replace existing values). The opposite behavior can be achieved by using the [`copy()`](container-functions-ctl2.md#copy) function. When appending to list, the function simply appends the values and does not check for duplicates.

##### Error states

- If the first argument is `null`, the function fails with an error.
- If the first argument is a `map` and the second argument is `null`, the function fails with an error.
- The variant version fails if one of the arguments is not a list or a map or both arguments are not of the same type.

##### Examples
Example 262. Usage of appendAll

```ctl
appendAll(["order_id", "customer_id", "order_date"], ["status", "total_amount"]);
// returns list ["order_id", "customer_id", "order_date", "status", "total_amount"]

appendAll({ "SKU-1001" -> 25, "SKU-1002" -> 10, "SKU-1003" -> 0 }, { "SKU-1004" -> 8, "SKU-1005" -> 12 });
// returns map { "SKU-1001" -> 25, "SKU-1002" -> 10, "SKU-1003" -> 0, "SKU-1004" -> 8, "SKU-1005" -> 12 }

appendAll({ "SKU-1001" -> 25, "SKU-1002" -> 10, "SKU-1003" -> 0 }, { "SKU-1003" -> 15, "SKU-1005" -> 12 });
// returns map { "SKU-1001" -> 25, "SKU-1002" -> 10, "SKU-1003" -> 0, "SKU-1005" -> 12 }
```

##### Compatibility

- The `appendAll(element_type[], element_type[])` function is available since **CloverDX 6.4.0**.
- The `appendAll(map[key_type, value_type], map[key_type, value_type])` function is available since **CloverDX 6.4.0**.
- The `appendAll(variant, variant)` function is available since **CloverDX 6.4.0**.

##### See also

- [append](container-functions-ctl2.md#append)
- [copy](container-functions-ctl2.md#copy)

---

#### binarySearch

```ctl
integer binarySearch(element_type[] searchList, element_type value);
```

The `binarySearch()` function searches the `searchList` for the first occurrence of `value` using the binary search algorithm. The elements of the list must be comparable (e.g., `byte` or `cbyte` cannot be used) and the list must be **sorted in ascending order**. If the it is not sorted, the results are undefined.

If `value` is in the list, the function returns a non-negative integer (≥ 0) - and index of the `value` in the `searchList`. If the `value` is not in `searchList`, the function returns a negative number defined as (-(*insertion_point*) - 1). The *insertion_point* is defined as the point at which the key would be inserted into the list to maintain the list properly sorted.

If the list contains multiple elements equal to the `value`, the function does not make any guarantees about which one will be found (by definition, all of them will be next to each other in the `searchList`).

##### Error states

- The function fails if either of the arguments is `null` or if `element_type` is not comparable.

##### Examples
Example 263. Usage of binarySearch

```ctl
binarySearch(["bronze", "gold", "silver"], "gold")
// returns 1, because the index of "gold" is 1.

binarySearch(["bronze", "gold", "silver"], "platinum")
// returns -3, because "platinum" would be inserted at position 2 (before "silver").
```

##### Compatibility

- The `binarySearch()` function is available since **CloverETL 4.1.0-M1**.

##### See also

- [containsValue](container-functions-ctl2.md#containsvalue)

---

#### clear

```ctl
void clear(element_type[] target);
void clear(map[key_type, value_type] target);
void clear(variant target);
```

Empties the given list or map (removes all elements from them). If the `target` is a variant, it must be either a list or a map, it cannot be just plain value.

##### Error states

- If the `target` is `null`, the function fails with an error.

##### Examples
Example 264. Usage of clear

```ctl
list[string] listOfStrings = ["new", "paid"];
clear(listOfStrings); // listOfStrings is now an empty list: []

map[string, string] mapOfStrings = {"order_id" -> "ORD-1001", "status" -> "paid"};
clear(mapOfStrings); // mapOfStrings is now an empty map: {}

variant varList = ["John", 34];
clear(varList); // varList is now an empty list: []

variant varMap = {"name" -> "John", "age" -> 34};
clear(varMap); // varMap is now an empty map: {}
```

##### Compatibility

- The `clear(element_type[])` and `clear(map[key_type, value_type])` functions are available since **CloverETL 3.0.0**.
- The `clear(variant)` function is available since **CloverDX 5.7.0**.

##### See also

- [poll](container-functions-ctl2.md#poll)
- [pop](container-functions-ctl2.md#pop)
- [remove](container-functions-ctl2.md#remove)

---

#### containsAll

```ctl
boolean containsAll(element_type[] collection, element_type[] subList);
```

The `containsAll()` function returns `true` if the `collection` list contains every element of the `subList` list, i.e. if the second list is a sublist of the first list.

##### Error states

- If either of the given lists is `null`, the function fails with an error.

##### Examples
Example 265. Usage of containsAll

```ctl
containsAll(["new", "paid", "shipped"], ["paid", "shipped"])
// returns true.

containsAll(["new", "paid", "shipped"], ["cancelled", "paid", "shipped"])
// returns false.
```

##### Compatibility

The `containsAll(element_type[],element_type[])` function is available since **CloverETL 3.3.x**.

##### See also

- [containsKey](container-functions-ctl2.md#containskey)
- [containsValue](container-functions-ctl2.md#containsvalue)

---

#### containsKey

```ctl
boolean containsKey(map[key_type, value_type] searchMap, key_type key);
boolean containsKey(variant searchMap, variant key);
```

Returns `true`, if the `searchMap` contains element with key `key`. Note that this function does not need to iterate over the map - it works in constant time.

##### Error states

- If `searchMap` is `null`, the function fails with an error.

##### Examples
Example 266. Usage of containsKey

```ctl
containsKey({ "order_id" -> "ORD-1001", "status" -> "paid" }, "order_id");
// returns true

containsKey({ "order_id" -> "ORD-1001", "status" -> "paid" }, "customer_id");
// returns false
```

##### Compatibility

- The `containsKey(map[key_type, value_type], key_type)` function is available since **CloverETL 3.3.x**.
- The `containsKey(variant, variant)` function is available since **CloverDX 5.6.0**.

##### See also

- [containsValue](container-functions-ctl2.md#containsvalue)
- [findAllValues](container-functions-ctl2.md#findallvalues)
- [getKeys](container-functions-ctl2.md#getkeys)

---

#### containsValue

```ctl
boolean containsValue(element_type[] searchIn, element_type value);
boolean containsValue(map[key_type, value_type] searchIn, value_type value);
boolean containsValue(variant searchIn, variant value);
```

The function returns `true` if container `searchIn` contains value `value`. The function iterates over the whole container - linear time search.

The `containsValue(map, value)` function returns `true` if the specified map maps one or more keys to the specified value.

The `containsValue(list, value)` function returns `true` if the specified list contains the specified value. Note that the list does not have to be sorted. If you have a sorted list, use [`binarySearch`](container-functions-ctl2.md#binarysearch) since it is faster on longer lists.

The `containsValue(variant, variant)` function works as one of the two functions above, depending on whether the first argument contains a list or a map.

##### Error states

- If the first argument is `null`, the function fails with an error.

##### Examples
Example 267. Usage of containsValue

```ctl
map[integer, integer] mapOfIntegers = { 1 -> 17, 5 -> 19 };
boolean mapContains23 = containsValue(mapOfIntegers, 23); // false
boolean mapContains17 = containsValue(mapOfIntegers, 17); // true because key 1 maps to 17
boolean mapContains5 = containsValue(mapOfIntegers, 5); // false, 5 is a key, not a value

list[integer] listOfIntegers = [10, 17, 19, 30];
boolean listContains23 = containsValue(listOfIntegers, 23); // false
boolean listContains17 = containsValue(listOfIntegers, 17); // true

variant varMap = { "name" -> "John", "age" -> 34 };
boolean varMapContainsHarry = containsValue(varMap, "Harry"); // false
boolean varMapContainsJohn = containsValue(varMap, "John"); // true
boolean varMapContains34 = containsValue(varMap, 34); // true
boolean varMapContainsName = containsValue(varMap, "name"); // false, "name" is a key, not a value

variant varList = ["John", 34];
boolean varListContainsHarry = containsValue(varList, "Harry"); // false
boolean varListContainsJohn = containsValue(varList, "John"); // true
boolean varListContains34 = containsValue(varList, 34); // true
```

##### Compatibility

- The `containsValue(map[key_type, value_type], value_type)` function is available since **CloverETL 3.3.x**.
- The function `containsValue(element_type[], element_type)` is available since **CloverETL 4.0.0**.
- The function `containsValue(variant, variant)` is available since **CloverDX 5.7.0**.

##### See also

- [containsKey](container-functions-ctl2.md#containskey)
- [findAllValues](container-functions-ctl2.md#findallvalues)
- [getValues](container-functions-ctl2.md#getvalues)
- [binarySearch](container-functions-ctl2.md#binarysearch)

---

#### copy

```ctl
element_type[] copy(element_type[] target, element_type[] source);
map[key_type, value_type] copy(map[key_type, value_type] target, map[key_type, value_type] source);
```

The `copy` function copies data from the `source` container to the `target` container. It modifies the `target` container and then returns it.

For lists, the function appends the items from the `source` list to the end of the `target` list.

For maps, the function adds the key-value pairs from the `source` map to the `target` map. If the same key exists in both maps, the value from the `source` map replaces the value in the `target` map. Use `appendAll` if you want to keep the original value.

##### Error states

- If one of the arguments is `null`, the function fails with an error.

##### Examples
Example 268. Usage of copy

```ctl
list[string] sourceFiles = ["orders.csv", "customers.csv"];
list[string] additionalFiles = ["products.csv", "payments.csv"];

list[string] allFiles = copy(sourceFiles, additionalFiles);
   // both sourceFiles and allFiles are now
   // ["orders.csv", "customers.csv", "products.csv", "payments.csv"]
   // additionalFiles is not modified

map[string, string] orderData = {
   "order_id" -> "ORD-1001",
   "status" -> "new"
};
map[string, string] orderUpdate = {
   "status" -> "paid",
   "currency" -> "USD"
};

map[string, string] updatedOrderData = copy(orderData, orderUpdate);
   // both orderData and updatedOrderData are now
   // { "order_id" -> "ORD-1001", "status" -> "paid", "currency" -> "USD" }
   // orderUpdate is not modified
```

##### Compatibility

- The `copy(element_type[], element_type[])` function is available since **CloverETL 3.0.0**.

##### See also

- [append](container-functions-ctl2.md#append)
- [appendAll](container-functions-ctl2.md#appendall)
- [insert](container-functions-ctl2.md#insert)
- [poll](container-functions-ctl2.md#poll)
- [push](container-functions-ctl2.md#push)

---

#### findAllValues

```ctl
variant findAllValues(variant container, variant key);
```

Returns the list of all values associated with the specified key at any level of the structure passed as the first argument. Returns an empty list if nothing is found.

The container can be of any data type, however if it contains no map, the result will be an empty list.

##### Error states

- If the key` is a record, byte, or `cbyte array, the function fails with an error.

##### Examples
Example 269. Usage of findAllValues

```ctl
variant json = { // usually obtained by parseJson('...');
    "name" -> "CloverDX",
    "addresses" -> [
        { "city" -> "Arlington", "street" -> "2311 Wilson Blvd" },
        { "city" -> "London", "street" -> "91-94 Lower Marsh" },
        { "city" -> "Prague", "street" -> "Vinohradska 174"},
        { "city" -> "Brno", "street" -> "IBC Prikop 6"}
    ]
};
variant cities = findAllValues(json, "city");
// returns the list ["Arlington", "London", "Prague", "Brno"]

variant numbers = { 1 -> 2, 3 -> 4 };
findAllValues(numbers, 3); // returns [4]
findAllValues(numbers, 0); // returns [] (an empty list)

variant objects = [
        {
            "id" -> 1,
            "content" -> {
                "id" -> 2,
                "content" -> "Order confirmation"
            }
        },
        {
            "id" -> 3,
            "content" -> "Shipping update"
        }
];
findAllValues(objects, "content");
// Returns [{"id" -> 2, "content" -> "Order confirmation"}, "Order confirmation", "Shipping update"]
// the result contains all values associated with the key "content", including the nested object.

findAllValues("completed", "status");
// returns an empty list - "completed" is not a map
```

##### Compatibility

- The `findAllValues(variant, variant)` function is available since **CloverDX 5.7.0**.

##### See also

- [containsKey](container-functions-ctl2.md#containskey)
- [containsValue](container-functions-ctl2.md#containsvalue)
- [getKeys](container-functions-ctl2.md#getkeys)
- [getValues](container-functions-ctl2.md#getvalues)

---

#### getKeys

```ctl
list[K] getKeys(map[key_type, value_type] map);
variant getKeys(variant map);
```

Returns the list of keys from the specified map. The returned list has elements of the same type as the map’s keys. Order of returned keys is not specified - the function does not sort its result (use [`sort`](container-functions-ctl2.md#sort) to sort the result if needed).

##### Error states

- If a given map is `null`, the function fails with an error.
- The variant version fails if the argument is not a map.

##### Examples
Example 270. Usage of getKeys

```ctl
map[string, integer] orderTotals = { "ORD-1001" -> 129, "ORD-1002" -> 250 };
list[string] listOfKeys = getKeys(orderTotals); // ["ORD-1001", "ORD-1002"]

$out.0.variantField = orderTotals;
listOfKeys = getKeys($out.0.variantField); // ["ORD-1001", "ORD-1002"]

variant orderStatusFlags = { "paid" -> true, "cancelled" -> false };
variant listOfVariantKeys = getKeys(orderStatusFlags); // ["paid", "cancelled"]
```

##### Compatibility

- The `getKeys(map[key_type, value_type])` function is available since **CloverETL 3.3.x**.
- The `getKeys(variant)` function is available since **CloverDX 5.6.0**.

##### See also

- [containsKey](container-functions-ctl2.md#containskey)
- [containsValue](container-functions-ctl2.md#containsvalue)
- [findAllValues](container-functions-ctl2.md#findallvalues)
- [getValues](container-functions-ctl2.md#getvalues)

---

#### getValues

```ctl
value_type[] getValues(map[key_type, value_type] map);
variant getValues(variant map);
```

Returns the values contained in the specified map as a list. If the argument is an empty map, the function returns an empty list. The order of elements in the result is not specified - the function does not sort its result (use [`sort`](container-functions-ctl2.md#sort) to sort the result if needed).

##### Error states

- If the argument is `null`, the function fails.

##### Compatibility

- The `getValues(map[key_type, value_type])` function is available since **CloverETL 4.0.0**.
- The `getValues(variant)` function is available since **CloverDX 5.7.0**.
Example 271. Usage of getValues

```ctl
map[string, string] statusLabels = { "N" -> "new", "P" -> "paid" };
list[string] statusLabelValues = getValues(statusLabels); // ["new", "paid"]

map[string, string] emptyMap = {};
list[string] emptyMapValues = getValues(emptyMap); // an empty list: []

variant varMap = { "name" -> "John", "age" -> 34 };
variant varMapValues = getValues(varMap); // the list ["John", 34]
```

##### See also

- [containsKey](container-functions-ctl2.md#containskey)[findAllValues](container-functions-ctl2.md#findallvalues)[getKeys](container-functions-ctl2.md#getkeys)[toMap](container-functions-ctl2.md#tomap)

---

#### in

```ctl
boolean in(element_type element, element_type[] list);
boolean in(key_type key, map[key_type, value_type] map);
boolean in(element_type element, variant collection);
```

Returns `true` if the specified collection contains the specified element. If the collection is a map, returns `true` if the map contains the element as a key (the function does not search in values).

Note that seach in list is performed as linear search and can be slow for large lists. Searching in maps is constant time since only keys are searched.

##### Examples
Example 272. Usage of in

```ctl
in("paid", ["new", "paid"]); // returns true

in(10, [10, 20]); // returns true

map[string, string] streetTypes = { "str" -> "street", "ave" -> "avenue", "ct" -> "court", "ln" -> "lane" };
in("str", streetTypes); // true
in("street", streetTypes); // false, "street" is a value, not a key
```

Note that for lists and maps of a specific numeric type, e.g. `number[]` or a map with keys of type number, the searched-for element is automatically converted to the target type if possible (e.g., integers are converted to numbers).

For variant, there is no such automatic type conversion, the types must exactly match for the function to return true.
Example 273. Type conversion when using in

```ctl
integer i = 2;

list[number] numbers = [2.1, 2.0, 2.2];
boolean result = in(i, numbers); // true because 2 is automatically converted to number 2.0

variant varNumbers = [2.1, 2.0, 2.2];
result = in(i, varNumbers); // false, no automatic conversion, the types must exactly match
```

##### Compatibility

- The `in(element_type, element_type[])` function is available since **CloverETL 3.3.x**.
- The `in(key_type, map[key_type, value_type])` function is available since **CloverETL 3.3.x**.
- The `in(element_type, variant)` function is available since **CloverDX 5.7.0**.

##### See also

- [containsValue](container-functions-ctl2.md#containsvalue)
- [containsKey](container-functions-ctl2.md#containskey)

---

#### insert

```ctl
element_type[] insert(element_type[] target, integer position, element_type... elements);
element_type[] insert(element_type[] target, integer position, element_type[] source);
variant insert(variant target, integer position, variant... elements);
```

Inserts one or more elements into the list at the specified position, indexed from 0. Moves the element currently at that position (if any) and all subsequent elements to the right. Modifies the `target` list and returns the modified list.

##### Error states

- If the list given as the first argument is `null`, the function fails with an error.

##### Examples
Example 274. Usage of insert

```ctl
list[string] originalList = ["extract", "load", "archive"];
list[string] modifiedList = insert(originalList, 1, "validate");
   // both originalList and modifiedList are now ["extract", "validate", "load", "archive"]

// inserting multiple elements:
list[string] multiple = insert(["receive_order", "archive_order", "receive_order", "archive_order"], 2, "validate_order", "process_payment", "ship_order");
   // ["receive_order", "archive_order", "validate_order", "process_payment", "ship_order", "receive_order", "archive_order"]

// inserting a list of elements:
list[string] twoLists = insert(["receive_order", "archive_order", "receive_order", "archive_order"], 2, ["validate_order", "ship_order"]);
   // ["receive_order", "archive_order", "validate_order", "ship_order", "receive_order", "archive_order"]

// variant:
variant varList = ["John", 34, true];
variant varModified = insert(varList, 2, { "street" -> "Wilson Blvd "}, ["John", "Thompson"]);
   // both varList and varModified are now
   // ["John", 34, {"street" -> "Wilson Blvd"}, ["John", "Thompson"], true]
```

##### Compatibility

- The `insert(element_type[], integer, E…)` and `insert(element_type[], integer, element_type[])` functions are available since **CloverETL 3.0.0**.
- The `insert(variant, integer, variant…)` function is available since **CloverDX 5.7.0**.

##### See also

- [isNull](field-access-functions-ctl2.md#isnull)
- [push](container-functions-ctl2.md#push)
- [remove](container-functions-ctl2.md#remove)

---

#### isEmpty

```ctl
boolean isEmpty(element_type[] list);
boolean isEmpty(map[key_type, value_type] map);
boolean isEmpty(variant listOrMap);
```

Returns `true` if the specified list, map or variant is empty.

##### Error states

- If the argument is `null`, the function fails with an error.

##### Examples
Example 275. Usage of isEmpty

```ctl
// list:
boolean b1 = isEmpty(["new", "paid"]); // false
list[string] emptyList = [];
boolean b2 = isEmpty(emptyList); // true

// map:
boolean b3 = isEmpty({ "order_id" -> "ORD-1001" }); // false
map[string, integer] emptyMap = {};
boolean b4 = isEmpty(emptyMap); // true

// variant:
variant varMap = { "status" -> "paid" }; // map with one key-value pair
boolean b5 = isEmpty(varMap); // false
variant varList = []; // empty list
boolean b6 = isEmpty(varList); // true
```

##### Compatibility

- The `isEmpty(element_type[])` and `isEmpty(map[key_type, value_type])` functions are available since **CloverETL 3.0.0**.
- The `isEmpty(variant)` function is available since **CloverDX 5.7.0**.

##### See also

- [isEmpty(string)](string-functions-ctl2.md#isempty) a string function to test for empty strings
- [poll](container-functions-ctl2.md#poll)
- [pop](container-functions-ctl2.md#pop)

---

#### length

```ctl
integer length(byte value);
integer length(cbyte value);
integer length(string value);
integer length(element_type[] list);
integer length(map[key_type, value_type] map);
integer length(record recordValue);
integer length(variant value);
```

Returns the number of elements forming a given structured data type. The type of elements that are counted depend on argument type:

- For `byte` and `cbyte` the function counts bytes
- For `string` the function counts number of Unicode code units in the string. In many cases this will correspond to number of characters, but not always (e.g., if you use East Asian languages, emoji, etc.). For more complete discussion about string representation see [string data type](language-reference-ctl2.md#string).
- For lists it counts number of elements in the list. Note that for nested lists, the top-level list is counted.
- For maps it counts number of entries (key-value pairs) in the map.
- For records it counts the number of fields in the record.
- For variant it depends on what the variant is - string, list, or map. Then it applies rules listed above.

##### Error states

- If the argument is `null`, the function returns `0`.

##### Examples
Example 276. Usage of length

```ctl
byte byteVal = hex2byte("f09f92a9");
length(byteVal); // Returns 4

length(["new", "paid", "shipped"]); // Returns 3

// Nested lists
list[list[string]] listOfLists = [
    ["order_id", "customer_id"],
    ["status", "total_amount", "currency"]
];
length(listOfLists); // Returns 2

map[string, string] streetTypes = { "str" -> "street", "ave" -> "avenue", "ct" -> "court", "ln" -> "lane" };
length(streetTypes); // Returns 4

length($in.0); // Returns number of fields on the first input port.

MyRecord myRec;
length(myRec); // Returns number of fields in MyRecord metadata.
```

##### Compatibility

- The `length(element_type[])` and `length(map[key_type, value_type])` functions are available since **CloverETL 3.0.0**.
- The `length(variant)` function is available since **CloverDX 5.6.0**.

##### See also

- [length(string)](string-functions-ctl2.md#length) to count length of a string
- [length(record)](field-access-functions-ctl2.md#length) to count number of fields in a record

---

#### poll

```ctl
element_type poll(element_type[] list);
```

The `poll` function removes the **first** element from a given list and returns this element. The list specified as the argument changes to this new value (without the removed first element).

If the `list` is empty, the function returns `null`.

##### Error states

- If `list` is `null`, the function fails with an error.

##### Examples
Example 277. Usage of poll

```ctl
string[] statuses = ["new", "paid", "shipped"];
string firstStatus = poll(statuses);  //  returns "new", statuses contains ["paid", "shipped"] after the function call.
```

##### Compatibility

- The `poll(element_type[])` function is available since **CloverETL 3.0.0**.

##### See also

- [append](container-functions-ctl2.md#append)
- [insert](container-functions-ctl2.md#insert)
- [pop](container-functions-ctl2.md#pop)
- [remove](container-functions-ctl2.md#remove)

---

#### pop

```ctl
element_type pop(element_type[] list);
```

The `pop` function removes the **last** element from a given list and returns this element. The list specified as the argument changes to this new value (without the removed last element).

##### Error states

- If `list` is `null`, the function fails with an error.

##### Examples
Example 278. Usage of pop

```ctl
string[] statuses = ["new", "paid", "shipped"];
string firstStatus = pop(statuses);  //  returns "shipped", statuses contains ["new", "paid"] after the function call.
```

##### Compatibility

The `pop(element_type[])` function is available since **CloverETL 3.0.0**.

##### See also

- [append](container-functions-ctl2.md#append)
- [isEmpty(container)](container-functions-ctl2.md#isempty)
- [poll](container-functions-ctl2.md#poll)
- [push](container-functions-ctl2.md#push)
- [remove](container-functions-ctl2.md#remove)

---

#### push

```ctl
element_type[] push(element_type[] target, element_type element);
variant push(variant target, variant element);
```

Adds an element `element` to the end of the `target` list. Modifies the `target` list and then returns the modified list.

This function is an alias of the `append` function.

##### Error states

- If the given list is `null`, the function fails with an error.
- The variant version fails if the first argument is not a list or if it is `null`.

##### Examples
Example 279. Usage of push

```ctl
// list:
list[string] originalList = ["new", "paid", "shipped"];
list[string] modifiedList = push(originalList, "delivered");
   // both originalList and modifiedList are now ["new", "paid", "shipped", "delivered"]

// variant:
variant varList = ["John", 34, true];
variant varModified = push(varList, {"street" -> "Wilson Blvd"});
   // both varList and varModified are now ["John", 34, true, {"street" -> "Wilson Blvd"}]
```

##### Compatibility

- The `push(element_type[], element_type)` function is available since **CloverETL 3.0.0**.
- The `push(variant, variant)` function is available since **CloverDX 5.7.0**.

##### See also

- [append](container-functions-ctl2.md#append)
- [insert](container-functions-ctl2.md#insert)
- [pop](container-functions-ctl2.md#pop)
- [remove](container-functions-ctl2.md#remove)

---

#### remove

```ctl
element_type remove(element_type[] removeFrom, integer position);
value_type remove(map[key_type, value_type] removeFrom, key_type key);
variant remove(variant removeFrom, variant position);
```

The function removes:

- **from a list or variant containing a list** the element at the positions specified by `position` and returns the removed element. The list specified as the first argument is modified by removing the value at given position (i.e., it will be one element shorter). List elements are indexed starting from 0.
- **from a map or variant containing a map** the key-value pair identified by the `key` and returns the removed value. The map is modified to no longer include given key.

##### Error states

- If `removeFrom` is `null`, the function fails with an error.

##### Examples
Example 280. Usage of remove

```ctl
//  list:
string[] statuses = ["new", "paid", "shipped"];
string secondItem = remove(statuses, 1); // returns "paid", statuses is changed to ["new", "shipped"]

//  map:
map[string, integer] stockBySku = { "SKU-1001" -> 25, "SKU-1002" -> 10, "SKU-1003" -> 0 };
integer deletedValue = remove(stockBySku, "SKU-1002"); // returns 10, stockBySku is updated to { "SKU-1001" -> 25, "SKU-1003" -> 0 }
```

##### Compatibility

- The `remove(element_type[], integer)` function is available since **CloverETL 3.0.0**.
- The `remove(map[key_type, value_type], key_type)` function is available since **CloverDX 5.0.0**.
- The `remove(variant, variant)` function is available since **CloverDX 5.6.0**.

##### See also

- [append](container-functions-ctl2.md#append)
- [insert](container-functions-ctl2.md#insert)
- [poll](container-functions-ctl2.md#poll)
- [push](container-functions-ctl2.md#push)

---

#### reverse

```ctl
element_type[] reverse(element_type[] list);
variant reverse(variant list);
string reverse(string value);
```

Reverses the order of elements of given list and returns the modified list (original list is modified).

##### Error states

- If the argument is `null`, the function fails with an error.
- The variant version fails if the argument is not a list or if it is `null`.

##### Examples
Example 281. Usage of reverse

```ctl
// list:
list[string] originalList = ["extract", "validate", "load", "archive"];
list[string] modifiedList = reverse(originalList);
   // both originalList and modifiedList are now ["archive", "load", "validate", "extract"]

// variant:
variant varList = [["Atlanta"], ["Boston", "Chicago"], ["New York"], ["Chicago", "Dallas"]];
variant varModified = reverse(varList);
   // both varList and varModified are now [["Chicago", "Dallas"], ["New York"], ["Boston", "Chicago"], ["Atlanta"]]
   // note that nested lists are not affected
```

##### Compatibility

- The `reverse(element_type[])` function is available since **CloverETL 3.1.2**.
- The `reverse(variant)` function is available since **CloverDX 5.7.0**.

##### See also

- [sort](container-functions-ctl2.md#sort)
- [reverse(string)](string-functions-ctl2.md#reverse) to reverse characters in a string

---

#### sort

```ctl
element_type[] sort(element_type[] list);
```

The `sort` function sorts the elements of a given list in ascending order according to their values and returns such new value of the list specified as the first argument. Sorting is done in-place - the original list is modified as well. `null` values are listed at the end of the sorted list, if present.

##### Error states

- The function will fail if the input list is `null`.

##### Examples
Example 282. Usage of sort

```ctl
string[] cities = ["London", "Prague", "Berlin"];
string[] sortedCities = sort(cities);
// Both cities and sortedCities will be ["Berlin", "London", "Prague"]

string[] withNull = ["C", null, "B", null, "A"];
string[] withNullSorted = sort(withNull);
// Both withNull and withNullSorted will be ["A", "B", "C", null, null]
```

##### Compatibility

- The `sort(element_type[])` function is available since **CloverETL 3.0.0**.

##### See also

- [reverse(list)](container-functions-ctl2.md#reverse)

---

#### toMap

```ctl
map[key_type, value_type] toMap(key_type[] keys, value_type[] values);
map[key_type, value_type] toMap(key_type[] keys, value_type value);
```

The function `toMap(key_type[], value_type[])` creates a map from two lists. Elements of the first list will become keys and corresponding elements from the second list will be value (first key will map to first value, etc.). Note that both lists must be the same length.

The function `toMap(key_type[], value_type)` create a map which maps all keys from the first list to the same value set by `value`.

Note that `values` and `keys` can contain `null` values which will become keys or values as needed. Same for `value` in the second overload of the function - it will result in a map where all values are `null`.

##### Error states

- If the parameter `keys` is `null`, the function fails.
- If the parameter `values` is `null`, the function `toMap(key_type[], value_type[])` fails.
- If length of the `keys` and `values` lists are not the same, the first overload fails.

##### Compatibility

- The `toMap` function is available since **CloverETL 4.0.0**.
Example 283. Usage of toMap

```ctl
string[] columnLabels = ["Order ID", "Customer ID", "Order Date"];
string[] columnNames = ["order_id", "customer_id", "order_date"];
map[string, string] columns = toMap(columnNames, columnLabels);
// Returns map {"Order ID" -> "order_id", "Customer ID" -> "customer_id", "Order Date" -> "order_date"}

string[] empty; // This will be an empty list
map[string, string] emptyMap = toMap(empty, empty);
// Return an empty map {}

string[] products = ["SKU-1001", "SKU-1002", "SKU-1003"];
integer[] counts = [10, 20, 30];
map[string, integer] availability = toMap(products, counts);
// Returns map {"SKU-1001" -> 10, "SKU-1002" -> 20, "SKU-1003" -> 30}

map[string, integer] availabilityWhenEmpty = toMap(products, 0);
// Returns map {"SKU-1001" -> 0, "SKU-1002" -> 0, "SKU-1003" -> 0}
```

##### See also

- [getKeys](container-functions-ctl2.md#getkeys)
- [getValues](container-functions-ctl2.md#getvalues)
- [record2map](conversion-functions-ctl2.md#record2map)
