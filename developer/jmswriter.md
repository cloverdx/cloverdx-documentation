<!-- Development > Component reference > Writers > JMSWriter -->

### JMSWriter

![JMSWriter 64x64](../figures/JMSWriter-64x64.png)

| [Short description](jmswriter.md#short-description) |
| --- |
| [Ports](jmswriter.md#ports) |
| [Metadata](jmswriter.md#metadata) |
| [JMSWriter attributes](jmswriter.md#jmswriter-attributes) |
| [Details](jmswriter.md#details) |
| [Examples](jmswriter.md#examples) |
| [Best practices](jmswriter.md#best-practices) |
| [See also](jmswriter.md#see-also) |

#### Short description

**JMSWriter** converts **CloverDX** data records into JMS messages.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| jms messages | 1 | 0 | **✓** | **⨯** | **✓** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For data records | Any |

#### Metadata

**JMSWriter** does not propagate metadata.

**JMSWriter** has no metadata templates.

Metadata on the input port may contain a field specified in the **Message body field** attribute.

#### JMSWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| JMS connection | yes | ID of the JMS connection to be used. See [JMS connections](jms-connections.md). |  |
| Processor code |  | Transformation of records to JMS messages written in the graph in Java. |  |
| Processor URL |  | Name of an external file, including the path, containing the transformation of records to JMS messages written in Java. |  |
| Processor class |  | Name of an external class defining the transformation of records to JMS messages. The default processor value (`org.jetel.component.jms. DataRecord2JmsMsgProperties`) is sufficient for most cases. It produces `javax.jms.TextMessage`. | DataRecord2JmsMsgProperties (default) \| other class |
| Processor source charset |  | Encoding of external file containing the transformation in Java.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | UTF-8 \| other encoding |
| Advanced |  |  |  |
| Message body field |  | Name of the field of metadata from which the body of the message should be gotten and sent out. This attribute is used by the default processor implementation (`JmsMsg2DataRecordProperties`). If no **Message body field** is specified, the field whose name is `bodyField` will be used as a resource for the body of the message contents. If no field for the body of the message is contained in metadata (either explicitly specified or the default one), the processor tries to set a field named *bodyField*, but it’s silently ignored if such field doesn’t exist in output record metadata. The other fields from metadata serve as resources of message properties with the same names as field names. | bodyField (default) \| other name |

#### Details

**JMSWriter** receives **CloverDX** data records, converts them into JMS messages and sends these messages out. Component uses a processor transformation which implements a `DataRecord2JmsMsg` interface or inherits from a `DataRecord2JmsMsgBase` superclass. Methods of `DataRecord2JmsMsg` interface are described below.

Details on threads are described in [*Details in JMSReader*](jmsreader.md#details).

##### Message Body, Message Header etc.

Data inserted into the body or header of a message depends on the implementation of the `Processor` class. The default implementation is `org.jetel.component.jms.DataRecord2JmsMsgProperties`. The message body may be filled with textual representation of one field of the record. You can specify name of such field by the component attribute **Message body field**.

All the other fields are saved using string properties in the message header. Property names are same as field names. Values contain textual representation of field values. Last message has same format as all the others. Terminating message is not used.

##### Java interfaces for JMSWriter

The transformation implements methods of the `DataRecord2JmsMsg` interface and inherits other common methods from the `Transform` interface. See [Common Java interfaces](transformations.md#common-java-interfaces). You can use [Public CloverDX API](genericcomponent.md#public-cloverdx-api) too.

Following are the methods of `DataRecord2JmsMsg` interface:

- `void init(DataRecordMetadata metadata, Session session, Properties props)`
  Initializes the processor.
- `void preExecute(Session session)`
  This is also an initialization method, which is invoked before each separate graph run. Contrary to the `init()` procedure, only resources for this graph run should be allocated here. All resources allocated here should be released in the `postExecute()` method.
  `session` may be used for creation of JMS messages. Each graph execution has its own session opened. Thus the session set in the `init()` method is usable only during the first execution of the graph instance.
- `Message createMsg(DataRecord record)`
  Transforms data record to JMS message. Is called for all data records.
- `Message createLastMsg()`
  This method is called after last record and is supposed to return a message terminating the JMS output. If it returns null, no terminating message is sent. Since 2.8.
- `String getErrorMsg()`
  Returns an error message.
- `Message createLastMsg(DataRecord record)` (deprecated)
  This method is not called explicitly since 2.8. Use `createLastMsg()` instead.

#### Examples

##### Writing Records to JMS Queue

There is a message queue `clover-queue` on `localhost:61616`. Write 5 records into the message queue.

###### Solution

Create a JMS Connection `MyJMSConnection`. The details are described in the example [Read text message from message queue](jmsreader.md#read-text-message-from-message-queue) in documentation on **JMSReader**.

Configure the **JMSWriter** component.

| Attribute | Value |
| --- | --- |
| JMS Connection | MyJMSConnection |
| Message body field | e.g. field1 |

#### Best practices

If **Processor URL** is used, we recommend users to explicitly specify **Processor source charset**.

#### See also

| [JMSReader](jmsreader.md) |
| --- |
| [JMS connections](jms-connections.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
