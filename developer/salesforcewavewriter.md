<!-- Development > Component reference > Writers > SalesforceEinsteinWriter -->

### SalesforceEinsteinWriter

![SalesforceEinsteinWriter 64x64](../figures/SalesforceEinsteinWriter-64x64.png)

| [Short description](salesforcewavewriter.md#short-description) |
| --- |
| [Ports](salesforcewavewriter.md#ports) |
| [Metadata](salesforcewavewriter.md#metadata) |
| [SalesforceEinsteinWriter attributes](salesforcewavewriter.md#salesforceeinsteinwriter-attributes) |
| [Details](salesforcewavewriter.md#details) |
| [Best practices](salesforcewavewriter.md#best-practices) |
| [Compatibility](salesforcewavewriter.md#compatibility) |
| [See also](salesforcewavewriter.md#see-also) |

#### Short description

**SalesforceEinsteinWriter** writes data to Salesforce CRM Analytics (formerly *Salesforce Einstein Analytics* or *Wave*) data sets.
> [!NOTE]
> Salesforce Einstein Analytics is now **Salesforce CRM Analytics**. The functionality described here remains the same in **Salesforce CRM Analytics**.

| Data output | Input ports | Output ports | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 1 | 2 | **⨯** | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For records to be inserted | Input 0 |
| Output | 0 | **⨯** | Successful load information | Output 0 |
| 1 | **⨯** | Unsuccessful load information | Output ~ |  |

#### Metadata

**SalesforceEinsteinWriter** does not propagate metadata.

**SalesforceEinsteinWriter** has metadata templates on its output ports.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 1 | Status | string | Status of successfully finished load |

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| 1 | Status | string | Status of an unsuccessfully finished load. |
| 2 | StatusMessage | string | A more descriptive message. |

#### SalesforceEinsteinWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | yes | Salesforce connection. |  |
| Dataset Name | yes | Name of the data set.  The Dataset Name should contain only alpha-numeric characters and underscore, and it should start with a letter. | E.g. flowers |
| Dataset Label |  | Label of data set to be displayed in Einstein platform. This property is only used when a dataset is initially created. | E.g. Nice flowers |
| Operation |  | Operation to be performed on data set | Overwrite (default) \| Append \| Delete \| Upsert |
| Unique ID field | (yes) | An input field that is considered as a unique identifier. It will be used to match records in the **Upsert** operation or select records to delete in the **Delete** operation. Mandatory for Delete and Upsert operations. Forbidden for Append operation. |  |
| Advanced |  |  |  |
| Metadata JSON |  | JSON specifying structure of the loaded dataset. |  |
| Metadata JSON File URL |  | An external file with the JSON metadata of the dataset. |  |
| Metadata JSON File URL Charset |  | Character set of Metadata JSON File. | E.g. UTF-8 |
| Result polling interval (seconds) |  | The time between two checks of result of data upload. |  |

#### Details

**SalesforceEinsteinWriter** loads records into Salesforce CRM Analytics (formerly known as *Einstein Analytics* or *Wave*). See *[Explore Data and Take Action with CRM Analytics](https://help.salesforce.com/articleView?id=bi.htm&language=en_US&type=0)*

##### Supported Operations

**Overwrite** - creates a new dataset or overwrites an existing one.

**Append** - appends records into an existing dataset.

**Delete** - deletes records from an existing dataset. The records to be deleted are selected using the **Unique ID field** property.

**Upsert** - inserts or updates records in an existing dataset. The records are matched using the **Unique ID field** property to decide whether to update or insert.

#### Examples

##### Writing records to Salesforce CRM

This example shows the basic use case of writing records to Salesforce CRM Analytics. A new data set in Salesforce CRM Analytics will be created.

Insert data records containing properties on different car types into CRM Analytics as "car properties" data set.

###### Solution

In **SalesforceEinsteinWriter** set **Connection**, **Dataset Name** and **Dataset Label**.

| Attribute | Value |
| --- | --- |
| Connection | A Salesforce Connection |
| Dataset Name | car_properties |
| Dataset Label | car properties |

Note that **Dataset name** contains an underscore character as it should not contain a space character.

#### Best practices

If you use **Metadata JSON File URL** attribute, explicitly specify **Metadata JSON File URL Charset**.

Insert all date fields in UTC timezone. If the timezone of the input fields is different, the values are automatically converted to UTC before upload. This is necessary to ensure correct upload.

You can specify format of date fields inserted to Salesforce CRM by changing **Format** property on the input metadata field. For a list of supported date formats, see *[External Data Metadata Format Reference](https://developer.salesforce.com/docs/atlas.en-us.bi_dev_guide_ext_data_format.meta/bi_dev_guide_ext_data_format/bi_ext_data_schema_reference.htm)*

#### Notes and limitations

**Metadata JSON** is generated automatically based on **CloverDX** metadata on input edge. You can override this behavior by specifying the JSON yourself. Documentation on all possible properties usable in the JSON metadata is available here: *[External Data Metadata Format Reference](https://developer.salesforce.com/docs/atlas.en-us.bi_dev_guide_ext_data_format.meta/bi_dev_guide_ext_data_format/bi_ext_data_schema_reference.htm)*

##### Usage of API calls

The component uses several Salesforce API calls during its run:

1. Login
2. Start the upload job.
3. Upload the data. A single API call is necessary for every 10MB of data.
4. Close the upload job.
5. Get job completion status. This call is repeated in interval specified by the **Result polling interval** attribute until the job is completed.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.5.0-M1 | **SalesforceWaveWriter** is available since **4.5.0-M1**. It uses Salesforce SOAP API version 37.0. |
| 4.5.0-M2 | **SalesforceWaveWriter** uses Salesforce SOAP API version 39.0. |
| 5.2.0 | **SalesforceWaveWriter** uses Salesforce SOAP API version 45.0. |
| 5.3.0 | **SalesforceWaveWriter** uses Salesforce SOAP API version 46.1. |
| 5.13.0 | **SalesforceWaveWriter** was renamed to **SalesforceEinsteinWriter**. |
| 5.16.0 | **SalesforceEinsteinWriter** uses Salesforce SOAP API version 55.2. |

#### See also

| [SalesforceReader](salesforcereader.md) |
| --- |
| [SalesforceBulkReader](salesforcebulkreader.md) |
| [SalesforceWriter](salesforcewriter.md) |
| [SalesforceBulkWriter](salesforcebulkwriter.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
| [Salesforce connections](salesforce-connections.md) |
