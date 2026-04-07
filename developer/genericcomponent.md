<!-- Development > Component reference > Others > CustomJavaComponent -->

### CustomJavaComponent

![CustomJavaComponent 64x64](../figures/CustomJavaComponent-64x64.png)

| [Short description](genericcomponent.md#short-description) |
| --- |
| [Ports](genericcomponent.md#ports) |
| [Metadata](genericcomponent.md#metadata) |
| [CustomJavaComponent attributes](genericcomponent.md#customjavacomponent-attributes) |
| [Details](genericcomponent.md#details) |
| [Public CloverDX API](genericcomponent.md#public-cloverdx-api) |
| [Examples](genericcomponent.md#examples) |
| [Best practices](genericcomponent.md#best-practices) |
| [Compatibility](genericcomponent.md#compatibility) |
| [See also](genericcomponent.md#see-also) |

#### Short description

**CustomJavaComponent** executes user-defined Java code.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | - | 0-n | 0-n | - | **✓** | **⨯** | **⨯** |

#### Ports

Number of ports depends on the Java code.

#### Metadata

By default, **CustomJavaComponent** does not propagate metadata. Metadata propagation can be configured using the [Metadata propagation algorithm](genericcomponent.md#cjc-mpa) and [Metadata propagation algorithm class](genericcomponent.md#cjc-mpac) attributes (see also the [Custom metadata propagation](genericcomponent.md#custom-metadata-propagation) example).

**CustomJavaComponent** has no metadata templates.

Requirements on metadata depend on user-defined transformation.

#### CustomJavaComponent attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Algorithm | [[1]](genericcomponent.md#customjavacomponent-attributes-fn01) | A runnable transformation in Java defined in a graph. |  |
| Algorithm URL | [[1]](genericcomponent.md#customjavacomponent-attributes-fn01) | A URL to an external file defining a runnable transformation in Java. |  |
| Algorithm class | [[1]](genericcomponent.md#customjavacomponent-attributes-fn01) | An external runnable transformation class. |  |
| Advanced |  |  |  |
| Metadata propagation algorithm |  | An algorithm for metadata propagation written in Java. |  |
| Metadata propagation algorithm class |  | An external metadata propagation class. |  |
| Algorithm source charset |  | The encoding of the external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | UTF-8 |

| 1 |  One of these must be set. These transformation attributes must be specified. |
| --- | --- |

#### Details

**CustomJavaComponent** executes Java transformation.

There are specialized custom java components: [CustomJavaReader](genericreader.md), [CustomJavaWriter](genericwriter.md) and [CustomJavaTransformer](generictransformer.md). These components differ just in the provided Java template.

You can use **Public CloverDX API** in this component. See [Public CloverDX API](genericcomponent.md#public-cloverdx-api).

##### External JAR Files

The default folder for external `.jar` files in a local project is `./lib`.

On the Server, external `.jar` files can also be placed on the classpath of the Worker.

You should add the `.jar` files to `classpath`. Open **Project Properties** dialog **Project** ****Properties**. Switch to **Java Build Path** ****Libraries**. Click **Add JARs…​** and select the `.jar` files.

##### Running on Cluster

All `.java` and `.class` files should reside in a shared sandbox.

##### Editing Code in Another Tab

If you click the **Algorithm** or **Metadata propagation algorithm** attribute value, a dialog for editing of build-in java code opens. Use the **Switch to Java editor** button to convert the transformation in Java to a `.java` file. The file is opened as a new tab having Java editor with syntax highlighting associated.

##### Java interfaces for CustomJavaComponent

Transformation required by the component must extend the `org.jetel.component.AbstractGenericTransform` class.

Following are methods of the `AbstractGenericTransform` class:

- `ConfigurationStatus checkConfig(ConfigurationStatus status)`
  Use this method to check the configuration of a custom component: custom attributes and their values, ports and metadata.
- `void execute()`
  Define your transformation here. The method is called once when the component is started.
- `void init()`
  Initializes Java class/function. This method is called only once at the beginning of the transformation process. Any object allocation/initialization should happen here.
- `void preExecute()`
  This is also an initialization method, which is invoked before each separate graph run. Contrary to the `init()` procedure, only resources for this graph run should be allocated here. All resources allocated here should be released in the `postExecute()` method.
- `void postExecute()`
  This is a de-initialization method for a single graph run. All resources allocated in the `preExecute()` method should be released here. It is guaranteed that this method is invoked after a graph finish, at the latest. For some graph elements, for instance components, this method is called immediately after a phase finish.
- `Node getComponent()`
  Returns an instance of component. Useful for accessing component attributes.
- `File getFile(String fileUrl)`
  Returns a file for a given file URL.
- `InputStream getInputStream(String fileUrl)`
  Returns `InputStream` for a given file URL.
- `OutputStream getOutputStream(String fileUrl, boolean append)`
  Returns `OutputStream` for a given file URL.

##### Custom metadata propagation for CustomJavaComponent

**CustomJavaComponent** can propagate metadata using a custom algorithm (see the [example](genericcomponent.md#custom-metadata-propagation)). Metadata propagation algorithm must extend the `org.jetel.component.GenericMetadataProvider` class.

Following are methods of the `GenericMetadataProvider` class:

- `void propagateMetadata()`
  Define your metadata propagation algorithm here. Use the `setInputMetadata()` and `setOutputMetadata()` methods to propagate metadata to connected ports. The `propagateMetadata()` method may be called multiple times before the graph is executed. Results of any expensive operations should be cached (e.g. in instance fields). Any resources opened in this method must also be closed in this method.
- `DataRecordMetadata getMetadataFromInputPort(int portIndex)`
  Returns an instance of metadata that is currently propagated from outside to input port.
- `DataRecordMetadata getMetadataFromOutputPort(int portIndex)`
  Returns an instance of metadata that is currently propagated from outside to output port.
- `void setInputMetadata(int portIndex, DataRecordMetadata metadata)`
  Assigns given metadata to input port of this component.
- `void setOutputMetadata(int portIndex, DataRecordMetadata metadata)`
  Assigns given metadata to output port of this component.
- `Node getComponent()`
  Returns an instance of component. Useful for accessing component attributes.
- `File getFile(String fileUrl)`
  Returns a file for a given file URL.

#### Public CloverDX API

| [Data record](genericcomponent.md#data-record) |
| --- |
| [Data field](genericcomponent.md#data-field) |
| [Metadata](genericcomponent.md#metadata) |
| [Dictionaries](genericcomponent.md#dictionaries) |
| [Lookup tables](genericcomponent.md#lookup-tables) |
| [Graph parameters](genericcomponent.md#graph-parameters) |
| [Component attributes](genericcomponent.md#component-attributes) |
| [Sequences](genericcomponent.md#sequences) |
| [Database connections](genericcomponent.md#database-connections) |
| [Opening streams](genericcomponent.md#opening-streams) |
| [Logging](genericcomponent.md#logging) |

**Public CloverDX API** is a set of **CloverDX** Java classes you can use in transformations in **CustomJavaComponent** and other components using Java transformation.

Public **CloverDX** API uses the `@CloverPublicAPI` annotation. Classes annotated by `@CloverPublicAPI` are part of the API and can be used in your transformation. Details on particular classes are documented in javadoc. The following pieces of code serve to point to particular classes suitable for a particular purpose.

You can use the standard Java classes and classes provided by the API in your transformations. Do not use **CloverDX** Java classes not included in the API! The classes not included in the API may be changed in the next release, or removed.

##### Data record

One single record is represented by the `DataRecord` class.

```java
DataRecord record;
```

To create a data record not connected to any particular port, use the static method `newRecord()` of `DataRecordFactory`. It requires record metadata.

```java
String metadataId = getGraph().getDataRecordMetadataByName("recordName1");
DataRecordMetadata metadata = getGraph().getDataRecordMetadata(metadataId);
DataRecord record = DataRecordFactory.newRecord(metadata);
```

To read a record from the input port, use `readRecordFromPort()` function. The index of the input port (starting from 0) is specified in the parameter of the function.

```java
record = readRecordFromPort(0);
```

The function returns `null` if no other records are available.

```java
while ((record = readRecordFromPort(0)) != null) {
    // Do something
}
```

To write a record to the output port, use the `writeRecordToPort()` function. Parameters define the index of the output port and record to be written.

```java
writeRecordToPort(0, record);
```

If you create a component with a variable number of the input or output ports, use

```java
getComponent().getInputPortsMaxIndex()
```

or

```java
getComponent().getOutputPortsMaxIndex()
```

to get the maximal index of input or output ports.

Note that the first input port has index 0. A component with N input ports has N-1 as the maximal index of input port.

##### Data field

Data field is represented by the `DataField` class. You can get fields of data record using `getFields()` of `DataRecord`. You can get a particular field using `getField()` taking the field index or field name as a parameter.

```java
DataRecord record;
DataField dataField1;
dataField1 = record.getField(0);
DataField dataField2;
dataField2 = record.getField("field2");
```

Use `getValue()` and `setValue()` methods of `DataField` to work with field values.

```java
DataField field = record.getField(0);
String value = field.getValue();
field.setValue("some new value");
```

##### Metadata

There are two classes necessary to work with metadata: `DataRecordMetadata` and `DataFieldMetadata`. `DataRecordMetadata` represents metadata of the whole record whereas `DataFieldMetadata` represents metadata of particular field.

Use `getMetadata()` method of `DataRecord` to get access to metadata of a record.

```java
DataRecord record;
record = ...
DataRecordMetadata metadata = record.getMetadata();
```

Use `getMetadata()` method of `DataField` to get access to metadata of a field.

```java
DataField dataField;
dataField = ...
DataFieldMetadata fieldMetadata = dataField.getMetadata();
```

To use metadata depending on its name, use `getDataRecordMetadataByName()` to get metadata id and subsequently use `getDataRecordMetadata()` to get metadata corresponding to the id.

```java
String metadataId = getGraph().getDataRecordMetadataByName("recordName1");
DataRecordMetadata metadata = getGraph().getDataRecordMetadata(metadataId);
```

##### Dictionaries

To read a value from a dictionary, use the `getValue()` function, to write to a dictionary use the `setValue()` function:

```java
Dictionary dictionary = getGraph().getDictionary();
dictionary.setValue("mykey1", "NewValue");
String s = dictionary.getValue("mykey2");
```

##### Lookup tables

The `LookupTable` interface gives you an access to lookup tables. Use `put()` to insert a data record into an existing lookup table. Note that `getLookupTable()` requires **lookup table ID**. The parameter is not the lookup table name!

```java
LookupTable lookup = getGraph().getLookupTable("LookupTable0");
DataRecord record = ...;
lookup.put(record);
```

Use `createLookup()` to search for items matching the key.

```java
LookupTable lt;
lt = ...

DataRecord patternRecord = DataRecordFactory.newRecord(lt.getMetadata());
patternRecord.getField(0).setValue("keyToBeSearchedPart1");
patternRecord.getField(2).setValue("keyToBeSearchedPart2");
String [] lookupFields = {"field1", "field3"};
RecordKey recordKey = new RecordKey(lookupFields, lt.getMetadata());
Lookup lookup;
lookup = lt.createLookup(recordKey, patternRecord);
lookup.seek();

while (lookup.hasNext()){
    DataRecord record = lookup.next();
    // process the result found
    writeRecordToPort(0, record);
}
```

##### Graph parameters

Graph parameters can be obtained from `TransformationGraph` using `getGraphParameters()`. To get a particular parameter use `getGraphParameter()` with the parameter name.

```java
TransformationGraph graph = getGraph();
GraphParameters graphParameters = graph.getGraphParameters();
GraphParameter graphParameter = graphParameters.getGraphParameter("MY_PARAMETER");
```

Use `getValue()` or `getValueResolved()` to get the parameter value.

```java
String value = graphParameter.getValue();
String valueResolved = graphParameter.getValueResolved(RefResFlag.REGULAR);
```

##### Component attributes

You can get a value of component attributes using the `getProperty()` functions applied on `TypedProperties`.

```java
String myStringValue = getProperties().getStringProperty("myCustomPropertyName1");
```

```java
Integer myIntegerValue = getProperties().getIntProperty("myCustomPropertyName2");
```

##### Sequences

A sequence is accessible from `TransformationGraph` via the `getSequence()` function with the sequence ID as a parameter.

```java
Sequence seq = getGraph().getSequence("Sequence0");
```

Use `nextValueInt()`, `nextValueLong()` or `nextValueString()` to increment the sequence and return the incremented value. A first call of any of the `nextValue*()` functions initializes the sequence to the initial sequence value and returns an unincremented initial value.

```java
String sequenceValue = seq.nextValueString();
int sequenceValueInt = seq.nextValueInt();
long sequenceValueLong = seq.nextValueLong();
```

To get the last value returned by functions above use `currentValueInt()``currentValueLong()` or `currentValueString()`. If none of the `nextValue*()` functions have been called before, the current value is the start value of the sequence.

```java
String sequenceValue = seq.currentValueString();
int sequenceValueInt = seq.currentValueInt();
long sequenceValueLong = seq.currentValueLong();
```

##### Database Connections

Database connections are accessible via the `getDBConnection()` method of `AbstractGenericTransform`. The method requires **connection name** or **connection ID** as a parameter.

```java
Connection connection = getDBConnection("myUniqueID");
```

The `getDBConnection(String)` method is available since **4.7.0-M2**. The access to database connection in earlier versions was different.

###### JNDI

To connect to JNDI data source from **Custom Java Component**, create a database connection using the JNDI data source. Use this connection in your source code in the same way as in the case of connecting to a database without a JNDI data source. See the example above.

##### Opening streams

If you work with paths, use the `getFile()` function to resolve the path correctly.

```java
String param = getProperties().getStringProperty("InputFile");
File file = getFile(param);
```

You can access files via streams. Use `getOutputStream()` or `getInputStream();`

```java
String param = getProperties().getStringProperty("InputFile");
InputStream is = getInputStream(param);
```

```java
String param = getProperties().getStringProperty("OutputFile");
OutputStream os = getOutputStream(param, true);
```

##### Logging

Use the `log()` function to log messages of important events of your Java-defined transformation.

```java
getLogger().log(Level.INFO, "Some message" );
```

#### Examples

| [Remover of empty directories](genericcomponent.md#remover-of-empty-directories) |
| --- |
| [Checking configuration of custom component](genericcomponent.md#checking-configuration-of-custom-component) |
| [Custom metadata propagation](genericcomponent.md#custom-metadata-propagation) |

##### Remover of empty directories

Create a component removing empty directories.

###### Solution

Add a new attribute **Directory** to the component.

Use the following code.

```java
package jk;

import java.io.File;

import org.jetel.component.AbstractGenericTransform;

/**
 * This is an example custom component. It shows how you can remove empty
 * directories.
 */
public class CustomJavaComponentExample01 extends AbstractGenericTransform {

    private void removeEmptyDirectories(File dir) {
        if (!dir.isDirectory() || !dir.canRead() || !dir.canWrite()) {
        return;
        }

        for (File f : dir.listFiles()) {
            if (f.isDirectory()) {
                removeEmptyDirectories(f);
                if (f.listFiles().length == 0) {
                f.delete();
                }
            }
        }
    }

    @Override
    public void execute() {
        String directory = getProperties().getStringProperty("Directory");
        File dir = getFile(directory);
        removeEmptyDirectories(dir);
    }

}
```

##### Checking configuration of custom component

The component has to have one input port and one output port connected. Each port should have metadata assigned. The component has the attribute **Multiplier** having integral value.

###### Solution

Use the `checkConfig()` function of a component’s template.

```java
@Override
public ConfigurationStatus checkConfig(ConfigurationStatus status) {
    super.checkConfig(status);

    if (getComponent().getInPorts().size() != 1 || getComponent().getOutPorts().size() != 1) {
        status.add("One input and one output port must be connected!", Severity.ERROR, getComponent(), Priority.NORMAL);
        return status;
    }

    DataRecordMetadata inMetadata = getComponent().getInputPort(0).getMetadata();
    DataRecordMetadata outMetadata = getComponent().getOutputPort(0).getMetadata();
    if (inMetadata == null || outMetadata == null) {
        status.add("Metadata on input or output port not specified!", Severity.ERROR, getComponent(), Priority.NORMAL);
    }

    if (!getProperties().containsKey("Multiplier")) {
        status.add("Multiplier property is missing or is not set.", Severity.ERROR, getComponent(), Priority.NORMAL, "Multiplier");
        return status;
    }

    try {
        Integer.parseInt(getProperties().getStringProperty("Multiplier"));
    } catch(Exception e){
        status.add("Multiplier is not integer!", Severity.ERROR, getComponent(), Priority.NORMAL, "Multiplier");
    }

    return status;
}
```

##### Custom metadata propagation

Below is an example of the code which adds an additional `Date` field to any metadata coming from input, and propagates the enhanced metadata to output port:

```java
DataRecordMetadata metadataFromInputPort = getMetadataFromInputPort(0); // Look up metadata from input port 0.

if (metadataFromInputPort != null) { // Always check for null, the metadata may not be available initially.
    metadataFromInputPort.setName(metadataFromInputPort.getName() + "_modified"); // Modify the name of the metadata.

    // Add additional field to the metadata that came from input port.
    DataFieldMetadata additionalField = new DataFieldMetadata("CreatedDate", DataFieldType.DATE, null);
    additionalField.setFormatStr("yyyy-MM-dd"); // Configure the format property of our new field.
    metadataFromInputPort.addField(additionalField);

    setOutputMetadata(0, metadataFromInputPort); // Propagate the modified metadata to output port.
}
```

#### Best practices

If the transformation is specified in an external file (with **Algorithm URL**), we recommend users to explicitly specify **Algorithm source charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | **CustomJavaComponent** is available since **4.1.0-M1**. It replaced **JavaExecute**. |
| 5.3.0 | **CustomJavaComponent** can now propagate metadata - added new attributes [Metadata propagation algorithm](genericcomponent.md#cjc-mpa) and [Metadata propagation algorithm class](genericcomponent.md#cjc-mpac). |

#### See also

| [CustomJavaReader](genericreader.md) |
| --- |
| [CustomJavaTransformer](generictransformer.md) |
| [CustomJavaWriter](genericwriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
| [Debugging Java transformations](transformations.md#debugging-java-transformations) |
