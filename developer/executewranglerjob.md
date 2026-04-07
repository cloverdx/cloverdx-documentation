<!-- Development > Component reference > Job Control > ExecuteWranglerJob -->

### ExecuteWranglerJob

Jobflow Component

![ExecuteWranglerJob 64x64](../figures/ExecuteWranglerJob-64x64.png)

| [Short description](executewranglerjob.md#short-description) |
| --- |
| [Ports](executewranglerjob.md#ports) |
| [ExecuteWranglerJob attributes](executewranglerjob.md#executewranglerjob-attributes) |
| [Details](executewranglerjob.md#details) |
| [Best practices](executewranglerjob.md#best-practices) |
| [See also](executewranglerjob.md#see-also) |

#### Short description

**ExecuteWranglerJob** allows running of Wrangler job with user-specified settings and provides execution results to output ports.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 0-1 | 0-2 | **✓** | **⨯** | **✓** | **✓** |

#### Ports

Please refer to [ExecuteGraph ports](executegraph.md#ports).

#### ExecuteWranglerJob attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Wrangler Job URL | yes | A path to an executed Wrangler job. Only a single job can be specified in this attribute. The value can be overridden by a value from input token, see the `Input mapping` attribute. |  |
| Execution type | no | Specifies a type of execution - synchronous (sequential) or asynchronous (parallel) execution model. Can be overridden by a value from input token, see the `Input mapping` attribute. See [Execution type](executegraph.md#execution-type). | synchronous (default) \| asynchronous |
| Timeout (ms) | no | The maximal amount of time dedicated for a job run; by default in milliseconds, but other [time units](components.md#time-intervals) may be used. If the timeout interval elapses, the job is aborted. The value can be overridden by a value from an input token, see the `Input mapping` attribute.  The **Timeout** attribute is ignored for asynchronous execution type. | 0 (unlimited) \| positive number |
| Input mapping | no | Input mapping defines how data from an incoming token overrides default execution settings. See [Input mapping](executegraph.md#input-mapping). | CTL transformation |
| Output mapping | no | Output mapping maps results of successful job to the first output port. See [Output mapping](executegraph.md#output-mapping). | CTL transformation |
| Error mapping | no | Error mapping maps results of unsuccessful job to the second output port. See [Error mapping](executegraph.md#error-mapping). | CTL transformation |
| Redirect error output | no | By default, results of failed jobs are sent to the second output port (error port). If this switch is set to `true`, results of unsuccessful jobs are sent to the first output port in the same way as successful jobs. | false (default) \| true |
| Advanced |  |  |  |
| Execution group | no | The name of an execution group to which the executed job belongs. An execution group can be used by KillGraph component as a named handler for a set of jobs to be interrupted. | string |
| Execution label | no | A text displayed in an execution view before a job name. | E.g. MyLabel |
| Cluster node ID | no | A Cluster node ID which will be used for execution of a job. | string |
| Execute Wrangler job as daemon | no | By default, all jobs are executed in non-daemon mode, so none of them can live longer than the parent graph. **CloverDX Server** automatically ensures for finished jobs that all non-daemon jobs are interrupted if they have not finished yet. If you want to start a job which can live longer than the parent graph, set this switch to `true`. | false (default) \| true |
| Stop processing on fail | no | By default, any failed job causes the component to stop executing other jobs; information about skipped tokens is sent to the error output port. This behavior can be turned off by this attribute. **Note:** this function works only if an edge is connected to the component’s error port. | true (default) \| false |
| Number of executors | no | By default, jobs executed in synchronous mode are triggered one after the other - the next job is executed right after the previous one finishes. This option allows to increment the number of simultaneously running jobs. The `Number of executors` attribute defines how many jobs can be executed at once. All of them are monitored and once one of the running jobs finishes processing, another one is executed. This option is applied only to jobs executed in a synchronous mode. | positive number (1 is default) |

#### Best practices
> [!TIP]
> If you drag a `.wjob` file and drop it into the jobflow pane, you will add the **ExecuteWranglerJob** component.

#### Details

**ExecuteWranglerJob** offers an alternative way of executing Wrangler jobs. Wrangler jobs are usually executed directly from Wrangler where they have been created. If there is a need to orchestrate execution of Wrangler jobs as part of a larger hierarchy or manually schedule them the **ExecuteWranglerJob** component is the universal tool for that.

This component works similarly to **ExecuteGraph.** See [ExecuteGraph](executegraph.md) component documentation.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job Control comparison](common-of-job-control.md#job-control-comparison) |
