<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Container functions -->

### Container functions

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

###### Functions you can use with containers

#### append

```ctl
<element type>[] append(<element type>[] arg, <element type>);
variant append(variant arg, variant);
```

Adds the second argument to the end of the list specified as the first argument. The function returns the modified list.

This function is an alias of the `push` function.

If the given list is `null`, the function fails with an error.

The variant version fails if the first argument is not a list.

**Compatibility**

The `append(E[],E)` function is available since **CloverETL 3.0.0**.

The `append(variant,variant)` function is available since **CloverDX 5.6.0**.
Example 252. Usage of append

```ctl
append(["a", "b", "d"], "c"); // returns list ["a", "b", "d", "c"]
```

**See also:**[insert](container-functions-ctl2.md#insert), [pop](container-functions-ctl2.md#pop), [push](container-functions-ctl2.md#push)

#### appendAll

```ctl
list[E]  appendAll(list[E] target,  list[E] source);
map[K,V] appendAll(map[K,V] target, map[K,V] source);
variant  appendAll(variant target,  variant source);
```

Adds the list or map specified as second argument to the end of the list or map specified as the first argument. The function returns the modified list or map.

If the given first argument is `null`, the function fails with an error.

If the given first argument is a `map` and the second argument is `null`, the function fails with an error.

The variant version fails if one of the given arguments is not a list or a map or both of the arguments are not of the same type.

When appending a map with conflicting keys the original values are preserved. The opposite behavior can be achieved by using the [`copy()`](container-functions-ctl2.md#copy) function.

**Compatibility**

The `appendAll(list[],list[])` function is available since **CloverDX 6.4.0**.

The `appendAll(map[],map[])` function is available since **CloverDX 6.4.0**.

The `appendAll(variant,variant)` function is available since **CloverDX 6.4.0**.
Example 253. Usage of appendAll

```ctl
appendAll(["a", "b", "d"], ["c", "e"]);
   // returns list ["a", "b", "d", "c", "e"]

appendAll({ "A" -> 1, "B" -> 2, "C" -> 3 }, { "D" -> 4, "E" -> 2 });
   // returns map { "A" -> 1, "B" -> 2, "C" -> 3, "D" -> 4, "E" -> 2 }

appendAll({ "A" -> 1, "B" -> 2, "C" -> 3 }, { "C" -> 4, "E" -> 2 });
   // returns map { "A" -> 1, "B" -> 2, "C" -> 3, "E" -> 2 }
```

**See also:**[append](container-functions-ctl2.md#append), [copy](container-functions-ctl2.md#copy)

#### binarySearch

```ctl
integer binarySearch(<element type>[] arg, <element type>);
```

The `binarySearch()` function searches a specified list for a specified object using the binary search algorithm.

The elements of the list must be comparable and the list must be **sorted in ascending order**. If it is not sorted, the results are undefined.

Returns the index of the search key (≥ 0) if it is contained in the list. Otherwise, returns a negative number defined as (-(*insertion point*) - 1). The *insertion point* is defined as the point at which the key would be inserted into the list.

If the list contains multiple objects equal to the search key, there is no guarantee which one will be found.

The function fails if either of the arguments is `null` or if <element type> is not comparable.

**Compatibility**

The `isEmpty()` function is available since **CloverETL 4.1.0-M1**.
Example 254. Usage of binarySearch
`binarySearch(["a", "b", "d"], "b")` returns `1`, because the index of `"b"` is 1.

`binarySearch(["a", "b", "d"], "c")` returns `-3`, because `"c"` would be inserted at position 2.

**See also:**[containsValue](container-functions-ctl2.md#containsvalue)

#### clear

```ctl
void clear(list[<element type>] arg);
void clear(map[<type of key>,<type of value>] arg);
void clear(variant arg);
```

Empties the given list or map.

If the given argument is `null`, the function fails with an error.

**Compatibility**

The `clear(list[E])` and `clear(map[K,V])` functions are available since **CloverETL 3.0.0**.

The `clear(variant)` function is available since **CloverDX 5.7.0**.
Example 255. Usage of clear

```ctl
list[string] listOfStrings = ["a", "b"];
clear(listOfStrings); // listOfStrings is now an empty list: []

map[string, string] mapOfStrings = {"a" -> "aa", "b" -> "bbb"};
clear(mapOfStrings); // mapOfStrings is now an empty map: {}

variant varList = ["John", 34];
clear(varList); // varList is now an empty list: []

variant varMap = {"name" -> "John", "age" -> 34};
clear(varMap); // varMap is now an empty map: {}
```

**See also:**[poll](container-functions-ctl2.md#poll), [pop](container-functions-ctl2.md#pop), [remove](container-functions-ctl2.md#remove)

#### containsAll

```ctl
boolean containsAll(<element type>[] list, <element type>[] subList);
```

The `containsAll()` function returns `true` if the list specified as the first argument contains every element of the list specified as the second argument, i.e. the second list is a sublist of the first list.

If one of the given list has a `null` reference, the function fails with an error.

**Compatibility**

The `containsAll(E[],E[])` function is available since **CloverETL 3.3.x**.
Example 256. Usage of containsAll
The function `containsAll([1, 3, 5], [3, 5])` returns `true`.

The function `containsAll([1, 3, 5], [2, 3, 5])` returns `false`.

**See also:**[containsKey](container-functions-ctl2.md#containskey), [containsValue](container-functions-ctl2.md#containsvalue)

#### containsKey

```ctl
boolean containsKey(map[<type of key>,<type of value>] arg, <type of key> key);
boolean containsKey(variant arg, variant key);
```

Returns `true`, if the specified map (or variant containing a map) contains a mapping for the specified key.

If the given map is `null`, the function fails with an error.

**Compatibility**

The `containsKey(map[K,V],K)` function is available since **CloverETL 3.3.x**.

The `containsKey(variant,variant)` function is available since **CloverDX 5.6.0**.
Example 257. Usage of containsKey

```ctl
containsKey({ 1 -> 17, 5 -> 10 }, 1); // returns true
containsKey({ 1 -> 17, 5 -> 10 }, 2); // returns false
```

**See also:**[containsValue](container-functions-ctl2.md#containsvalue), [findAllValues](container-functions-ctl2.md#findallvalues), [getKeys](container-functions-ctl2.md#getkeys)

#### containsValue

```ctl
boolean containsValue(map[<type of key>,<type of value>] map, <type of value> value);
boolean containsValue(list[<element type>] list, <element type> value);
boolean containsValue(variant listOrMap, variant value);
```

The `containsValue(map, value)` function returns `true` if the specified map maps one or more keys to the specified value.

The `containsValue(list, value)` function returns `true` if the specified list contains the specified value.

The `containsValue(variant, variant)` function works as one of the two functions above, depending on whether the first argument contains a list or a map.

If the first argument is `null`, the function fails with an error.

**Compatibility**

The `containsValue(map[K,V],V)` function is available since **CloverETL 3.3.x**.

The function `containsValue(list[E],E)` is available since **CloverETL 4.0.0**.

The function `containsValue(variant, variant)` is available since **CloverDX 5.7.0**.
Example 258. Usage of containsValue

```ctl
map[integer, integer] mapOfIntegers = { 1 -> 17, 5 -> 19 };
boolean mapContains23 = containsValue(mapOfIntegers, 23); // false
// mapOfIntegers contains 17 under the key 1
boolean mapContains17 = containsValue(mapOfIntegers, 17); // true
// 5 is a key, not a value
boolean mapContains5 = containsValue(mapOfIntegers, 5); // false

list[integer] listOfIntegers = [10, 17, 19, 30];
boolean listContains23 = containsValue(listOfIntegers, 23); // false
boolean listContains17 = containsValue(listOfIntegers, 17); // true

variant varMap = { "name" -> "John", "age" -> 34 };
boolean varMapContainsHarry = containsValue(varMap, "Harry"); // false
boolean varMapContainsJohn = containsValue(varMap, "John"); // true
boolean varMapContains34 = containsValue(varMap, 34); // true
// "name" is a key, not a value
boolean varMapContainsName = containsValue(varMap, "name"); // false

variant varList = ["John", 34];
boolean varListContainsHarry = containsValue(varList, "Harry"); // false
boolean varListContainsJohn = containsValue(varList, "John"); // true
boolean varListContains34 = containsValue(varList, 34); // true
```

**See also:**[containsKey](container-functions-ctl2.md#containskey), [findAllValues](container-functions-ctl2.md#findallvalues), [getValues](container-functions-ctl2.md#getvalues), [binarySearch](container-functions-ctl2.md#binarysearch)

#### copy

```ctl
<element type>[] copy(<element type>[] to, <element type>[] from);
```

The `copy()` function copies items from one list to another.

The function accepts two list arguments of the same data types. The function takes the second argument, adds it to the end of the first list and returns the new value of the list specified as the first argument.

If one of the given lists has a `null` reference, the function fails with an error.

**Compatibility**

The `copy(E[],E[])` function is available since **CloverETL 3.0.0**.
Example 259. Usage of copy There are two lists. The list `s1 = ["a", "b"]` and the list `s2 = ["c", "d"]`. The function `copy(s1, s2)` returns `["a", "b", "c", "d"]`. The list `s1` has been modified and contains values `["a", "b", "c", "d"]`.

```ctl
map[<type of key>, <type of value>] copy(map[<type of key>, <type of value>] to, map[<type of key>, <type of value>] from);
```

The `copy()` function accepts two map arguments of the same data type. The function takes the second argument, adds it to the end of the first map replacing existing key mappings and returns the new value of the map specified as the first argument.

If one of the given maps has a `null` reference, the function fails with an error.

If some key exists in both maps, the result will contain value from the second one.
Example 260. Usage of copy
Let us have following lines of code.

```ctl
map[string, string] map1;
map1["a"] = "aa";
map1["b"] = "bbb";
map[string, string] map2;
map2["c"] = "cc";
map2["d"] = "ddd";

$out.0.field1 = map1;
$out.0.field2 = map2;
$out.0.field3 = copy(map1, map2);
$out.0.field4 = map1;
$out.0.field5 = map2;
```

The field `field1` contains `{ a=aa, b=bbb }`. The field `field2` contains `{ c=cc, d=ddd }`. The field `field3` contains `{ a=aa, b=bbb, c=cc, d=ddd }`. The field `field4` contains `{ a=aa, b=bbb, c=cc, d=ddd }`. The function `copy` copies values from the second argument (`map2`) to the first argument (`map1`). The field `field5` contains `{c=cc, d=ddd}`.

**See also:**[append](container-functions-ctl2.md#append), [appendAll](container-functions-ctl2.md#appendall), [insert](container-functions-ctl2.md#insert), [poll](container-functions-ctl2.md#poll), [push](container-functions-ctl2.md#push)

#### findAllValues

```ctl
variant findAllValues(variant container, variant key);
```

Returns the list of all values associated with the specified key at any level of the structure specified as the first argument.

Returns an empty list if nothing was found.

The container can be of any data type, however if this object contains no map the result will be an empty list.

If the key is a record or a byte array, the function fails with an error.

**Compatibility**

The `findAllValues(variant, variant)` function is available since **CloverDX 5.7.0**.
Example 261. Usage of findAllValues

```ctl
variant json = { // usually obtained by parseJson('...');
    "name" -> "CloverDX",
    "addresses" -> [
        { "city" -> "Arlington", "street" -> "2311 Wilson Blvd" },
        { "city" -> "London", "street" -> "24 Southwark Bridge Road" },
        { "city" -> "Prague", "street" -> "Vinohradska 174"},
        { "city" -> "Brno", "street" -> "IBC Prikop 6"}
    ]
};
variant cities = json.findAllValues("city");
    // returns the list ["Arlington", "London", "Prague", "Brno"]

variant numbers = { 1 -> 2, 3 -> 4 };
numbers.findAllValues(3); // returns [4]
numbers.findAllValues(0); // returns an empty list

variant objects = [
        {
            "id" -> 1,
            "content" -> {
                "id" -> 2,
                "content" -> "aaa"
            }
        },
        {
            "id" -> 3,
            "content" -> "bbb"
        }
];
objects.findAllValues("content");
    // returns [{"id" -> 2, "content" -> "aaa"}, "aaa", "bbb"]
    // the result contains all values associated with the key "content",
    // including the nested object

findAllValues("randomString", "r");
    // returns an empty list - "randomString" is not a map
```

**See also:**[containsKey](container-functions-ctl2.md#containskey), [containsValue](container-functions-ctl2.md#containsvalue), [getKeys](container-functions-ctl2.md#getkeys), [getValues](container-functions-ctl2.md#getvalues)

#### getKeys

```ctl
<type of key>[] getKeys(map[<type of key>, <type of value>] arg);
variant getKeys(variant arg);
```

Returns the list of *keys* of the specified map.

The returned list is of the same type as the map’s keys.

If a given map is `null`, the function fails with an error.

The variant version fails if the argument is not a map.

**Compatibility**

The `getKeys(map[K,V])` function is available since **CloverETL 3.3.x**.

The `getKeys(variant)` function is available since **CloverDX 5.6.0**.
Example 262. Usage of getKeys

```ctl
map[string, integer] myMap = { "first" -> 1, "second" -> 2 };
list[string] listOfKeys = getKeys(myMap); // ["first", "second"]

$out.0.variantField = myMap;
listOfKeys = getKeys($out.0.varianField); // ["first", "second"]

variant myMapVariant = { 1 -> true, "hello" -> false };
variant listOfVariantKeys = getKeys(myMapVariant); // [1, "hello"]
```

**See also:**[containsKey](container-functions-ctl2.md#containskey), [containsValue](container-functions-ctl2.md#containsvalue), [findAllValues](container-functions-ctl2.md#findallvalues), [getValues](container-functions-ctl2.md#getvalues)

#### getValues

```ctl
list[<type of value>] getValues(map[<type of key>, <type of value>] arg);
variant getValues(variant arg);
```

Returns the values contained in the specified map as a list.

If the argument is an empty map, the function returns an empty list.

If the argument is `null`, the function fails.

**Compatibility**

The `getValues(map[K, V])` function is available since **CloverETL 4.0.0**.

The `getValues(variant)` function is available since **CloverDX 5.7.0**.
Example 263. Usage of getValues

```ctl
map[string, string] greek = { "a" -> "alpha", "b" -> "beta" };
list[string] greekValues = getValues(greek); // ["alpha", "beta"]

map[string, string] emptyMap = {};
list[string] emptyMapValues = getValues(emptyMap); // an empty list: []

variant varMap = { "name" -> "John", "age" -> 34 };
variant varMapValues = getValues(varMap); // the list ["John", 34]

$out.0.variantField = varMap;
variant varMapValues = getValues($out.0.variantField); // the list ["John", 34]
```

**See also:**[containsKey](container-functions-ctl2.md#containskey), [findAllValues](container-functions-ctl2.md#findallvalues), [getKeys](container-functions-ctl2.md#getkeys), [toMap](container-functions-ctl2.md#tomap)

#### in

```ctl
boolean in(<any type> element, <collection type> collection);
```

Returns true if the specified collection contains the specified element.

If the collection is a map, returns true if the map contains the element as a key.

**Compatibility**

The `in(map[K,V], V)` function is available since **CloverETL 3.3.x**.

The function `in(list[E], E)` is available since **CloverETL 3.3.x**.

The function `in(any type, variant)` is available since **CloverDX 5.7.0**.
Example 264. Usage of in

```ctl
"abc".in(["abc", "b"]); // returns true

in(10, [10, 20]); // returns true

10.in([10, 20]); // returns true

// assumes that $in.0 contains listField of type list[string]
in("abc", $in.0.listField); // returns true if "abc" is in the list

// assumes that $in.0 contains mapField of type map[string, string]
in("abc", $in.0.mapField); // returns true if "abc" is a key in the map
```

> [!NOTE]
> Note that searching for an element in a large list may be slow in comparison with searching for a key in a map, because list elements need to be checked one by one.
>
> For lists and maps of a specific numeric type, e.g. list[number] or a map with keys of type number, the searched-for element is automatically converted to the target type if possible, e.g. integers are converted to numbers. For variant, there is no such automatic type conversion, the types must exactly match for the function to return true.
>
>
> ```ctl
> integer i = 2;
>
> list[number] numbers = [2.1, 2.0, 2.2];
> // 2 is automatically converted to number 2.0
> boolean result = i.in(numbers); // true
>
> variant varNumbers = [2.1, 2.0, 2.2];
> // no automatic conversion, the types must exactly match
> result = i.in(varNumbers); // false
> ```

**See also:**[containsValue](container-functions-ctl2.md#containsvalue), [containsKey](container-functions-ctl2.md#containskey)

#### insert

```ctl
list[<element type>] insert(list[<element type>] targetList, integer, <element type>);
list[<element type>] insert(list[<element type>] targetList, integer, list[<element type>]);
variant insert(variant targetList, integer, variant);
```

Inserts one or more elements into the list at the specified position, indexed from 0. Moves the element currently at that position (if any) and all subsequent elements to the right. Returns the modified list.

If the list given as the first argument is `null`, the function fails with an error.

**Compatibility**

The `insert(list[E], integer, E…)` and `insert(list[E], integer, list[E])` functions are available since **CloverETL 3.0.0**.

The `insert(variant, integer, variant…)` function is available since **CloverDX 5.7.0**.
Example 265. Usage of insert

```ctl
list[string] originalList = ["a", "d", "b"];
list[string] modifiedList = insert(originalList, 1, "c");
// both originalList and modifiedList are now ["a", "c", "d", "b"]

// inserting multiple elements:
list[string] multiple = insert(["a", "b", "a", "b"], 2, "c", "d", "e");
// ["a", "b", "c", "d", "e", "a", "b"]

// inserting a list of elements:
list[string] twoLists = insert(["a", "b", "a", "b"], 2, ["c", "d"]);
// ["a", "b", "c", "d", "a", "b"]

// variant:
variant varList = ["John", 34, true];
variant varModified = insert(varList, 2,
     { "street" -> "Wilson Blvd "}, ["John", "Thompson"]);
// both varList and varModified are now
//   ["John", 34, {"street" -> "Wilson Blvd"}, ["John", "Thompson"], true]
```

**See also:**[isNull](field-access-functions-ctl2.md#isnull), [push](container-functions-ctl2.md#push), [remove](container-functions-ctl2.md#remove)

#### isEmpty

```ctl
boolean isEmpty(list[<element type>] arg);
boolean isEmpty(map[<type of key>, <type of value>] arg);
boolean isEmpty(variant arg);
```

Returns true if the specified list, map or string is empty.

If the argument is `null`, the function fails with an error.

**Compatibility**

The `isEmpty(list[E])` and `isEmpty(map[K,V])` functions are available since **CloverETL 3.0.0**.

The `isEmpty(variant)` function is available since **CloverDX 5.7.0**.
Example 266. Usage of isEmpty

```ctl
// list:
boolean b1 = isEmpty(["a", "b"]); // false
list[string] emptyList = [];
boolean b2 = isEmpty(emptyList); // true

// map:
boolean b3 = isEmpty({ "a" -> "alpha" }); // false
map[string, integer] emptyMap = {};
boolean b4 = isEmpty(emptyMap); // true

// variant:
variant varMap = { "b" -> "beta" }; // map with one key-value pair
boolean b5 = isEmpty(varMap); // false
variant varList = []; // empty list
boolean b6 = isEmpty(varList); // true
```

**See also:** String function: [isEmpty(string)](string-functions-ctl2.md#isempty), [poll](container-functions-ctl2.md#poll), [pop](container-functions-ctl2.md#pop)

#### length

```ctl
integer length(structuredtype arg);
```

Returns the number of elements forming a given structured data type.

The argument can be one of following: `string`, `list`, `map`, `record` or `variant` containing any of these types.

For maps the function returns the number of key-value pairs and for nested lists it returns the size of the top-level list.

If the argument is `null`, the function returns `0`.

**Compatibility**

The `length(E[])` and `length(map[K,V])` functions are available since **CloverETL 3.0.0**.

The `length(variant)` function is available since **CloverDX 5.6.0**.
Example 267. Usage of length:

```ctl
length(["a", "d", "c"]); // returns 3
list[list[string]] listOfLists = [
    ["a", "d"],
    ["d", "e", "f"]
];
length(listOfLists); // returns 2
```

**See also:** String functions: [length(string)](string-functions-ctl2.md#length), Record functions: [length(record)](field-access-functions-ctl2.md#length)

#### poll

```ctl
<element type> poll(<element type>[] arg);
```

The `poll()` function removes the first element from a given list and returns this element.

The list specified as the argument changes to this new value (without the removed first element).

If a given list has a `null` reference, the function fails with an error.

**Compatibility**

The `poll(E[])` function is available since **CloverETL 3.0.0**.
Example 268. Usage of poll The function `poll(["a", "d", "c"])` returns `a`. The list given as argument contains `["d", "c"]` after the function call.
**See also:**[append](container-functions-ctl2.md#append), [insert](container-functions-ctl2.md#insert), [pop](container-functions-ctl2.md#pop), [remove](container-functions-ctl2.md#remove)

#### pop

```ctl
<element type> pop(<element type>[] arg);
```

The `pop()` function removes the last element from a given list and returns this element.

The list specified as the argument changes to this new value (without the removed last element).

If a given list has a `null` reference, the function fails with an error.

**Compatibility**

The `pop(E[])` function is available since **CloverETL 3.0.0**.
Example 269. Usage of pop
- The function `pop(["a", "b", "c"])` returns `c`.
- The function `pop` modifies list `s1`:
  ```ctl
  string[] s1 = ["a", "b", "c"];
  $out.0.field1 = s1;
  $out.1.field2 = pop(s1);
  $out.0.field3 = s1;
  ```
  `field1` on first output port contains `["a", "b", "c"]`.
  `field2` on second output port contains `c`.
  `field3` on first output port contains `["a", "b"]`.

**See also:**[append](container-functions-ctl2.md#append), [isEmpty(container)](container-functions-ctl2.md#isempty), [poll](container-functions-ctl2.md#poll), [push](container-functions-ctl2.md#push), [remove](container-functions-ctl2.md#remove)

#### push

```ctl
list[<element type>] push(list[<element type>] targetList, <element type>);
variant push(variant targetList, variant);
```

Adds an element to the end of the specified list. Returns the modified list.

This function is an alias of the `append` function.

If the given list is `null`, the function fails with an error.

The variant version fails if the first argument is not a list.

**Compatibility**

The `push(list[E], E)` function is available since **CloverETL 3.0.0**.

The `push(variant, variant)` function is available since **CloverDX 5.7.0**.
Example 270. Usage of push

```ctl
// list:
list[string] originalList = ["a", "b", "c"];
list[string] modifiedList = push(originalList, "d");
// both originalList and modifiedList are now ["a", "b", "c", "d"]

// variant:
variant varList = ["John", 34, true];
variant varModified = push(varList, {"street" -> "Wilson Blvd"});
// both varList and varModified are now ["John", 34, true, {"street" -> "Wilson Blvd"}]
```

**See also:**[append](container-functions-ctl2.md#append), [insert](container-functions-ctl2.md#insert), [pop](container-functions-ctl2.md#pop), [remove](container-functions-ctl2.md#remove)

#### remove

```ctl
<element type> remove(<element type>[] arg, integer);
variant remove(variant arg, variant);
```

```ctl
<value type> remove(map[<key type>, <value type>] arg, <key type>);
variant remove(variant arg, variant);
```

The function removes:

- **from a given list (or variant containing a list)** the element at the specified `position` and returns the removed element.
  The list specified as the first argument changes its value to the new one. List elements are indexed starting from 0.
- **from a given map (or variant containing a map)** the key/value pair identified by the `key` and returns the value.

If the given list or map is null, the function fails with an error.

**Compatibility**

The `remove(E[], integer)` function is available since **CloverETL 3.0.0**.

The `remove(map[K,V], K)` function is available since **CloverDX 5.0.0**.

The `remove(variant, variant)` function is available since **CloverDX 5.6.0**.
Example 271. Usage of remove - list

```ctl
remove(["a", "b", "c"], 1); // returns "b"

list[string] s = ["a", "b", "c"];

list[string] backup = s; // assigns a copy of 's' to 'backup'
string removed = remove(s, 1); // removes "b" from 's' and assigns it to 'removed'
// s == ["a", "c"]
list[string] modified = s; // assigns a copy of modified 's' to 'modified'

// backup == ["a", "b", "c"]
// removed == "b"
// modified == ["a", "c"]
```

Example 272. Usage of remove - map

```ctl
map[string, integer] aMap = { "a" -> 1, "b" -> 2, "c" -> 3 };

integer deletedValue = remove(aMap, "b");

integer aValue = aMap["a"]; // 1
integer bValue = aMap["b"]; // null
integer cValue = aMap["c"]; // 3
```

**See also:**[append](container-functions-ctl2.md#append), [insert](container-functions-ctl2.md#insert), [poll](container-functions-ctl2.md#poll), [push](container-functions-ctl2.md#push)

#### reverse

```ctl
list[<element type>] reverse(list[<element type>] arg);
variant reverse(variant arg);
```

Reverses the order of elements of the given list and returns the modified list.

If the argument is `null`, the function fails with an error.

The variant version fails if the argument is not a list.

**Compatibility**

The `reverse(list[E])` function is available since **CloverETL 3.1.2**.

The `reverse(variant)` function is available since **CloverDX 5.7.0**.
Example 273. Usage of reverse

```ctl
// list:
list[string] originalList = ["a", "b", "c", "d"];
list[string] modifiedList = reverse(originalList);
// both originalList and modifiedList are now ["d", "c", "b", "a"]

// variant:
variant varList = [["a"], ["b", "c"], ["ab"], ["c", "d"]];
variant varModified = reverse(varList);
// both varList and varModified are now [["c", "d"], ["ab"], ["b", "c"], ["a"]]
```

**See also:**[sort](container-functions-ctl2.md#sort), String functions: [reverse(string)](string-functions-ctl2.md#reverse)

#### sort

```ctl
<element type>[] sort(<element type>[] arg);
```

The `sort()` function sorts the elements of a given list in ascending order according to their values and returns such new value of the list specified as the first argument.

Null values are listed at the end of the list, if present.

If a given list has a `null` reference, the function fails with an error.

**Compatibility**

The `sort()` function is available since **CloverETL 3.0.0**.
Example 274. Usage of sort The function `sort(["a", "e", "c"])` returns `["a", "c", "e"]`.
**See also:**[reverse(list)](container-functions-ctl2.md#reverse)

#### toMap

```ctl
map[<type of key>,<type of value>] toMap(<type of key>[] keys, <type of value>[] values);
map[<type of key>,<type of value>] toMap(<type of key>[] keys, <type of value> value);
```

The function `toMap(k[], v[])` converts a list of `keys` and lists of `values` to the map. The function `toMap(k[], v)` converts a list of `keys` and `value` to the map.

The `keys` is a list containing the keys of the returned map.

The `values` is a list of values corresponding to the keys. If only one `value` is defined, the `value` corresponds to all keys in the returned map.

The data types of list of keys must correspond to the data type of key in the map, the data type(s) of value(s) must correspond to the data type of values in the map.

The length of the list of keys (`keys` argument) must be equal to the length of list of the values (`values` argument).

If the parameter `keys` is `null`, the function fails.

If the parameter `values` is `null`, the function `toMap(<type of key>[],<type of value>[])` fails.

If the parameter `value` is null, the function `toMap(<type of key>[],<type of value>)` returns a map having `null` for all keys.

**Compatibility**

The `toMap()` function is available since **CloverETL 4.0.0**.
Example 275. Usage of toMap

```ctl
string[] alphaValues = ["alpha", "bravo", "charlie", "delta"];
    string[] abcKeys = ["a", "b", "c", "d"];
    map[string, string] alphabet = toMap(abcKeys, alphaValues);
```

The map `alphabet` has the value `alpha` accessible under the key `"a"`, `bravo` accessible under the key `"b"`, etc.

```ctl
string[] alphaValues = ["alpha", "bravo", "charlie", "delta"];
    string[] abcKeys = ["a", "b", "c"];
    map[string, string] alphabet = toMap(abcKeys, alphaValues);
```

The function `toMap()` in this example fails as the list of keys (`abcKeys`) and the list of values (`alphaValues`) are of the different size.

```ctl
string[] s = null;
    map[string, string] result = toMap(abcKeys, s);
```

The function `toMap()` fails in this example. The list of values cannot be `null`.

```ctl
string[] keys;
    string[] values;
    map[string, string] result = toMap(keys, values);
```

The `result` is an empty map. The second argument of the function is a single value; therefore, it can be `null`.

```ctl
string[] products = ["ProductA", "ProductB", "ProductC"];
    map[string, string] availability = toMap(products, "available");
```

The variable `availability` contains `{ ProductA=available, ProductB=available, ProductC=available }`. All products all available.

```ctl
string[] keys = ["a", "b", "c"];
    string val = null;
    map[string, string] result = toMap(keys, val);
```

The map `result` has three values: `{ a=null, b=null, c=null }`.

```ctl
string[] keys;
    string valueNull = null;
    map[string, string] result = toMap(keys, valueNull);
```

The `result` is an empty list.

**See also:**[getKeys](container-functions-ctl2.md#getkeys), [getValues](container-functions-ctl2.md#getvalues), [record2map](conversion-functions-ctl2.md#record2map)
