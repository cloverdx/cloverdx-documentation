<!-- Development > Component reference > Writers > CustomJavaWriter -->

### CustomJavaWriter

![CustomJavaWriter 64x64](../figures/CustomJavaWriter-64x64.png)

| [Short description](genericwriter.md#short-description) |
| --- |
| [Ports](genericwriter.md#ports) |
| [Metadata](genericwriter.md#metadata) |
| [CustomJavaWriter attributes](genericwriter.md#customjavawriter-attributes) |
| [Details](genericwriter.md#details) |
| [Examples](genericwriter.md#examples) |
| [Best practices](genericwriter.md#best-practices) |
| [Compatibility](genericwriter.md#compatibility) |
| [See also](genericwriter.md#see-also) |

#### Short description

**CustomJavaWriter** executes a user-defined Java code.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | - | 0-n | 0-n | - | **✓** | **⨯** | **⨯** |

#### Ports

The number of ports depends on the Java code.

#### Metadata

By default, **CustomJavaWriter** does not propagate metadata. Metadata propagation can be configured using the [Metadata propagation algorithm](genericwriter.md#cjw-mpa) and [Metadata propagation algorithm class](genericwriter.md#cjw-mpac) attributes.

**CustomJavaWriter** has no metadata templates.

Requirements on metadata depend on a user-defined transformation.

#### CustomJavaWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Algorithm | [[1]](genericwriter.md#customjavawriter-attributes-fn01) | A runnable transformation in Java defined in the graph. |  |
| Algorithm URL | [[1]](genericwriter.md#customjavawriter-attributes-fn01) | A URL to an external file defining a runnable transformation in Java. |  |
| Algorithm class | [[1]](genericwriter.md#customjavawriter-attributes-fn01) | An external runnable transformation class. |  |
| Advanced |  |  |  |
| Metadata propagation algorithm |  | An algorithm for metadata propagation written in Java. |  |
| Metadata propagation algorithm class |  | An external metadata propagation class. |  |
| Algorithm source charset |  | The encoding of the external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | UTF-8 |

| 1 |  One of these must be set. These transformation attributes must be specified. |
| --- | --- |

#### Details

**CustomJavaWriter** executes the Java transformation. **CustomJavaWriter** is a more specific **CustomJavaComponent** focused on writing data.

There are other similar Java components: **CustomJavaReader**, **CustomJavaTransformer** and **CustomJavaComponent**. All these components use a transformation defined in Java, they differ in templates being used.

You can use **Public CloverDX API** in this component. General parts of custom Java components and **Public CloverDX API** are described in [CustomJavaComponent](genericcomponent.md).

##### Java interfaces for CustomJavaWriter

A transformation required by the component must extend the `org.jetel.component.AbstractGenericTransform` class.

The component has the same Java interface as **CustomJavaComponent**, but it provides a different Java template. See [Java interfaces for CustomJavaComponent](genericcomponent.md#java-interfaces-for-customjavacomponent).

##### Custom metadata propagation for CustomJavaWriter

**CustomJavaWriter** can propagate metadata using a custom algorithm. Metadata propagation algorithm must extend the `org.jetel.component.GenericMetadataProvider` class.

The component has the same Java interface as **CustomJavaComponent**, see [Custom metadata propagation for CustomJavaComponent](genericcomponent.md#custom-metadata-propagation-for-customjavacomponent).

#### Examples

##### Writing Maps and Lists

Create a component capable of writing all input metadata fields as strings. Input metadata fields can include maps and lists.

###### Solution

```java
package jk;

import java.io.IOException;
import java.io.OutputStream;

import org.jetel.component.AbstractGenericTransform;
import org.jetel.data.DataField;
import org.jetel.data.DataRecord;
import org.jetel.exception.JetelRuntimeException;

/**
 * This is an example custom writer. It shows how you can write string
 * representations of fields into file.
 */
public class CustomJavaWriterExample01 extends AbstractGenericTransform {
    @Override
    public void execute() {
        String fileUrl = getProperties().getStringProperty("FileUrl");
        DataRecord record;

        try (OutputStream os = getOutputStream(fileUrl, false)) {
            while ((record = readRecordFromPort(0)) != null) {
                StringBuffer sb = new StringBuffer();
                DataField[] dataFields = record.getFields();

                int fieldCount = 1;
                for (DataField df : dataFields) {
                    sb.append(df.getValue() != null ? df.getValue().toString() : "");
                    if (df.getMetadata().getDelimiter() != null) {
                        sb.append(df.getMetadata().getDelimiter());
                    } else {
                        if (fieldCount != dataFields.length) {
                            sb.append(record.getMetadata().getFieldDelimiter());
                        }
                    }
                    ++fieldCount;
                }
                sb.append(record.getMetadata().getRecordDelimiter());
                os.write(sb.toString().getBytes("UTF-8"));
            }
        } catch (IOException e) {
            throw new JetelRuntimeException(e);
        }
    }
}
```

#### Best practices

If **Algorithm URL** is used, we recommend to explicitly specify **Charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | **CustomJavaWriter** is available since **4.1.0-M1**. |
| 5.3.0 | **CustomJavaWriter** can now propagate metadata - added new attributes [Metadata propagation algorithm](genericwriter.md#cjw-mpa) and [Metadata propagation algorithm class](genericwriter.md#cjw-mpac). |

#### See also

| [CustomJavaComponent](genericcomponent.md) |
| --- |
| [CustomJavaReader](genericreader.md) |
| [CustomJavaTransformer](generictransformer.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
