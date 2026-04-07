<!-- Development > Component reference > Readers > KafkaCommit -->

### KafkaCommit

![KafkaCommit 64x64](../figures/KafkaCommit-64x64.png)

| [Short description](kafkacommit.md#short-description) |
| --- |
| [Ports](kafkacommit.md#ports) |
| [KafkaCommit attributes](kafkacommit.md#kafkacommit-attributes) |
| [Details](kafkacommit.md#details) |
| [See also](kafkacommit.md#see-also) |

#### Short description

**KafkaCommit** commits processed offsets for Kafka topics.

It must be used in combination with a **KafkaReader** component to commit offsets explicitly, after all the consumed events processing is complete.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| - | 1 | 0 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | Offsets to be committed | KafkaCommitInput |

#### Metadata

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 1 | topic | string | Event topic |
| 2 | partition | string | Event partition |
| 3 | offset | long | Event offset |

The metadata are used in the component’s input mapping. The metadata fields are required to identify the event offset to be committed.

#### KafkaCommit attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Kafka reader component |  | A reference to a reader component which consumes the events to be committed. With only a single **KafkaReader** in the graph, it is auto-detected. With multiple **KafkaReader** components, this attribute is required. | e.g. KafkaReader (id:KAFKA_READER) |
| Commit interval |  | The interval, in which incoming offsets are committed. | e.g. 500ms \| 3s \| 1m |
| Input mapping |  | Defines the mapping of input metadata fields to **KafkaCommit** fields. |  |

#### Details

In Kafka, reading normally starts from the last committed offset. Committing an offset means that the event with this offset is marked as already consumed/processed.

The default behavior of **KafkaReader** is to auto-commit consumed events periodically.

To have a better control over when the offsets are actually committed, you may use the **KafkaCommit** component.

**KafkaCommit** has to be used in pair with a reader component, as it is the reader that consumes the events to be committed. To identify the reader, it has to be specified in the **Kafka reader component** property. In case there is only one reader component in the graph, it is auto-detected.

If the input port is not connected, consumed offsets in the paired reader can be committed in a one-time fashion. In this case, the **KafkaCommit** component should be in a later graph phase than the reader itself.

When the input port is connected, the offsets (uniquely identified by topic, partition and offset) sent over the input edge are committed periodically.

##### Notes and limitations

It is not possible to pair **KafkaCommit** with a reader component from another graph (job).

Similarily to **KafkaReader**, it is not possible to achieve atomic committing of each incoming offset, as committing is performed periodically. It can be beneficial to lower the commit interval, but keeping it too low is not recommended as it vastly increases read/write load on the Kafka cluster.

#### See also

| [KafkaReader](kafkareader.md) |
| --- |
| [KafkaWriter](kafkawriter.md) |
| [Kafka connections](kafka-connections.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |

##### External links

*[https://kafka.apache.org/documentation/#consumerapi](https://kafka.apache.org/documentation/#consumerapi)*

*[https://kafka.apache.org/documentation/#consumerconfigs](https://kafka.apache.org/documentation/#consumerconfigs)*
