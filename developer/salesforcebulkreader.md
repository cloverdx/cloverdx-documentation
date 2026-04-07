<!-- Development > Component reference > Readers > SalesforceBulkReader -->

### SalesforceBulkReader

![SalesforceBulkReader 64x64](../figures/SalesforceBulkReader-64x64.png)

| [Short description](salesforcebulkreader.md#short-description) |
| --- |
| [Ports](salesforcebulkreader.md#ports) |
| [Metadata](salesforcebulkreader.md#metadata) |
| [SalesforceBulkReader attributes](salesforcebulkreader.md#salesforcebulkreader-attributes) |
| [Details](salesforcebulkreader.md#details) |
| [Examples](salesforcebulkreader.md#examples) |
| [Compatibility](salesforcebulkreader.md#compatibility) |
| [See also](salesforcebulkreader.md#see-also) |

#### Short description

**SalesforceBulkReader** reads records from **Salesforce** using **Bulk API**.
> [!NOTE]
> Which Salesforce reader?
> If you need to read a small number of records, read attachments or use subqueries, use [SalesforceReader](salesforcereader.md).
>
> If you need to read a large number of records, use **SalesforceBulkReader**.

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Database | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | SOQL query results | output0 |

#### Metadata

**SalesforceBulkReader** does not propagate metadata.

**SalesforceBulkReader** has no metadata templates.

**SalesforceBulkReader** has no special requirements on metadata names or field data types.

#### SalesforceBulkReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | yes | A Salesforce connection. See [Salesforce connections](salesforce-connections.md). | e.g. MySFConnection |
| SOQL query | yes | A query for retrieving data from Salesforce.  The component allows you to use subset of the SOQL language. It is the constraint of the Bulk API.  If you query the records, you should use **API names** for objects and fields. The API name can differ from the name of an object in Salesforce web GUI.  You can use graph parameters in a SOQL query. | e.g. SELECT Name, Website FROM Account WHERE Industry = 'Energy' |
| Output mapping |  | Mapping from query fields to output metadata fields. | Map by name (default) |
| Advanced |  |  |  |
| Read mode |  | Enables or disables reading deleted or archived reports. You can choose between **Do not return deleted or archived records (default)** and **Return also deleted or archived records**.  This attribute is available since **4.6.0-M2**. |  |
| Result polling interval (seconds) |  | Time between queries for results of asynchronous calls.  The default value is taken from the connection configuration. | 5 (default) |

#### Details

**SalesforceBulkReader** reads records from Salesforce using Bulk API. Bulk API performs the operations asynchronously. It sends a request to Salesforce, waits several seconds and queries Salesforce for a result. The time interval is configured with the **Result polling interval** attribute. A shorter interval leads to quicker results, but consumes more of your Salesforce requests.

To use the component, create a Salesforce connection, enter an SOQL query, and specify the output mapping. If you perform the steps in this order, the transform editor can provide you with metadata extracted from the SOQL query. Therefore, you will be able to map the fields with drag and drop.

##### SOQL

**SalesforceBulkReader** uses Salesforce Object Query Language (SOQL) to query data in Salesforce. However, only a subset of the language is supported by the Bulk API. Because of that, following parts of SOQL are not supported by **SalesforceBulkReader**:

- COUNT
- ROLLUP
- SUM
- GROUP BY
- OFFSET
- FIELDS
- Nested queries
- Relationship fields

##### Order of Output Records

The output records come out in arbitrary order unless you use **ORDER BY** in your query.

##### SOAP or Bulk API

If you read more than 10-15,000 records, it is better to use Bulk API because it will use less API requests.

##### Notes and limitations

##### Address and Geolocation Compound Fields

Bulk API does not allow you to read compound fields, e.g. address compound fields. See [Compound fields](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/compound_fields.htm)

###### Attachments

Bulk API does not allow you to read base64 fields. Therefore, attachments cannot be read using **SalesforceBulkReader**.

###### API requests

**SalesforceBulkReader** uses multiple API calls during its run. All of them count towards your Salesforce **API request limit**. The precise call flow is:

1. Login
2. Extract fields of an expected result set from Salesforce object.
3. Create a bulk query job.
4. Create a batch with **SOQL query**.
5. Get job completion status. This call is repeated in an interval specified by the **Result polling interval** attribute until the job is completed.
6. Download a list of results sets.
7. Download query results. The number of calls depends on the size of returned data. Salesforce limits the size of a single query result to 1GB.
8. Close the bulk query job.

##### Error messages

When working with **SalesforceBulkReader**, you can hit the limitations of the Bulk API. The following error messages should help you identify the problem.

###### FUNCTIONALITY_NOT_ENABLED: Selecting compound data not supported in Bulk Query

The SOQL query asks for a compound data field (e.g. address), but this operation is not supported by the Bulk API. Query the particular fields of the compound field instead.

See [Address Compound Fields](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/compound_fields_address.htm)

#### Examples

| [Reading records from Salesforce](salesforcebulkreader.md#reading-records-from-salesforce) |
| --- |
| [Reading addresses](salesforcebulkreader.md#reading-addresses) |
| [Reading object IDs](salesforcebulkreader.md#reading-object-ids) |

##### Reading records from Salesforce

This example shows the basic use case of **SalesforceBulkReader**.

Read **Account name**, **Industry** and **Website** fields from **Account**.

###### Solution

Create a Salesforce connection.

In **SalesforceBulkReader**, set up the **Connection**, **SOQL Query** and **Output mapping** attributes.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| SOQL query | SELECT Name, Industry, Website FROM Account |
| Output mapping | See the code below |

```ctl
//#CTL2

function integer transform() {
    $out.0.Name = $in.0.Name;
    $out.0.Industry = $in.0.Industry;
    $out.0.Website = $in.0.Website;

    return ALL;
}
```

You can use output mapping if you have specified the SOQL query attribute.
> [!TIP]
> Creating a metadata with SalesforceBulkReader
> Connect an edge to the output port. In Output mapping, select the fields in the left side and drag them to the right side.

##### Reading addresses

This example shows a way to read addresses.

Read the names and shipping addresses (street, city, state/province, postal code, and country) of customers from energy industry.

###### Solution

Create a Salesforce connection.

In **SalesforceBulkReader**, fill in the **Connection**, **SOQL Query** and **Output mapping** attributes.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| SOQL query | SELECT Name, ShippingStreet, ShippingCity, ShippingPostalcode, ShippingState, ShippingCountry FROM Account WHERE Industry = 'Energy' |
| Output mapping | See the code below |

```ctl
//#CTL2

function integer transform() {
    $out.0.Name = $in.0.Name;
    $out.0.ShippingStreet = $in.0.ShippingStreet;
    $out.0.ShippingCity = $in.0.ShippingCity;
    $out.0.ShippingPostalCode = $in.0.ShippingPostalCode;
    $out.0.ShippingState = $in.0.ShippingState;
    $out.0.ShippingCountry = $in.0.ShippingCountry;

    return ALL;
}
```

##### Reading object IDs

This example shows reading object IDs from Salesforce.

Read product names and object IDs of our Animal product family.

###### Solution

Create a Salesforce connection.

In **SalesforceBulkReader**, set **Connection**, **SOQL query** and **Output mapping**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| SOQL query | SELECT Id, Name FROM Product2 WHERE Family = 'Animal' |
| Output mapping | See the code below |

```ctl
//#CTL2

function integer transform() {
    $out.0.Id = $in.0.Id;
    $out.0.Name = $in.0.Name;

    return ALL;
}
```

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.3.0-M2 | **SalesforceBulkReader** is available since **4.3.0-M2**. It uses Salesforce Bulk API version 37.0. |
| 4.5.0-M2 | **SalesforceBulkReader** uses Salesforce Bulk API version 39.0. |
| 4.6.0-M2 | **SalesforceBulkReader** can now also read deleted or archived records. Use the **Read mode** attribute. |
| 5.2.0 | **SalesforceBulkReader** uses Salesforce Bulk API version 45.0. |
| 5.3.0 | **SalesforceBulkReader** uses Salesforce Bulk API version 46.1. |
| 5.16.0 | **SalesforceBulkReader** uses Salesforce Bulk API version 55.2. |

#### See also

| [SalesforceReader](salesforcereader.md) |
| --- |
| [SalesforceBulkWriter](salesforcebulkwriter.md) |
| [SalesforceWriter](salesforcewriter.md) |
| [SalesforceEinsteinWriter](salesforcewavewriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
| [Salesforce connections](salesforce-connections.md) |
| [Extracting metadata from Salesforce](creating-metadata.md#extracting-metadata-from-salesforce) |
