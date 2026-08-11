<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Mapping functions -->

### Mapping functions

Use these functions to parse field mapping parameters that are produced by the **Field mapping editor** for graph parameters which have **Field mapping** type.

A field mapping provides mapping between one or more source records and one target record. The mapping allows you to configure parameters to say "field X should map to field Y" and then handle this in code in some way using the functions described in this chapter.

Each mapping must map between at least one source record and exactly one target record. A mapping for single source record is composed of a semi-colon delimited list of target field - source field pairs. Each field name starts with a dollar sign (`$`). Semicolon at the end of the list (after last pair) is required.

```ctl
$targetField1=$sourceFieldA;$targetField2=$sourceFieldB;
```

A mapping that contains multiple sources includes multiple such strings separated by a hash (`#`) character like this:

```ctl
$targetField1=$firstSourceFieldA;$targetField2=$firstSourceFieldB;#$targetField3=$secondSourceFieldA;
```

Mappings are many-to-many - a source field can be mapped to multiple target fields, and multiple source fields can be mapped to one target field.

#### List of functions

| [getMappedSourceFields](mapping-functions-ctl2.md#getmappedsourcefields) |
| --- |
| [getMappedTargetFields](mapping-functions-ctl2.md#getmappedtargetfields) |
| [isSourceFieldMapped](mapping-functions-ctl2.md#issourcefieldmapped) |
| [isTargetFieldMapped](mapping-functions-ctl2.md#istargetfieldmapped) |

#### getMappedSourceFields

```ctl
list[string] getMappedSourceFields(string mapping, string targetField, integer sourceIndex);
list[string] getMappedSourceFields(string mapping, string targetField);
list[string] getMappedSourceFields(string mapping);
```

The `getMappedSourceFields` function returns the source fields at the specified source index (starting at 0) that are mapped to the named target field.

If `sourceIndex` is omitted, the function returns fields from all sources that are mapped to the named target field. The result can be ambiguous if the sets of source fields are not disjoint.

If `targetField` is also omitted, the function returns all source fields that are mapped to any target field.

##### Error states

- The function throws an exception if `mapping` is invalid or `null`.
- It also throws an exception if `sourceIndex` is out of bounds or `null`.

##### Examples
Example 248. Usage of getMappedSourceFields

```ctl
getMappedSourceFields("$customerId=$crmId;$email=$crmEmail;#$customerId=$orderCustomerId;$status=$orderStatus;", "customerId", 1);
   // returns ["orderCustomerId"]

getMappedSourceFields("$customerId=$accountId;$customerId=$legacyId;$status=$orderStatus;", "customerId");
   // returns ["accountId", "legacyId"]

getMappedSourceFields("$customerId=$accountId;$customerId=$legacyId;$status=$orderStatus;");
   // returns ["accountId", "legacyId", "orderStatus"]
```

##### Compatibility

- The `getMappedSourceFields` function is available since **CloverETL 4.1.0**.

##### See also

- [getMappedTargetFields](mapping-functions-ctl2.md#getmappedtargetfields)
- [isSourceFieldMapped](mapping-functions-ctl2.md#issourcefieldmapped)

---

#### getMappedTargetFields

```ctl
list[string] getMappedTargetFields(string mapping, string sourceField, integer sourceIndex);
list[string] getMappedTargetFields(string mapping, string sourceField);
list[string] getMappedTargetFields(string mapping);
```

The `getMappedTargetFields` function returns the corresponding target fields mapped from the named field at the specified source index (starting at 0).

If `sourceIndex` is omitted, the function returns target fields mapped from fields with the specified name in any source.

If `sourceField` is also omitted, the function returns all target fields that have a mapping.

##### Error states

- The function throws an exception if `mapping` is invalid or `null`.
- It also throws an exception if `sourceIndex` is out of bounds or `null`.

##### Examples
Example 249. Usage of getMappedTargetFields

```ctl
getMappedTargetFields("$billingCity=$city;$shippingCity=$city;#$billingCity=$location;$warehouseCity=$city;", "city", 1);
   // returns ["warehouseCity"]

getMappedTargetFields("$billingCity=$city;$shippingCity=$city;#$billingCity=$location;$warehouseCity=$city;", "city");
   // returns ["billingCity", "shippingCity", "warehouseCity"]

getMappedTargetFields("$customerId=$accountId;$customerId=$legacyId;$status=$orderStatus;");
   // returns ["customerId", "status"]
```

##### Compatibility

- The `getMappedTargetFields` function is available since **CloverETL 4.1.0**.

##### See also

- [getMappedSourceFields](mapping-functions-ctl2.md#getmappedsourcefields)
- [isTargetFieldMapped](mapping-functions-ctl2.md#istargetfieldmapped)

---

#### isSourceFieldMapped

```ctl
boolean isSourceFieldMapped(string mapping, string sourceField, integer sourceIndex);
boolean isSourceFieldMapped(string mapping, string sourceField);
```

The `isSourceFieldMapped` function returns `true` if the named field at the specified source index is mapped to any target field.

If `sourceIndex` is omitted, the function returns `true` if a field with the specified name in any source is mapped to a target field.

##### Error states

- The function throws an exception if `mapping` is invalid or `null`.
- It also throws an exception if `sourceIndex` is out of bounds or `null`.

##### Examples
Example 250. Usage of isSourceFieldMapped

```ctl
isSourceFieldMapped("$customerId=$crmId;$email=$crmEmail;#$customerId=$orderCustomerId;$status=$orderStatus;", "orderStatus", 1);
   // returns true

isSourceFieldMapped("$customerId=$crmId;$email=$crmEmail;#$customerId=$orderCustomerId;$status=$orderStatus;", "orderStatus", 0);
   // returns false

isSourceFieldMapped("$customerId=$accountId;$customerId=$legacyId;$status=$orderStatus;", "legacyId");
   // returns true

isSourceFieldMapped("$customerId=$accountId;$customerId=$legacyId;$status=$orderStatus;", "invoiceId");
   // returns false
```

##### Compatibility

- The `isSourceFieldMapped` function is available since **CloverETL 4.1.0**.

##### See also

- [getMappedSourceFields](mapping-functions-ctl2.md#getmappedsourcefields)
- [isTargetFieldMapped](mapping-functions-ctl2.md#istargetfieldmapped)

---

#### isTargetFieldMapped

```ctl
boolean isTargetFieldMapped(string mapping, string targetField);
```

The `isTargetFieldMapped` function returns `true` if any source field is mapped to the specified target field.

The function throws an exception if `mapping` is invalid or `null`.

##### Compatibility

- The `isTargetFieldMapped` function is available since **CloverETL 4.1.0**.
Example 251. Usage of isTargetFieldMapped

```ctl
isTargetFieldMapped("$customerId=$crmId;$email=$crmEmail;#$customerId=$orderCustomerId;$status=$orderStatus;", "status");
   // returns true

isTargetFieldMapped("$customerId=$accountId;$customerId=$legacyId;$status=$orderStatus;", "email");
   // returns false
```

##### See also

- [getMappedTargetFields](mapping-functions-ctl2.md#getmappedtargetfields)
- [isSourceFieldMapped](mapping-functions-ctl2.md#issourcefieldmapped)
