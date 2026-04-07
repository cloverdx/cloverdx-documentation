<!-- Development > Component reference > Writers > TransactionalDataSetCommit -->

### TransactionalDataSetCommit

![DataSetCommit 64x64](../figures/DataSetCommit-64x64.png)

| [Short description](datasetcommit.md#short-description) |
| --- |
| [Ports](datasetcommit.md#ports) |
| [Metadata](datasetcommit.md#metadata) |
| [Attributes](datasetcommit.md#transactionaldatasetcommit-attributes) |
| [Details](datasetcommit.md#details) |
| [See also](datasetcommit.md#see-also) |

#### Short description

**TransactionalDataSetCommit** commits records that were previously approved in the selected transactional data set in the Data Manager. This is a signal to the Data Manager that the records have been fully processed and can be removed once their **Retention period** expires.
> [!NOTE]
> This component must run in a server project within a CloverDX Server environment that has either a **locally configured Data Manager** or is set up to access a **Data Manager remotely**. For more information, refer [here](../admin/data-manager-administration.md#data-manager-configuration).

| Data output | Input ports | Output ports | Transformation | Transf. req. | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Any transactional data set in Data Manager | 1 | 2 | **⨯** | **⨯** | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For ids of the records that must be updated in the Data Manager. | Auto-propagated metadata containing just an id of the record to update. |
| Output | 0 | **⨯** | For records successfully committed to the data set. | Auto-propagated metadata containing just an id of the record that was updated. |
| Output | 1 | **⨯** | For records that failed to be updated in the data set. | Auto-propagated metadata containing an id of the record to that failed to be updated and error message with the failure reason. |

#### Metadata

All metadata on all ports is auto-propagated. Since the component does not implement any input or output mapping, this metadata must be used when interfacing with the component.

##### Input port 0: TransactionalDataSetCommit_Input

| Field name | Type | Description |
| --- | --- | --- |
| `_id` | `long` | Id of the record to update to *Committed* status. |

##### Output port 0: TransactionalDataSetCommit_Output

| Field name | Type | Description |
| --- | --- | --- |
| `_id` | `long` | Id of the record that was successfully updated. |

##### Output port 1: TransactionalDataSetCommit_Error

| Field name | Type | Description |
| --- | --- | --- |
| `_id` | `long` | Id of the record that failed to update. |
| `error` | `string` | Error message providing the details of why the record status update failed. |

#### TransactionalDataSetCommit attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Data Set | **✓** | Data set to update. Clicking on the **Edit set** button will show all transactional data sets that your user (when using a local Data Manager connection) or the user configured in the remote connection (when using a remote Data Manager connection) has permission to approve. See [Data set permissions](../user/data-manager-introduction.md#data-set-permissions).  Data set is identified by its code. The code is assigned to the data set when it is created and does not change when the data set is renamed. |  |

#### Details

**TransactionalDataSetCommit** notifies the Data Manager that a record has been fully processed. In most cases this means that the record that was read from the Data Manager has been loaded to the target system.

The commit is needed since it is possible for the target system to reject a record or to fail during processing. See [Unloading data from Data Manager](datasetreader.md#unloading-data-from-data-manager) for more details.

#### See also

| [TransactionalDataSetReader](datasetreader.md) |
| --- |
| [TransactionalDataSetWriter](datasetwriter.md) |
| [ReferenceDataSetReader](referencedatasetreader.md) |
| [ReferenceDataSetWriter](referencedatasetwriter.md) |
