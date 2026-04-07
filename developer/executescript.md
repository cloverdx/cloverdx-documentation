<!-- Development > Component reference > Job Control > ExecuteScript -->

### ExecuteScript

![ExecuteScript 64x64](../figures/ExecuteScript-64x64.png)

| [Short description](executescript.md#short-description) |
| --- |
| [Ports](executescript.md#ports) |
| [Metadata](executescript.md#metadata) |
| [ExecuteScript attributes](executescript.md#executescript-attributes) |
| [Details](executescript.md#details) |
| [Examples](executescript.md#examples) |
| [Best practices](executescript.md#best-practices) |
| [See also](executescript.md#see-also) |

#### Short description

**ExecuteScript** is a component that runs either shell scripts or scripts interpreted by a selected interpreter. It either runs a script only once or repeatedly for each incoming record. Each incoming record can redefine almost all parameters of a run including the script itself.

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | Parameters of a script run (including a script itself if needed). | Any |
| Output | 0 | **⨯** | A component input and results of a script run. | Any |
| Error | 1 | **⨯** | A component input and results of a script run. Records for scripts that cannot run or return 1. | Any |

#### Metadata

**ExecuteScript** does not propagate metadata from left to right or from right to left.

This component has metadata templates available. See general details on [metadata templates](components.md#metadata-templates).

The metadata template **ExecuteScript_RunConfig** available on the first input port is described in [Input mapping fields description](executescript.md#input-mapping-fields-description).

The metadata template **ExecuteScript_RunResult** available on output ports is described in [Output mapping fields description](executescript.md#output-mapping-fields-description).

#### ExecuteScript attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Script | no | Code of a script to be executed. If the interpreter attribute value is kept default, the script must be code of a shell script. Thus, it can easily be used for running one or more system commands. Otherwise, the code format depends on a chosen interpreter. |  |
| Script URL | no | A URL of a script to be executed. If the interpreter attribute value is kept default, the script must be code of a shell script. Thus, it can easily be used for running one or more system commands. Otherwise, the code format depends on the chosen interpreter. If both the **Script** and **Script URL** attributes are specified, only **Script URL** is used. |  |
| Script charset | no | This character encoding is used for an executed script file. A script file reference is specified either in the **Script URL** attribute or a temporary batch file is created automatically from the **Script** attribute.  The default encoding depends on DEFAULT_CHARSET_DECODER in defaultProperties. | UTF-8 (default) \| <other encodings> |
| Working directory | no | A working directory of the executed script. All relative paths used inside the script will be interpreted with respect to this directory. By default, it is set to the root of the **CloverDX** project containing the graph. |  |
| Timeout | no | A limit for script execution (in milliseconds). The limit can be set in other units than milliseconds. See [Time Intervals](components.md#time-intervals).  When a script runs longer than the limit, the components terminates it. In this case in the output, record fields are set as follows: exitValue is set to 1, reachedTimeout to `true` and duration is greater or equal to timeout. | 0 (unlimited) \| positive number |
| Input Mapping | no | Input mapping defines how data from an incoming token overrides default component settings. See [input mapping fields description](executescript.md#input-mapping-fields-description) | CTL transformation |
| Output Mapping | no | Output mapping maps results of successful script executions to the first output port. See [output mapping fields description](executescript.md#output-mapping-fields-description) | CTL transformation |
| Error Mapping | no | Error mapping maps results of unsuccessful scripts to the second output port. See [output mapping fields description](executescript.md#output-mapping-fields-description) | CTL transformation |
| Redirect Error Output | no | By default, results of failed scripts are sent to the second output port (error port). If this switch is set to `true`, results of unsuccessful scripts are sent to the first output port in the same way as successful scripts. | false (default) \| true |
| Advanced |  |  |  |
| Interpreter | no | Set an interpreter to be used for running a script. When an interpreter is executed, `${}` is substituted with a name of a temporary batch file that contains a copy of the script. If an interpreter is sensitive to an extension of a script file, it is necessary to set **Script file extension** property so that a temporary file will have the right extension. | A path to an interpreter followed by `${}`. By default a script is interpreted by a system shell (e.g. `cmd`in Windows and `sh` in Linux). |
| Environment variables | no | Sets environment variables values in the script. It allows either setting them or appending to them. Appending to a non-existing variable leads to defining it and setting its value. Note that variable values are only visible inside of the script, i.e. setting `PATH` cannot be used for setting a path to an interpreter. Variable values set in this property can be overridden by mapping of input to **EnvironmentVariables** metadata in an input mapping dialog.  If you are appending a value to the system variable (e.g. $PATH), the correct system-dependent path delimiter should be used at the beginning of the appended value (colon on Linux, semicolon on Windows). |  |
| Standard input | no | Contents of a standard input that will be sent to the script. Be aware that if the script expects more input lines than available, it may hang. | string |
| Standard input file URL | no | A file URL to contents of a standard input that will be sent to the script. Be aware that if the script expects more input lines than available, it may hang. |  |
| Standard output file URL | no | A file URL of a file to store a standard output of the script. The file content is either rewritten or appended depending on the **append** flag. |  |
| Error output file URL | no | A file URL of a file to store an error output of the script. The file content is either rewritten or appended depending on the **append** flag. |  |
| Append | no | Sets whether a standard output and error output written into files (**Standard output file URL** and **Error output file URL** attributes) should rewrite existing content or it should be appended. | false (default) \| true |
| Data charset | no | Character encoding used to encode a standard input passed from an input port and to decode a standard and error output to be passed to output ports. | UTF-8 (default) \| <other encodings> |
| Script file extension | no | Sets an extension of a batch file that is given to the interpreter (its name is substituted for `${}` in the interpreter setting). | `bat` (default) \| string |
| Stop processing on fail | no | By default, any failed script causes the component to stop executing other scripts and information about skipped tokens is sent to the error output port. This behavior can be disabled by this attribute. **Note:** this function works only if an edge is connected to the component’s error port. | true (default) \| false |
> [!NOTE]
> The contents of the **Script** attribute are copied to a temporary batch file. On Microsoft Windows, it is often useful to start the script with `@echo off` to disable echoing the executed commands.

#### Details

| [Input mapping fields description](executescript.md#input-mapping-fields-description) |
| --- |
| [Output mapping fields description](executescript.md#output-mapping-fields-description) |

**ExecuteScript** runs a script with a given interpreter (default system shell by default).

When there is no edge connected to an input port, the component runs the script only once. One output record is produced in this case.

When there are records coming to an input port, one script execution per record is performed and one output record per script execution is produced.

If the script is successful, the component continues with processing of the next input tokens. Otherwise, component stops executing other scripts and from now on, all incoming tokens are ignored and information about ignored tokens is sent to the error output port. This behavior can be changed in the **Stop processing on fail** parameter.

The output record contains all important information about a script run (times, exit value, error reports and standard output). Mapping of these values to user-defined output metadata can be defined in **Output Mapping** and **Error Mapping** attributes. If the Output mapping is empty, fields of the RunStatus record are mapped to the output by name.

All script execution parameters can be set via input records using the **Input Mapping** attribute. The mapping sets which values for the input are used as script execution parameters. Input and output mapping are common to [job control](job-control.md) components.

A single run of a script is performed as follows:

- The script code is copied to a temporary batch file.
- An interpreter is run with a `${}` string substituted with the name of the temporary file.
- When the script is over, the output record is produced and sent to the first output port for successful runs and to the second output port for unsuccessful runs.

For more detailed information see [attribute description](executescript.md#executescript-attributes).

##### Input Mapping Fields Description

Input records can be mapped to two different metadata: **RunConfig** and **EnvironmentVariables**.

Fields of **RunConfig** have the following functionality:

| Field | Description |
| --- | --- |
| script | Overrides the attribute **Script**. |
| scriptURL | Overrides the attribute **Script URL**. |
| scriptCharset | Overrides the attribute **Script charset**. |
| interpreter | Overrides the attribute **Interpreter**. |
| workingDirectory | Overrides the attribute **Working Directory**. |
| timeout | Overrides the attribute **Timeout**. |
| environmentVariables | Overrides the attribute **Environment Variables**. It is expected that the value contains a list of variable assignments delimited with ";". An assignment with a simple "=" symbol assigns a value to an assigned environment variable. An assignment with a "+=" symbol appends a value to an assigned environment variable. |
| stdIn | Overrides the attribute **Standard Input**. |
| stdInFileURL | Overrides the attribute **Standard Input File URL**. |
| stdOutFileURL | Overrides the attribute **Standard Output File URL**. |
| errOutFileURL | Overrides the attribute **Error Output File URL**. |
| append | Overrides the attribute **Append**. |
| dataCharset | Overrides the attribute **Data charset**. |
| scriptFileExtension | Overrides the attribute **Script File Extension**. |
> [!NOTE]
> In **Input mapping**, you can use the `$out.0.script` field to create a dynamic command line. Just map a script and its parameters onto the field. Example:
>
> `$out.0.script = "md5.exe " + $in.0.filePath;`
> [!NOTE]
> Environment variables provided to the executed script can be defined in three different ways:
>
> 1. Use the component’s **Environmental variables** attribute for static definition of environment variables. Variable names and values are defined once for all script executions.
> 2. The output record **EnvironmentVariables** populated in **Input mapping** is the second way how environment variables can be defined. Set of variable names is still statically defined by the record structure, but values of variables can be derived from input tokens.
> 3. The most complex way how environment variables can be defined is to populate the **environmentVariables** field in the output record **RunConfig** in **Input mapping**. Value of this field has the same syntax and meaning as the **Environment variables** attribute. Set of variables as well as their values can be defined fully dynamically in this case.
> [!NOTE]
> If you want to append a string to an environment variable in **Input mapping**, use the **getEnvironmentVariables()** CTL function. Example:
>
> `$out.1.PATH = getEnvironmentVariables()["PATH"] + ":" + $in.0.additionalPath;`

##### Output mapping fields description

If output mapping is empty, fields of the input record and result record are mapped to the output by name.

| Field | Description |
| --- | --- |
| stdOut | Standard output of a script. |
| errOut | Error output of a script. |
| startTime | Start time of a script. |
| stopTime | Stop time of a script. |
| duration | Duration of a script. (duration = stopTime - startTime) |
| exitValue | Value returned by the script. Typically, 0 means no error, non-zero values stand for errors. |
| reachedTimeout | Boolean determining whether the script reached timeout. |
| errException | If the script call finishes with an error, it may contain an exception that caused the error. This happens only in a situation when the script has not started (e.g. the path to the script is not valid) or its run has been interrupted (e.g. when a timeout has been reached). |
| errMessage | Message reported by the exception in errException. |

##### Difference between SystemExecute and ExecuteScript

**SystemExecute** uses a data-oriented approach. It allows you to stream data from and to the script.

**ExecuteScript** executes scripts in steps. It allows you to receive scripts from an input edge and execute them one by one.

#### Examples

| [Run shell script](executescript.md#run-shell-script) |
| --- |
| [Using timeout](executescript.md#using-timeout) |
| [Running scripts one by one](executescript.md#running-scripts-one-by-one) |

##### Run shell script

This example shows way to run a simple script. The script is specified in the component.

Use **ExecuteScript** to run `last` command.

###### Solution

Attach an edge to the first output port of **ExecuteScript** component.

Configure the **ExecuteScript** component in the following way.

| Attribute | Value |
| --- | --- |
| Script | last |
| Interpreter | /bin/bash ${} |

##### Using timeout

Scripts may hang or run too long. This example shows how to set timeout in **ExecuteScript**.

Use **ExecuteScript** to run `my_calculation` program, which is on the PATH. The program should not run longer than 5 seconds.

###### Solution

| Attribute | Value |
| --- | --- |
| Script | my_calculation |
| Timeout (ms) | 5s |
| Interpreter | /bin/bash ${} |

If the timeout is specified without units, it is in millisecond. It can be set in other units. See [Time intervals](components.md#time-intervals).

If you need to terminate the script, but the graph should not fail, connect an edge to the second output port of **ExecuteScript**.

##### Running scripts one by one

**ExecuteScript** allows you to receive scripts from an input edge. This example shows a way to execute scripts one by one.

Execute shell commands received from an input edge.

###### Solution

Connect edges to input and output ports. The commands to be executed are received in the `script` field.

| Attribute | Value |
| --- | --- |
| Input mapping | ```ctl function integer transform() {     $out.0.script = $in.0.script;      return ALL; } ``` |
| Interpreter | /bin/bash ${} |

#### Best practices

We recommend users to specify **Data charset**.

If the script is in an external file (specified with **Script URL**), we recommend users to explicitly specify **Script charset** too.

#### See also

| [SystemExecute](sysexecute.md) |
| --- |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Job Control](common-of-job-control.md) |
