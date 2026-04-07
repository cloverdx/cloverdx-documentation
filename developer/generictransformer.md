<!-- Development > Component reference > Transformers > CustomJavaTransformer -->

### CustomJavaTransformer

![CustomJavaTransformer 64x64](../figures/CustomJavaTransformer-64x64.png)

| [Short description](generictransformer.md#short-description) |
| --- |
| [Ports](generictransformer.md#ports) |
| [Metadata](generictransformer.md#metadata) |
| [CustomJavaTransformer attributes](generictransformer.md#customjavatransformer-attributes) |
| [Details](generictransformer.md#details) |
| [Examples](generictransformer.md#examples) |
| [Best practices](generictransformer.md#best-practices) |
| [Compatibility](generictransformer.md#compatibility) |
| [See also](generictransformer.md#see-also) |

#### Short description

**CustomJavaTransformer** executes user-defined Java code.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | - | 0-n | 0-n | - | **✓** | **⨯** | **⨯** |

#### Ports

The number of ports depends on the Java code.

#### Metadata

By default, **CustomJavaTransformer** does not propagate metadata. Metadata propagation can be configured using the [Metadata propagation algorithm](generictransformer.md#cjt-mpa) and [Metadata propagation algorithm class](generictransformer.md#cjt-mpac) attributes.

**CustomJavaTransformer** has no metadata templates.

Requirements on metadata depend on a user-defined transformation.

#### CustomJavaTransformer attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Algorithm | [[1]](generictransformer.md#customjavatransformer-attributes-fn01) | A runnable transformation in Java defined in the graph. |  |
| Algorithm URL | [[1]](generictransformer.md#customjavatransformer-attributes-fn01) | A URL to an external file defining a runnable transformation in Java. |  |
| Algorithm class | [[1]](generictransformer.md#customjavatransformer-attributes-fn01) | An external runnable transformation class. |  |
| Advanced |  |  |  |
| Metadata propagation algorithm |  | An algorithm for metadata propagation written in Java. |  |
| Metadata propagation algorithm class |  | An external metadata propagation class. |  |
| Algorithm source charset |  | The encoding of the external file defining the transformation.  The default encoding depends on DEFAULT_SOURCE_CODE_CHARSET in defaultProperties. | UTF-8 |

| 1 |  One of these must be set. These transformation attributes must be specified. |
| --- | --- |

#### Details

**CustomJavaTransformer** executes the Java transformation. **CustomJavaTransformer** is a more specific **CustomJavaComponent** focused on transforming data.

There are other similar Java components: **CustomJavaReader**, **CustomJavaWriter** and **CustomJavaComponent**. All these components use a transformation defined in Java, they differ in templates being used.

You can use **Public CloverDX API** in this component. General parts of custom Java components and **Public CloverDX API** are described in [CustomJavaComponent](genericcomponent.md).

##### Java interfaces for CustomJavaTransformer

A transformation required by the component must extend the `org.jetel.component.AbstractGenericTransform` class.

The component has the same Java interface as **CustomJavaComponent**, but it provides a different Java template. See [Java interfaces for CustomJavaComponent](genericcomponent.md#java-interfaces-for-customjavacomponent).

##### Custom metadata propagation for CustomJavaTransformer

**CustomJavaTransformer** can propagate metadata using a custom algorithm. Metadata propagation algorithm must extend the `org.jetel.component.GenericMetadataProvider` class.

The component has the same Java interface as **CustomJavaComponent**, see [Custom metadata propagation for CustomJavaComponent](genericcomponent.md#custom-metadata-propagation-for-customjavacomponent).

#### Examples

##### Record Duplicator

Create a component duplicating input records.

###### Solution

```java
package jk;

import org.jetel.component.AbstractGenericTransform;
import org.jetel.data.DataRecord;
import org.jetel.exception.JetelRuntimeException;

/**
 * This is an example custom transformer. It shows how you can
 * duplicate all incoming records.
 */
public class CustomJavaTransformerExample01 extends AbstractGenericTransform {

    @Override
    public void execute() {
        try {
            DataRecord inRecord = inRecords[0];

            while ((inRecord = readRecordFromPort(0)) != null) {
                writeRecordToPort(0, inRecord);
                writeRecordToPort(0, inRecord);
            }
        } catch (Exception e) {
            throw new JetelRuntimeException(e);
        }
    }
}
```

Metadata on the input and output port must be the same for this example.

#### Best practices

If the transformation is specified in an external file (with **Algorithm URL**), we recommend to explicitly specify **Algorithm source charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.1.0-M1 | **CustomJavaTransformer** is available since **4.1.0-M1**. It replaced **JavaExecute**. |
| 5.3.0 | **CustomJavaTransformer** can now propagate metadata - added new attributes [Metadata propagation algorithm](generictransformer.md#cjt-mpa) and [Metadata propagation algorithm class](generictransformer.md#cjt-mpac). |

#### See also

| [CustomJavaComponent](genericcomponent.md) |
| --- |
| [CustomJavaReader](genericreader.md) |
| [CustomJavaWriter](genericwriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
