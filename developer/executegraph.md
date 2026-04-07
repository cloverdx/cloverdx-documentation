<!-- Development > Component reference > Job Control > ExecuteGraph -->

### ExecuteGraph

Jobflow Component

![ExecuteGraph 64x64](../figures/ExecuteGraph-64x64.png)

| [Short description](executegraph.md#short-description) |
| --- |
| [Ports](executegraph.md#ports) |
| [Metadata](executegraph.md#metadata) |
| [ExecuteGraph attributes](executegraph.md#executegraph-attributes) |
| [Details](executegraph.md#details) |
| [Examples](executegraph.md#examples) |
| [Best practices](executegraph.md#best-practices) |
| [Compatibility](executegraph.md#compatibility) |
| [See also](executegraph.md#see-also) |

#### Short description

**ExecuteGraph** runs graphs with user-specified settings and provides execution results and tracking details to output ports.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 0-1 | 0-2 | **✓** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | Input tokens with graph execution settings. | Any |
| Output | 0 | **⨯** | Execution information for successful graphs. | Any |
| 1 | **⨯** | Execution information for unsuccessful graphs. | Any |  |

The component can have a single input port and two output ports attached.

#### Metadata

**ExecuteGraph** does not propagate metadata from left to right or from right to left. It propagates metadata of its templates.

This component has metadata templates on all its ports. The templates are described in [Details](executegraph.md#details). See details on [metadata templates](components.md#metadata-templates).

#### ExecuteGraph attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Graph URL | yes | A path to an executed graph. Only a single graph can be specified in this attribute. The value can be overridden by a value from input token, see the `Input mapping` attribute. The graph referenced by this attribute is also used for all mapping dialogs - they display dictionary entries and tracking information based on this graph. |  |
| Execution type | no | Specifies a type of execution - synchronous (sequential) or asynchronous (parallel) execution model. Can be overridden by a value from input token, see the `Input mapping` attribute. See [Execution type](executegraph.md#execution-type). | synchronous (default) \| asynchronous |
| Timeout (ms) | no | The maximal amount of time dedicated for a graph run; by default in milliseconds, but other [time units](components.md#time-intervals) may be used. If the timeout interval elapses, the graph is aborted. The value can be overridden by a value from an input token, see the `Input mapping` attribute.  The **Timeout** attribute is ignored for asynchronous execution type. Use the **MonitorGraph** component to watch the running graph. | 0 (unlimited) \| positive number |
| Input mapping | no | Input mapping defines how data from an incoming token overrides default execution settings. See [Input mapping](executegraph.md#input-mapping). | CTL transformation |
| Output mapping | no | Output mapping maps results of successful graphs to the first output port. See [Output mapping](executegraph.md#output-mapping). | CTL transformation |
| Error mapping | no | Error mapping maps results of unsuccessful graphs to the second output port. See [Error mapping](executegraph.md#error-mapping). | CTL transformation |
| Redirect error output | no | By default, results of failed graphs are sent to the second output port (error port). If this switch is set to `true`, results of unsuccessful graphs are sent to the first output port in the same way as successful graphs. | false (default) \| true |
| Advanced |  |  |  |
| Auto-propagate graph parameters | no | Passes parameter values to executed graph (subgraph) without explicit mapping.  If a parameter exists in both jobflow and executed graph and if the parameter is public in the executed graph, the parameter value is passed to the executed graph. | no (default) \| yes |
| Execution group | no | The name of an execution group to which the executed graph belongs. An execution group can be used by KillGraph component as a named handler for a set of graphs to be interrupted. | string |
| Execution label | no | A text displayed in an execution view before a graph name. | E.g. MyLabel |
| Cluster node ID | no | A Cluster node ID which will be used for execution of a graph. | string |
| Execute graph as daemon | no | By default, all graphs are executed in non-daemon mode, so none of them can live longer than the parent graph. **CloverDX Server** automatically ensures for finished jobs that all non-daemon graphs are interrupted if they have not finished yet. If you want to start a graph which can live longer than the parent graph, set this switch to `true`. | false (default) \| true |
| Skip checkConfig | no | By default, the pre-execution configuration check of the graph is performed only if the check was performed on the parent job. This attribute can explicitly enable or disable the check. | boolean (default is inherited from parent job) |
| Stop processing on fail | no | By default, any failed graph causes the component to stop executing other graphs; information about skipped tokens is sent to the error output port. This behavior can be turned off by this attribute. **Note:** this function works only if an edge is connected to the component’s error port. | true (default) \| false |
| Number of executors | no | By default, graphs executed in synchronous mode are triggered one after the other - the next graph is executed right after the previous one finishes. This option allows to increment the number of simultaneously running graphs. The `Number of executors` attribute defines how many graphs can be executed at once. All of them are monitored and once one of the running graphs finishes processing, another one is executed. This option is applied only to graphs executed in a synchronous mode. | positive number (1 is default) |
| Locale | no | The default [Locale](metadata-records-and-fields.md#locale) of the executed graph. | locale ID, see [List of all Locale](metadata-records-and-fields.md#locale-list-all) |
| Time zone | no | The default [Time zone](metadata-records-and-fields.md#timezone) of the executed graph. | time zone ID, e.g. `America/New_York` |

#### Details

| [Execution type](executegraph.md#execution-type) |
| --- |
| [Input mapping](executegraph.md#input-mapping) |
| [Output mapping](executegraph.md#output-mapping) |
| [Error mapping](executegraph.md#error-mapping) |

The **ExecuteGraph** component runs a graph with specific settings, waits for the graph to finish and monitors the graph results and tracking information.

The `.sgrf` files can be run by the **ExecuteGraph** component as well as **CloverDX** graphs.

##### Execution Flow in Details

The component reads an input token, executes a graph based on incoming data values, waits for the graph to finish and sends results to a corresponding port. Results of a successful graph are sent to the first output port. Results of a failed graph are sent to the second output port (error port).

If the graph run was successful, the component continues with processing of the next input tokens. Otherwise, the component stops executing other graphs, and from that moment on, all incoming tokens are ignored and information about ignored tokens is sent to the error output port. The behavior related to processing after the first graph failure can be changed via the **Stop processing on fail** attribute. If you set **Stop processing on fail** to `false`, the following graphs are executed.

##### Connected and disconnected ports

In case no input port is attached, only one graph is executed with default settings specified in the component’s attributes.

In case the first output port is not connected, the component just prints out the graph results to the log.

In case the second output port (error port) is not attached, the first failed graph causes interruption of the parent job. If you use **Redirect error output**, the disconnected error port does not cause interruption of the parent job.

##### Component configuration

For a graph execution, it is necessary to specify a graph location. Optionally, you can set up an execution type, initial values of graph parameters and dictionary content, timeout, execution group and several other attributes.

Most of the execution settings can be specified on the component via component attributes described bellow. These settings could be considered as a default execution settings.

The default execution settings can be changed dynamically and individually for each graph execution based on the data from the incoming token. The **Input mapping** attribute is the place where this override is defined.
> [!TIP]
> Right-click the component and click **Open Graph** to access the graph that is executed. Similarly, in the **ExecuteJobflow** component, there is the **Open Jobflow** option.

##### Execution type

The component supports synchronous (sequential) and asynchronous (parallel) graph execution.

- **synchronous execution mode** (default) - the component blocks until the graph has finished processing, so graphs are monitored by this component until the end of run.
- **asynchronous execution mode** - the component starts a graph and immediately sends the status information to the output. Graphs are only started by this component, the **MonitorGraph** component should be used for monitoring asynchronously executed graphs.
  If the jobflow that executes the graph finishes earlier than the executed graph, the graph is killed. To avoid killing the graph, set **Execute graph as daemon** to **true**.

##### Input mapping

The **Input mapping** attribute allows to override the settings of the component based on the data from the incoming token. Moreover, initial dictionary content and graph parameters of an executed graph can be changed in **Input mapping**.

**Input mapping** is a regular CTL transformation which is executed before each graph execution. An input token, if any, is only input for this mapping. The transformation’s outputs consist of three records: RunConfig, JobParameters and Dictionary.

- The **RunConfig** record represents execution settings. If a field of the record is not populated by this mapping, a default value from the respective attribute of the component is used instead.
  | Field Name | Type | Description |
  | --- | --- | --- |
  | jobURL | string | Overrides the component attribute **Graph URL**. |
  | executionType | string | Overrides the component attribute **Execution type**. |
  | timeout | long | Overrides the component attribute **Timeout**. |
  | executionGroup | string | Overrides the component attribute **Execution group**. |
  | executionLabel | string | Overrides the component attribute **Execution label**. |
  | clusterNodeId | string | Overrides the component attribute **Cluster node ID**. |
  | daemon | boolean | Overrides the component attribute **Execute graph as daemon**. |
  | skipCheckConfig | boolean | Overrides the component attribute **Skip checkConfig**. |
  | locale | string | Overrides the component attribute **Locale**. |
  | timeZone | string | Overrides the component attribute **Time zone**. |
  | jobParameters | map[string, string] | Graph parameters passed to the executed graph. Primary way of the definition of graph parameters is direct mapping to JobParameters record available in Input mapping dialog, where you can easily populate prepared graph parameters extracted from executed graph.  Graph parameters defined via this map have the highest priority. This map can be used in case the set of graph parameters is not available in design time of jobflow. |
- The **JobParameters** record represents all internal and external graph parameters of a triggered graph.
- The **Dictionary** record represents input dictionary entries of a triggered graph.
> [!NOTE]
> JobParameters and Dictionary records are available in the transform dialog only if the component attribute **Graph URL** links to an existing graph which is used as a template for extraction of graph parameters and a dictionary structure. Only graph parameters and input dictionary entries from this graph can be populated by input mapping, no matter which graph will be actually executed in a runtime.

##### Output mapping

**Output mapping** is a regular CTL transformation which is used to populate a token passed to the first output port. The mapping is executed for successful graphs. Up to four input data records are available for this mapping.

If the output mapping is empty, fields of **RunStatus** record are mapped to output by name.

- The input token configuring the graph execution. This record is not available for a component without an input connector. This record has **Port 0** displayed in the **Type** column.
  This is very helpful for passing through some fields from input token to output token.
- **RunStatus** record provides information about graph execution.
  | Field Name | Type | Description |
  | --- | --- | --- |
  | runId | long | A unique identifier of a graph run. In the case of an asynchronous execution type, the value can be used for graph monitoring or interruption. |
  | originalJobURL | string | The path to an executed graph. |
  | submitTime | long | Time when the graph execution was requested. The graph can be enqueued and started later, see `startTime` below. See [Job queue](../operations/job-queue.md) for more details about job queue. |
  | startTime | long | Time of graph startup. If the graph was enqueued, this is the time when the graph was taken from the queue and started. See [Job queue](../operations/job-queue.md) for more details about job queue. |
  | endTime | long | Time of graph finish, or null for asynchronous execution. |
  | duration | long | Graph execution time in milliseconds. |
  | executionGroup | string | The name of execution group to which the executed graph belongs. |
  | executionLabel | string | The execution label with which the graph was executed. |
  | status | string | The final graph execution status (FINISHED_OK \| ERROR \| ABORTED \| TIMEOUT \| RUNNING for asynchronous execution). |
  | errException | string | Cause exception for failed graphs only. |
  | errMessage | string | An error message for failed graphs only. |
  | errComponent | string | The ID of the component which caused graph fail. |
  | errComponentType | string | The type of the component which caused graph fail. |
- The dictionary record provides content of output dictionary entries of the graph. This record is available for the mapping only if the **Graph URL** attribute refers to a graph instance which has an output dictionary entry.
- The tracking record provides tracking information usually available only in the JMX interface of the running graph. This record is available for the mapping only if the **Graph URL** attribute refers to a graph instance.
  - Tracking fields available for a whole graph:
    | Field Name | Type | Description |
    | --- | --- | --- |
    | startTime | long | Time of graph execution. |
    | endTime | long | Time of the graph finish or null for the running graph. |
    | executionTime | long | Graph execution time in milliseconds. |
    | graphName | string | The name of an executed graph. |
    | result | string | The graph execution status (FINISHED_OK \| ERROR \| ABORTED \| TIMEOUT \| RUNNING). |
    | runningPhase | integer | An index of a running phase or null if the graph is already finished. |
  - Tracking fields available for a graph phase:
    | Field Name | Type | Description |
    | --- | --- | --- |
    | startTime | date | Time of phase execution. |
    | endTime | date | Time of the phase finish or null for running phase. |
    | executionTime | long | Phase execution time in milliseconds. |
    | memoryUtilization | long | Amount of used heap by the entire JVM at the time of phase execution (in bytes). |
    | result | string | Phase execution status (FINISHED_OK \| ERROR \| ABORTED \| RUNNING). |
  - Tracking fields available for a component:
    | Field Name | Type | Description |
    | --- | --- | --- |
    | name | string | The name of the component. |
    | usageCPU | number | Actual CPU time used by the component (user + system mode) expressed by a number from an interval (0, n) (0 means no CPU is used by the component, 1 means one CPU core is fully used by the component). |
    | usageUser | number | Actual CPU time used by the component in a user mode expressed by a number from an interval (0, n) (0 means no CPU is used by the component, 1 means one CPU core is fully used by the component). |
    | peakUsageCPU | number | Maximal CPU time used by the component (user + system mode) expressed by a number from an interval (0, n) (0 means no CPU is used by the component, 1 means one CPU core is fully used by the component). |
    | peakUsageUser | number | Maximal CPU time used by the component in user mode expressed by a number from an interval (0, n) (0 means no CPU is used by the component, 1 means one CPU core is fully used by the component). |
    | totalCPUTime | long | The number of milliseconds of CPU time used by this component (user + system mode). |
    | totalUserTime | long | The number of milliseconds of CPU time in the user mode used by this component. |
    | lifetimeMemoryAllocation | long | The cumulative number of bytes on heap allocated by this component during its lifetime. |
    | result | string | The component execution status (FINISHED_OK \| ERROR \| ABORTED \| RUNNING). |
  - Tracking fields available for an input or output port:
    | Field Name | Type | Description |
    | --- | --- | --- |
    | byteFlow | integer | The number of bytes passed through this port per seconds. |
    | bytePeak | integer | The maximal **byteFlow** registered on this port. |
    | totalBytes | long | The number of bytes passed through this port. |
    | recordFlow | integer | The number of records passed through this port per second. |
    | recordPeak | integer | The maximal **recordFlow** registered on this port. |
    | totalRecords | long | The total number of records passed through this port. |
    | waitingRecords | integer | The number of records cached on the edge connected to the port. |
    | averageWaitingRecords | integer | The average number of records cached on the edge connected to the port. |

##### Error mapping

**Error mapping** is a regular CTL transformation. The fields are the same as in **Output mapping**.

Error mapping is used only if the graph finished unsuccessfully and the second output port is populated instead of the first one.

If **Error mapping** is empty, fields of the **RunStatus** record are mapped to output by name.

#### Examples

##### Executing graph

This example shows the basic usage of **ExecuteGraph** component.

Execute the graph **invoice-processing.grf**.

###### Solution

| Attribute | Value |
| --- | --- |
| Graph URL | ${GRAPH_DIR}/invoice-processing.grf |

#### Best practices
> [!TIP]
> If you drag a `*.grf` file and drop it into the jobflow pane, you will add the **ExecuteGraph** component.

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 4.0.0-M2 | You can now set up the **Execution label** attribute. |
| 4.1.0 | You can now auto-propagate graph parameters.  Empty output mapping and error mapping work as mapping fields by name:  `$out.0.* = $in.0.*; $out.0.* = $in.1.*;` |

#### See also

| [RunGraph](rungraph.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job control comparison](common-of-job-control.md#job-control-comparison) |
