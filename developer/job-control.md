<!-- Development > Component reference > Job Control -->

## 41. Job Control

| [Common properties of Job Control](common-of-job-control.md) |
| --- |

Some components are focused on execution and monitoring of various job types. We call this group of components: **Job control**.

Job control components are usually tightly bound with [*jobflow*](part-jobflow.md#jobflow-overview). However, a few of them can be used even in regular Graphs.

These components allow running Graphs, jobflows and any interpreted scripts. Graphs and jobflows can be monitored and optionally aborted.

We can distinguish each component of the **Job control** group according to the task it performs.

- [Barrier](barrier.md) waits for results of jobs running in parallel and sends an aggregated result to the output port.
- [Condition](condition.md) routes incoming tokens to one of its output ports based on the result of a specified condition.
- [ExecuteGraph](executegraph.md) runs graphs with user-specified settings.
- [ExecuteJobflow](executejobflow.md) runs jobflows with user-specified settings.
- [ExecuteWranglerJob](executewranglerjob.md) runs Wrangler job with user-specified settings.
- [ExecuteScript](executescript.md) runs either shell scripts or scripts interpreted by a selected interpreter.
- [Fail](fail.md) aborts a parent job.
- [GetJobInput](getjobinput.md) produces a single record populated by dictionary content.
- [KillGraph](killgraph.md) aborts specified graphs.
- [KillJobflow](killjobflow.md) aborts specified jobflows.
- [Loop](loop.md) allows repeated execution of a group of components.
- [MonitorGraph](monitorgraph.md) watches running graphs.
- [MonitorJobflow](monitorjobflow.md) watches running jobflows.
- [SetJobOutput](setjoboutput.md) sets incoming values to dictionary content.
- [Sleep](sleep.md) waits specified time on each incoming token.
- [Success](success.md) consumes all incoming tokens or records which are considered successful.
- [TokenGather](tokengather.md) copies incoming tokens from any input port to all output ports.

### See also

| [Components](components.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
