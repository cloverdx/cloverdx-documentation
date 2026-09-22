<!-- Development > Component reference > Readers > XMLReader -->

### XMLReader

![XMLReader 64x64](../figures/XMLReader-64x64.png)

| [Short description](xmlreader.md#short-description) |
| --- |
| [Ports](xmlreader.md#ports) |
| [Metadata](xmlreader.md#metadata) |
| [XMLReader attributes](xmlreader.md#xmlreader-attributes) |
| [Details](xmlreader.md#details) |
| [Examples](xmlreader.md#examples) |
| [Best practices](xmlreader.md#best-practices) |
| [Compatibility](xmlreader.md#compatibility) |
| [See also](xmlreader.md#see-also) |

#### Short description

**XMLReader** reads data from XML files using DOM technology. It can also read data from compressed files, input port, and dictionary.
> [!NOTE]
> Which XML Component?
> Generally, use [XMLExtract](xmlextract.md). It is fast and has GUI to map elements to records. It is based on SAX.
>
> **XMLReader** can use more complex XPath expressions than **XMLExtract**; for example, it allows you to reference siblings. On the other hand, **XMLReader** is slower and needs more memory than **XMLExtract**. **XMLReader** is based on DOM.
>
> **XMLReader** supersedes the original [XMLXPathReader](xmlxpathreader.md). **XMLXPathReader** can use more complex XPath expressions than **XMLExtract**. **XMLXPathReader** uses DOM.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs[[1]](xmlreader.md#xmlreader-footnote1) | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| XML file | 0-1 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

| 1 |  **XMLReader**, **XMLExtract** and **XMLXPathReader** send data to ports as defined in their **Mapping** or **Mapping URL** attribute. |
| --- | --- |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | For port reading. See [Reading from input port](examples-of-file-url-in-readers.md#reading-from-input-port). | One field (`byte`, `cbyte`,`string`). |
| Output | 0 …​ n-1 | **✓** | For correct data records. Connect more than one output ports if your mapping requires that. | Any |
| n | **⨯** | Error port | Restricted format. See [Metadata](xmlreader.md#metadata). |  |

#### Metadata

##### Metadata Propagation

XMLReader does not propagate metadata.

##### Metadata Templates

XMLReader has metadata templates on the error port. There are two templates: **XMLReader_TreeReader_ErrPortWithoutFile** and **XMLReader_TreeReader_ErrPortWithFile**.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 0 | port | integer | The number of the output port where errors occurred. |
| 1 | recordNumber | integer | Record number (per source and port). |
| 2 | fieldNumber | integer | Field number |
| 3 | fieldName | string | Field name |
| 4 | value | string | The value which caused the error. |
| 5 | message | string | Error message |
| 6 | file | string | Source name; This field is optional |

##### Requirements on Metadata

Input metadata has one field with datatype `byte`, `cbyte` or `string`.

The metadata on each of the output ports does not need to be the same. Each of these metadata can use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

If you intend to use the last output port for error logging, metadata must have a fixed format. Field names can be arbitrary, field types must be same as from the template.

#### XMLReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| File URL | yes | Specifies which data source(s) will be read (XML file, input port, dictionary). See [Supported file URL formats for Readers](examples-of-file-url-in-readers.md). |  |
| Charset |  | Encoding of records that are read. When reading from files, the charset is detected automatically (unless you specify it yourself).  **Important:** if you are reading from a port or dictionary, always set **Charset** explicitly (otherwise errors will occur). There is no autodetection as in reading from files. | ISO-8859-1 (default) \| <other encodings> |
| Data policy |  | Determines what should be done when an error occurs. For more information, see [Data policy](data-policy.md) | Strict (default) \| Controlled \| Lenient |
| Mapping | [[1]](xmlreader.md#xmlreader-attributes-fn01) | The mapping of the input XML structure to output ports. For more information, see [Mapping definition](xmlreader.md#defining-the-mapping). |  |
| Mapping URL | [[1]](xmlreader.md#xmlreader-attributes-fn01) | An external text file containing the mapping definition. For more information, see [Mapping definition](xmlreader.md#defining-the-mapping). |  |
| Implicit mapping |  | If true, map element values to the fields having a same name in record. Example: An element (`salary`) is automatically mapped onto field of the same name (`salary`). | false (default) \| true |
| Advanced |  |  |  |
| XML features |  | A sequence of individual `true`/`false` expressions related to XML features which should be validated. The expressions are separated from each other by a semicolon. For more information, see [XML features](xml-features.md). |  |

| 1 |  One of these has to be specified. If both are specified, **Mapping URL** has a higher priority. |
| --- | --- |

#### Details

| [Mapping definition](xmlreader.md#defining-the-mapping) |
| --- |
| [Context Tag attributes](xmlreader.md#xmlreader-context-tag-attributes) |
| [Mapping Tag attributes](xmlreader.md#xmlreader-mapping-tag-attributes) |
| [Input Mapping attributes](xmlreader.md#xmlreader-input-mapping-attributes) |
| [Reading multivalue fields](xmlreader.md#reading-multivalue-fields) |
| [Mapping Input Fields](xmlreader.md#mapping-input-fields) |

Records and fields to be send out to the output ports are specified using XML elements and attributes. Each `Context` element corresponds to one output port attached. Each `Mapping` element defines a mapping to one field. See the example below.
Example 385. Mapping in XMLReader

```xml
<Context xpath="/employees/employee" outPort="0">
    <Mapping nodeName="salary" cloverField="basic_salary"/>
    <Mapping xpath="name/firstname" cloverField="firstname"/>
    <Mapping xpath="name/surname" cloverField="surname"/>
    <Context xpath="child" outPort="1" parentKey="empID" generatedKey="parentID"/>
    <Context xpath="benefits" outPort="2" parentKey="empID;jobID" generatedKey="empID;jobID"
            sequenceField="seqKey" sequenceId="Sequence0">
        <Context xpath="financial" outPort="3" parentKey="seqKey" generatedKey="seqKey"/>
    </Context>
    <Context xpath="project" outPort="4" parentKey="empID;jobID" generatedKey="empID;jobID">
        <Context xpath="customer" outPort="5" parentKey="projName;projManager;inProjectID;Start"
                generatedKey="joinedKey"/>
    </Context>
</Context>
```

The nested structure of `<Context>` tags is similar to the nested structure of XML elements in input XML files.

However, the **Mapping** attribute does not need to copy whole XML structure, it can start at the specified level inside the whole XML file.

##### Defining the Mapping

- The **Mapping** definition is specified in the **Mapping URL** attribute or in the **Mapping** attribute.
- Every **Mapping** definition consists of `<Context>` tags. Each `<Context>` tag defines a mapping of particular XML subtree to record being sent to the specified output port.
- Each `<Context>` tag can surround a serie of nested `<Mapping>` tags. These allow to map XML elements or attributes to Clover fields.
- Each of these `<Context>` and `<Mapping>` tags contains some [Context Tag attributes](xmlreader.md#xmlreader-context-tag-attributes) and [Mapping Tag attributes](xmlreader.md#xmlreader-mapping-tag-attributes), respectively.

###### XMLReader Context Tags and Mapping Tags

- **Empty Context Tag (Without a Child)**
  `<Context xpath="xpathexpression" />`
  See [Context Tag attributes](xmlreader.md#xmlreader-context-tag-attributes).
- **Non-Empty Context Tag (Parent with a Child)**
  `<Context xpath="xpathexpression">`
  `(nested Context and Mapping elements (only children, parents with one or more children, etc.)`
  `</Context>`
  See [Context Tag attributes](xmlreader.md#xmlreader-context-tag-attributes).
- **Empty Mapping Tag (Renaming Tag)**
  - `xpath` is used:
    `<Mapping xpath="xpathexpression" />`
  - `nodeName` is used:
    `<Mapping nodeName="elementname" />`
  [Mapping Tag attributes](xmlreader.md#xmlreader-mapping-tag-attributes)

##### XMLReader Context Tag attributes

| [xpath](xmlreader.md#xmlreader-context-xpath) |
| --- |
| [outPort](xmlreader.md#xmlreader-outport) |
| [parentKey](xmlreader.md#xmlreader-parentkey) |
| [generatedKey](xmlreader.md#xmlreader-generatedkey) |
| [sequenceId](xmlreader.md#xmlreader-sequenceid) |
| [sequenceField](xmlreader.md#xmlreader-sequencefield) |
| [namespacesPath](xmlreader.md#xmlreader-context-tag-namespacepaths) |

- `xpath`
  Required
  The xpath expression can be any XPath query.
  Example: `xpath="/tagA/…/tagJ"`
- `outPort`
  Optional
  The number of an output port to which data is sent. If not defined, no data from this level of **Mapping** is sent out using such level of **Mapping**.
  Example: `outPort="2"`
- `parentKey`
  Both `parentKey` and `generatedKey` must be specified.
  The sequence of metadata fields on the next parent level separated by a semicolon, colon, or pipe. Number and data types of all these fields must be the same in the `generatedKey` attribute or all values are concatenated to create a unique string value. In such a case, the key has only one field.
  Example: `parentKey="first_name;last_name"`
  Equal values of these attributes assure that such records can be joined in the future.
- `generatedKey`
  Both `parentKey` and `generatedKey` must be specified.
  The sequence of metadata fields on the specified level separated by a semicolon, colon, or pipe. Number and data types of all these fields must be the same in the `parentKey` attribute or all values are concatenated to create a unique string value. In such a case, the key has only one field.
  Example: `generatedKey="f_name;l_name"`
  Equal values of these attributes assure that such records can be joined in the future.
- `sequenceId`
  When a pair of `parentKey` and `generatedKey` does not insure a unique identification of records, a sequence can be defined and used.
  Id of the sequence.
  Example: `sequenceId="Sequence0"`
- `sequenceField`
  When a pair of `parentKey` and `generatedKey` does not insure a unique identification of records, a sequence can be defined and used.
  A metadata field on the specified level in which the sequence values are written. Can serve as `parentKey` for the next nested level.
  Example: `sequenceField="sequenceKey"`
- `namespacePaths`
  Optional
  Default namespaces that should be used for the `xpath` attribute specified in the `<Context>` tag.
  Pattern: `namespacePaths='prefix1="URI1";…;prefixN="URIN"'`
  Example: `namespacePaths='n1="http://www.w3.org/TR/html4/";n2="http://ops.com/"'`.
  > [!NOTE]
  > Remember that if the input XML file contains a default namespace, this `namespacePaths` must be specified in the corresponding place of the **Mapping** attribute. In addition, `namespacePaths` is inherited from the `<Context>` element and used by the `<Mapping>` elements.

##### XMLReader Mapping Tag attributes

| [xpath](xmlreader.md#xmlreader-mapping-xpath) |
| --- |
| [nodeName](xmlreader.md#xmlreader-mapping-nodename) |
| [cloverField](xmlreader.md#xmlreader-cloverfield) |
| [trim](xmlreader.md#xmlreader-trim) |
| [namespacePaths](xmlreader.md#xmlreader-mapping-tag-namespacepaths) |

- `xpath`
  Either `xpath` or `nodeName` must be specified in the `<Mapping>` tag.
  XPath query.
  Example: `xpath="tagA/…/salary"`
- `nodeName`
  Either `xpath` or `nodeName` must be specified in the `<Mapping>` tag. Using `nodeName` is faster than using `xpath`.
  XML node that should be mapped to Clover field.
  Example: `nodeName="salary"`
- `cloverField`
  Required
  A Clover field to which XML node should be mapped.
  The name of the field in the corresponding level.
  Example: `cloverField="SALARY"`
- `trim`
  Optional
  Specifies whether leading and trailing white spaces should be removed. By default, it removes both leading and trailing white spaces.
  Example: `trim="false"` (white spaces will not be removed)
- `namespacePaths`.
  Optional
  Default namespaces that should be used for the `xpath` attribute specified in the `<Mapping>` tag.
  Pattern:¨`namespacePaths='prefix1="URI1";…;prefixN="URIN"'`
  Example: `namespacePaths='n1="http://www.w3.org/TR/html4/";n2="http://ops.com/"'`
  > [!NOTE]
  > Remember that if the input XML file contains a default namespace, this `namespacePaths` must be specified in the corresponding place of the **Mapping** attribute. In addition, `namespacePaths` is inherited from the `<Context>` element and used by the `<Mapping>` elements.

##### XMLReader Input Mapping attributes

- `cloverField`
  Required
  Output Clover field to input should be mapped.
  Example: `cloverField="SALARY"`
- `inputField`
  Required
  Input field to be used.
  Example: `inputField="SALARY"`

##### Reading multivalue fields

You can read only lists, however (see [Multivalue fields](multivalue-fields.md)).
> [!NOTE]
> Reading maps is handled as reading pure `string` (for all data types as map’s values).
Example 386. Reading lists with XMLReader
An example input file containing these elements (just a code snippet):

```xml
...
<attendees>John</attendees>
<attendees>Vicky</attendees>
<attendees>Brian</attendees>
...
```

can be read back by the component with this mapping:

```xml
<Mapping xpath="attendees" cloverField="attendanceList"/>
```

where `attendanceList` is a field of your metadata. The metadata has to be assigned to the component’s output edge. After you run the graph, the field gets populated by XML data like this (this will be seen in **View data**):

`[John,Vicky,Brian]`

##### Mapping Input Fields

If you use input port reading in `discrete` or `source` mode, you can map particular input fields to output fields using the `inputField` attribute.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Context xpath="/rootPath" outPort="0">
 	<Mapping cloverField="field2" inputField="field2"/>
</Context>
```

#### Examples

| [Reading an XML File](xmlreader.md#reading-an-xml-file) |
| --- |
| [Mapping Input Fields to Output](xmlreader.md#mapping-input-fields-to-output) |
| [Sending Nested Elements to Different Output Ports](xmlreader.md#sending-nested-elements-to-different-output-ports) |
| [Reading XML with namespace](xmlreader.md#reading-xml-with-namespace) |

##### Reading an XML File

This example shows the basic usage of **XMLReader**.

You have a `retail.xml` file with data about your retail sale.

```xml
<?xml version="1.0" ?>
<orders>
    <order id="1">
        <firstname>John</firstname>
        <surname>Smith</surname>
        <emails>
            <email>john.black@example.com</email>
            <email>jblack@example.info</email>
        </emails>
        <item>
            <goodName>table</goodName>
            <items>1</items>
        </item>
    </order>
    <order id="2">
        <firstname>Ellen</firstname>
        <surname>Smith</surname>
        <emails>
            <email>e-tailor@example.net</email>
        </emails>
        <item>
            <goodName>chair</goodName>
            <items>3</items>
        </item>
        <item>
            <goodName>tablecloth</goodName>
            <item>2</item>
        </item>
    </order>
</orders>
```

Create a list containing order_id, customer first name, surname and email(s).

###### Solution

Create a **metadata** having 4 fields: order_id (integer), name (string), surname (string), email (string[]).

Set up the attributes **File URL**, **Implicit mapping** and **Mapping**.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/retail.xml |
| Mapping | See the xml below. |
| Implicit mapping | true |

If you set **Implicit mapping** to `true`, fields name and surname are populated by values of corresponding elements.

Content of the **Mapping** attribute:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Context xpath="/orders/order" outPort="0">
    <Mapping cloverField="order_id" xpath="@id"/>
    <Mapping cloverField="email" xpath="./emails/email"/>
</Context>
```

The **XMLReader** will send following 2 records to its first output port.

```
1  John   Smith  [john.black@example.com, jblack@example.info]
2  Ellen  Smith  [e-tailor@example.net]
```

##### Mapping Input Fields to Output

This example shows reading an input file while some input fields are mapped to an output.

Given a list of customers and paths to the files with orders.

```
C001|./file001.xml
C002|./file002.xml
```

Each file can contain one or more products:

```xml
<?xml version="1.0" ?>
<products>
    <product>A</product>
    <product>B</product>
</products>
```

Create a list with customers and products:

```
C001|A
C001|B
C002|E
```

###### Solution

Use the **File URL**, **Charset** and **Mapping** attributes.

| Attribute | Value |
| --- | --- |
| File URL | port:$0.filename:source |
| Charset | UTF-8 |
| Mapping | See the code below |

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>

<Context xpath="/products/product" outPort="0">
    <Mapping cloverField="productID" xpath="."/>
    <Mapping cloverField="customerID" inputField="ID"/>
</Context>
```

##### Sending Nested Elements to Different Output Ports

This example shows reading of an input file with nested elements. The nested elements on different levels are sent out to the different output ports.

The input file `countries-and-counties.xml` contains a list of countries. Each country has a name and contains several counties. Each county has a name.

```xml
<?xml version="1.0"?>
<countries>
    <country>
        <name>England</name>
        <county>
            <name>Bristol</name>
        </county>
        <county>
            <name>Cumbria</name>
        </county>
        <county>
            <name>Devon</name>
        </county>
    </country>
    <country>
        <name>Scotland</name>
        <county>
            <name>Edinburgh</name>
        </county>
        <county>
            <name>Fife</name>
        </county>
    </country>
</countries>
```

Make a list of countries, and a list of counties with corresponding countries.

###### Solution

Assign metadata **country** with the field **countryName** to the edge on the first output port.

Assign metadata **county** with the fields **countryName** and **countyName** to the edge on the second output port.

Use the **File URL**, **Charset** and **Mapping** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/countries-and-counties.xml |
| Charset | UTF-8 |
| Mapping | See the code below |

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Context xpath="/countries/country" outPort="0">
    <Mapping cloverField="countryName" xpath="name"/>
    <Context xpath="./county" outPort="1">
        <Mapping cloverField="countryName" xpath="../name" />
        <Mapping cloverField="countyName" xpath="name"/>
    </Context>
</Context>
```

The records sent to the first output port are:

```
England
Scotland
```

The records sent to the second output port are:

```
England	 | Bristol
England  | Cumbria
England  | Devon
Scotland | Edinburgh
Scotland | Fife
```

##### Reading XML with namespace

This example shows you how to read XML that contains different namespaces.

A web page contains SVG graphics and links to other web pages. The links (`<a>`) are of two namespaces: `xhtml` and `svg`. Get URLs of the links from SVG image.

```xml
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    </head>
    <body>
        <svg width="1024" height="768"
            xmlns="http://www.w3.org/2000/svg" version="1.1">
            <a href="http://www.cloverdx.com">
                <circle cx="512" cy="384" r="80"/>
            </a>
        </svg>
        <p>
            <a href="http://www.example.com">www.example.com</a>
        </p>
    </body>
</html>
```

###### Solution

Use the **File URL**, **Charset** and **Mapping** attributes.

| Attribute | Value |
| --- | --- |
| File URL | ${DATAIN_DIR}/page.xhtml |
| Charset | UTF-8 |
| Mapping | See the code below |

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Context xpath="/xhtml:html//svg:a"
         namespacePaths='xhtml="http://www.w3.org/1999/xhtml";svg="http://www.w3.org/2000/svg"'
         outPort="0">
    <Mapping cloverField="field1" xpath="@href"/>
</Context>
```

The output contains URL:

```
http://www.cloverdx.com
```

#### Best practices

##### Implicit Mapping

To avoid typing lines like:

```xml
<Mapping xpath="salary" cloverField="salary"/>
```

Switch on the [implicit mapping](xmlreader.md#xmlreader-implicit-mapping) and use explicit mapping only to populate fields with data from distinct elements.

##### Avoid Unnecessary Context Elements

The `<Context>` element should be used only if you intend to send record corresponding to subtree to the output.

Use

```xml
<Context xpath="/elem1/elem11" outPort="0">
    <Mapping cloverField="field1" xpath="elem111"/>
</Context>
```

instead of

```xml
<Context xpath="/elem1">
    <Context xpath="elem11" outPort="0">
        <Mapping cloverField="field1" xpath="elem111"/>
    </Context>
</Context>
```

##### Specify Charset

We recommend users to explicitly specify **Charset**.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 3.3 | **XMLReader** is available since **3.3.x**.  Reading multivalue fields is now supported; however, you can read only lists (see [Multivalue fields](multivalue-fields.md)). |
| 4.1.0-M1 | You can now assign values of fields from an input port to fields on an output port. |

#### See also

| [JSONReader](jsonreader.md) |
| --- |
| [XMLExtract](xmlextract.md) |
| [XMLXPathReader](xmlxpathreader.md) |
| [XMLWriter](extxmlwriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
