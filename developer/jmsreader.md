<!-- Development > Component reference > Readers > JMSReader -->

### JMSReader

![JMSReader 64x64](../figures/JMSReader-64x64.png)

| [Short description](jmsreader.md#short-description) |
| --- |
| [Ports](jmsreader.md#ports) |
| [Metadata](jmsreader.md#metadata) |
| [JMSReader attributes](jmsreader.md#jmsreader-attributes) |
| [Details](jmsreader.md#details) |
| [Examples](jmsreader.md#examples) |
| [Best practices](jmsreader.md#best-practices) |
| [See also](jmsreader.md#see-also) |

#### Short description

**JMSReader** converts JMS messages into **CloverDX** data records.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| JMS messages | 0 | 1 | **✓** | **⨯** | **✓** | **⨯** | **✓** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | For correct data records | Any |

All the connected output ports send out all data records.

#### Metadata

JMSReader does not propagate metadata.

JMSReader has no metadata templates.

Metadata on the output port may contain a field specified in the **Message body field** attribute. Metadata can also use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### JMSReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| JMS connection | yes | ID of the JMS connection to be used. See [JMS connections](jms-connections.md). |  |
| Processor code | [[1]](jmsreader.md#jmsreader-attributes-fn01) | Transformation of JMS messages to records written in the graph in Java. |  |
| Processor URL | [[1]](jmsreader.md#jmsreader-attributes-fn01) | Name of an external file, including the path, containing the transformation of JMS messages to records written in Java. |  |
| Processor class | [[1]](jmsreader.md#jmsreader-attributes-fn01) | Name of an external class defining the transformation of JMS messages to records. The default processor value is sufficient for most cases. It can process both `javax.jms.TextMessage` and `javax.jms.BytesMessage`. | JmsMsg2DataRecordProperties (default) \| other class |
| JMS message selector |  | Standard JMX "query" used to filter the JMS messages that should be processed. In effect, it is a string query using message properties and syntax that is a subset of SQL expressions. For more information, see [Interface message](http://docs.oracle.com/javaee/7/api/javax/jms/Message.html). |  |
| Message charset |  | Encoding of JMS messages contents. This attribute is also used by the default processor implementation (`JmsMsg2DataRecordProperties`). And it is used for `javax.jms.BytesMessage` only. | ISO-8859-1 (default) \| other encoding |
| Advanced |  |  |  |
| Processor source charset |  | Encoding of external file containing the transformation in Java. | ISO-8859-1 (default) \| other encoding |
| Max msg count |  | Maximum number of messages to be received. 0 means without limitation. For more information, see [Limit of run](jmsreader.md#limit-of-run). | 0 (default) \| 1-N |
| Timeout |  | Maximum time to receive messages in milliseconds. 0 means without limitation. For more information, see [Limit of run](jmsreader.md#limit-of-run). | 0 (default) \| 1-N |
| Message body field |  | Name of the field to which the message body should be written. This attribute is used by the default processor implementation (`JmsMsg2DataRecordProperties`). If no **Message body field** is specified, the field whose name is `bodyField` will be filled with the body of the message. If no field for the body of the message is contained in metadata, the body will not be written to any field. | bodyField (default) \| other name |

| 1 |  One of these may be set. Any of these transformation attributes implements a `JmsMsg2DataRecord` interface. |
| --- | --- |

For more information, see [Java interfaces for JMSReader](jmsreader.md#java-interfaces-for-jmsreader).

For detailed information about transformations, see [Defining transformations](transformations.md#defining-transformations).

#### Details

**JMSReader** receives JMS messages, converts them into **CloverDX** data records and sends these records to the connected output port. The component uses a processor transformation which implements a `JmsMsg2DataRecord` interface or inherits from a `JmsMsg2DataRecordBase` superclass. Methods of `JmsMsg2DataRecord` interface are described below in [Java interfaces for JMSReader](jmsreader.md#java-interfaces-for-jmsreader).

##### Limit of run

You can choose to limit the number of received messages and/or time of processing.

- **Limited Run**
  If you specify the maximum number of messages (**Max msg count**), the timeout (**Timeout**)or both, the processing will be limited by the number of messages, or time of processing, or both of these attributes. They need to be set to positive values.
  When the specified number of messages is received, or when the process lasts some defined time, the process stops. Whichever of them will be achieved first, such attribute will be applied.
  > [!NOTE]
  > Remember that you can also limit the graph run by using the `endOfInput()` method of `JmsMsg2DataReader` interface. It returns a boolean value and can also limit the run of the graph. Whenever it returns `false`, the processing stops.
- **Unlimited Run**
  If you do not specify either of these two attributes (**Max msg count** and **Timeout**), the processing will never stop.
  This is the default setting of **JMSReader**. Both the attributes are set to 0 by default. Thus, the processing is limited by neither the number of messages nor the elapsed time.

##### Thread Safety and Parallel Access

Each JMS Connection used in a graph creates one JMS session in AUTO_ACKNOWLEDGE mode. All JMS components get the "consumer" or "producer" from the shared session. It’s possible to use more consumers/producers in parallel, but the session is single-threaded, so the requests for JMS broker are synchronized. To achieve really parallel access, each JMS component should have its own JMS connection.

##### Message Body, Message Header etc.

Data that is inserted into the body or header of a message depends on the implementation of the `Processor` class. The default implementation is `org.jetel.component.jms.JmsMsg2DataRecordProperties`. It is the class transforming JMS messages (TextMessage or BytesMessage) to data records.

One field of the record may be filled with body of the message. The name of the field is specified by component attribute **Message body field**.

If message is of type `BytesMessage`, use the attribute **msgCharset** to specify encoding of characters in the message.

All the other fields are saved using string properties in the message header. Property names are same as respective field names. Values contain textual representation of field values. Default property field of Map<StringÎ may be defined to which all "unmappable" properties of header are saved as [key=property name]-Î[value=property value]

Last message has a same format as all the others. Terminating message is not supported.

#### Java interfaces for JMSReader

The transformation implements methods of the `JmsMsg2DataRecord` interface and inherits other common methods from the `Transform` interface. See [Common Java interfaces](transformations.md#common-java-interfaces). See [Public CloverDX API](genericcomponent.md#public-cloverdx-api).

Following are the methods of `JmsMsg2DataRecord` interface:

- `void init(DataRecordMetadata metadata, Properties props)`
  Initializes the processor.
- `boolean endOfInput()`
  May be used to end processing of input JMS messages when it returns `false`. For more information, see [Limit of run](jmsreader.md#limit-of-run).
- `DataRecord extractRecord(Message msg)`
  Transforms JMS message to data record. `null` indicates that the message is not accepted by the processor.
- `String getErrorMsg()`
  Returns error message.

#### Examples

##### Read Text Message from Message Queue

There is a message queue `clover-queue` accessible at `localhost:61616`. Read 5 records from the queue.

###### Solution

Create a JMS connection `MyJMSConnection`:

| Property | Value |
| --- | --- |
| Name | MyJMSConnection |
| Libraries | e.g. C:/opt/apache-activemq-5.12.0/activemq-all-5.12.0.jar |
| Initial ctx factory class | org.apache.activemq.jndi.ActiveMQInitialContextFactory |
| URL | tcp://localhost:61616 |
| Connection factory JNDI name | QueueConnectionFactory |
| Destination JNDI | dynamicQueues/clover-queue |
| User name | ActiveMQ_user_name |
| Password | ActiveMQ_password |

`User name` and `Password` are credentials for reading messages from message queue. E.g. Apache ActiveMQ has default values `admin:admin`.

The `activemq-all-5.12.0.jar` file is a JMS provider. The library file must be available on your file system and accessible to **CloverDX**. You can use another message provider.

Configure **JMSReader** component. Use the above mentioned connection in the component configuration.

| Attribute | Value |
| --- | --- |
| JMS Connection | MyJMSConnection |
| Max msg count | 5 |
| Message body field | e.g. field1 |

#### Best practices

We recommend users to explicitly specify the **Message charset** attribute.

If the transformation is specified in an external file (with **Processor URL**), **Processor source charset** should be specified too.

#### See also

| [JMSWriter](jmswriter.md) |
| --- |
| [JMS connections](jms-connections.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
