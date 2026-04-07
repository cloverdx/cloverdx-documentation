<!-- Development > Component reference > Transformers > Filter -->

### Filter

![ExtFilter 64x64](../figures/ExtFilter-64x64.png)

| [Short description](extfilter.md#short-description) |
| --- |
| [Ports](extfilter.md#ports) |
| [Metadata](extfilter.md#metadata) |
| [Filter attributes](extfilter.md#filter-attributes) |
| [Details](extfilter.md#details) |
| [Examples](extfilter.md#examples) |
| [Compatibility](extfilter.md#compatibility) |
| [See also](extfilter.md#see-also) |

#### Short description

**Filter** component filters input records according to a specified condition.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-2 | - | - | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For allowed data records | Input 0 |
| 1 | **⨯** | For rejected data records | Input 0 |  |

This component has one input port and one or two output ports. The first input port and the first output port are mandatory. The optional second output port can be used for rejected data if it is connected to another component.

#### Metadata

**Filter** has no metadata template.

Metadata can be propagated through this component.

All output metadata must be the same.

#### Filter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Filter expression | [[1]](extfilter.md#extfilter-attributes-fn01) | An expression according to which records are filtered. It is a CTL expression returning boolean. | e.g. `$in.0.field1==2` |
| Advanced |  |  |  |
| Filter class | [[1]](extfilter.md#extfilter-attributes-fn01) | Name of an external class defining which records pass the filter. |  |

| 1 | One of these attributes must be specified. In case both **Filter expression** and **Filter class** is specified, the former will be used. The Java class referenced by the **Filter class** attribute is expected to implement the `RecordFilter` interface. |
| --- | --- |

#### Details

**Filter** receives records through input port and filters them according to a logical expression. It sends all records corresponding to the filter expression to the first output port and all rejected records to the second output port.

Unmatched records are sent to the second output port only if it is connected. If no edge is connected to the second output port, unmatched records are discarded.

##### Filter expression

To configure this component, specify the **Filter expression**. The filter expression can be very simple - just a comparison or a single CTL function returning boolean.

```ctl
//#CTL2
$in.0.count == 1
```

```ctl
//#CTL2
isInteger($in.0.field2)
```

The filter expression can consist of several subexpressions connected with logical operators.

```ctl
//#CTL2
$in.0.isInteger($in.0.count) && $in.0.weightKgs <= 1500
```

To express precedence of particular subexpressions, use parentheses.

```ctl
//#CTL2
( $in.0.weightKgs > 0 && $in.0.weightKgs < 1500 ) || $in.0.product == "C"
```

For these subexpressions, there is a set of functions that can be used and set of comparison operators (greater than, greater than or equal to, less than, less than or equal to, equal to, not equal to). The latter can be selected in the **Filter editor** dialog as the mathematical comparison signs (>, >=, <, <=, ==, !=) or as textual abbreviations (`.gt.`, `.ge.`, `.lt.`, `.le.`, `.eq.`, `.ne.`).

All of the record field values should be expressed by their port numbers preceded by a dollar sign, dot and their names. For example, `$in.0.employeeid`.

##### Components with similar functionality

You can also use the [Partition](partition.md) component as a filter instead of **Filter**. With the [Partition](partition.md) component you can define much more sophisticated filter expressions and distribute data records among more output ports.

Or you can use the [Map](reformat.md) component as a filter.

##### Java interface for filter

Beside filter expression, it is possible to define filtering by Java class implementing `org.jetel.component.RecordFilter` interface. The class requires a default (no arguments) constructor. The interface consists of the following methods:

- `void init()`
  Called before `isValid()` is used.
- `void setTransformationGraph(TransformationGraph)`
  Associates a transformation graph with the filter class instance.
- `boolean isValid(DataRecord)`
  Is called for each incoming data record. The implementor shall answer `true` if the record passes the filter, `false` otherwise.

#### Examples

##### Filtering according to a single field value

This example shows the basic use case of the **Filter**.

The input contains data on the products sold in the last year. We are interested in figures related to one particular product, e.g. pencils. Filter out other products.

The metadata contains **Product**, **Count** and **Location** fields.

```
Pen       | 324 | Edinburgh
Pencil    | 543 | Edinburgh
Sharpener | 54  | Edinburgh
Pen       | 150 | Glasgow
Pencil    | 834 | Glasgow
Pen       | 92  | Stirling
Pencil    | 257 | Stirling
```

###### Solution

Use **Filter**. In the component, specify the **Filter Expression**.

| Attribute | Value |
| --- | --- |
| Filter expression | ```ctl $in.0.Product == "Pencil" ``` |

The following records have been sent to the first output port. Other records have been filtered out.

```
Pencil    | 543 | Edinburgh
Pencil    | 834 | Glasgow
Pencil    | 257 | Stirling
```

Note that comparison with `==` operator is case sensitive.

To compare the strings case-insensitively, convert both operands to the same case first.

```ctl
//#CTL2
lowerCase( $in.0.Product ) == "pencil"
```

See [lowerCase](string-functions-ctl2.md#lowercase) or [upperCase](string-functions-ctl2.md#uppercase).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.5.0-M2 | **ExtFilter** was renamed to **Filter**. |

#### See also

| [Partition](partition.md) |
| --- |
| [Validator](validator.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
