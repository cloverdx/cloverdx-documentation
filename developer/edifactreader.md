<!-- Development > Component reference > Readers > EDIFACTReader -->

### EDIFACTReader

![EDIFACTReader 64x64](../figures/EDIFACTReader-64x64.png)

| [Short description](edifactreader.md#short-description) |
| --- |
| [Ports](edifactreader.md#ports) |
| [Metadata](edifactreader.md#metadata) |
| [EDIFACTReader attributes](edifactreader.md#edifactreader-attributes) |
| [Details](edifactreader.md#details) |
| [EDIFACTReader Mapping Editor and message schema](edifactreader.md#edifactreader-mapping-editor-and-message-schema) |
| [Examples](edifactreader.md#examples) |
| [See also](edifactreader.md#see-also) |

#### Short description

**EDIFACTReader** reads data in EDIFACT format. All EDIFACT versions from `D.93A` to `D.22A` are supported.
> [!NOTE]
> Please note that **EDIFACTReader** component is only available in certain CloverDX plans. To find out more about licensing requirements, please contact *[sales@cloverdx.com](mailto:sales@cloverdx.com)*.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| EDIFACT file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For port reading. See [Reading from input port](examples-of-file-url-in-readers.md#reading-from-input-port). | One field (`byte`, `cbyte`, `string`) for specifying an input of the component. |
| Output | 0 | **✓** | For correct data records | Any[[1]](edifactreader.md#edifactreader-ports-note-1) |
| 1-n | [[2]](edifactreader.md#edifactreader-ports-note-2) | For correct data records | Any [[1]](edifactreader.md#edifactreader-ports-note-1) (each port can have different metadata). |  |

| 1 |  Metadata on each output port does not need to be the same. Each metadata can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions). |
| --- | --- |

| 2 |  Other output ports are required if the mapping requires it. |
| --- | --- |

#### Metadata

**EDIFACTReader** does not propagate metadata.

**EDIFACTReader** has a metadata template on its output port available.

Metadata on optional input port must contain `string`, `byte` or `cbyte` field.

Metadata on each output port does not need to be the same.

Each metadata can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### EDIFACTReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | Attribute specifying what data source(s) will be read (EDIFACT file, input port, dictionary). See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| EDIFACT version |  | Attribute specifying version of EDIFACT message. |  |
| EDIFACT message |  | Attribute specifying type of EDIFACT message. Possible values depend on selected **EDIFACT version**. |  |
| Mapping | [[1]](edifactreader.md#edifactreader-reference-1) | Mapping of the input EDIFACT structure to output ports. For more information, see [XMLExtract mapping definition](xmlextract.md#xmlextract-mapping-definition). |  |
| Mapping URL | [[1]](edifactreader.md#edifactreader-reference-1) | Name of an external file, including its path which defines mapping of the input EDIFACT structure to output ports. For more information, see [XMLExtract mapping definition](xmlextract.md#xmlextract-mapping-definition). |  |
| Advanced |  |  |  |
| Strict validation |  | Enables strict validation of the incoming values, their sizes and data types. Also checks that composite elements are not present in places where only simple elements are allowed. Produces error if any validation check finds a problem. | true (default) \| false |

| 1 |  One of these must be specified if **EDIFACT version** and **EDIFACT message** are used. If both are specified, **Mapping URL** has higher priority. |
| --- | --- |

#### Details

**EDIFACTReader** reads data from EDIFACT files using SAX technology.

**EDIFACTReader** can read individual values or entire subtrees of the EDIFACT structure. Individual values can be converted to any field type. Subtrees can be converted to **variant** fields. When reading into **variant** fields, all data types in the field will be **string** type.

Using **EDIFACTReader** is very similar to **XMLExtract**. attributes **EDIFACT version** and **EDIFACT message** define the expected structure (schema) of the input data. The schema is generated automatically.

Specifying **EDIFACT version** and **EDIFACT message** is optional. You can leave both attributes empty, in which case **EDIFACTReader** will read entire input data into a single **variant** field on first output port. Defining a mapping is not possible in this case.

#### EDIFACTReader Mapping Editor and message schema

**EDIFACTReader Mapping Editor** serves to define mapping from EDIFACT message structure to one or more output ports by drag and drop.

To be able to use the editor you have to specify **EDIFACT version** and **EDIFACT message**. The schema is created internally and cannot be modified.

Any other operations to set up mapping are described in above mentioned **XMLExtract**.

In **EDIFACTReader**, you can map input fields to the output in the same way as you map message fields. The input field mapping works in all three processing modes.

#### Examples

Mapping parts of EDIFACT message onto output metadata. It is possible to map a whole message or its part onto **variant** field or to map individual values to fields of other data types.

![EDIFACTReader example 01](../figures/EDIFACTReader-example-01.png)
*Figure 350. EDIFACTReader - mapping part of a message*

![EDIFACTReader example 02](../figures/EDIFACTReader-example-02.png)
*Figure 351. EDIFACTReader - mapping fields of a message*

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.13 | **EDIFACTReader** is available since **5.13.0**. |

#### See also

| [EDIFACTWriter](edifactwriter.md) |
| --- |
| [X12Reader](x12reader.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
