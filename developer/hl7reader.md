<!-- Development > Component reference > Readers > HL7Reader -->

### HL7Reader

![HL7Reader 64x64](../figures/HL7Reader-64x64.png)

| [Short description](hl7reader.md#short-description) |
| --- |
| [Ports](hl7reader.md#ports) |
| [Metadata](hl7reader.md#metadata) |
| [HL7Reader attributes](hl7reader.md#hl7reader-attributes) |
| [See also](hl7reader.md#see-also) |

#### Short description

**HL7Reader** reads data in HL7® version 2 format. [[1]](hl7reader.md#hl7reader-footnote1)

All HL7® v2 versions from `2.1` to `2.9` are supported.
> [!NOTE]
> Please note that **HL7Reader** component is only available in certain CloverDX plans. To find out more about licensing requirements, please contact *[sales@cloverdx.com](mailto:sales@cloverdx.com)*.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| HL7® v2 file | 0-1 | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For port reading. See [Reading from input port](examples-of-file-url-in-readers.md#reading-from-input-port). | One field (`byte`, `cbyte`, `string`) for specifying an input of the component. |
| Output | 0 | **✓** | For correct data records | Any[[1]](hl7reader.md#hl7reader-ports-note-1) |
| 1 | **⨯** | For validation errors (if **Strict validation** is enabled) | Any |  |

| 1 | Metadata have to have first field of the type **variant**. Metadata can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions). |
| --- | --- |

#### Metadata

**HL7Reader** propagates metadata on both output ports.

Metadata on optional input port must contain `string`, `byte` or `cbyte` field.

Metadata on first output port have to have first field of the type **variant**.

Metadata on first output port can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### HL7Reader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | **✓** | Attribute specifying what data source(s) will be read (HL7® v2 file, input port, dictionary). See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| Error mapping | **⨯** | Defines mapping of errors to the error output port. |  |
| Advanced |  |  |  |
| Strict validation |  | Enables strict schema validation of the input messages. Reports missing required segments, fields, components and subcomponents. Also reports if there are more fields, components and subcomponents than expected. Produces error if any validation check finds a problem. | true (default) \| false |
| Message schema URL | **⨯** | Attribute specifying XML schema used for parsing and validation of HL7® v2 message. By default the schema is auto-detected in the HL7® v2 message content. |  |
| Segments schema URL | **⨯** | Attribute specifying XML schema used for parsing and validation of HL7® v2 segments. By default the schema is auto-detected in the HL7® v2 message content. |  |

#### Details

**HL7Reader** reads data from HL7® version 2 files using SAX technology.

**HL7Reader** reads entire input file with the HL7® version 2 structure to structured **variant** field. All data types in the **variant** field will be **string** type.

Version and message type of the HL7® v2 standard are auto-detected. You can override auto-detection of version and message type by using external schema.

#### User defined message schema

**HL7Reader** can use user defined external schema. This schema has to have a XML structure defined internally in **CloverDX Designer**.

You can modify already existing message schema. Schema XML files are stored in jar file `hl7v2schema-[version].jar` which can be found in **CloverDX Designer** installation dir in path `plugins/com.cloveretl.gui.commercial_[version]/lib/plugins/org.jetel.component.commercial/lib`.

Schema files are organized in directories named by HL7® v2 version and each filename contains HL7® v2 message structure type. You can unpack required schema XML file, modify it and directly use it with **HL7Reader**. These files contain description of content and structure of particular HL7® v2 message. Content and structure of HL7® v2 segments is stored in `segments.xml`.

When modifying a schema the names of elements and attributes must stay the same, but their values can be changed.

When creating a new HL7® v2 segment the attribute **name** has to follow naming convention defined by HL7® standards.

Group segment is segment which serves as a logical group of segments. It’s never present in HL7® v2 message and unlike standard segments its name can be longer than 3 characters. For example **PATIENT**.

Standard HL7®v2 segment has to have an **name** in a form of 3 capital letters or numbers. For example **EVN**, **PID** or **PV1**.

When modifying segment structure in `segments.xml` its elements **field**, **component** and **subcomponent** has to be on a proper level since there can be only 3 levels. Field attribute **name** doesn’t have any fixed naming convention.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.16.0 | **HL7Reader** is available since **5.16.0**. |
| 6.0 | Format of XML schema used in **Message schema URL** and **Segments schema URL** was changed and schema from **5.16.0** can’t be used anymore. |

#### See also

| [EDIFACTReader](edifactreader.md) |
| --- |
| [X12Reader](x12reader.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |

| 1 | HL7® and FHIR® are the registered trademarks of Health Level Seven International. Use of these trademarks do not constitute an endorsement from HL7®. |
| --- | --- |
