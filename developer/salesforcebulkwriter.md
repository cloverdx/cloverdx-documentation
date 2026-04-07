<!-- Development > Component reference > Writers > SalesforceBulkWriter -->

### SalesforceBulkWriter

![SalesforceBulkWriter 64x64](../figures/SalesforceBulkWriter-64x64.png)

| [Short description](salesforcebulkwriter.md#short-description) |
| --- |
| [Ports](salesforcebulkwriter.md#ports) |
| [Metadata](salesforcebulkwriter.md#metadata) |
| [SalesforceBulkWriter attributes](salesforcebulkwriter.md#salesforcebulkwriter-attributes) |
| [Details](salesforcebulkwriter.md#details) |
| [Examples](salesforcebulkwriter.md#examples) |
| [Compatibility](salesforcebulkwriter.md#compatibility) |
| [See also](salesforcebulkwriter.md#see-also) |

#### Short description

**SalesforceBulkWriter** writes, updates, or deletes records in Salesforce using Bulk API.

| Data output | Input ports | Output ports | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 1 | 2 | **✓** | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For data records to be inserted, updated, or deleted | input0 |
| Output | 0 | **⨯** | For accepted data records | input0 plus ObjectId field |
| Output | 1 | **⨯** | For rejected data records | input0 plus Error message field |

If you do not map an error port and an error occurs, the component fails.

#### Metadata

**SalesforceBulkWriter** propagates metadata from left to right.

The metadata on the right side on the first output port have an additional field **ObjectId**. If the operation is Upsert, the output metadata on the first output port also have an additional field **Created**.

The metadata on the right side on the second output port have and additional field **Error**.

Metadata cannot use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### SalesforceBulkWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | yes | A Salesforce connection. See [Salesforce connections](salesforce-connections.md). | e.g. MySFConnection |
| Salesforce object | yes | An object affected by operation | e.g. Account |
| Operation |  | An operation performed on the Salesforce object | insert (default) \| update \| upsert \| delete \| hardDelete |
| Input mapping |  | Mapping of fields to be inserted/updated/deleted in Salesforce  Unmapped mandatory output fields have an exclamation mark icon. | Map by name (default) |
| Output mapping |  | Mapping of successfully inserted/updated/deleted fields | Map by name (default) |
| Error mapping |  | Mapping of records that were not inserted/updated/deleted | Map by name (default) |
| Advanced |  |  |  |
| Result polling interval (seconds) |  | Time between queries for results of the batch processing.  The default value is taken from the connection configuration. | 5 (default) |
| Upsert external ID field | (yes) | A field of object specified in **Salesforce object** which will be used to match records in the Upsert operation. Mandatory for the Upsert operation. Not used in any other operation. | e.g. Id |
| Job concurrency mode |  | If **SalesforceBulkWriter** uses the parallel mode, all batches in the job run at once. Using the parallel mode improves speed of processing and lowers needed API requests (less polling requests for a job status), but it can introduce lots of lock contention on Salesforce objects.  See documentation on parallel and serial modes: *[General Guidelines for Data Loads](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_planning_guidelines.htm)* | parallel (default) \| serial |
| Batch size |  | Size of the batch. The default value is 10,000 records. | e.g. 10000 |

#### Details

##### Supported Operations

**Insert** - inserts new records

**Update** - updates existing records

**Upsert** - inserts or updates records

**Delete** - moves records to recycle bin.

**HardDelete** - removes records permanently. The operation requires a special permission.

According to the operation you have chosen, different output metadata in **Input mapping** is displayed in the transform editor.
> [!NOTE]
> Bulk API does asynchronous calls. Therefore data records written to Salesforce may appear in the Salesforce web GUI after several seconds or even minutes.

###### SOAP or Bulk API

If you write more than 1,500-2,000 records, it is better to use Bulk API because it will use less API requests.

###### Mapping Dialogs

Mapping dialogs uses SOAP API to extract metadata fields on the Salesforce-side of the dialog.

###### Names of Objects and fields

When specifying Salesforce objects and fields, always use the **API Name** of the element.

##### Notes and limitations

**SalesforceBulkWriter** does not support writing attachments.

###### Details on API Calls

**SalesforceBulkWriter** automatically groups records to batches and uploads them to Salesforce. Batch size limit is 10,000 records or 10MB of data. The limit is introduced by the Salesforce Bulk API.

**SalesforceBulkWriter** uses multiple API calls during its run. All of them count towards your Salesforce **API request limit**. The precise call flow is:

1. Login
2. Extract fields of object specified in the **Salesforce object** attribute.
3. Create a bulk job.
4. Upload batches. The number of calls is the same as the number of batches.
5. Close the bulk job.
6. Get job completion status. This call is repeated in an interval specified by the **Result polling interval** attribute until the job is completed.
7. Download batch results. The number of calls is the same as the number of batches.

#### Examples

| [Insert records into Salesforce](salesforcebulkwriter.md#insert-records-into-salesforce) |
| --- |
| [Updating records](salesforcebulkwriter.md#updating-records) |
| [Upserting records](salesforcebulkwriter.md#upserting-records) |
| [Deleting records](salesforcebulkwriter.md#deleting-records) |
| [Hard-deleting records](salesforcebulkwriter.md#hard-deleting-records) |

##### Insert records into Salesforce

This example shows a basic use case with insertion of records.

Insert records with new products into Salesforce. Input data fields have the same field names as Salesforce data fields.

###### Solution

Connect input port of **SalesforceBulkWriter** with data source.

Create a Salesforce connection.

In **SalesforceBulkWriter**, fill in **Connection** and **Object**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the second step |
| Object | Product2 |

You do not have to specify the operation, as **insert** is the default one. You do not have to specify **Input mapping**, as metadata field names are the same as Salesforce field names and the default mapping (by name) is used.

You can attach an edge to the first output port to obtain object IDs of inserted records. You can attach an edge to the second output port to obtain records that have not been inserted.

##### Updating records

This example shows updating of Salesforce objects.

We do not sell products from our 'PaddleSteamer' family anymore. Set IsActive to false for all products of this family.

###### Solution

In this example, we have to read IDs of the objects to be updated first (with **SalesforceBulkReader**). Secondly, set IsActive to false. Finally, update the records in Salesforce (with **SalesforceBulkWriter**).

Create a Salesforce connection. In **SalesforceBulkReader**, set **Connection**, **SOQL query** and **Output mapping**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| SOQL query | SELECT Id FROM Product2 WHERE Family = 'PaddleSteamer' |
| Output mapping | See the code below |

```ctl
//#CTL2

function integer transform() {
 	$out.0.Id = $in.0.Id;
 	$out.0.IsActive = false;

 	return ALL;
}
```

In **SalesforceBulkWriter**, set **Connection**, **Salesforce object**, and **Operation**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Product2 |
| Operation | Update |

In **SalesforceBulkWriter**, no output mapping is specified as mapping by field names is used.

##### Upserting records

This example shows usage of Upsert operation.

There is a list of companies and their web sites. Update the websites in Salesforce.

###### Solution

Read records with the company name and object ID from Account object. Match the companies with their websites. Write only the new records or records that have been updated.

Create a Salesforce connection.

In **SalesforceBulkWriter**, use the **Connection**, **Salesforce Object****Operation**, **Output mapping** and **Upsert external ID field** attributes.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Account |
| Operation | Upsert |
| Input Mapping | See the code below |
| Upsert external ID field | Id |

```ctl
//#CTL2

function integer transform() {
 	$out.0.Id = $in.0.Id;

 	return ALL;
}
```

> [!NOTE]
> The records containing valid record ID are updated; the records with ID set to null are inserted.

##### Deleting records

This example shows deleting records.

The product called 'abc' has been inserted multiple times. Furthermore, we do not have 'abc' product anymore. Remove the 'abc' product.

###### Solution

Create a Salesforce connection.

Read object IDs of 'abc' product with **SalesforceBulkReader**.

In **SalesforceBulkWriter**, set **Connection**, **Salesforce object** and **Operation**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Product2 |
| Operation | Delete |

##### Hard-Deleting records

This example shows usage of Hard Delete.

Permanently delete records of specified IDs from Account object. The IDs are received from an input edge.

###### Solution

Create a Salesforce connection.

In **SalesforceBulkWriter**, set **Connection**, **Salesforce object**, **Operation** and **Input mapping**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Account |
| Operation | Hard Delete |
| Input mapping | See the code below. |

```ctl
//#CTL2

function integer transform() {
 	$out.0.Id = $in.0.Id;

 	return ALL;
}
```

> [!NOTE]
> The user has to have **Bulk API Hard Delete** privilege to use the **Hard Delete** operation.
>
> See [Activation of Bulk API hard delete on system administrator profile](https://help.salesforce.com/apex/HTViewSolution?id=000171306&language=en_US).

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.3.0-M2 | **SalesforceBulkWriter** is available since **4.3.0-M2**. It uses Salesforce Bulk API version 37.0. |
| 4.5.0-M2 | **SalesforceBulkWriter** uses Salesforce Bulk API version 39.0. |
| 4.5.0 | You can now set **job concurrency mode** and **batch size**. |
| 5.2.0 | **SalesforceBulkWriter** uses Salesforce Bulk API version 45.0. |
| 5.3.0 | **SalesforceBulkWriter** uses Salesforce Bulk API version 46.1. |
| 5.16.0 | **SalesforceBulkWriter** uses Salesforce Bulk API version 55.2. |

#### See also

| [SalesforceBulkReader](salesforcebulkreader.md) |
| --- |
| [SalesforceWriter](salesforcewriter.md) |
| [SalesforceEinsteinWriter](salesforcewavewriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Readers](common-of-readers.md) |
| [Readers comparison](common-of-readers.md#readers-comparison) |
| [Salesforce connections](salesforce-connections.md) |
| [Extracting metadata from Salesforce](creating-metadata.md#extracting-metadata-from-salesforce) |
