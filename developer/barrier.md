<!-- Development > Component reference > Job Control > Barrier -->

### Barrier

Jobflow Component

![Barrier 64x64](../figures/Barrier-64x64.png)

| [Short description](barrier.md#short-description) |
| --- |
| [Ports](barrier.md#ports) |
| [Metadata](barrier.md#metadata) |
| [Barrier attributes](barrier.md#barrier-attributes) |
| [Details](barrier.md#details) |
| [Examples](barrier.md#examples) |
| [See also](barrier.md#see-also) |

#### Short description

**Barrier** allows to wait for results of parallel running jobs and react to the success or failure of groups of jobs in a simple way.

Barrier waits for all input tokens belonging to a group, evaluates this group and based on the results sends output token(s) to the first or second output port.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **⨯** | **⨯** | 1-n | 1-2 | **⨯** | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | Input tokens with job results. | Any |
| 1-n | **⨯** | Input tokens with job results. | Any |  |
| Output | 0 | **⨯** | Tokens for successful groups of jobs. | Any |
| 1 | **⨯** | Tokens for unsuccessful groups of jobs. | Any |  |

#### Metadata

##### Input ports

Any metadata is possible on input ports, only the **status** field is expected by the **Token evaluation expression** attribute, by default (`$status == "FINISHED_OK"`).

##### Output ports

Any metadata is possible on output ports, but tokens sent to output ports are copied based on field names from input ports, so only fields with equal names are populated.

#### Barrier attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Input grouping | no | The type of algorithm defining how the incoming tokens are split into groups of jobs, which are evaluated independently. See [Logical grouping of incoming records](barrier.md#logical-grouping-of-incoming-records) | Tuple (default) \| All |
| Token evaluation expression | no | A boolean CTL expression which is applied to each incoming token to decide whether the token represents successful or unsuccessful job run - final job status. See [Group evaluation](barrier.md#group-evaluation) | default CTL expression '$status == "FINISHED_OK"' |
| Group evaluation criteria | no | A logical operation which is applied to the job status (see the **Token evaluation expression** attribute) to decide whether the group of jobs is successful or unsuccessful. See [Group evaluation](barrier.md#group-evaluation) | AND (default) \| OR |
| Output | no | Defines the number of output tokens per group of jobs. See [Generating output tokens](barrier.md#generating-output-tokens) | Single token (default) \| All tokens |

#### Details

**Barrier** is mainly used for management of parallel running jobs. Barrier receives all incoming tokens, which carry information about job results, and splits them to logical groups of jobs. Each job group is evaluated independently. Results of groups evaluated as successful are sent to the first output port. Results of the unsuccessful groups are sent to the second output port.

##### Logical grouping of incoming records

The component’s attribute **Input grouping** provides two options on how the incoming tokens are split to logical groups of jobs.

- **All** - all incoming tokens are considered as a single group, exactly one group is processed by the component. This covers the most common scenarios, e.g. checking that all previous jobs were successful.
- **Tuple** - a group consists of a single token from all input ports, i.e. the groups are created by "waves" of tokens coming from input ports. Tokens which arrive first from each input port form the first logical group, the second tokens from each input port form the second logical group, etc. (i.e. n-th group consists of n-th input token from all input ports) This setting covers checking result of waves of parallel job.

##### Group evaluation

Each token in a group is evaluated by CTL boolean expression from the **Token evaluation expression** attribute - let’s call it job status. The group is considered successful if and only if the job statuses joined by logical operation AND or OR (the **Group evaluation criteria** attribute) are true. So in the case of AND operation, all incoming tokens need to be successful for a success of whole group. On the other hand in the case of OR operation, at least one token from the group needs to be successful for a group success.

##### Generating output tokens

Successful groups send their results to the first output port and the unsuccessful groups send their results to the second output port. The number and content of output tokens is specified by the **Output** attribute:

- **Single token** - only one token is sent to an output port per group, the token is populated by all group tokens - fields are copied based on fields names (input tokens order to be copied is not guaranteed).
- **All tokens** - each incoming token from the group is sent to the dedicated output port; in the case of incompatible metadata, fields are copied based on field names.
> [!NOTE]
> Output ports are not required. Tokens routed to a missing edge are quietly discarded.

#### Examples

Let’s look at simple example of usage.

![Barrier Basic Concept](../figures/Barrier-Basic-Concept.png)
*Figure 424. Example of typical usage of Barrier component*

In this example, three different graphs are synchronously executed by three **ExecuteGraph** components. All three graphs are running in parallel. **Barrier** is a collection point for graph execution outcomes; it waits for all graphs to finish prior to moving on to the next step. If all graphs finished successfully, an output token is sent to the first output port. On the other hand, if one or more graphs failed, an output token is sent to the second output port. This component allows simple evaluation for status of the whole job group.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
| [Job control comparison](common-of-job-control.md#job-control-comparison) |
