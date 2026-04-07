<!-- Development > Component reference > Writers > LDAPWriter -->

### LDAPWriter

![LDAPWriter 64x64](../figures/LDAPWriter-64x64.png)

| [Short description](ldapwriter.md#short-description) |
| --- |
| [Ports](ldapwriter.md#ports) |
| [Metadata](ldapwriter.md#metadata) |
| [LDAPWriter attributes](ldapwriter.md#ldapwriter-attributes) |
| [Details](ldapwriter.md#details) |
| [See also](ldapwriter.md#see-also) |

#### Short description

**LDAPWriter** writes information to an LDAP directory.

It provides the logic to update information on an LDAP directory. An update can be add/delete entries, add/replace/remove attributes. Metadata must match LDAP object attribute name. "DN" metadata attribute is required.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| LDAP directory tree | 1 | 0-1 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For correct data records | Any |
| Output | 0 | **⨯** | For rejected records.  If the rejected port is connected, input records rejected by LDAP server get copied to output with fields with autofilling "ErrText" populated with an error message. | Input 0 |

#### Metadata

LDAPWriter does not propagate metadata.

LDAPWriter has no metadata template.

Metadata on the input must precisely match the LDAP object attribute name. The **Distinguished Name** metadata attribute is required. As the LDAP attributes are multivalued, their values can be separated by a pipe or a specified separator. String and byte are the only metadata types supported.

**Note** that [metadata field names](metadata-editor.md#metadata-field-name) have strict naming conventions; therefore, to map an LDAP attribute containing special characters (e.g. a dash) in its name, use a [metadata field label](metadata-editor.md#metadata-field-name). Metadata field labels can contain special characters and have a higher priority than field names for LDAP mapping. For example, to write into the `msDS-PrincipalName` LDAP attribute, use a field with label `msDS-PrincipalName` and any name that follows the naming convention (e.g. `msDS_PrincipalName`).

#### LDAPWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| LDAP URL | yes | The LDAP URL of the directory. Can be a list of URLs separated by a pipe. | pattern: `ldap://host:port/` |
| Action |  | Defines the action to be performed with the entry. | replace_attributes (default) \| add_entry \| remove_entry \| remove_attributes |
| User |  | User DN to be used when connecting to the LDAP directory. Similar to the following: `cn=john.smith,dc=example,dc=com`. |  |
| Password |  | The password to be used when connecting to the LDAP directory. |  |
| Advanced |  |  |  |
| Multi-value separator |  | **LDAPWriter** can handle keys with multiple values. These are delimited by this string or character. <none> is a special escape value which turns off this functionality, then only the first value is written. This attribute can only be used for `string` data type. When `byte` type is used, the first value is the only one that is written. | "\|" (default) \| other character or string |
| Fields to ignore |  | A semicolon-separated list of fields not to be sent to LDAP. For example, an ignored field which is optionally populated with an error message when sent out. |  |
| Binary attributes | no | A list of field names containing binary attributes.  By default `objectGUID` is added to the list of binary attributes. | e.g. objectGUID |
| LDAP Connection Properties | no | Java Property-like style of key-value definitions which will be added to LDAP connection environment. |  |

#### Details

`String`, `byte` and `cbyte` are the only metadata types supported. Most of the LDAP types are compatible with **CloverDX** string; however, for instance, the `userPassword` LDAP type is necessary to populate from byte data field. LDAP rules are applied: to add an entry, required attributes (even object class) are required in metadata.
> [!NOTE]
> LDAP attribute may be multivalued. The default value separator is a pipe and is reasonable only for string data fields.

##### Multivalue fields

LDAP attributes may be multivalued. It depends on the input field type how multi values are handled. If Single type, then separator in the field’s value may be used. If List, then each item from the list becomes one value of an attribute.

Only `string` and `byte` (`cbyte`) field types are supported, both in Single and List container types. If input data/record contains Map<String> field, then keys are mapped on attribute names and values become attribute values. In the case of a value string with **multiValueSeparator** (if defined), the value is first split into individual items which then become attribute’s multivalues.

#### See also

| [LDAPReader](ldapreader.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
