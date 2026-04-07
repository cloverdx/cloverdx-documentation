<!-- Development > Component reference > Writers > ReferenceDataSetWriter -->

### ReferenceDataSetWriter

![DataSetWriter 64x64](../figures/DataSetWriter-64x64.png)

| [Short description](referencedatasetwriter.md#short-description) |
| --- |
| [Ports](referencedatasetwriter.md#ports) |
| [Metadata](referencedatasetwriter.md#metadata) |
| [Attributes](referencedatasetwriter.md#referencedatasetwriter-attributes) |
| [Details](referencedatasetwriter.md#details) |
| [See also](referencedatasetwriter.md#see-also) |

#### Short description

**ReferenceDataSetWriter** writes new changes to the selected reference data set in the Data Manager. The changes must be approved in the Data Manager before they can be read.
> [!NOTE]
> This component must run in a server project within a CloverDX Server environment that has either a **locally configured Data Manager** or is set up to access a **Data Manager remotely**. For more information, refer [here](../admin/data-manager-administration.md#data-manager-configuration).

| Data output | Input ports | Output ports | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Any reference data set in Data Manager | 1 | 2 | **✓** | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For the data to write to the data set. | Auto-propagated based on the layout of the selected data set with two extra fields called `_id` and `_enabled`. For more information on these two fields and their related logic, see [Details](referencedatasetwriter.md#details). Fields `_valid_from` and `_valid_to` are present when **Effective dates** are enabled on the Reference Data Set.  Custom metadata and **Input mapping** can also be used. |
| Output | 0 | **⨯** | For records successfully written to the data set. | Auto-propagated based on the layout of the selected data set – contains all data set fields.  Custom metadata can be used as well with mapping between data set and the output implemented in **Output mapping**. |
| Output | 1 | **⨯** | For records which failed to be written. | Auto-propagated metadata with layout derived from DataSet, with two added fields `errorMessage` and `exception`, which contain information about the error that occurred during writing. |

#### Metadata

The **ReferenceDataSetWriter** component propagates metadata on the input port. The input metadata is created based on the layout of the selected data set. If different metadata is used, you can configure the **Input mapping** to map the incoming records to records required by the data set.

#### ReferenceDataSetWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Data Set | **✓** | Data set to write to. Clicking on the **Edit set** button will show all reference data sets that your user (when using a local Data Manager connection) or the user configured in the remote connection (when using a remote Data Manager connection) has permission to edit. See [Data set permissions in Data Manager](../user/data-manager-introduction.md#data-set-permissions).  Data set is identified by its code. The code is assigned to the data set when it is created and does not change when the data set is renamed. |  |
| Input mapping |  | Allows you to map incoming records to records in the data set. Default mapping (when nothing is configured) is to map by name. |  |
| Output mapping |  | Allows you to map data written to the data set to the output port. By default, this is set to *Map by name* and fields with matching names and types will be mapped automatically. This is consistent with the common usage where the metadata on output port 0 is auto-propagated and will match the data set exactly. |  |
| Error mapping |  | Allows you to map information about errors that occurred when writing to the data set. By default, this is set to *Map by name* and fields with matching names and types will be mapped automatically. |  |

#### Details

**ReferenceDataSetWriter** connects to an instance of Data Manager running on the same Server as the component and inserts new records into the selected reference data set, or updates existing records.

If you do not provide the `_id` in the **Input mapping** (i.e, the `_id` is `null`) a new record will be created. This record will get new, auto-generated `_id` value that will be returned via the **Output mapping**.

If you provide an `_id` value, then:

- If the `_id` matches an existing record in the lookup, a new change record is written for the record with this `_id`. If a change record already exists, it is completely overwritten (there can be only one change record for each `_id` value).
- If the `_id` does not match an existing record, a record with the error information is written to the error port or the graph fails if the port is not connected.

The `_enabled` field in the **Input mapping** is optional. If not specified, it defaults to `true`.

Changes made by **ReferenceDataSetWriter** are not published automatically, but require an approval by the *Data Approver* user in the Data Manager. Only approved changes can be read by **ReferenceDataSetReader** component.

#### See also

| [ReferenceDataSetReader](referencedatasetreader.md) |
| --- |
| [TransactionalDataSetReader](datasetreader.md) |
| [TransactionalDataSetWriter](datasetwriter.md) |
| [TransactionalDataSetCommit](datasetcommit.md) |
