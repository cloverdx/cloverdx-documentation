<!-- Development > Component reference > Others > SequenceChecker -->

### SequenceChecker

![SequenceChecker 64x64](../figures/SequenceChecker-64x64.png)

| [Short description](sequencechecker.md#short-description) |
| --- |
| [Ports](sequencechecker.md#ports) |
| [Metadata](sequencechecker.md#metadata) |
| [SequenceChecker attributes](sequencechecker.md#sequencechecker-attributes) |
| [See also](sequencechecker.md#see-also) |

#### Short description

**SequenceChecker** checks the sort order of input data records.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs[[1]](sequencechecker.md#sequencechecker-footnote1) | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1-n | **✓** | **⨯** | **⨯** | **✓** |

| 1 |  The component sends each data record to all connected output ports. |
| --- | --- |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0-n | **⨯** | For checked and copied data records. | Input 0[[1]](sequencechecker.md#sequencechecker-footnote2) |

| 1 |  If data records are sorted properly, they can be sent to the connected output port(s). |
| --- | --- |

#### Metadata

All metadata must be the same.

Metadata can be propagated through this component.

#### SequenceChecker attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Sort key | yes | The key according to which records should be sorted. If they are sorted in any other way, the graph fails. For more information, see [Sort key](components.md#sort-key). |  |
| Unique keys |  | By default, values of **Sort key** should be unique. If set to `false`, values of **Sort key** can be duplicated. | true (default) \| false |
| Equal NULL |  | By default, records with null values of fields are considered to be equal. If set to `false`, nulls are considered to be different. | true (default) \| false |
| Deprecated |  |  |  |
| Sort order |  | Order of sorting (`Ascending` or `Descending`). Can be denoted by the first letter (`A` or `D`) only. The same for all key fields. Default sort order is ascending. If records are not sorted this way, the graph fails. | Ascending (default) \| Descending |
| Locale |  | Locale to be used when internationalization is set to `true`. By default, a system value is used unless the value of **Locale** specified in the `defaultProperties` file is uncommented and set to desired **Locale**. For more information on how **Locale** may be changed in the `defaultProperties`, see [Engine configuration](../admin/designer-configuration.md#engine-configuration). | a system value or specified default value (default) \| other locale |
| Use internationalization |  | By default, no internationalization is used. If set to `true`, sorting according national properties is performed. | false (default) \| true |

#### Details

**SequenceChecker** receives data records through its single input port and checks their sort order. If this does not correspond to the specified **Sort key**, the graph fails. If the sort order corresponds to the specified **Sort key**, data records can optionally be sent to all connected output port(s).

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
