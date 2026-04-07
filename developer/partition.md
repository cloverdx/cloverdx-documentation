<!-- Development > Component reference > Transformers > Partition -->

### Partition

![Partition 64x64](../figures/Partition-64x64.png)

| [Short description](partition.md#short-description) |
| --- |
| [Ports](partition.md#ports) |
| [Metadata](partition.md#metadata) |
| [Partition attributes](partition.md#partition-attributes) |
| [Details](partition.md#details) |
| [CTL interface](partition.md#ctl-interface) |
| [Java interface](partition.md#java-interface) |
| [Examples](partition.md#examples) |
| [Best practices](partition.md#best-practices) |
| [See also](partition.md#see-also) |

#### Short description

**Partition** distributes individual input data records among different output ports.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-n | [[1]](partition.md#partition-component-fn01) | [[1]](partition.md#partition-component-fn01) | **✓** |

| 1 |  **Partition** can use either a transformation or two other attributes (**Ranges** and/or **Partition key**). |
| --- | --- |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **✓** | For output data records | Input 0 |
| 1-N | **⨯** | For output data records | Input 0 |  |

#### Metadata

Partition propagates metadata in both directions. Partition does not change priority of propagated metadata.

**Partition** has no metadata template.

Input and output fields can have any data types.

Metadata on input and output ports cannot differ. (Input and output records can have different names but the metadata fields of both records must be identical.)

#### Partition attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Partition | [[1]](partition.md#partition-attributes-fn01) | Definition of the way how records should be distributed among output ports written in the graph in CTL or Java. |  |
| Partition URL | [[1]](partition.md#partition-attributes-fn01) | The name of the external file, including the path, containing the definition of the way how records should be distributed among output ports written in CTL or Java. |  |
| Partition class | [[1]](partition.md#partition-attributes-fn01) | The name of the external class defining the way how records should be distributed among output ports. |  |
| Ranges | [[1]](partition.md#partition-attributes-fn01) [[2]](partition.md#partition-attributes-fn02) | Ranges expressed as a sequence of individual ranges separated from each other by a semicolon. Each individual range is a sequence of intervals for some set of fields that are adjacent to each other without any delimiter. It is expressed also whether the minimum and maximum margin is included in the interval or not by a bracket and parenthesis, respectively. Example of **Ranges**: `<1,9)(,31.12.2008);<1,9)<31.12.2008,);<9,)(,31.12.2008);<9,)<31.12.2008)`. |  |
| Partition key | [[1]](partition.md#partition-attributes-fn01)  [[2]](partition.md#partition-attributes-fn02) | Key according to which input records are distributed among different output ports. Expressed as a sequence of individual input field names separated from each other by a semicolon. Example of **Partition key**: `first_name;last_name`. |  |
| Advanced |  |  |  |
| Partition source charset |  | Encoding of the external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | UTF-8 \| other encoding |
| Deprecated |  |  |  |
| Locale |  | Locale to be used when internationalization is set to `true`. By default, system value is used unless the value of **Locale** specified in the `defaultProperties` file is uncommented and set to the desired **Locale**. For more information on how **Locale** may be changed in the `defaultProperties`, see [Engine configuration](../admin/designer-configuration.md#engine-configuration). | system value or specified default value (default) \| other locale |
| Use internationalization |  | By default, no internationalization is used. If set to `true`, sorting according to national properties is performed. | false (default) \| true |

| 1 |  If one of these transformation attributes is specified, both **Ranges** and **Partition key** will be ignored since they have lesser priority. |
| --- | --- |

| 2 |  If no transformation attribute is defined, **Ranges** and **Partition key** are used in one of the three ways as described in details. |
| --- | --- |

#### Details

To distribute data records, user-defined transformation, ranges of **Partition key** or RoundRobin algorithm may be used. In this component, no mapping may be defined since it does not change input data records. It only distributes them unchanged among output ports.

Transformation uses a CTL template for **Partition** or implements a `PartitionFunction` interface. Its methods are listed below.

If no transformation attribute is defined, **Ranges** and **Partition key** are used in one of following ways:

- Both **Ranges** and **Partition key** are set.
  The records in which the values of the fields are inside the margins of specified range will be sent to the same output port. The number of the output port corresponds to the order of the range within all values of the fields.
- **Ranges** are not defined. Only **Partition key** is set.
  Records will be distributed among output ports in such a way that all records with the same values of **Partition key** fields will be sent to the same port.
  The output port number will be determined as the hash value computed from the key fields modulo the number of output ports.
- Neither **Ranges** nor **Partition key** are defined.
  RoundRobin algorithm will be used to distribute records among output ports.
> [!TIP]
> Note that you can use the **Partition** component as a filter similarly to **Filter**. With the **Partition** component, you can define much more sophisticated filter expressions and distribute input data records among more than 2 outputs.
>
> Neither **Partition** nor **Filter** allow to modify records.
> [!IMPORTANT]
> **Partition** is a high-performance component, thus you cannot modify input and output records - it would result in an error. If you need to do so, consider using **Map** instead.

#### CTL interface

| [CTL templates for partition (or ParallelPartition)](partition.md#ctl-templates-for-partition-or-parallelpartition) |
| --- |
| [Access to input and output fields](partition.md#access-to-input-and-output-fields) |

Transformation in CTL can be specified in the **Partition** or **Partition URL** attributes.

##### CTL templates for Partition (or ParallelPartition)

This transformation template is used in **Partition**, and **ParallelPartition**.

You can convert existing transformation in CTL to Java language code using the button at the upper right corner of the tab.

You can open the transformation definition as another tab of a graph (in addition to the **Graph** and **Source** tabs of **Graph Editor**) by clicking the corresponding button at the upper right corner of the tab.

| CTL Template Functions |  |
| --- | --- |
| **void init(integer partitionCount)** |  |
| Required | No |
| Description | Initialize the component, setup the environment, global variables. |
| Invocation | Called before processing the first record. |
| Input Parameters | `integer partitionCount` |
| Returns | `void` |
| **integer getOutputPort()** |  |
| Required | yes |
| Input Parameters | none |
| Returns | Integer numbers. For detailed information, see [Return values of transformations](transformations.md#return-values-of-transformations). |
| Invocation | Called repeatedly for each input record. |
| Description | It does not transform the records, it does not change them nor remove them, it only returns integer numbers. Each of these returned numbers is a number of the output port to which individual record should be sent. In **ParallelPartition**, these ports are virtual and mean Cluster nodes.  If `getOutputPort()` fails and user has not defined any `getOutputPortOnError()`, the whole graph will fail.  If any part of the `getOutputPort()` function for some output record causes fail of the `getOutputPort()` function and if the user has defined the function `getOutputPortOnError()`, processing continues in `getOutputPortOnError()` at the place where `getOutputPort()` failed.  The `getOutputPortOnError()` function gets the information gathered by `getOutputPort()` that was get from previously successfully processed code. Also an error message and stack trace are passed to `getOutputPortOnError()`. |
| Example | ```ctl function integer getOutputPort() {     switch (expression) {       case const0 : return 0; break;       case const1 : return 1; break;       ...       case constN : return N; break;       [default : return N+1;]    } } ``` |
| **integer getOutputPortOnError(string errorMessage, string stackTrace)** |  |
| Required | no |
| Input Parameters | `string errorMessage` |
| `string stackTrace` |  |
| Returns | Integer numbers. For detailed information, see [Return values of transformations](transformations.md#return-values-of-transformations). |
| Invocation | Called if `getOutputPort()` throws an exception. |
| Description | It does not transform the records, it does not change them nor remove them, it only returns integer numbers. Each of these returned numbers is a number of the output port to which individual record should be sent. In **ParallelPartition**, these ports are virtual and mean Cluster nodes.  If any part of the `getOutputPort()` function for some output record causes a failure of the `getOutputPort()` function and if the user has defined the function `getOutputPortOnError()`, processing continues in this `getOutputPortOnError()` at the place where `getOutputPort()` failed.  The `getOutputPortOnError()` function gets the information gathered by `getOutputPort()` that was get from previously successfully processed code. Also error message and stack trace are passed to `getOutputPortOnError()`. |
| Example | ```ctl function integer getOutputPortOnError(                     string errorMessage,                     string stackTrace) {    printErr(errorMessage);    printErr(stackTrace); } ``` |
| **string getMessage()** |  |
| Required | No |
| Description | Prints an error message specified and invoked by user. |
| Invocation | Called in any time specified by user (called only when either `getOutputPort()` or `getOutputPortOnError()` returns a value less than or equal to -2). |
| Returns | `string` |
| **void preExecute()** |  |
| Required | No |
| Input parameters | None |
| Returns | `void` |
| Description | May be used to allocate and initialize resources. All resources allocated within this function should be released by the `postExecute()` function. |
| Invocation | Called during each graph run before the transform is executed. |
| **void postExecute()** |  |
| Required | No |
| Input parameters | None |
| Returns | `void` |
| Description | Should be used to free any resources allocated withinthe `preExecute()` function. |
| Invocation | Called during each graph run after the entire transform was executed. |

##### Access to input and output fields

###### Input records or fields

Input records or fields are accessible within the `getOutputPort()` and `getOutputPortOnError()` functions only.

###### Output records or fields

Output records or fields are not accessible at all as records are mapped to the output without any modification and mapping.
> [!WARNING]
> All of the other CTL template functions allow to access neither inputs nor outputs.
>
> Remember that if you do not hold these rules, NPE will be thrown!

#### Java interface

The transformation implements methods of the `PartitionFunction` interface and inherits other common methods from the `Transform` interface. See [Common Java interfaces](transformations.md#common-java-interfaces) and [Public CloverDX API](genericcomponent.md#public-cloverdx-api).

Following are the methods of `PartitionFunction` interface:

- `void init(int numPartitions,RecordKey partitionKey)`
  Called before `getOutputPort()` is used. The `numPartitions` argument specifies how many partitions should be created. The `RecordKey` argument is the set of fields composing a key based on which the partition should be determined.
- `boolean supportsDirectRecord()`
  Indicates whether the partition function supports operation on serialized records /aka direct. Returns `true` if the `getOutputPort(ByteBuffer)` method can be called.
- `int getOutputPort(DataRecord record)`
  Returns the port number which should be used for sending data out. For more information about return values and their meaning, see [Return values of transformations](transformations.md#return-values-of-transformations).
- `int getOutputPortOnError(Exception exception, DataRecord record)`
  Returns the port number which should be used for sending data out. Called only if `getOutputPort(DataRecord)` throws an exception.
- `int getOutputPort(ByteBuffer directRecord)`
  Returns the port number which should be used for sending data out. For more information about return values and their meaning, see [Return values of transformations](transformations.md#return-values-of-transformations).
- `int getOutputPortOnError(Exception exception, ByteBuffer directRecord)`
  Returns port number which should be used for sending data out. Called only if `getOutputPort(ByteBuffer)` throws an exception.

#### Examples

| [Simple example](partition.md#simple-example) |
| --- |
| [Partitioning even and odd numbers](partition.md#partitioning-even-and-odd-numbers) |

##### Simple example

Split data into 2 parts. Each part has to contain the same number of records. The number of records can differ by one if the number of input records is odd.

###### Solution

Place the **Partition** component into graph and connect the corresponding edges. No attribute has to be set up.

##### Partitioning even and odd numbers

Partition records according to the value of field `id`. Send record with even id to output port `0` and odd numbers to output port `1`. If id is not known, send record to port `2`.

###### Solution

Use **Partition** attribute.

| Attribute | Value |
| --- | --- |
| Partition | See the code below |

```ctl
//#CTL2

function integer getOutputPort() {
    return $in.0.id % 2;
}

function integer getOutputPortOnError(string errorMessage, string stackTrace) {
    return 2;
}
```

#### Best practices

If the transformation is specified in an external file (**Partition URL**), we recommend the user to explicitly specify **Partition source charset**.

#### See also

| [Filter](extfilter.md) |
| --- |
| [ParallelPartition](clusterpartition.md) |
| [ParallelRepartition](clusterrepartition.md) |
| [LoadBalancingPartition](loadbalancingpartition.md) |
| [SimpleGather](simplegather.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Transformers](common-of-transformers.md) |
| [Transformers comparison](common-of-transformers.md#transformers-comparison) |
