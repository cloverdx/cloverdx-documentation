<!-- Development > Component reference > Joiners > DBJoin -->

### DBJoin

![DBJoin 64x64](../figures/DBJoin-64x64.png)

| [Short description](dbjoin.md#short-description) |
| --- |
| [Ports](dbjoin.md#ports) |
| [Metadata](dbjoin.md#metadata) |
| [DBJoin attributes](dbjoin.md#dbjoin-attributes) |
| [Details](dbjoin.md#details) |
| [Examples](dbjoin.md#examples) |
| [Best practices](dbjoin.md#best-practices) |
| [Compatibility](dbjoin.md#compatibility) |
| [See also](dbjoin.md#see-also) |

#### Short description

**DBJoin** receives data through a single input port and joins it with data from a database table. These two data sources can potentially have different metadata structures.

| Same input metadata | Sorted inputs | Slave inputs | Outputs | Output for drivers without slave | Output for slaves without driver | Joining based on equality | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 1 (virtual) | 1-2 | **✓** | **⨯** | **✓** | **✓** |

#### Ports

After the data from an input port and database table are joined, they are sent to the first output port. The second output port can optionally be used to capture unmatched master records.

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | Master input port | Any |
| 1 (virtual) | **✓** | Slave input port | Any |  |
| Output | 0 | **✓** | Output port for the joined data | Any |
| 1 | **⨯** | The optional output port for master data records without slave matches. (Only if the **Join type** attribute is set to `Inner join`.) This applies only to **LookupJoin** and **DBJoin**. | Input 0 |  |

#### Metadata

**DBJoin** propagates metadata from the first input port to the second output port and vice versa.

**DBJoin** has no metadata template.

If mapping is not defined, **DBJoin** requires output metadata to match metadata of a query result. If mapping is defined, metadata of a query result must match metadata defined in the **DBJoin** attribute.

#### DBJoin attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Join key | yes | Key according to which the incoming data flows are joined. See [Join key](dbjoin.md#join-key). |  |
| Left outer join |  | If set to `true`, driver records without corresponding slave are parsed, as well. Otherwise, `inner join` is performed. | false (default) \| true |
| DB connection | yes | The ID of a DB connection to be used as a resource of slave records. |  |
| DB metadata |  | The ID of DB metadata to be used. If not set, metadata is extracted from a database using an **SQL query**. |  |
| Query URL | [[1]](dbjoin.md#dbjoin-attributes-fn-queryurl) | The name of an external file, including the path, defining an SQL query. |  |
| SQL query | [[1]](dbjoin.md#dbjoin-attributes-fn-queryurl) | The SQL query defined in a graph. |  |
| Transform | [[2]](dbjoin.md#dbjoin-attributes-fn02)[[3]](dbjoin.md#dbjoin-attributes-fn03) | Transformation in CTL or Java defined in the graph. |  |
| Transform URL | [[2]](dbjoin.md#dbjoin-attributes-fn02)[[3]](dbjoin.md#dbjoin-attributes-fn03) | An external file defining the transformation in CTL or Java. |  |
| Transform class | [[2]](dbjoin.md#dbjoin-attributes-fn02)[[3]](dbjoin.md#dbjoin-attributes-fn03) | An external transformation class. |  |
| Cache size |  | The maximum number of records with different key values that can be stored in memory. | 100 (default) |
| Advanced |  |  |  |
| Transform source charset |  | Encoding of an external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | E.g. UTF-8 |
| Deprecated |  |  |  |
| Error actions |  | The definition of an action that should be performed when the specified transformation returns an **Error code**. See [Return values of transformations](transformations.md#return-values-of-transformations). |  |
| Error log |  | A URL of the file to which error messages for specified **Error actions** should be written. If not set, they are written to **Console**. |  |

| 1 |  One of these attributes must be specified. If both are defined, **Query URL** has the highest priority. |
| --- | --- |

| 2 |  One of these transformation attributes should be set. Any of them must use a common CTL template for **Joiners** or implement a `RecordTransform` interface. |
| --- | --- |

For more information, see [CTL scripting specifics](dbjoin.md#ctl-scripting-specifics) or [Java interfaces](dbjoin.md#java-interfaces).

For detailed information about transformations, see also [Defining transformations](transformations.md#defining-transformations).

| 3 |  A unique exception is the case when none of these three attributes are specified, but the **SQL query** attribute defines what records will be read from the DB table. Values of **Join key** contained in the input records serve to select the records from db table. These are unloaded and sent unchanged to the output port without any transformation. |
| --- | --- |

#### Details

| [Join key](dbjoin.md#join-key) |
| --- |
| [Transformation](dbjoin.md#transformation) |

**DBJoin** receives data through a single input port and joins it with data from a database table. These two data sources can potentially have different metadata structure. It is a general purpose joiner usable in most common situations. It does not require the input to be sorted and is very fast as data is processed in memory.

The data attached to the first input port is called **master**, the second data source is called **slave**. Its data is considered as if it were incoming through the second (virtual) input port. Each master record is matched to the slave record on one or more fields known as a join key. The output is produced by applying a transformation that maps joined inputs to the output.

##### Join key

**Join key** is a sequence of field names from a master data source separated from each other by a semicolon, colon, or pipe. You can define the key in the **Edit key** wizard.

The order of these field names must correspond to the order of the key fields from the database table (and their data types). The slave part of **Join key** must be defined in the **SQL query** attribute.

One of the query attributes must contain the expression of the following form: `... where field_K=? and field_L=?`.
Example 397. Join key for DBJoin

```ctl
$first_name;$last_name
```

This is the master part of fields that should serve to join master records with slave records.

The **SQL query** must contain an expression that can look like this:

```ctl
... where fname=? and lname=?
```

Corresponding fields will be compared and matching values will serve to join master and slave records.

##### Transformation

The transform in **DBJoin** lets you define a transformation that sends records to the first output port. The unjoined master records sent to the second output port cannot be modified within the **DBJoin** transformation.

#### CTL scripting specifics

All **Joiners** share the same transformation template which can be found in [CTL templates for Joiners](ctl-templates-for-joiners.md).

For detailed information about **CloverDX** Transformation Language, see [CTL2 - CloverDX Transformation Language](part5.md).

#### Java interfaces

If you define your transformation in Java, it must implement the following interface that is common for all **Joiners**:

[Java interfaces for Joiners](java-interfaces-for-joiners.md)

See [Public CloverDX API](genericcomponent.md#public-cloverdx-api).

#### Examples

##### Joining on Exact Key

Input records contain one field `customerId` with values:

```
1
35535
255
```

The `customers` database table has the following structure and data:

```
customer_id | customer_name | customer_surname
 1          | John          | Doe
 3          | Anna          | Smith
10          | Jane          | Brown
```

Join incoming records with data from the database on `customerId`.

###### Solution

Create input metadata with one field `customerId` (`integer`) and output metadata with the `customerId (integer)`, `customerName (string)`, `customerSurname (string)` fields.

Set the **Join key** and **SQL query** attributes of **DBJoin**.

| Attribute | Value |
| --- | --- |
| Join key | customerId |
| DBConnection | Your DBConnection |
| SQL query | select * from "customers" where customer_id=? |

Only records with `customerId` found in the database are sent to output.

##### Matching Range

Input records contain a product code and date of order.

```
productCode | orderDate
1           | 2015-10-20
2           | 2015-10-30
1           | 2015-11-06
```

Price of a particular product on particular date can be found in the database.

```
productCode | dateFrom   | dateTo     | price
1           | 2014-01-01 | 2015-10-31 |  10.99
1           | 2015-11-01 | 2099-12-31 |  14.99
2           | 2015-07-01 | 2099-12-31 | 109.99
```

Match the price to particular product orders.

###### Solution

Create input metadata (productCode, orderDate), output metadata (productCode, orderDate, price) and metadata for DBJoin ( productCode, price).

Set attributes:

| Attribute | Value |
| --- | --- |
| Join key | product;orderDate;orderDate |
| Metadata | DBJoinMetadata |
| DBConnection | Your DBConnection |
| SQL query | select product_id,price_per_unit from "dbjoin_example_02" where product_id=? and valid_from<=? and ?<=valid_to |
| Transform | See the code below. |

```ctl
//#CTL2

function integer transform() {
    $out.0.* = $in.0.*;
    $out.0.* = $in.1.*;

    return ALL;
}
```

#### Best practices

If the transformation is specified in an external file (with **Transform URL**), we recommend users to explicitly specify **Transform source charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.2.0-M1 | **DBJoin** now propagates metadata between the first input port and the second output port. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Joiners](common-of-joiners.md) |
| [Joiners comparison](common-of-joiners.md#joiners-comparison) |
| [DBExecute](dbexecute.md) |
