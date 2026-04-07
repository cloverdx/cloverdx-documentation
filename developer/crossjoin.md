<!-- Development > Component reference > Joiners > CrossJoin -->

### CrossJoin

![CrossJoin 64x64](../figures/CrossJoin-64x64.png)

| [Short description](crossjoin.md#short-description) |
| --- |
| [Ports](crossjoin.md#ports) |
| [Metadata](crossjoin.md#metadata) |
| [CrossJoin attributes](crossjoin.md#crossjoin-attributes) |
| [Details](crossjoin.md#details) |
| [Examples](crossjoin.md#examples) |
| [Best practices](crossjoin.md#best-practices) |
| [Compatibility](crossjoin.md#compatibility) |
| [See also](crossjoin.md#see-also) |

#### Short description

**CrossJoin** creates a Cartesian product of records from connected input ports.

| Same input metadata | Sorted inputs | Slave inputs | Outputs | Output for driver without slave | Output for slaves without driver | Joining based on equality | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 0-n | 1 | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | Master input port | Any1 |
| 1-n | **⨯** | Slave input port(s) | Any2 |  |
| Output | 0 | **✓** | For output data records | Any3 |

#### Metadata

**CrossJoin** automatically generates metadata on the output port from metadata on its input ports. The generated metadata can be seen as a dynamic template.

#### CrossJoin attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Advanced |  |  |  |
| Transform | [[1]](crossjoin.md#crossjoin-attributes-fn01) | A transformation in CTL or Java defined in the graph. |  |
| Transform URL | [[1]](crossjoin.md#crossjoin-attributes-fn01) | An external file defining the transformation in CTL or Java. |  |
| Transform class | [[1]](crossjoin.md#crossjoin-attributes-fn01) | An external transformation class. |  |
| Transform source charset |  | Encoding of an external file defining the transformation. | e.g. UTF-8 |

| 1 | At most one of these attributes can be set. |
| --- | --- |

#### Details

**CrossJoin** creates a Cartesian product of input records.

It works in the following way: the component takes the first record from the first port, the first record from the second port (…​) and the first record from the last port and generates the output record. Subsequently, it takes the first record from the first port, the first record from the second port (…​) and the **second** record from the last port. It continues with the third record from the last input port and so on.

##### Processing Large Number of Records

If you process a very large number of records, temporary files with the swapped records may be created on your hard drive. This prevents excessive memory usage.

#### Examples

##### Simple CrossJoin example

Given a list of customers and a list of products of "All on the Store Ltd."

Customers:

```
Brown
Smith
Jones
```

Goods:

```
Pineapple
Turnip
Spaceship
```

Create a list containing all possibilities.

###### Solution

You only need to connect sources of data with **CrossJoin** component. No setup of attributes of the component is necessary.

The result is

```
Brown|Pineapple
Brown|Turnip
Brown|Spaceship
Smith|Pineapple
Smith|Turnip
Smith|Spaceship
Jones|Pineapple
Jones|Turnip
Jones|Spaceship
```

#### Best practices

The edge giving the most records should be connected to the first input port.

If the transformation is specified in an external file (with **Transform URL**), we recommend users to explicitly specify **Transform source charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | The **CrossJoin** component is available since **4.1.0-M1**. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Joiners comparison](common-of-joiners.md#joiners-comparison) |
