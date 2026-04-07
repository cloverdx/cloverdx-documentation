<!-- Development > Component reference > Readers > ReferenceDataSetReader -->

### ReferenceDataSetReader

![DataSetReader 64x64](../figures/DataSetReader-64x64.png)

| [Short description](referencedatasetreader.md#short-description) |
| --- |
| [Ports](referencedatasetreader.md#ports) |
| [Metadata](referencedatasetreader.md#metadata) |
| [Attributes](referencedatasetreader.md#referencedatasetreader-attributes) |
| [Details](referencedatasetreader.md#details) |
| [See also](referencedatasetreader.md#see-also) |

#### Short description

**ReferenceDataSetReader** reads published rows from the selected reference data set in the Data Manager.
> [!NOTE]
> This component must run in a server project within a CloverDX Server environment that has either a **locally configured Data Manager** or is set up to access a **Data Manager remotely**. For more information, refer [here](../admin/data-manager-administration.md#data-manager-configuration).

| Data source | Input ports | Output ports | Each to all outputs | Different to different outputs | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Any reference data set in Data Manager | 0 | 1 | **⨯** | **⨯** | **✓** | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Output | 0 | **✓** | For the data read from the selected data set. | Auto-propagated based on the layout of the selected data set.  Custom metadata and **Output mapping** can also be used. |

#### Metadata

The **ReferenceDataSetReader** component propagates metadata on the output port. Metadata is created based on the layout of the selected data set.

If different metadata is used, the mapping from data set’s metadata to the metadata on the output port can be done via the **Output mapping** component attribute.

#### ReferenceDataSetReader attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Data Set | **✓** | Data set to read from. Clicking on the **Edit set** button will show all reference data sets that are accessible to your user (when using a local Data Manager connection) or to the user configured in the remote connection (when using a remote Data Manager connection). See [Data set permissions in Data Manager](../user/data-manager-introduction.md#data-set-permissions).  Data set is identified by its code. The code is assigned to the data set when it is created and does not change when the data set is renamed. |  |
| Record status |  | Allows you to filter the records based on their status. Default value is *Enabled*. | All (any status) **Enabled** (default)  Disabled |
| Output mapping |  | Allows you to map data read from the data set to the output port. By default, this is set to *Map by name* and fields with matching names and types will be mapped automatically. This is consistent with the common usage where the metadata on output port 0 is auto-propagated and will match the data set exactly. |  |

#### Details

**ReferenceDataSetReader** connects to an instance of Data Manager running on the same Server as the component and returns data from the selected reference data set.

The component returns only published data - records approved by the *Data Approver* user in the Data Manager. If a record in the data set is new and not approved yet, component will not return that record. If a record in the data set was approved, but contains pending (not approved) changes, component will return only approved data.

#### See also

| [ReferenceDataSetWriter](referencedatasetwriter.md) |
| --- |
| [TransactionalDataSetReader](datasetreader.md) |
| [TransactionalDataSetWriter](datasetwriter.md) |
| [TransactionalDataSetCommit](datasetcommit.md) |
