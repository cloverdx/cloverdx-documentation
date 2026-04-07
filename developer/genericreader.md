<!-- Development > Component reference > Readers > CustomJavaReader -->

### CustomJavaReader

![CustomJavaReader 64x64](../figures/CustomJavaReader-64x64.png)

| [Short description](genericreader.md#short-description) |
| --- |
| [Ports](genericreader.md#ports) |
| [Metadata](genericreader.md#metadata) |
| [CustomJavaReader attributes](genericreader.md#customjavareader-attributes) |
| [Details](genericreader.md#details) |
| [Examples](genericreader.md#examples) |
| [Best practices](genericreader.md#best-practices) |
| [Compatibility](genericreader.md#compatibility) |
| [See also](genericreader.md#see-also) |

#### Short description

**CustomJavaReader** executes a user-defined Java code.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | - | 0-n | 0-n | - | **✓** | **⨯** | **⨯** |

#### Ports

Number of ports depends on the Java code.

#### Metadata

By default, **CustomJavaReader** does not propagate metadata. Metadata propagation can be configured using the [Metadata propagation algorithm](genericreader.md#cjr-mpa) and [Metadata propagation algorithm class](genericreader.md#cjr-mpac) attributes.

**CustomJavaReader** has no metadata templates.

Requirements on metadata depend on a user-defined transformation.

#### CustomJavaReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Algorithm | [[1]](genericreader.md#customjavareader-attributes-fn01) | A runnable transformation in Java defined in a graph. |  |
| Algorithm URL | [[1]](genericreader.md#customjavareader-attributes-fn01) | A URL to an external file defining a runnable transformation in Java. |  |
| Algorithm class | [[1]](genericreader.md#customjavareader-attributes-fn01) | An external runnable transformation class. |  |
| Advanced |  |  |  |
| Metadata propagation algorithm |  | An algorithm for metadata propagation written in Java. |  |
| Metadata propagation algorithm class |  | An external metadata propagation class. |  |
| Algorithm source charset |  | The encoding of the external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | UTF-8 |

| 1 |  One of these must be set. These transformation attributes must be specified. |
| --- | --- |

#### Details

**CustomJavaReader** executes the Java transformation. **CustomJavaReader** is a more specific **CustomJavaComponent** focused on reading data.

There are other similar Java components: **CustomJavaWriter**, **CustomJavaTransformer** and **CustomJavaComponent**. All these components use a transformation defined in Java, they differ in templates being used.

You can use **Public CloverDX API** in this component. General features of custom Java components and **Public CloverDX API** are described in [CustomJavaComponent](genericcomponent.md).

##### Java interfaces for CustomJavaReader

A transformation required by the component must extend `org.jetel.component.AbstractGenericTransform` class.

The component has the same Java interface as **CustomJavaComponent**, but it provides a different Java template. See [Java interfaces for CustomJavaComponent](genericcomponent.md#java-interfaces-for-customjavacomponent).

##### Custom metadata propagation for CustomJavaReader

**CustomJavaReader** can propagate metadata using a custom algorithm. Metadata propagation algorithm must extend the `org.jetel.component.GenericMetadataProvider` class.

The component has the same Java interface as **CustomJavaComponent**, see [Custom metadata propagation for CustomJavaComponent](genericcomponent.md#custom-metadata-propagation-for-customjavacomponent).

#### Examples

| [Generating random bytes](genericreader.md#generating-random-bytes) |
| --- |
| [Reading records with header and variable-length field](genericreader.md#reading-records-with-header-and-variable-length-field) |

##### Generating random bytes

Generate a user-defined number of sequences of random bytes, each sequence is of 32 bytes.

###### Solution

Use **CustomJavaReader** to create a new user-defined component.

Add a new custom attribute **RecordCount** to the component and set up a value to the attribute, e.g. to 5.

Define the transformation.

```java
package jk;

import java.security.SecureRandom;
import org.jetel.component.AbstractGenericTransform;
import org.jetel.data.DataRecord;

/**
 * This is an example custom reader. It shows how you can create records using a
 * data source.
 */
public class CustomJavaReaderExample01 extends AbstractGenericTransform {

    @Override
    public void execute() {
        Integer recordCount = getProperties().getIntProperty("RecordCount");

        // Output record prepared for writing to output port 0.
        DataRecord record = outRecords[0];

        SecureRandom secureRandom = new SecureRandom();

        for (int i = 0; i < recordCount; ++i) {
            byte[] b = new byte[32];

            secureRandom.nextBytes(b);
            record.getField("field1").setValue(b);
            writeRecordToPort(0, record);
            record.reset();
        }
    }
}
```

Metadata on the output port must have one field named **field1**. The field has the **byte** data type.

##### Reading records with header and variable-length field

Read binary data from a file. Each record has one byte header and a variable length payload. The length of the payload is defined by the integer value of the header. Read the length and payload from each record. The file to be read has to be configured by the component attribute.

Example of source data:

```
!123456789012345678901234567890123"abcdefghijklmnopqrstuvwxyz78901234
```

###### Solution

Add the **FileUrl** attribute to the component.

```java
package jk;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

import org.jetel.component.AbstractGenericTransform;
import org.jetel.data.DataRecord;
import org.jetel.exception.JetelRuntimeException;

/**
 * This is an example custom reader. It shows how you can read data from file
 * with specific format.
 */
public class CustomJavaReaderExample02 extends AbstractGenericTransform {

    @Override
    public void execute() {
        DataRecord record = outRecords[0];
        String fileUrl = getProperties().getStringProperty("FileUrl");
        File file = getFile(fileUrl);

        try (FileInputStream inputStream = new FileInputStream(file)) {
            for (int length = inputStream.read(); length > 0; length = inputStream.read()) {
                byte[] b = new byte[length];
                inputStream.read(b, 0, length);

                record.getField("field1").setValue(length);
                record.getField("field2").setValue(>b);
                writeRecordToPort(0, record);
                record.reset();
            }
        } catch (IOException e) {
            throw new JetelRuntimeException(e);
        }
    }
}
```

**Note:** input data is in binary format. The first header contains a character `!` which corresponds to the value `33`. Thirty-three characters follow. The header of the second record has the value `34` which is displayed as a character `"`. Thirty-four bytes follow.

Metadata on the output port must have two fields named **field1** and **field2** with the types **integer** and **byte**.

#### Best practices

If the **Algorithm URL** attribute is used, we recommend to explicitly specify **Algorithm source charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | **CustomJavaReader** is available since **4.1.0-M1**. |
| 5.3.0 | **CustomJavaReader** can now propagate metadata - added new attributes [Metadata propagation algorithm](genericreader.md#cjr-mpa) and [Metadata propagation algorithm class](genericreader.md#cjr-mpac). |

#### See also

| [CustomJavaComponent](genericcomponent.md) |
| --- |
| [CustomJavaWriter](genericwriter.md) |
| [CustomJavaTransformer](generictransformer.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
