<!-- Development > Component reference > Readers > SalesforceReader -->

### SalesforceReader

![SalesforceReader 64x64](../figures/SalesforceReader-64x64.png)

| [Short description](salesforcereader.md#short-description) |
| --- |
| [Ports](salesforcereader.md#ports) |
| [Metadata](salesforcereader.md#metadata) |
| [SalesforceReader attributes](salesforcereader.md#salesforcereader-attributes) |
| [Details](salesforcereader.md#details) |
| [Examples](salesforcereader.md#examples) |
| [Compatibility](salesforcereader.md#compatibility) |
| [See also](salesforcereader.md#see-also) |

#### Short description

**SalesforceReader** reads records from **Salesforce** using **SOAP API**.
> [!NOTE]
> Which Salesforce reader?
> If you need to read a small number of records, read attachments or use functions and subqueries, use **SalesforceReader**.
>
> If you need to read a large number of records, use [SalesforceBulkReader](salesforcebulkreader.md).

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Database | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | SOQL query results | output0 |

#### Metadata

**SalesforceReader** does not propagate metadata.

**SalesforceReader** has no metadata templates.

**SalesforceReader** has no special requirements on metadata names or field data types.

#### SalesforceReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | yes | A Salesforce connection. See [Salesforce connections](salesforce-connections.md). | e.g. MySFConnection |
| SOQL query | yes | A query for retrieving data from Salesforce.  The component allows you to use subset of the SOQL language.  If you query the records, you should use **API names** for objects and fields. The API name can differ from the name of an object in Salesforce web GUI.  You can use graph parameters in SOQL query. | e.g. SELECT Name, Website FROM Account WHERE Industry = 'Energy' |
| Output mapping |  | Mapping from query fields to output metadata fields | Map by name (default) |
| Read mode |  | Defines in what way records are read from Salesforce. You can enable reading deleted records, and then such records will be returned by the component. To distinguish deleted and not deleted records, query the `isDeleted` field. For an example, see [Reading deleted records details](salesforcereader.md#reading-deleted-records-details) and [Reading deleted records](salesforcereader.md#reading-deleted-records). | Do not return deleted or archived records (default) \| Return also deleted or archived records |

#### Details

**SalesforceReader** reads records from Salesforce using SOAP API, which performs the operations synchronously making it suitable for retrieving small datasets.

To use the component, create a Salesforce connection, enter an SOQL query and specify the output mapping. If you perform the steps in this order, the transform editor can provide you with metadata extracted from the SOQL query. Therefore, you will be able to map the fields with drag and drop.

##### SOQL

**SalesforceReader** uses Salesforce Object Query Language (SOQL) to query data in Salesforce.

##### List of Supported SOQL Functions

Due to different implementation of almost each function in API, we support the following functions.

| [Aggregate functions](salesforcereader.md#aggregate-functions) |
| --- |
| [Date functions](salesforcereader.md#date-functions) |
| [Misc functions](salesforcereader.md#misc-functions) |

###### Aggregate functions

The table shows returned data type for particular argument data type.

| Function | Parameter type |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| Boolen | Decimal | Integer | Date | String |  |
| `avg()` | - | Decimal[[1]](salesforcereader.md#salesforcereader-fn2) | Decimal[[1]](salesforcereader.md#salesforcereader-fn2) | - | - |
| `count()` | - | Integer | Integer | Integer | Integer |
| `count_distinct()` | no | Integer | Integer | Integer | Integer |
| `min()` | - | Decimal[[2]](salesforcereader.md#salesforce-fn1) | Integer | Date | String |
| `max()` | - | Decimal[[2]](salesforcereader.md#salesforce-fn1) | Integer | Date | String |
| `sum()` | - | Decimal[[3]](salesforcereader.md#salesforcereader-footnote3) | Integer | - | - |

| 1 | Decimal with 'maximal' precision and scale is used (decimal[64, 32]) |
| --- | --- |

| 2 | Precision and scale are derived from the first function parameter. |
| --- | --- |

| 3 | Scale is derived from the first function parameter and precision is fixed to 64. |
| --- | --- |

See also the Salesforce documentation on *[Aggregate functions](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_agg_functions.htm)*.

###### Date functions

| Function | Result type | Note |
| --- | --- | --- |
| `CALENDAR_MONTH()` | Integer |  |
| `CALENDAR_QUARTER()` | Integer |  |
| `CALENDAR_YEAR()` | Integer |  |
| `DAY_IN_MONTH()` | Integer |  |
| `DAY_IN_WEEK()` | Integer |  |
| `DAY_IN_YEAR()` | Integer |  |
| `DAY_ONLY()` | Date |  |
| `FICSAL_MONTH()` | Integer |  |
| `FISCAL_QUARTER()` | Integer |  |
| `FISCAL_YEAR()` | Integer |  |
| `HOUR_IN_DAY()` | Integer |  |
| `WEEK_IN_MONTH()` | Integer |  |
| `WEEK_IN_YEAR()` | Integer |  |
| `convertTimezone()` | Date | Must be used in a date function. For example `HOUR_IN_DAY(convertTimezone(CreatedDate))`  See also documentation on *[convertTimezone()](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_convert_time_zone.htm)* |

See also Salesforce documentation on *[Date Functions](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_date_functions.htm)*.

###### Misc functions

| Function | Result type | Note |
| --- | --- | --- |
| `convertCurrency()` | Decimal [[1]](salesforcereader.md#salesforcereader-footnote4) | *[convertCurrency()](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_sosl_querying_currency_fields.htm)* |
| `format()` | String | *[FORMAT()](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_sosl_format.htm)* |
| `distance()` | Decimal [[2]](salesforcereader.md#salesforcereader-footnote5) | *[Location-Based SOQL Queries](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_geolocate.htm)* |
| `toLabel()` | String metadata | *[Translating Results](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_tolabel.htm)* |
| `grouping()` | Integer | *[grouping()](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_groupby_grouping.htm)* |

| 1 | decimal[64, 6] |
| --- | --- |

| 2 | Decimal with 'maximal' precision and scale is used (decimal[64, 32])) |
| --- | --- |

##### Subqueries and join type

When the SOQL query contains a subquery, LEFT OUTER JOIN is performed to provide flat data structure. If no records have been returned by the subquery, `null` values are returned for subquery fields.

For example, if you select opportunities in a subquery and an account from a root query has no opportunity, a single record with `null` subquery fields is returned for this account. If the account has multiple opportunities, multiple records are produced.

###### Order of output records

The output records come out in arbitrary order unless you use **ORDER BY** in your query.

###### SOAP or Bulk API

If you read less than 10-15,000 records, it is generally better to use SOAP API because it will use less API requests.

##### Notes and limitations

###### Address and geolocation compound fields

Compound fields group together several fields to represent a complex data type, such as addresses or locations. **SalesforceReader** does not support reading compound fields as a whole, you need to read their separate parts. The dialog for defining SOQL shows the individual fields of compound fields, e.g. BillingStreet, BillingCity, etc.

For example, to read BillingAddress it is **not** possible to use the following SOQL:

`SELECT BillingAddress FROM Account`

Instead you need to read its individual component fields:

`SELECT BillingStreet, BillingCity, BillingPostalCode FROM Account`

See **[Compound Fields](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/compound_fields.htm)**.

###### Aggregate functions

In subqueries, you cannot read data from binary fields or use aggregate functions. This is a limitation of the SOAP API.

###### Reading deleted records details

When a Salesforce record is deleted it is first moved to Recycle Bin, from where it can be restored. Then automatically after a time interval, or after manually emptying the Recycle Bin, the record will be marked to be permanently deleted. Records marked to be permanently deleted cannot be restored, and are wiped from the database automatically by a background process.

If a record is deleted using the **Hard Delete** operation, it skips the Recycle Bin and is immediately ready to be permanently deleted.

Reading deleted records returns records which are not wiped yet, including those that are not in the Recycle Bin anymore but were not permanently deleted yet.

###### API Requests

**SalesforceReader** uses multiple API calls during its run. All of them count towards your Salesforce **API request limit**. The precise call flow is:

1. Login
2. Extract metadata of an expected result of a query. The number of requests depends on complexity of the query. In general, every unique Salesforce object used in the query will result in 1 API request.
3. Send the query and iterate over the result. An API request must be sent for every 2,000 returned records, so the number of requests depends on the number of records in the result. This is a limitation of the SOAP API.

#### Examples

| [Reading records from Salesforce](salesforcereader.md#reading-records-from-salesforce) |
| --- |
| [Query on multiple objects (tables)](salesforcereader.md#query-on-multiple-objects-tables) |
| [Query on multiple objects (tables) II](salesforcereader.md#query-on-multiple-objects-tables-ii) |
| [Using aggregate functions](salesforcereader.md#using-aggregate-functions) |
| [Reading deleted records](salesforcereader.md#reading-deleted-records) |

##### Reading records from Salesforce

This example shows the basic functionality of **SalesforceReader**.

Select **FirstName**, **LastName** and **Email** from **Contact**.

###### Solution

Create a Salesforce connection.

In **SalesforceReader**, set up the **Connection**, **SOQL query** and **Output mapping** parameters.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| SOQL query | SELECT FirstName, LastName, Email FROM Contact |
| Output mapping | ```ctl function integer transform() {  	$out.0.Email = $in.0.Email;  	$out.0.FirstName = $in.0.FirstName;  	$out.0.LastName = $in.0.LastName;   	return ALL; } ``` |

##### Query on multiple objects (tables)

This example shows the way to query records from two objects (tables) with a parent-child relationship. The solution of this example and the following ones shows only the SOQL query as the rest of the configuration has already been shown in the first example.

Select an account name and corresponding parent account name from Account.

###### Solution

`SELECT Name, Parent.Name FROM Account`

##### Query on multiple objects (tables) II

Select an account name and details of corresponding opportunities: name, type, amount, description.

###### Solution

`SELECT Account.Name, (SELECT Opportunity.Name, Opportunity.Type, Opportunity.Amount, Opportunity.Description FROM Opportunities) FROM Account`

##### Using aggregate functions

This example shows the way to use Salesforce aggregate functions.

Select account names and for each account count the sum from opportunities we won. The result should be sorted according to the sum in descending order.

###### Solution

`SELECT Account.Name, SUM(Amount) FROM Opportunity WHERE IsWon = true GROUP BY Account.Name ORDER BY SUM(Amount) DESC`

##### Reading deleted records

This example shows how to read deleted records. For more details on how records are deleted in Salesforce, see *[Reading deleted records details](salesforcereader.md#reading-deleted-records-details)*. Reading deleted records can be used for backup or for synchronization with a data warehouse where you need to mirror the delete operations.

###### Solution

Set the SalesforceReader attribute **Read mode** to **Return also deleted or archived records**.

Read the records and their **IsDeleted** field to distinguish deleted and not deleted records:

`SELECT Name, IsDeleted FROM Account`

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.4.0-M2 | **SalesforceReader** is available since **4.4.0-M2**. It uses Salesforce SOAP API version 37.0. |
| 4.5.0-M2 | **SalesforceReader** uses Salesforce SOAP API version 39.0. |
| 5.2.0 | **SalesforceReader** uses Salesforce SOAP API version 45.0. |
| 5.3.0 | **SalesforceReader** uses Salesforce SOAP API version 46.1. |
| 5.16.0 | **SalesforceReader** uses Salesforce SOAP API version 55.2. |

#### See also

| [SalesforceBulkReader](salesforcebulkreader.md) |
| --- |
| [SalesforceWriter](salesforcewriter.md) |
| [SalesforceBulkWriter](salesforcebulkwriter.md) |
| [SalesforceEinsteinWriter](salesforcewavewriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
| [Salesforce connections](salesforce-connections.md) |
| [Extracting metadata from Salesforce](creating-metadata.md#extracting-metadata-from-salesforce) |

##### External links

*[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_intro.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_quickstart_intro.htm)*

*[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/compound_fields.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/compound_fields.htm)*

*[https://developer.salesforce.com/blogs/developer-relations/2013/05/basic-soql-relationship-queries.html](https://developer.salesforce.com/blogs/developer-relations/2013/05/basic-soql-relationship-queries.html)*

*[https://resources.docs.salesforce.com/246/latest/en-us/sfdc/pdf/salesforce_soql_sosl.pdf](https://resources.docs.salesforce.com/246/latest/en-us/sfdc/pdf/salesforce_soql_sosl.pdf)*
