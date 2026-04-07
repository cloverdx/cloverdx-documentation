<!-- Development > Component reference > Job Control > Common properties of Job Control components -->

### Common properties of Job Control components

**Job Control** is a group of components managing various job types - executing, monitoring and optionally aborting Graphs, jobflows and interpreted scripts. Most of these components are tightly bound with [*jobflow*](part-jobflow.md#jobflow-overview).

All execution components **ExecuteGraph**, **ExecuteJobflow**, **ExecuteScript** and few other Job Control components have a similar approach to job execution management. Each of them has an optional input port.

Each incoming token from this port is interpreted by an execution component and a respective job is started. Default execution settings are specified directly through various component attributes. These default settings can be overridden by values from incoming token - the **Input mapping** attribute specifies the override.

Results of successful jobs are sent to the first output port and unsuccessful job runs are sent to the second output port. Content of these output tokens is defined in **Output mapping** and **Error mapping**.

In case no input port is attached, only a single job is started with execution settings specified directly in component attributes. In case the first output port is not connected, job results are printed out to a log file. And finally in case the second output port is not connected, the first unsuccessful job causes a failure of a whole jobflow.

The **Redirect error output** attribute can be used to route all successful and even unsuccessful job results to the first output port - **Output mapping** is used for all job executions.

Below is an overview of all **Job control** components:

| Component | Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Barrier](barrier.md) | **⨯** | **⨯** | 1-n | 1-n | - | - | **⨯** |
| [Condition](condition.md) | - | **⨯** | 1 | 1-2 | - | - | **✓** |
| [ExecuteGraph](executegraph.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [ExecuteJobflow](executejobflow.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [ExecuteWranglerJob](executewranglerjob.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [ExecuteMapReduce](executemapreduce.md) | **⨯** | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [ExecuteScript](executescript.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [Fail](fail.md) | - | **⨯** | 0-1 | 0 | **⨯** | **✓** | **⨯** |
| [GetJobInput](getjobinput.md) | - | **⨯** | 0 | 1 | **⨯** | **✓** | **⨯** |
| [KillGraph](killgraph.md) | - | **⨯** | 0-1 | 0-1 | **⨯** | **✓** | **✓** |
| [KillJobflow](killjobflow.md) | - | **⨯** | 0-1 | 0-1 | **⨯** | **✓** | **✓** |
| [Loop](loop.md) | **✓** | **⨯** | 2 | 2 | **⨯** | **✓** | **✓** |
| [MonitorGraph](monitorgraph.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [MonitorJobflow](monitorjobflow.md) | - | **⨯** | 0-1 | 0-2 | **⨯** | **✓** | **✓** |
| [SetJobOutput](setjoboutput.md) | - | **⨯** | 1 | 0 | **⨯** | **✓** | **⨯** |
| [Sleep](sleep.md) | - | **⨯** | 1 | 1-n | **⨯** | **✓** | **✓** |
| [Success](success.md) | **⨯** | **⨯** | 0-n | 0 | - | - | **⨯** |
| [TokenGather](tokengather.md) | **⨯** | **⨯** | 1-n | 1-n | - | - | **✓** |
