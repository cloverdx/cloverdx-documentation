<!-- Development > Component reference > Readers > KafkaReader -->

### KafkaReader

![KafkaReader 64x64](../figures/KafkaReader-64x64.png)

| [Short description](kafkareader.md#short-description) |
| --- |
| [Ports](kafkareader.md#ports) |
| [Metadata](kafkareader.md#metadata) |
| [KafkaReader attributes](kafkareader.md#kafkareader-attributes) |
| [Details](kafkareader.md#details) |
| [Examples](kafkareader.md#examples) |
| [See also](kafkareader.md#see-also) |

#### Short description

**KafkaReader** reads events (messages) from a Kafka cluster.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Kafka cluster | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | Consumed Kafka events | KafkaMetadata |

#### Metadata

**KafkaReader** does not propagate metadata.

**KafkaReader** has a metadata template on its output port available.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 1 | topic | string | Event topic |
| 2 | partition | integer | Topic partition of the event |
| 3 | key | string | Event key |
| 4 | value | string | Event value |
| 5 | timestamp | date | Event timestamp |
| 6 | headers | map[string, byte] | Optional event metadata headers |
| 7 | offset | long | Event offset (order) in its respective partition |

#### KafkaReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | yes | A Kafka connection to be used. See [Kafka connections](kafka-connections.md). | e.g. MyKafkaConnection |
| Topic |  | A Kafka topic to consume events from. A single topic name or a semicolon-separated list of topic names can be used.  Either this attribute or **Topic pattern** attribute must be specified. If both are specified, **Topic pattern** takes precedence. | e.g. my-events \| topic1;topic2 |
| Topic pattern |  | A regular expression pattern to match Kafka topic names to be consumed from.  Either this attribute or **Topic** attribute must be specified. If both are specified, **Topic pattern** takes precedence. | e.g. my-topics\d+ |
| Group | yes | A consumer group this consumer belongs to. It is required for parition auto-assignment among multiple consumers.  Corresponds to Kafka `group.id` consumer property. | e.g. my-group |
| Key type |  | Event key data type to use.  Corresponds to Kafka `key.deserializer` consumer property. | String (default) \| Bytes |
| Value type |  | Event value data type to use. Corresponds to Kafka `value.deserializer` consumer property. | String (default) \| Bytes |
| Auto-commit |  | When enabled, the consumer’s offset will be periodically committed in the background.  Corresponds to Kafka `enable.auto.commit` consumer property. | true (default) \| false |
| Maximum time for new event |  | The maximum waiting time for new Kafka events to appear. | e.g. 500ms \| 3s \| 1m |
| Requested number of events |  | The maximum number of events to be consumed. The actual number of consumed events might be higher because the events are consumed in batches. The size of this batch can be changed by setting the Kafka `max.poll.records` consumer property. | e.g. 1000 |
| Maximum time of reading |  | The total maximum time of reading. | e.g. 10s \| 1m |
| Output mapping |  | Defines the mapping of results to a standard output port. |  |
| Advanced |  |  |  |
| Assigned topic partition |  | Topic partition to consume events from. If not specified it will be assigned automatically. | natural numbers |
| Seek to offset |  | A specific event offset to start consuming from. | natural numbers |
| Seek to boundary |  | Set to start consuming from the first or last event offset. | Seek to beginning \| Seek to end |
| Seek to timestamp |  | Set to start consuming from a specific event offset based on specified timestamp. | e.g. 2020-12-01 06:00:00 |
| Commit position after seek |  | Set to commit position after seeking. Practically only affects behavior with auto-commit disabled. | true (default) \| false |
| Auto-commit interval |  | Time interval in which consumed offsets are committed when auto-commit is enabled.  Corresponds to Kafka `auto.commit.interval.ms` consumer property. | e.g. 500ms \| 3s \| 1m |
| Consumer configuration |  | Additional Kafka consumer properties. See [Apache Kafka documentation](https://kafka.apache.org/documentation/#consumerconfigs) for details. | {fetch.min.bytes=512} |

#### Details

**KafkaReader** allows you to subscribe to (read and process) events from Kafka using the Kafka Consumer API.

Using the **Group** attribute, readers can be organized into consumer groups - each reader within the group reads from a unique partition and the group as a whole consumes all messages from the entire topic.

Besides the configuration available through the component attributes, any other Kafka consumer property can be configured in the **Consumer configuration** attribute.

##### Managing committed offsets

1. Auto-commit - with auto-commit option enabled (default), the offset is committed periodically in the background (with configurable time interval). The drawback of this option is that it does not allow to rollback in case of further event processing failure.
2. Manual commit - to commit processed events manually you need to disable the auto-commit option and design your job to use offset of the last successfully processed event (e.g. stored as a job parameter) in the `Seek to offset` attribute or use a dedicated
   **KafkaCommit** component. You can find more details in the
   [KafkaCommit](kafkacommit.md) component section.

#### Examples

| [Basic reading from a Kafka topic](kafkareader.md#basic-reading-from-a-kafka-topic) |
| --- |
| [Reading from a Kafka topic in parallel](kafkareader.md#reading-from-a-kafka-topic-in-parallel) |

##### Basic reading from a Kafka topic

1. Create a new Kafka connection to an existing Kafka Cluster by following
   [Creating Kafka connection](kafka-connections.md#creating-kafka-connection) .
2. Place a new
   **KafkaReader** component, in its
   **Connection** attribute, select the previously created connection.
3. Specify the topic name to consume from in the
   **Topic** attribute, e.g. `example-topic` .
4. Specify an arbitrary consumer group ID in the
   **Group** attribute,e.g. `example-group` .
5. When the job is executed, the events in the specified Topic will be consumed.

##### Reading from a Kafka topic in parallel

1. Have a Kafka topic with multiple, let’s say 3 partitions and some events produced in them.
2. Add multiple KafkaReader components to your job, up to the number of partitions in the topic. Having more readers than the number of partitions has no effect, the additional readers will not read any records.
3. Configure the reader components, set the
   **Connection** ,
   **Topic** and
   **Group** to be the same in each of the components.
4. Connect the reader output edges.
5. When the job is executed, the readers will get partition assigned automatically and events will get consumed evenly.

#### See also

| [KafkaWriter](kafkawriter.md) |
| --- |
| [KafkaCommit](kafkacommit.md) |
| [Kafka connections](kafka-connections.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |

##### External links

*[https://kafka.apache.org/documentation/#consumerapi](https://kafka.apache.org/documentation/#consumerapi)*

*[https://kafka.apache.org/documentation/#consumerconfigs](https://kafka.apache.org/documentation/#consumerconfigs)*
