<!-- Development > Component reference > Writers > SalesforceWriter -->

### SalesforceWriter

![SalesforceWriter 64x64](../figures/SalesforceWriter-64x64.png)

| [Short description](salesforcewriter.md#short-description) |
| --- |
| [Ports](salesforcewriter.md#ports) |
| [Metadata](salesforcewriter.md#metadata) |
| [SalesforceWriter attributes](salesforcewriter.md#salesforcewriter-attributes) |
| [Details](salesforcewriter.md#details) |
| [Examples](salesforcewriter.md#examples) |
| [Compatibility](salesforcewriter.md#compatibility) |
| [See also](salesforcewriter.md#see-also) |

#### Short description

**SalesforceWriter** writes, updates or deletes records in Salesforce using SOAP API.

| Data output | Input ports | Output ports | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 1 | 2 | **✓** | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For data records to be inserted, updated or deleted | input0 |
| Output | 0 | **⨯** | For accepted data records | input0 plus ObjectId field |
| Output | 1 | **⨯** | For rejected data records | input0 plus Error message field |

If you do not map an error port and an error occurs, the component fails.

#### Metadata

**SalesforceWriter** propagates metadata from left to right.

The metadata on the right side on the first output port have an additional field **ObjectId**. If the operation is **Upsert**, the output metadata on the first output port also have an additional field **Created**.

The metadata on the right side on the second output port have an additional field **Error**.

Metadata cannot use [Autofilling functions](metadata-records-and-fields.md#autofilling-functions).

#### SalesforceWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | yes | A Salesforce connection. See [Salesforce connections](salesforce-connections.md). | e.g. MySFConnection |
| Salesforce object | yes | An object affected by an operation | e.g. Account |
| Operation |  | An operation performed on the Salesforce object | Insert (default) \| Update \| Upsert \| Delete |
| Input mapping |  | Mapping of fields to be inserted/updated/deleted in Salesforce | Map by name (default) |
| Output mapping |  | Mapping of successfully inserted/updated/deleted fields | Map by name (default) |
| Error mapping |  | Mapping of records that were not inserted/updated/deleted | Map by name (default) |
| Advanced |  |  |  |
| Upsert external ID field | (yes) | A field of object specified in **Salesforce object** which will be used to match records in the Upsert operation. Mandatory for the Upsert operation. Not used in any other operation. | e.g. Id |
| Batch size |  | Size of the batch. The default and maximum batch size is 200 records.  In some cases, it is beneficial to reduce the batch size to a lower number, because for example, the APEX triggers exceed the 10s limit for the call and the whole write fails. | e.g. 150 |

#### Details

##### Supported Operations

**Insert** - inserts new records

**Update** - updates existing records

**Upsert** - inserts or updates records

**Delete** - moves records to Recycle Bin.

According to the operation you have chosen, different output metadata in **Input mapping** are displayed in the transform editor.

##### SOAP or Bulk API

If you write less than 1,500-2,000 records, it is better to use SOAP API because it will use less API requests.

##### Writing attachments

**SalesforceWriter** supports writing attachments. You can either receive the attachment from byte fields or read the attachment from files.

Both options are mutually exclusive. If both options are specified, reading the attachment from byte fields has a higher priority over reading the attachment from files.

###### Attachments from byte fields

The attachment can be read from the input metadata field of byte or cbyte data type. The field containing the attachment is to be mapped to byte field, e.g. **Body** field in Attachment object.

###### Attachments from files

To read attachments from files, map the field with file URL to a string field with the **_FileURL** suffix, which is below the corresponding byte field, e.g. **Body_FileURL** field in Attachment object.

You can map only one file per record. Wild cards in file names are not supported.

##### Notes and limitations

When specifying Salesforce objects and fields, always use the **API Name** of the element.

SOAP API does not support **HardDelete** operation. If you need **HardDelete** operation, use [SalesforceBulkWriter](salesforcebulkwriter.md).

###### Limits introduced by Salesforce API

Single API soap call cannot contain more than 200 objects.

Single soap message cannot exceed 50MB (encoded as UTF-8).

The component attempts to bundle as many objects (records) as possible together into a single call to reduce the number of used API requests. In most cases, all 200 records will fit into the 50MB limit, so the component will need 1 API request for 200 records.

When writing very long text fields or attachments, it is possible that a smaller number of records will use all 50MB. In such a case, the component sends as many records as possible in every call but ensures that the soap message will not exceed 50MB limit. The rest of the records will be sent in another call. You don’t need to worry about sizing the messages yourself. If you want, you can monitor the bundling of records, as well. The number of records and expected size of the message is included in graph log on DEBUG level.

###### Usage of API calls

The component uses several API calls during its run:

1. Login
2. Describe schema of target object - to extract metadata
3. 1 call per every 200 records or 50MB of data, whichever comes first

#### Examples

| [Inserting records](salesforcewriter.md#inserting-records) |
| --- |
| [Updating records](salesforcewriter.md#updating-records) |
| [Upserting records](salesforcewriter.md#upserting-records) |
| [Deleting records](salesforcewriter.md#deleting-records) |
| [Inserting attachments received from byte fields](salesforcewriter.md#inserting-attachments-received-from-byte-fields) |
| [Inserting attachments from files](salesforcewriter.md#inserting-attachments-from-files) |

##### Inserting records

This example shows a basic use case with insertion of records.

Insert records with new contacts into Salesforce. Input data fields have the same field names as Salesforce data fields.

###### Solution

Connect input port of **SalesforceWriter** with data source.

Create a Salesforce connection.

In **SalesforceWriter**, fill in **Connection** and **Salesforce object**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the second step |
| Salesforce object | Contact |

You do not have to specify the operation, as **insert** is the default one. You do not have to specify **Input mapping**, as metadata field names are the same as Salesforce field names and the default mapping (by name) is used.

You can attach an edge to the first output port to obtain object IDs of inserted records. You can attach an edge to the second output port to obtain records that have not been inserted.

##### Updating records

This example shows updating of Salesforce objects.

*Punch Cards Ltd.* has changed its name to *United Floppies Ltd.* Update the name in **Account** table/object.

###### Solution

Create a Salesforce connection, read ID of the company with **SalesforceBulkReader**, change the company name, update the record in Salesforce with **SalesforceWriter**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Account |
| Operation | Update |
| Input mapping | See the code below |

```ctl
//#CTL2

function integer transform() {
 	$out.0.Id = $in.0.Id;
 	$out.0.Name = "United Floppies Ltd.";

 	return ALL;
}
```

##### Upserting records

This example shows upserting records.

There is a list of contacts (name and last name) and new phone numbers. Update the phone numbers of the contacts. If there is no such contact, create a new one.

###### Solution

Read records from Contact table with **SalesforceBulkReader**. Join them with the records from the list. The result of join operation should contain only the records from the list. Write the records from the list only.

In **SalesforceWriter**, set **Connection**, **Salesforce object**, **Operation** and **Input mapping**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Contact |
| Operation | Upsert |
| Input mapping | See the code below |
| Upsert external ID field | Id |

```ctl
//#CTL2

function integer transform() {
 	$out.0.Id = $in.0.Id;
 	$out.0.FirstName = $in.0.FirstName;
 	$out.0.LastName  = $in.0.LastName;
 	$out.0.Phone     = $in.0.Phone;

 	return ALL;
}
```

##### Deleting records

This example shows deleting records.

A contact *Ab C* has been inserted by mistake. Delete the contact.

###### Solution

Create a Salesforce connection, read the contact ID with **SalesforceBulkReader**, and use the ID to delete it with **SalesforceWriter**.

In **SalesforceWriter** set **Connection**, **Salesforce object** and **Operation**.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Contact |
| Operation | Delete |

##### Inserting attachments received from byte fields

This example shows writing attachments into Salesforce. The content of the file is received from a byte field of input port metadata.

Insert an attachment to Account 'Floppies United'.

###### Solution

Create a Salesforce connection.

Read ID of the 'Floppies United' account with **SalesforceBulkReader**.

Read the attachment with **FlatFileReader** into a byte field. The metadata on the output port on **FlatFileReader** uses **EOF as delimiter**; set **record delimiter** and **default field delimiter** as empty.

Merge the data streams with **Combine**.

Write the attachment with **SalesforceWriter**.

In **SalesforceWriter**, use the **Connection**, **Salesforce object** and **Input mapping** attributes.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Attachment |
| Input mapping | See the code below. |

```ctl
//#CTL2

function integer transform() {
 	$out.0.ParentId = $in.0.Id;
 	$out.0.Body     = $in.0.FileContent;
 	$out.0.Name     = $in.0.FileName;

 	return ALL;
}
```

> [!NOTE]
> In **SalesforceWriter** you can read files to be uploaded directly. In the input mapping, map the URL of the file to the **Body_FileURL** field.

##### Inserting attachments from files

This example shows writing attachments to Salesforce. The content of the attachment is not received from byte fields, but read from files.

Input data to **SalesforceWriter** contains ContactID, Filename and the path to the file. Write the files to the Salesforce as attachments.

###### Solution

Create a Salesforce connection. In **SalesforceWriter**, set the **Connection**, **Salesforce object** and **Input mapping** attributes.

| Attribute | Value |
| --- | --- |
| Connection | Connection from the first step |
| Salesforce object | Attachment |
| Input mapping | See the code below. |

```ctl
//#CTL2

function integer transform() {
	$out.0.ParentId = $in.0.id;
	$out.0.Name = $in.0.name;
	$out.0.Body_FileURL = $in.0.filename;

	return ALL;
}
```

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.4.0-M1 | **SalesforceWriter** is available since **4.4.0-M1**. It uses Salesforce SOAP API version 37.0. |
| 4.5.0-M2 | **SalesforceWriter** uses Salesforce SOAP API version 39.0. |
| 4.5.0 | You can now set **batch size**. |
| 5.2.0 | **SalesforceWriter** uses Salesforce SOAP API version 45.0. |
| 5.3.0 | **SalesforceWriter** uses Salesforce SOAP API version 46.1. |
| 5.16.0 | **SalesforceWriter** uses Salesforce SOAP API version 55.2. |

#### See also

| [SalesforceReader](salesforcereader.md) |
| --- |
| [SalesforceBulkReader](salesforcebulkreader.md) |
| [SalesforceBulkWriter](salesforcebulkwriter.md) |
| [SalesforceEinsteinWriter](salesforcewavewriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
| [Salesforce connections](salesforce-connections.md) |
