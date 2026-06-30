<!-- Development > Component reference > Transformers > Map -->

### Map

![Map 64x64](../figures/Map-64x64.png)

| [Short description](reformat.md#short-description) |
| --- |
| [Ports](reformat.md#ports) |
| [Metadata](reformat.md#metadata) |
| [Map attributes](reformat.md#map-attributes) |
| [Details](reformat.md#details) |
| [Examples](reformat.md#examples) |
| [Best practices](reformat.md#best-practices) |
| [See also](reformat.md#see-also) |

#### Short description

**Map** manipulates record’s structure or content. This component was formerly called **Reformat**.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-N | **✓** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | for input data records | Any(In0) |
| Output | 0 | **✓** | for transformed data records | Any(Out0) |
| 1-n | **⨯** | for transformed data records | Any(OutPortNo) |  |

This component has one input port and at least one output port.

The component can send different records to different output ports or even send the same data record to more output ports.

#### Metadata

**Map** propagates metadata from the input port to the output port (from left to right), but it does not propagate metadata from the output port to the input port (from right to left).

Metadata propagation through Map has low priority.

#### Map attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Transform | [[1]](reformat.md#reformat-attributes-fn01) | The definition of how records should be mapped. Written in the graph source either in CTL or in Java. |  |
| Transform URL | [[1]](reformat.md#reformat-attributes-fn01) | The name of the external file, including the path, containing the definition of the way how records should be mapped; written in CTL or Java. |  |
| Transform class | [[1]](reformat.md#reformat-attributes-fn01) | The name of an external class defining the way how records should be mapped. |  |
| Transform source charset |  | Encoding of external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | E.g. UTF-8 |
| Deprecated |  |  |  |
| Error actions |  | The definition of an action that should be performed when the specified transformation returns an **Error code**. See [Return values of transformations](transformations.md#return-values-of-transformations). |  |
| Error log |  | The URL of the file to which error messages for specified **Error actions** should be written. If not set, they are written to **Console**. |  |

| 1 |  One of these must be specified. Any of these transformation attributes uses a CTL template for **Map** or implements a `RecordTransform` interface. |
| --- | --- |

For more information, see [CTL scripting specifics](reformat.md#ctl-scripting-specifics) or [Java interfaces for Map](reformat.md#java-interfaces-for-map).

For detailed information about transformations, see also [Defining transformations](transformations.md#defining-transformations).

#### Details

**Map** receives potentially unsorted data through the single input port, transforms each of them in a user-specified way and sends the resulting record to the port(s) specified by the user. Return values of the transformation are numbers of output port(s) to which data record will be sent.

A transformation must be defined. The transformation uses a CTL template for **Map**, implements a `RecordTransform` interface or inherits from a `DataRecordTransform` superclass. The interface methods are listed below.

##### CTL scripting specifics

When you define any of the three transformation attributes, specify a transformation that assigns a number of output port to each input record.

For detailed information about **CloverDX** Transformation Language, see [CTL2 - CloverDX Transformation Language](part5.md). (CTL is a full-fledged, yet simple language that allows you to perform almost any imaginable transformation.)

CTL scripting allows you to specify a custom transformation using the simple CTL scripting language.

##### CTL Templates for Map

**Map** uses the same transformation template as **DataIntersection** and **Joiners**. For more information, see [CTL templates for Joiners](ctl-templates-for-joiners.md).

#### Java interfaces for Map

**Map** implements the same interface as **DataIntersection** and **Joiners**. For more information, see [Java interfaces for Joiners](java-interfaces-for-joiners.md) and [Public CloverDX API](genericcomponent.md#public-cloverdx-api).

#### Examples

| [Using Map to drop field(s)](reformat.md#using-map-to-drop-fields) |
| --- |
| [Splitting the records](reformat.md#splitting-the-records) |
| [Filtering records](reformat.md#filtering-records) |

##### Using Map to drop field(s)

This example shows a way to use **Map** to drop unnecessary metadata fields.

Input metadata contains the **firstname**, **surname** and **address** fields. Output metadata contains the **firstname** and **surname** fields. Drop the **address** field.

###### Solution

In **Map**, specify the **Transform** attribute.

| Attribute | Value |
| --- | --- |
| Transform | ```ctl function integer transform() {     $out.0.firstname = $in.0.firstname;     $out.0.surname = $in.0.surname;      return ALL; } ``` |

You can use `$out.0.* = $in.0.*;` instead of specifying the mapping of particular fields.

##### Splitting the records

This example shows a way to use **Map** to split one record to multiple parts and send each part to a different output port.

Input metadata contains the **ID**, **firstname**, **surname** and **address** fields. Send **ID**, **firstname** and **surname** to the first output port and **ID** and **address** to the second output port.

###### Solution

In **Map**, set the **Transform** attribute.

| Attribute | Value |
| --- | --- |
| Transform | ```ctl function integer transform() {     $out.0.ID = $in.0.ID;     $out.0.firstname = $in.0.firstname; 	$out.0.surname = $in.0.surname;      $out.1.ID = $in.0.ID;     $out.1.address = $in.0.address;      return ALL; } ``` |

##### Filtering records

**Map** can be used as a filter.

Input metadata contains the **ID** and **color** fields. Valid colors are red, green, or blue. Send red items to the first output port; green items to the second output port; and blue items to the third output port. Items without correct color should be send to the fourth output port.

###### Solution

| Attribute | Value |
| --- | --- |
| Transform | ```ctl function integer transform() {     if ( $in.0.color == "red" ) {         $out.0.* = $in.0.*;         return 0;     }     if ( $in.0.color == "green" ) {         $out.1.* = $in.0.*;         return 1;     }     if ( $in.0.color == "blue") {         $out.2.* = $in.0.*;         return 2;     }      $out.3.* = $in.0.*;     return 3; } ``` |

There are components specialized on filtering of records: [Filter](extfilter.md) and [Validator](validator.md).

#### Best practices

##### Use Map To

- Drop unwanted fields
- Validate fields using functions or [regular expressions](language-reference-ctl2.md#regular-expressions)
- Calculate new or modify existing fields
- Convert data types

If the transformation is specified in an external file (with **Transform URL**), we recommend users to explicitly specify **Transform source charset**.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
