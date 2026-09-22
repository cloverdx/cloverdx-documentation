<!-- Development > Component reference > Transformers > DataIntersection -->

### DataIntersection

![DataIntersection 64x64](../figures/DataIntersection-64x64.png)

| [Short description](dataintersection.md#short-description) |
| --- |
| [Ports](dataintersection.md#ports) |
| [Metadata](dataintersection.md#metadata) |
| [DataIntersection attributes](dataintersection.md#dataintersection-attributes) |
| [Details](dataintersection.md#details) |
| [Best practices](dataintersection.md#best-practices) |
| [See also](dataintersection.md#see-also) |

#### Short description

**DataIntersection** intersects data from two inputs.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **✓** | 2 | 3 | **✓** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records (data flow A). | Any(In0)[[1]](dataintersection.md#dataintersection-ports-fn01) |
| 1 | **✓** | For input data records (data flow B). | Any(In1)[[1]](dataintersection.md#dataintersection-ports-fn01) |  |
| Output[[2]](dataintersection.md#dataintersection-ports-fn02) | 0 | **⨯** | For not-changed output data records (contained in flow A only). | Input 0 |
| 1 | **⨯** | For changed output data records (contained in both input flows) | Any (Out1) |  |
| 2 | **⨯** | For not-changed output data records (contained in flow B only). | Input 1 |  |

| 1 |  Part of them must be equivalent and comparable (**Join key**). |
| --- | --- |

| 2 |  At least one output port of the three provided is required. |
| --- | --- |

#### Metadata

The component propagates metadata from input port 0 to output port 0; from left to right or from right to left.

The component propagates metadata from input port 1 to output port 2; from left to right or from right to left.

The component does not propagate metadata to the output port 1 (the middle one).

Metadata on the **first** output port of **DataIntersection** component must have the same field names and field types as metadata on the **first** input port.

Metadata on the **third** output port of **DataIntersection** component must have the same field names and field types as metadata on the **second** input port.

#### DataIntersection attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Join key | yes | A key that compares data records from input ports. Only those pairs of records (one from each input) with equal value of this attribute are sent to a transformation. For more information, see [Join key](dataintersection.md#join-key-for-dataintersection). Records should be sorted in ascending order to get reasonable results. |  |
| Transform | [[1]](dataintersection.md#dataintersection-attributes-fn01) | A definition of the way how records should be intersected written in the graph in CTL or Java. |  |
| Transform URL | [[1]](dataintersection.md#dataintersection-attributes-fn01) | The name of an external file, including the path, containing the definition of the way how records should be intersected written in CTL or Java. |  |
| Transform class | [[1]](dataintersection.md#dataintersection-attributes-fn01) | The name of an external class defining the way how records should be intersected. |  |
| Transform source charset |  | Encoding of an external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | E.g. UTF-8 |
| Equal NULL |  | By default, records with null values of key fields are considered to be equal. If set to `false`, they are considered to be different from each other. | true (default) \| false |
| Advanced |  |  |  |
| Allow key duplicates |  | By default, all duplicates on inputs are allowed. If switched to `false`, records with duplicate key values are not allowed. If set to `false`, only the **first** record is used for join. | true (default) \| false |
| Deprecated |  |  |  |
| Error actions |  | Definition of the action that should be performed when the specified transformation returns an error code. See [Return values of transformations](transformations.md#return-values-of-transformations). |  |
| Error log |  | A URL of the file to which error messages for specified **Error actions** should be written. If not set, they are written to **Console**. |  |
| Slave override key |  | An older form of **Join key**. Contains fields from the second input port only. This attribute is deprecated now and we suggest you use the current form of the **Join key** attribute. |  |

| 1 |  |
| --- | --- |

 One of these must be specified. Any of these transformation attributes uses a CTL template for **DataIntersection** or implements a `RecordTransform` interface.

For more information, see [CTL scripting specifics](dataintersection.md#ctl-scripting-specifics) or [Java interfaces for DataIntersection](dataintersection.md#java-interfaces-for-dataintersection).

For detailed information about transformations, see also [Defining transformations](transformations.md#defining-transformations).

#### Details

**DataIntersection** receives sorted data from two inputs, compares the **Join key** values in both of them and processes the records in the following way:

Such input records that are on both input port 0 and input port 1 are processed according to the user-defined transformation and the result is sent to the output port 1. Such input records that are only on the input port 0 are sent unchanged to the output port 0. Such input records that are only on the input port 1 are sent unchanged to the output port 2.

Records are considered to be on both ports if the values of all **Join key** fields are equal in both of them. Otherwise, they are considered to be records on input 0 or 1 only.

A transformation must be defined if output port 1 is connected. The transformation uses a CTL template for **DataIntersection**, implements a `RecordTransform` interface or inherits from a `DataRecordTransform` superclass. The interface methods are listed below.
> [!NOTE]
> Note that this component is similar to **Joiners**: it does not need identical metadata on its inputs and processes records whose **Join key** is equal. Furthermore, duplicate records can be sent to transformation or not (**Allow key duplicates**).

- **Join key**
  Expressed as a sequence of individual subexpressions separated from each other by a semicolon. Each subexpression is an assignment of a field name from the first input port (prefixed by a dollar sign), on the left side, and a field name from the second input port (prefixed by a dollar sign), on the right side.
  Example 407. Join Key for DataIntersection`$first_name=$fname;$last_name=$lname`
  In this **Join key**, `first_name` and `last_name` are fields of metadata on the first input port and `fname` and `lname` are fields of metadata on the second input port.
  Pairs of records containing the same value of this key on both input ports are transformed and sent to the second output port. Records incoming through the first input port for which there is no counterpart on the second input port are sent to the first output port without being changed. Records incoming through the second input port for which there is no counterpart on the first input port are sent to the third output port without being changed.
> [!NOTE]
> The component may return a number of records different from the original input record number.
>
> If the **Allow key duplicates** is set to `false`, the number of output records may be lower than the number of input records as only the first of records with duplicated key is used.
>
> If the **Allow key duplicates** is set to `true`, the number of output records may be higher than the number of input records. The Cartesian product of records having the same key is created on the output.

#### CTL scripting specifics

When you define any of the three transformation attributes, you must specify a transformation that assigns a number of output port to each input record.

For detailed information about **CloverDX** Transformation Language, see [CTL2 - CloverDX Transformation Language](part5.md). (CTL is a full-fledged, yet simple language that allows you to perform almost any imaginable transformation.)

CTL scripting allows you to specify custom transformation using the simple CTL scripting language.

##### CTL Templates for DataIntersection

**DataIntersection** uses the same transformation template as **Map** and **Joiners**. For more information, see [CTL templates for Joiners](ctl-templates-for-joiners.md).

#### Java interfaces for DataIntersection

**DataIntersection** implements the same interface as **Map** and **Joiners**. For more information, see [Java interfaces for Joiners](java-interfaces-for-joiners.md) and [Public CloverDX API](genericcomponent.md#public-cloverdx-api).

#### Best practices

If the transformation is specified in an external file (with **Transform URL**), we recommend users to explicitly specify **Transform source charset**.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
