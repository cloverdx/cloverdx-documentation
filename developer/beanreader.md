<!-- Development > Component reference > Readers > JavaBeanReader -->

### JavaBeanReader

![JavaBeanReader 64x64](../figures/JavaBeanReader-64x64.png)

| [Short description](beanreader.md#short-description) |
| --- |
| [Ports](beanreader.md#ports) |
| [Metadata](beanreader.md#metadata) |
| [JavaBeanReader attributes](beanreader.md#javabeanreader-attributes) |
| [Details](beanreader.md#details) |
| [See also](beanreader.md#see-also) |

#### Short description

**JavaBeanReader** reads a [JavaBeans](http://en.wikipedia.org/wiki/Java_Bean) hierarchical structure which is stored in a dictionary. This allows *dynamic* data interchange between **CloverDX** graphs and external environment, such as the cloud. The dictionary you are reading to serves as an interface between the outer (e.g. the cloud) and inner worlds (**CloverDX**).

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Dictionary | 0 | 1-n | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | Successfully read records. | Any |
| 1-n | Connect other output ports if your mapping requires it. | Successfully read records. | Any. Each port can have different metadata. |  |

#### Metadata

JavaBeanReader does not propagate metadata.

JavaBeanReader has no metadata template.

#### JavaBeanReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Dictionary source | yes | The dictionary you want to read JavaBeans from. | The name of a dictionary you have previously defined. |
| Data policy |  | Determines the action after an error on reading occurs. For more information, see [Data policy](data-policy.md). | Strict (default) \| Controlled \| Lenient |
| Mapping | [[1]](beanreader.md#javabeanreader-attributes-fn01) | Mapping the input JavaBeans structure to output ports. For more information, see [JavaBeanReader mapping definition](beanreader.md#javabeanreader-mapping-definition). |  |
| Mapping URL | [[1]](beanreader.md#javabeanreader-attributes-fn01) | The external text file containing the mapping definition. |  |
| Implicit mapping |  | By default, you have to manually map input elements even to Clover fields of the same name. If you switch to `true`, JSON-to-CloverDX mapping on matching names will be performed automatically. This can save you a lot of effort in long and well-structured JSON files. See [JSON Mapping - Specifics](jsonreader.md#json-mapping-specifics). | false (default) \| true |

| 1 |  One of these has to be specified. If both are specified, **Mapping URL** has a higher priority. |
| --- | --- |

#### Details

**JavaBeanReader** reads data from JavaBeans through a dictionary. It maps Java attributes / collection elements to output records based on a mapping you define. You do not have to map the whole input file - you use XPath expressions to select only the data you need. The component sends data to different connected output records as defined by your mapping.

The mapping process is similar to the one in [XMLReader](xmlreader.md).

##### JavaBeanReader mapping definition

1. Every **Mapping** definition consists of `<Context>` tags which also contain some attributes and allow mapping of element names to Clover fields. Nested structure of `<Context>` tags is similar to the nested structure of elements in input JavaBeans.
2. Each `<Context>` tag can surround a serie of nested `<Mapping>` tags. These allow to rename JavaBeans elements to Clover fields. However, **Mapping** does not need to copy the whole input structure, it can start at an arbitrary depth in the tree.
3. Each of these `<Context>` and `<Mapping>` tags contains some [JavaBeanReader context tag attributes](beanreader.md#javabeanreader-context-tag-attributes) and [JavaBeanReader mapping tag attributes](beanreader.md#javabeanreader-mapping-tag-attributes), respectively.
   Example 365. Example Mapping in JavaBeanReader
   ```xml
   <Context xpath="/employees" outPort="0" sequenceId="empSeq" sequenceField="id">
           <Mapping xpath="firstName" cloverField="firstName"/>
           <Mapping xpath="lastName" cloverField="lastName"/>
           <Mapping xpath="salary" cloverField="salary"/>
           <Mapping xpath="jobTitle" cloverField="jobTitle"/>
           <Context xpath="children" outPort="1" parentKey="id" generatedKey="empID">
               <Mapping xpath="name" cloverField="chname"/>
               <Mapping xpath="age" cloverField="age"/>
           </Context>
           <Context xpath="benefits" outPort="2" parentKey="id" generatedKey="empID">
               <Mapping xpath="car" cloverField="car"/>
               <Mapping xpath="cellPhone" cloverField="mobilephone"/>
               <Mapping xpath="monthlyBonus" cloverField="monthlyBonus"/>
               <Mapping xpath="yearlyBonus" cloverField="yearlyBonus"/>
           </Context>
           <Context xpath="projects" outPort="3" parentKey="id" generatedKey="empID">
               <Mapping xpath="name" cloverField="projName"/>
               <Mapping xpath="manager" cloverField="projManager"/>
               <Mapping xpath="start" cloverField="Start"/>
               <Mapping xpath="end" cloverField="End"/>
               <Mapping xpath="customers" cloverField="customers"/>
           </Context>
       </Context>
   ```
   > [!IMPORTANT]
   > If you switch **Implicit mapping** to `true`, the elements (e.g. `salary`) will be automatically mapped onto fields of the same name (`salary`) and you do **not** have to write:
   >
   >
   > ```xml
   > <Mapping xpath="salary" cloverField="salary"/>
   > ```
   >
   >
   > and you map explicitly only to populate fields with data from distinct elements.
4. **JavaBeanReader Context Tags and Mapping Tags**
   - **Empty Context Tag (Without a Child)**
     `<Context xpath="xpathexpression"`[JavaBeanReader context tag attributes](beanreader.md#javabeanreader-context-tag-attributes)`/>`
   - **Non-Empty Context Tag (Parent with a Child)**
     `<Context xpath="xpathexpression"`[JavaBeanReader context tag attributes](beanreader.md#javabeanreader-context-tag-attributes)`>`
     `(nested Context and Mapping elements (only children, parents with one or more children, etc.)`
     `</Context>`
   - **Empty Mapping Tag (Renaming Tag)**
     - `xpath` is used:
       `<Mapping xpath="xpathexpression"`[JavaBeanReader mapping tag attributes](beanreader.md#javabeanreader-mapping-tag-attributes)`/>`
     - `nodeName` is used:
       `<Mapping nodeName="elementname"`[JavaBeanReader mapping tag attributes](beanreader.md#javabeanreader-mapping-tag-attributes)`/>`
5. **JavaBeanReader context tag and mapping tag attributes**
   1) **JavaBeanReader context tag attributes**
   - `xpath`
     Required
     The xpath expression can be any XPath query.
     Example: `xpath="/tagA/…/tagJ"`
   - `outPort`
     Optional
     The number of output port to which data is sent. If not defined, no data from this level of **Mapping** is sent out using such level of **Mapping**.
     Example: `outPort="2"`
   - `parentKey`
     Both `parentKey` and `generatedKey` must be specified.
     A sequence of metadata fields on the next parent level separated by a semicolon, colon, or pipe. The number and data types of all these fields must be the same in the `generatedKey` attribute or all values are concatenated to create a unique string value. In such a case, the key has only one field.
     Example: `parentKey="first_name;last_name"`
     Equal values of these attributes assure that such records can be joined in the future.
   - `generatedKey`
     Both `parentKey` and `generatedKey` must be specified.
     A sequence of metadata fields on the specified level separated by a semicolon, colon, or pipe. The number and data types of all these fields must be the same in the `parentKey` attribute or all values are concatenated to create a unique string value. In such a case, the key has only one field.
     Example: `generatedKey="f_name;l_name"`
     Equal values of these attributes assure that such records can be joined in the future.
   - `sequenceId`
     When a pair of `parentKey` and `generatedKey` does not insure unique identification of records, a sequence can be defined and used.
     Id of the sequence.
     Example: `sequenceId="Sequence0"`
   - `sequenceField`
     When a pair of `parentKey` and `generatedKey` does not insure unique identification of records, a sequence can be defined and used.
     A metadata field on the specified level in which the sequence values are written. Can serve as `parentKey` for the next nested level.
     Example: `sequenceField="sequenceKey"`

- `xpath`
  Either `xpath` or `nodeName` must be specified in the `<Mapping>` tag.
  XPath query.
  Example: `xpath="tagA/…/salary"`
- `nodeName`
  Either `xpath` or `nodeName` must be specified in the `<Mapping>` tag. Using `nodeName` is faster than using `xpath`.
  The JavaBeans node that should be mapped to Clover field.
  Example: `nodeName="salary"`
- `cloverField`
  Required
  Clover field to which the JavaBeans node should be mapped.
  The name of the field in the corresponding level.
  Example: `cloverFields="SALARY"`

##### Reading multivalue fields

As of **CloverDX 3.3**, reading multivalue fields is supported - you can read only lists, however (see [Multivalue fields](multivalue-fields.md)).
> [!NOTE]
> Reading maps is handled as reading pure `string` (for all data types as map’s values).
Example 366. Reading lists with JavaBeanReader
An example input file containing a list of three elements: `John, Vicky, Brian`

can be read back by the component with this mapping:

```xml
<Mapping xpath="attendees" cloverField="attendanceList"/>
```

where `attendanceList` is a field of your metadata. The metadata has to be assigned to the component’s output edge. After you run the graph, the field will get populated by data like this (what appears in **View data**):

`[John,Vicky,Brian]`

##### Data conversions in JavaBeanReader

The possible conversions of Java data types to CTL2 data types are described in the following table.

The list in the table means a list of corresponding data type.

|     Java data types | CTL2 data types |  |  |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Numeric data types |  |  |  | boolean | date | byte | cbyte | String | list | map |  |
| integer | long | number (double) | decimal |  |  |  |  |  |  |  |  |
| int | **✓** | **✓** | **✓** | **✓** | - | **⨯** | - | - | **✓** | **✓** | **⨯** |
| long | - | **✓** | **✓** | - | - | **✓** | - | - | **✓** | **✓** | **⨯** |
| float | - | - | **✓** | - | **⨯** | **⨯** | - | - | **✓** | **✓** | **⨯** |
| double | - | - | **✓** | - | **⨯** | **⨯** | - | - | **✓** | **✓** | **⨯** |
| boolean | **✓** | **✓** | **✓** | **⨯** | **✓** | **⨯** | - | - | **✓** | **✓** | **⨯** |
| java.util.Date | **⨯** | **✓** | **⨯** | **⨯** | **⨯** | **✓** | - | - | **✓** | **✓** | **⨯** |
| String | - | - | - | - | - | **⨯** | - | - | **✓** | **✓** | **⨯** |
| array [] | - | - | - | - | - | **⨯** | - | - | - | - | **⨯** |
| java.util.Collection | - | - | - | - | - | **⨯** | - | - | - | **✓** | **⨯** |

Conversions are explained below:

###### Java int to CTL2 boolean

Value 0 is converted to `false`, 1 is converted to `true`. If Java `int` contains other value, the graph fails.

###### Java int to CTL2 byte or cbyte

The value of the `int` variable is converted either to a character or to an empty string.

###### Java long to CTL2 integer

The value of the Java bean `long` variable can be read to the `integer` field provided the value is within the range of CTL2 `integer`. If the value is out of the range of CTL2 `integer`, the graph fails.

###### Java long to CTL2 decimal

The `decimal` needs to have a sufficient length to contain a value from `long` data type. The default length (12) might not be enough for all cases.

###### Java long to CTL2 boolean

The conversion from Java `long` to CTL2 `boolean` works in the same way as conversion from Java `int` to CTL2 `boolean`. 0 is converted to `false`, 1 is converted to `true`, other values cause a failure.

###### Java long to CTL2 byte or cbyte

See: Java `int` to CTL2 `byte` or `cbyte` conversion.

###### Java float to CTL2 integer

Value of the Java `float` variable can be converted to CTL2 `integer`. The value of the `float` number is being truncated in the conversion. If the value in `float` variable is out of range of `integer`, the conversion fails.

###### Java float to CTL2 long

The value of the Java `float` variable can be converted to CTL2 `long`. The value of the `float` number is being truncated. If the value stored in the float variable is positive and out of range of the `long` data type, the nearest `long` value is used. If the value stored in the float variable is negative and out of range of the `long` data type, the result is `null`.

###### Java float to CTL2 decimal

CTL2 `decimal` needs to have a sufficient length. If not, the conversion from Java `float` fails.

###### Java float to CTL2 byte and cbyte

The value of Java `float` is trimmed to its integral part and the result value is converted to a character. If the value is out of range of `byte`, an empty string is used.

###### Java double to CTL2 integer

The value of Java `double` needs to be within range of CTL2 `integer`. The value of Java `double` is truncated to its integral part towards zero. If the value is out of range, the conversion fails.

###### Java double to CTL2 long

If the value of Java `double`is within range of CTL2 `long`, the value is truncated to the nearest integral value towards zero. If the value of Java `double` is positive and out of range of CTL2 `long`, the result is the largest `long` number (`Long.MAX_VALUE`). If the value of Java `double` is negative and out of range of CTL `long`, the result is `null`.

###### Java double to CTL2 decimal

The CTL2 `decimal` needs to have a sufficient length to contain the value of Java `double`. In the case of insufficient length of CTL2 `decimal`, the conversion fails.

###### Java double to CTL2 byte and cbyte

The value of Java `double` is trimmed to its integral part and the result is converted to a character. If the value is out of range of `byte`, an empty string is used.

###### Java boolean to CTL2 byte and cbyte

The value of Java `boolean` converted to CTL2 `byte` or `cbyte` is a single unprintable character. The character has the code `0` if the input is `false` or `1` if the input is `true`.

###### Java Date to CTL2 byte and cbyte

The value of Java `Date` converted to `byte` or `cbyte` results in an empty string.

###### Java String to CTL2 integer or long

If the Java `String` variable contains *integral value* within range of `integer`, the number will be converted. Otherwise the conversion fails.

If the java `String` variable contains *integral value* within range of `long`, the number will be converted to `long`. Otherwise the conversion fails.

###### Java String to CTL2 number (double) or decimal

If the Java `String` contains a numeric value, the value is converted to `number` (`double`) or `decimal`. If the Java `String` does not contain a numeric value, the conversion fails.

###### Java String to CTL2 boolean

If the Java `String` contains the value `1`, `true`, `True` or `TRUE`, CTL2 `boolean` will hold `true`.

If Java `String` contains the value `0`, `false`, `False` or `FALSE`, CTL2 `boolean` will hold `false`.

If any other value is present in the Java `String`, the conversion fails.

###### Java String to CTL2 byte or cbyte

Java `String` to `byte` or `cbyte` conversion has an empty string as a result.

###### Java array to CTL2

The conversion of a Java bean array to `integer`, `long`, `number` (`double`) and `decimal` has zero as a result.

The result of the conversion from a Java array CTL2 `boolean` is `false`.

Java array converted to `byte` and `cbyte` is `null`.

###### Java Collection to CTL2

The conversion from Java `Collection` to `integer`, `long`, `double`, `decimal`, `String` returns first item of collection.

`Collection` to `byte` and `cbyte` conversion has an empty string as a result.

#### See also

| [Data Types in CTL2](language-reference-ctl2.md#data-types-in-ctl2) |
| --- |
| [Data types in metadata](metadata-records-and-fields.md#data-types-in-metadata) |
| [JavaBeanWriter](beanwriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
