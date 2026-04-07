<!-- Development > Component reference > Job Control > WranglerJob -->

### WranglerJob

![WranglerJob 64x64](../figures/WranglerJob-64x64.png)

| [Short description](wranglerjob.md#short-description) |
| --- |
| [Ports](wranglerjob.md#ports) |
| [Metadata](wranglerjob.md#metadata) |
| [WranglerJob attributes](wranglerjob.md#wranglerjob-attributes) |
| [Details](wranglerjob.md#details) |
| [See also](wranglerjob.md#see-also) |

#### Short description

The **WranglerJob** component allows you to execute a **Wrangler job** as part of a transformation graph, similarly to the [Subgraph](subgraph.md) component. Unlike [ExecuteWranglerJob](executewranglerjob.md), which runs Wrangler job as a standalone job, WranglerJob integrates the job directly into the graph execution and enables streaming of data through its ports.

The component can run the job in its entirety (including sources and targets) or act as a specific stage (Mapping, Source + Mapping, or Mapping + Target) by connecting or disconnecting its input and output ports.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| – | **⨯** | 0-1 | 0–2 | **⨯** | – | – | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **×** | Input data for the Wrangler job. If connected, the internal Wrangler source is bypassed. | Auto-propagated metadata matches the Wrangler job source, but the port accepts any metadata compatible with the transformation steps. [[1]](wranglerjob.md#wranglerjob-footnote1) |
| Output | 0 | **×** | Successful output records from the Wrangler mapping. If connected, the internal target is bypassed. | Transformation metadata representing the result of the transformation steps applied to input metadata. |
| Output | 1 | **×** | Rejected records containing error details. | Wrangler rejected record layout. |

| 1 |  Input metadata must contain all fields required by the transformation logic (e.g., a field named `field1` must exist if used in a step). |
| --- | --- |

#### Metadata

- **Input Port 0**: Automatically propagates metadata corresponding to the Wrangler job’s source, however the port accepts any metadata compatible with the transformation logic of the Wrangler job. The component does not provide internal mapping; transformations must be handled before the data reaches this port.
- **Output Port 0**: Automatically propagates metadata corresponding to the Wrangler job’s transformation result.
- **Output Port 1**: Automatically propagates a specific "Error" metadata layout, which includes diagnostic columns describing the error (e.g., "errorMessage" or "step") plus the original output fields. For a detailed description of the diagnostic columns, see the [Wrangler reject file format documentation](../user/data-sources-data-targets.md#reject-file-format).

**Output Port 1 auto-propagated metadata:**

These fields capture detailed error information. Note that **errorMessage**, **errorColumn**, and **step** are parallel lists of the same length; for any given row, the n-th entry in each list describes the same error event.

| Field Name | Type | Description |
| --- | --- | --- |
| errorMessage | list[string] | Full error message describing the errors in the current row. |
| errorColumn | list[string] | Name of the column(s) in which an error occurred. |
| step | list[string] | Description of the step(s) where the error causing the rejection occurred. |
| sourceRowNumber | long | Sequential row number as read from the data source (starting with 1). |
| [Output fields] | string | All output data fields from the transformation result, converted to string. |

**Metadata Conversions**

The **WranglerJob** component acts as a bridge between the CloverDX engine and the Wrangler. Because these two environments use different type systems, data types are converted when entering the component and converted again upon exit.

The table below shows the lifecycle of a field as it flows from the input port metadata, through the Wrangler transformation, and out to the output port metadata.

| Input Metadata type → | Wrangler type → | Output Metadata type | Conversion Notes |
| --- | --- | --- | --- |
| long | *integer* | long | Metadata of type long directly corresponds to the Wrangler integer type. |
| integer | *integer* | long | Integer from input port is converted to long on output port. |
| decimal(x, y) | *decimal* | decimal(32, 10) | Input decimals with any precision and scale are converted to a fixed decimal(32, 10) on the output. |
| number | *decimal* | decimal(32, 10) | Metadata of type number are automatically converted to decimal, as Wrangler does not have a native number representation. |
| string | *string* | string |  |
| boolean | *boolean* | boolean |  |
| date | *date* | date |  |
| Everything else | *Not supported* | - | Types such as byte, cbyte or variant are not supported and will result in a configuration error if passed to Wrangler. |

#### WranglerJob attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Wrangler job URL | yes | URL of the job to run. The File URL dialog shows all Wrangler workspaces accessible to the user. |  |

**Dynamic attributes**

**WranglerJob** component dynamically loads attributes based on the selected job’s configuration. These attributes are displayed in the following sections:

**Data Source Parameters**

- Visible only if the Wrangler job source exposes public parameters.
- Parameters correspond to source configuration.
- If the input port is connected, source parameters are ignored.

The specific parameters available depend on the source type:

- [CSV data source](../user/data-sources-data-targets.md#csv-data-sources): Includes [parameters](../user/data-sources-data-targets.md#configuring-csv-data-source) for Input file URL, Encoding, Delimiter, Quoting, and First line is a header.
- [Excel data source](../user/data-sources-data-targets.md#excel-data-sources): Includes [parameters](../user/data-sources-data-targets.md#configuring-excel-data-source) for Input file URL, Sheet name, Coordinates of the first data cell, First line is a header, and Read numbers as raw decimals.
- [Transactional data set source](../user/data-sources-data-targets.md#transactional-data-set-sources): Includes parameters for Data Set, Record status, Include hidden and system columns, Include deleted, and Complete batches only.
- [Reference data set source](../user/data-sources-data-targets.md#reference-data-set-sources): Includes the Data Set.
- [Data source connector](../user/data-sources-data-targets.md#data-source-connectors): Includes public parameters defined within the subgraph of the selected source connector.

**Data Target Parameters**

- Visible only if the Wrangler job target exposes public parameters.
- Parameters correspond to target configuration.
- If output port 0 is connected, target parameters are ignored.

The specific parameters available depend on the target type:

- [CSV data target](../user/data-sources-data-targets.md#csv-data-targets): Includes [parameters](../user/data-sources-data-targets.md#csv-data-target-configuration) for Output file URL, Encoding, Field delimiter, Record delimiter, Quoting, Column headers, and Append.
- [Excel data target](../user/data-sources-data-targets.md#excel-data-targets): Includes [parameters](../user/data-sources-data-targets.md#excel-data-target-configuration) for Output file URL, Sheet name, and Append.
- Data Manager targets ([Transactional](../user/data-sources-data-targets.md#transactional-data-set-targets) and [Reference](../user/data-sources-data-targets.md#reference-data-set-targets) data sets): Includes the Data Set.
- [Data target connector](../user/data-sources-data-targets.md#data-target-connectors): Includes public parameters defined within the subgraph of the selected target connector.

#### Details

**Execution Modes**

WranglerJob supports four execution modes depending on how input and output ports are connected:

| Mode | Input Port | Output Port 0 | Behavior |
| --- | --- | --- | --- |
| **Mapping only** | Connected | Connected | Only the transformation part of the Wrangler job runs - source and target do not run at all. |
| **Input + Mapping** | Not connected | Connected | Source and transformation run. Target does not run at all. |
| **Mapping + Output** | Connected | Not connected | Transformation and job target run, job source does not run. |
| **Full job** | Not connected | Not connected | Entire job runs including source and target. |
> [!NOTE]
> If the Wrangler job includes additional sources in Lookup steps, these sources run regardless of the processing mode.

**Error Handling (Port 1)**

The error handling configuration for the job is automatically detected based on the connection status of the Output Port 1:

- **Connectivity Restriction**: The Output port 1 (error port) can only be used when Output port 0 (standard output port) is connected.
- **Port 1 is connected**: The component behaves as if the **"Write rows with errors to reject file"** option is selected in target options; records that fail the Wrangler transformation are sent to this port.
- **Port 1 is not connected**: The component follows a **"Fail the job on the first error"** policy; any record rejection will cause the component and the graph execution to fail.

**Internal Subgraph Generation and Cleanup**

When a Wrangler job is executed via the **WranglerJob** component, it is translated into a CloverDX subgraph.

- **Temporary Files**: Translation-related temporary files are generated in the `<wrangler_home>/graph/temp` directory.
- **Automatic Cleanup**: The server periodically deletes temporary files older than one day.
- **Configuration**: This cleanup behavior can be managed via the server configuration property `wrangler.tempSubgraph.maxAge`. See [List of configuration properties](../admin/list-of-properties.md) for more details.

#### Compatibility

| Version | Compatibility notice |
| --- | --- |
| 7.4.0 | WranglerJob is available since CloverDX version 7.4. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
