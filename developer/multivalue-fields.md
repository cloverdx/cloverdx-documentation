<!-- Development > Job elements > Metadata > Multivalue fields -->

### Multivalue fields

| [Lists and maps support in components](multivalue-fields.md#lists-and-maps-support-in-components) |
| --- |
| [Joining on multivalue fields (comparison rules)](multivalue-fields.md#joining-on-multivalue-fields-comparison-rules) |

Each metadata field commonly stores only one value, e.g. one integer, one string, one date, etc. However, you can also set one field to carry more values *of the same type*.
Example 10. Example situations when you could take advantage of multivalue fields
- A record containing an employee’s `ID`, `Name` and `Address`. Since employees move from time to time, you might need to keep track of all their addresses, both current and past. Instead of creating new metadata fields each time an employee moves to a new address, you can store a **list** of all addresses into one field.
- You are processing an input stream of `CSV` files, each containing a different column count. Normally, that would imply creating new metadata for each file (each column count). Instead, you can define a generic **map** or **variant** in metadata and append fields to it each time they occur.

As implied above, there are three types of structures:

**list** - is a set containing elements of a given data type (any you want). In source code, lists are marked by the [] brackets, for example:

```ctl
integer[] list1 = [1, 367, -1, 20, 5, 0, -79]; // a list of integer elements
boolean[] list2 = [true, false, randomBoolean()]; // a list of three boolean elements
string[] list3; // a just-declared empty list to be filled by strings
```

**map** - is a pair of keys and their values. A key is always a `string` while a value can be any data type - but you cannot mix them (remember a map holds values *of the same type*). Example:

```ctl
map[string, date] dateMap; // declaration

// filling the map with values
dateMap["a"] = 2011-01-01;
dateMap["b"] = 2012-12-31;
dateMap["c"] = randomDate(2011-01-01,2012-12-31);
```

**variant** - can contain any data type or complex data structure including **list** or **map**.

```ctl
variant myVariant = {}; // declaration, variant containing empty map
integer[] ordersList = [1, 15, 63]; // declaration, list of integers

// filling the variant with values
myVariant["name"] = "John Doe";
myVariant["dateOfBirth"] = 2012-12-31;
myVariant["isCustomer"] = true;
myVariant["orderIds"] = ordersList;
```

For more information about maps, lists and variants, see [Data types in CTL2](language-reference-ctl2.md#data-types-in-ctl2).
> [!IMPORTANT]
> To change a field from single-value to list/map:
>
> 1. Go to **Metadata Editor**.
> 2. Click a field or create a new one.
> 3. In **Property** ****Basic**, switch **Container Type** either to **list** or **map**. (You will see an icon appears next to the field **Type** in the left hand record pane.)

#### Lists and maps support in components

An alphabetically sorted list of components which you can use multivalue fields in:

| Component | List | Map | Variant | Note |
| --- | --- | --- | --- | --- |
| [CloverDataReader](cloverreader.md) | **✓** | **✓** | **✓** |  |
| [CloverDataWriter](cloverwriter.md) | **✓** | **✓** | **✓** |  |
| [Concatenate](concatenate.md) | **✓** | **✓** | **✓** |  |
| [DataGenerator](datagenerator.md) | **✓** | **✓** | **✓** |  |
| [DataIntersection](dataintersection.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not a part of key |  |
| [DBJoin](dbjoin.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not a part of key |  |
| [Dedup](dedup.md) | **✓** | **⨯** | **⨯** | Sorted input |
| **✓** | **⨯** | **✓** | Unsorted input |  |
| **✓** | **✓** | **✓** | Map is not a part of key |  |
| [Denormalizer](denormalizer.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not a part of key |  |
| [ExtHashJoin](exthashjoin.md) | **✓** | **⨯** | **✓** |  |
| **✓** | **✓** | **✓** | Map is not a part of key |  |
| [ExtMergeJoin](extmergejoin.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not a part of key. |  |
| [ExtSort](extsort.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not a part of key. |  |
| [Filter](extfilter.md) | **✓** | **✓** | **✓** |  |
| [JavaBeanReader](beanreader.md) | **✓** | **⨯** | **✓** |  |
| [JavaBeanWriter](beanwriter.md) | **✓** | **⨯** | **⨯** |  |
| [JavaMapWriter](mapwriter.md) | **✓** | **✓** | **⨯** |  |
| [JSONExtract](jsonextract.md) | **✓** | **⨯** | **✓** |  |
| [JSONReader](jsonreader.md) | **✓** | **⨯** | **⨯** |  |
| [JSONWriter](jsonwriter.md) | **✓** | **⨯** | **✓** |  |
| [LookupJoin](lookupjoin.md) | **✓** | **✓** | **✓** |  |
| [LookupTableReaderWriter](lookuptablereaderwriter.md) | **✓** | **✓** | **✓** |  |
| [Merge](merge.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not part of key |  |
| [Normalizer](normalizer.md) | **✓** | **✓** | **✓** |  |
| [ParallelMerge](clustermerge.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not part of key |  |
| [ParallelPartition](clusterpartition.md) | **✓** | **✓** | **✓** | Round robin |
| **⨯** | **⨯** | **⨯** | Ranges |  |
| **✓** | **⨯** | **✓** | Partition key |  |
| **✓** | **✓** | **✓** | Partition class |  |
| [ParallelSimpleGather](clustersimplegather.md) | **✓** | **✓** | **✓** |  |
| [Partition](partition.md) | **✓** | **✓** | **✓** | Round robin |
| **⨯** | **⨯** | **⨯** | Ranges |  |
| **✓** | **⨯** | **✓** | Partition key |  |
| **✓** | **✓** | **✓** | Partition class |  |
| [Map](reformat.md) | **✓** | **✓** | **✓** |  |
| [RelationalJoin](relationaljoin.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not part of key |  |
| [Rollup](rollup.md) | **✓** | **⨯** | **⨯** | Sorted input |
| **✓** | **⨯** | **✓** | Unsorted input |  |
| **✓** | **✓** | **✓** | Map is not part of key |  |
| [SequenceChecker](sequencechecker.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not part of key |  |
| [SimpleCopy](simplecopy.md) | **✓** | **✓** | **✓** |  |
| [SimpleGather](simplegather.md) | **✓** | **✓** | **✓** |  |
| [Sleep](sleep.md) | **✓** | **✓** | **✓** |  |
| [SortWithinGroups](sortwithingroups.md) | **✓** | **⨯** | **⨯** |  |
| **✓** | **✓** | **✓** | Map/Variant is not part of key |  |
| [XMLExtract](xmlextract.md) | **✓** | **⨯** | **⨯** |  |
| [XMLReader](xmlreader.md) | **✓** | **⨯** | **⨯** |  |
| [XMLWriter](extxmlwriter.md) | **✓** | **✓** | **⨯** |  |

At the moment, `map`, `list` and `variant` structures cannot be extracted as metadata from flat files.

#### Joining on multivalue fields (comparison rules)

You can specify fields that are lists, maps or variants as **Join keys** (see [Join types](join-types.md)) just like any other fields. The only question is when two fields are equal.

A list/map/variant can:

- be `null` - its value is not specified;
  ```ctl
  map[string, date] myMap; // a just-declared map - no keys, no values
  ```
- contain empty elements
  ```ctl
  string[] myList = ["hello", ""]; // a list whose second element is empty
  ```
- contain *n* elements - an ordinary case described, e.g. in [Example situations when you could take advantage of multivalue fields](multivalue-fields.md#example-multivalue-fields)
- variant can contain a single value or a multivalue type
  ```ctl
  variant singleValue = "hello"; // variant containing string
  variant multiValue = ["hello", "world"]; // variant containing list of strings
  ```

**Two maps/lists/variants are equal if** both of them are not `null`, they have the same data type, element count and all element values (keys-values in maps) are equal.

**Two maps/lists/variants are not equal if** either of them is `null`.
> [!IMPORTANT]
> When comparing two lists, the order of their elements has to match, too. In maps and variants, there is no 'order' of elements, therefore you cannot use them in **Sort key**.
Example 11. Integer lists which are (not) equal - symbolic notation

```ctl
[1,2] == [1,2]
[null] != [1,2]
[1] != [1,2]
null != null // two unspecified lists
[null] == [null] // an extra case: lists which are not empty but whose elements are null
```
