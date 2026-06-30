<!-- Automation and operations > Server APIs > Simple HTTP API (deprecated) -->

## 15. Simple HTTP API (deprecated)

The Simple HTTP API is a basic Server automation tool that lets you control the Server from external applications using simple HTTP calls.
> [!NOTE]
> Simple HTTP API is deprecated. Use [REST API](rest-api.md) instead.

Most operations are accessible using the HTTP GET method and return plain text. Thus, both `request` and `response` can be conveniently sent and parsed using very simple tools (wget, grep, etc.).

If global security is on (on by default), the Basic HTTP authentication is used. Authenticated operations will require valid user credentials with corresponding permissions.

Note that the Graph-related operations `graph_run`, `graph_status` and `graph_kill` also work for jobflows.

The generic pattern for a request URL:

```
http://[domain]:[port]/[context]/[servlet]/[operation]?[param1]=[value1]&[param2]=[value2]...
```

**example:**`http://localhost:8080/clover/simpleHttpApi/help`
> [!NOTE]
> For backward compatibility, you can also use `http://localhost:8080/clover/request_processor/help`.

### CSRF protection

The Simple HTTP API provides protection against Cross-Site Request Forgery (CSRF) attacks. An example of such an attack is a case where the user is logged into the Server Console, and an attacker sends him a link to the Simple HTTP API such that it runs a graph. Clicking on such a link would call the Simple HTTP API and re-use the session of the logged-in user. There are also more complex variants of the attack that are harder to detect by the user.

The protection against such an attack is that the Simple HTTP API requires the presence of the `X-Requested-By` header in the HTTP request. Value of the header can be arbitrary (it is not checked). Such a header cannot be set by CSRF attack vectors, i.e. by clicking on a link in an email.

Examples of calling the API with the `X-Requested-By` header:

```bash
curl --header "X-Requested-By: arbitrary_value"  http://user:password@hostname:port/clover/simpleHttpApi/graph_run?sandbox=project&graphID=migration.grf
```

```bash
wget --header "X-Requested-By: arbitrary_value" --user=$USER --password=$PASS -O ./$OUTPUT_FILE $REQUEST_URL
```

The CSRF protection of Simple HTTP API can be disabled via the [security.csrf.protection.enabled](../admin/list-of-properties.md#lop-security-csrf-protection-enabled) configuration property. The CSRF protection is enabled by default. If the protection is disabled, it is not necessary to set the `X-Requested-By` header.

The Server Console’s page for testing the Simple HTTP API uses a different CSRF protection mechanism. The requests contain a `csrftoken` parameter. This is intended for usage only in the testing page.

### List of Operations

- [Operation help](simple-http-api.md#operation-help)
- [Operation graph_run](simple-http-api.md#operation-graph-run)
- [Operation graph_status](simple-http-api.md#operation-graph-status)
- [Operation graph_kill](simple-http-api.md#operation-graph-kill)
- [Operation server_jobs](simple-http-api.md#operation-server-jobs)
- [Operation sandbox_list](simple-http-api.md#operation-sandbox-list)
- [Operation sandbox_content](simple-http-api.md#operation-sandbox-content)
- [Operation executions_history](simple-http-api.md#operation-executions-history)
- [Operation suspend](simple-http-api.md#operation-suspend)
- [Operation resume](simple-http-api.md#operation-resume)
- [Operation sandbox_create](simple-http-api.md#operation-sandbox-create)
- [Operation sandbox_add_location](simple-http-api.md#operation-sandbox-add-location)
- [Operation sandbox_remove_location](simple-http-api.md#operation-sandbox-remove-location)
- [Operation download_sandbox_zip](simple-http-api.md#operation-download-sandbox-zip)
- [Operation upload_sandbox_zip](simple-http-api.md#operation-upload-sandbox-zip)
- [Operation cluster_status](simple-http-api.md#operation-cluster-status)
- [Operation export_server_config](simple-http-api.md#operation-export-server-config)
- [Operation import_server_config](simple-http-api.md#operation-import-server-config)

The HTTP API is disabled by default. You can enable it with the configuration property `http.api.enabled`. In the Server GUI, switch to **Configuration** ****Setup** and add the following line

```properties
http.api.enabled=true
```

to the properties file.

### Operation help

**parameters**

no

**returns**

a list of possible operations and parameters with its descriptions

**example**

```
http://localhost:8080/clover/simpleHttpApi/help
```

### Operation graph_run

Call this operation to start an execution of the specified job. The operation is called graph_run for backward compatibility, however it may execute a graph or a jobflow.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| graphID | yes | - | The file path to the job file, relative to the sandbox root. |
| sandbox | yes | - | The text ID of sandbox. |
| additional job parameters | no |  | Any URL parameter with the `param_` prefix is passed to the executed job and may be used in transformation XML as a placeholder, but without the `param_` prefix. e.g. `param_FILE_NAME` specified in URL may be used in the XML as `${FILE_NAME}`. These parameters are resolved only during loading of XML, so it cannot be pooled. |
| additional config parameters | no |  | URL parameters prefixed with `config_` can set some of the execution parameters. For graphs, the following parameters are supported:  - `config_skipCheckConfig` - when set to `false`, graph configuration will be checked before the execution. - `config_logLevel` - log level of the executed graph, one of OFF, FATAL, ERROR, WARN, INFO, DEBUG, TRACE, ALL. - `config_debugMode` - when set to `true`, debug mode for a given graph will be enabled. For more information, see [Execution Properties](sandboxes.md#execution-properties). |
| nodeID | no | - | In Cluster mode, it is the ID of a node which should execute the job. However it is not final. If the graph is distributed or the node is disconnected, the graph may be executed on another node. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

run ID: incremental number, which identifies each execution request

**example**

```
http://localhost:8080/clover/simpleHttpApi/graph_run?graphID=graph/graphDBExecute.grf&sandbox=mva
```

### Operation graph_status

Call this operation to obtain a status of a specified job execution. The operation is called graph_status for backward compatibility; however, it may return status of a graph or jobflow.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| runID | yes | - | Id of each graph execution |
| returnType | no | STATUS | STATUS \| STATUS_TEXT \| DESCRIPTION \| DESCRIPTION_XML |
| waitForStatus | no | - | Status code which we want to wait for. If it is specified, this operation will wait until the graph is in the required status. |
| waitTimeout | no | 0 | If `waitForStatus` is specified, it will wait only for the specified amount of milliseconds. Default 0 means forever, but it depends on an application server configuration. When the specified timeout expires and graph run still isn’t in a required status, the server returns code 408 (Request Timeout). 408 code may be also returned by an application server if its HTTP request timeout expires before. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

Status of a specified graph. It may be a number code, text code or a complex description in dependence on the optional parameter `returnType`. Description is returned as a plain text with a pipe as a separator, or as XML. A schema describing XML format of the XML response is accessible on **CloverDX Server** URL: `http://[host]:[port]/clover/schemas/executions.xsd` Depending on the `waitForStatus` parameter, it may return a result immediately or wait for a specified status.

**example**

```
http://localhost:8080/clover/simpleHttpApi/graph_status?runID=123456&returnType=DESCRIPTION&waitForStatus=FINISHED&waitTimeout=60000
```

### Operation graph_kill

Call this operation to abort/kill a job execution. The operation is called graph_kill for backward compatibility; however, it may abort/kill a graph or a jobflow.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| runID | yes | - | The ID of each graph execution |
| returnType | no | STATUS | STATUS \| STATUS_TEXT \| DESCRIPTION |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

The status of the specified graph after an attempt to kill it. It may be a number code, text code or a complex description in dependence on optional parameter.

**example**

```
http://localhost:8080/clover/simpleHttpApi/graph_kill?runID=123456&returnType=DESCRIPTION
```

### Operation server_jobs

**parameters**

no

**returns**

a list of runIDs of currently running jobs.

**example**

```
http://localhost:8080/clover/simpleHttpApi/server_jobs
```

### Operation sandbox_list

**parameters**

no

**returns**

List of all sandbox text IDs. In the next versions, it will return only accessible ones.

**example**

```
http://localhost:8080/clover/simpleHttpApi/sandbox_list
```

### Operation sandbox_content

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | yes | - | text ID of sandbox |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

A list of all elements in the specified sandbox. Each element may be specified as a file path relative to the sandbox root.

**example**

```
http://localhost:8080/clover/simpleHttpApi/sandbox_content?sandbox=mva
```

### Operation executions_history

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| from | no | - | Lower datetime limit of start of execution, including submitted time. This filter is based on *Submitted* time of job executions, not on *Started*, see [Job queue](job-queue.md) for more details. The operation will return only records after (and equal to) this datetime. Format: "yyyy-MM-dd HH:mm" (must be URL encoded). |
| to | no | - | The upper datetime limit of start of execution. The operation will return only records before (and equal to) this datetime. Format: "yyyy-MM-dd HH:mm" (must be URL encoded). |
| stopFrom | no | - | The lower datetime limit of stop of execution. The operation will return only records after (and equal to) this datetime. Format: "yyyy-MM-dd HH:mm" (must be URL encoded). |
| stopTo | no | - | The upper datetime limit of stop of execution. The operation will return only records before (and equal to) this datetime. Format: "yyyy-MM-dd HH:mm" (must be URL encoded). |
| status | no | - | Current execution status. The operation will return only records with specified `STATUS`. The values are `ENQUEUED` \| `RUNNING` \| `ABORTED` \| `FINISHED_OK` \| `ERROR` |
| sandbox | no | - | Sandbox code. The operation will return only records for graphs from a specified sandbox. |
| graphID | no | - | The text Id, which is unique in a specified sandbox. The file path is relative to the sandbox root. |
| orderBy | no | - | An attribute for list ordering. Possible values: `id` \| `graphId` \| `status` \| `submitTime` \| `startTime` \| `stopTime`. By default, there is no ordering. |
| orderDescend | no | true | A switch which specifies ascending or descending ordering. If true (default), ordering is descending. |
| returnType | no | IDs | Possible values are: `IDs` \| `DESCRIPTION` \| `DESCRIPTION_XML` \| `COUNT` |
| index | no | 0 | An index of the first returned records in a whole record set. |
| records | no | 1000 | The maximum amount of returned records. Set the value to `unlimited` for parameter to return an unlimited number of records. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

List of executions according to filter criteria.

For `returnType==IDs` returns a simple list of runIDs (with new line delimiter).

For `returnType==COUNT` returns only the number of entries. Note that filtering works, but the parameters `orderBy`, `orderDescend`, `index` and `records` are silently ignored.

For `returnType==DESCRIPTION` returns complex response which describes current status of selected executions, their phases, nodes and ports.

```
execution|[runID]|[status]|[username]|[sandbox]|[graphID]|[submittedDatetime]|[finishedDatetime]|[clusterNode]|[graphVersion] (1)
phase|[index]|[execTimeInMilis]
node|[nodeID]|[status]|[totalCpuTime]|[totalUserTime]|[cpuUsage]|[peakCpuUsage]|[userUsage]|[peakUserUsage]|[label]
port|[portType]|[index]|[avgBytes]|[avgRows]|[peakBytes]|[peakRows]|[totalBytes]|[totalRows]
```

| 1 | CloverDX no longer stores graphVersion, so the value is `null` |
| --- | --- |

**example of request**

```
http://localhost:8080/clover/simpleHttpApi/executions_history?from=&to=2008-09-16+16%3A40&status=&sandbox=def&graphID=&index=&records=&returnType=DESCRIPTION
```

**example of DESCRIPTION (plain text) response**

```
execution|13108|FINISHED_OK|clover|def|test.grf|2008-09-16 11:11:19|2008-09-16 11:11:58^|nodeA|2.4
phase|0|38733
node|DATA_GENERATOR1|FINISHED_OK|0|0|0.0|0.0|0.0|0.0|label_text
port|Output|0|0|0|0|0|130|10
node|TRASH0|FINISHED_OK|0|0|0.0|0.0|0.0|0.0|label_text
port|Input|0|0|0|5|0|130|10
node|SPEED_LIMITER0|FINISHED_OK|0|0|0.0|0.0|0.0|0.0|label_text
port|Input|0|0|0|0|0|130|10
port|Output|0|0|0|5|0|130|10
execution|13107|ABORTED|clover|def|test.grf|2008-09-16 11:11:19|2008-09-16 11:11:30
phase|0|11133
node|DATA_GENERATOR1|FINISHED_OK|0|0|0.0|0.0|0.0|0.0|label_text
port|Output|0|0|0|0|0|130|10
node|TRASH0|RUNNING|0|0|0.0|0.0|0.0|0.0|label_text
port|Input|0|5|0|5|0|52|4
node|SPEED_LIMITER0|RUNNING|0|0|0.0|0.0|0.0|0.0|label_text
port|Input|0|0|0|0|0|130|10
port|Output|0|5|0|5|0|52|4
```

For `returnType==DESCRIPTION_XML` returns a complex data structure describing one or more selected executions in XML format. A schema describing XML format of the XML response is accessible on **CloverDX Server** URL: http://[host]:[port]/clover/schemas/executions.xsd

### Operation suspend

Suspends the Server or sandbox (if specified). No graphs may be executed on suspended Server/sandbox.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | no | - | The text ID of a sandbox to suspend. If not specified, it suspends the whole Server. |
| atonce | no |  | If this parameter is set to true, running graphs from suspended Server (or just from sandbox) are aborted. Otherwise it can run until it is finished in standard way. |

**returns**

Result message

### Operation resume

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | no | - | The text Id of a sandbox to resume. If not specified, the Server will be resumed. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should the possible error message be. |

**returns**

Result message

### Operation sandbox_create

This operation creates a specified sandbox. If it is a sandbox of "partitioned" or "local" type, it also creates locations by "sandbox_add_location" operation.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | yes | - | The text ID of a sandbox to be created. |
| path | no | - | A path to the sandbox root if the Server is running in a standalone mode. |
| type | no | shared | Sandbox type: shared \| partitioned \| local. For a standalone Server may be left empty, since the default "shared" is used. |
| createDirs | no | true | Switch whether to create sandbox root path and a directory structure (only for a standalone Server or "shared" sandboxes in a Cluster environment). |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

Result message

### Operation sandbox_add_location

This operation adds a location to the specified sandbox. Can be only used with partitioned or local sandboxes.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | yes | - | A sandbox which we want to add a location to. |
| nodeId | yes | - | A location attribute - a node which has direct access to the location. |
| path | yes | - | A location attribute - a path to the location root on the specified node. |
| location | no | - | A location attribute - a location storage ID. If not specified, a new one will be generated. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

Result message

### Operation sandbox_remove_location

This operation removes a location from the specified sandbox. Only sandboxes of the partitioned or local type can have locations associated.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | yes | - | Removes a specified location from its sandbox. |
| location | yes | - | A location storage ID. If the specified location isn’t attached to the specified sandbox, the sandbox won’t be changed. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should possible error message be. |

**returns**

Result message

### Operation download_sandbox_zip

This operation downloads the content of a specified sandbox as a ZIP archive.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | yes | - | A code of the sandbox to be downloaded. |

**returns**

a content of a specified sandbox as a ZIP archive

**example**

```bash
wget --http-user=username --http-password=password http://localhost:8080/clover/simpleHttpApi/download_sandbox_zip?sandbox=my-sandbox
```

### Operation upload_sandbox_zip

This operation uploads the content of a ZIP archive into a specified sandbox.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| sandbox | yes | - | A code of the sandbox the ZIP file will be expanded to. |
| zipFile | yes | - | The ZIP archive file. |
| overwriteExisting | no | false | If `true`, the files already present in the sandbox will be overwritten. |
| deleteMissing | no | false | If `true`, the files not present in the ZIP file will be deleted from the sandbox. |

**returns**

Result message

**an example of request (with using curl CLI tool ([http://curl.haxx.se/)](http://curl.haxx.se/)))**

```bash
curl -u username:password -F "overwriteExisting=true"
    -F "zipFile=@/tmp/my-sandbox.zip"
    http://localhost:8080/clover/simpleHttpApi/upload_sandbox_zip
```

### Operation cluster_status

This operation displays Cluster’s nodes list.

**parameters**

no

**returns**

A list of Cluster nodes with information in the following format:

`<Node Name>|<Node HTTP URL>|<System Load Average>|<Node Status>`

**example**

```
node01|http://localhost:8083/clover|0.3|READY
```

**Note:** The value of system load average is calculated from the minute preceding the call. If it cannot be obtained, a negative value is returned (may be caused by the calculation’s unacceptable performance impact or lack of support by operating system).

### Operation export_server_config

This operation exports a current server configuration in XML format.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| include | no | all | Selection of items that will be included in the exported XML file; the parameter may be specified multiple times. Possible values are:  - `all` - include items of all types - `users` - include a list of users - `userGroups` - include a list of user groups - `sandboxes` - include a list of sandboxes - `jobConfigs` - include a list of job configuration parameters - `schedules` - include a list of schedules - `eventListeners` - include a list of event listeners - `tempSpaces` - include a list of temporary spaces - `secretManagers` - include a list of secret managers - `libraries` - include a list of libraries - `libraryRepositories` - include a list of library repositories |

**returns**

Current server configuration as an XML file.

**example**

```bash
wget --http-user=username --http-password=password http://localhost:8080/clover/simpleHttpApi/export_server_config
```

### Operation import_server_config

This operation imports server configuration.

**parameters**

| Name | Mandatory | Default | Description |
| --- | --- | --- | --- |
| xmlFile | yes | - | An XML file with server’s configuration. |
| dryRun | no | true | If `true`, a dry run is performed with no actual changes written. |
| verbose | no | MESSAGE | MESSAGE \| FULL - how verbose should the response be: `MESSAGE` for a simple message, `FULL` for a full XML report. |
| newOnly | no | false | If `true` only new items will be imported to the Server; the items already present on the Server will be left untouched. |
| override | no | false | If `override` is set to true, the import override existing configuration and the `newOnly` parameter is ignored. The parameter has an effect only if the configuration was exported from CloverDX Server 5.5.0 or newer. It doesn’t affect user and user groups configuration. |
| include | no | all | Selection of items that will be imported from the XML; the parameter may be specified multiple times. Possible values are:  - `all` - import items of all types - `users` - import users - `userGroups` - import user groups - `sandboxes` - import sandboxes - `jobConfigs` - import job configuration parameters - `schedules` - import schedules - `eventListeners` - import listeners - `tempSpaces` - import temporary spaces - `secretManagers` - import secret managers - `libraries` - import libraries - `libraryRepositories` - import library repositories |

**returns**

Result message or XML report

**an example of request (with using curl CLI tool ([http://curl.haxx.se/)](http://curl.haxx.se/)))**

```bash
curl -u username:password -F "dryRun=true" -F "verbose=FULL"
    -F "xmlFile=@/tmp/clover_configuration_2013-07-10_14-03-23+0200.xml"
    http://localhost:8080/clover/simpleHttpApi/import_server_config
```
