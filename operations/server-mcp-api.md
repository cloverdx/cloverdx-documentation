<!-- Automation and operations > Server APIs > CloverDX Model Context Protocol (MCP) API -->

## 14. CloverDX Model Context Protocol (MCP) API

MCP (Model Context Protocol) is an emerging standard that enables AI agents to interact with external services and data sources. It provides a standardized way for AI models to access tools, resources, and context from various applications, allowing them to perform tasks beyond their base capabilities.

CloverDX MCP Server exposes a comprehensive set of tools that enable AI agents to fully interact with CloverDX:

- **Sandbox Management**: browse, read, write, and organize files within CloverDX sandboxes.
- **Job Execution**: run graphs and jobflows, wait for results, monitor status, and abort running jobs.
- **Graph Editing**: create and modify CloverDX graphs and jobflows using structured XML operations.
- **Server Diagnostics**: access server logs, performance metrics, and internal system database.
- **Component Reference**: discover and configure CloverDX component types.
- **Knowledge Base**: access the CloverDX knowledge library and manage project-scoped knowledge entries.
- **External Databases**: query and inspect databases accessible via JDBC.
- **Support**: report issues directly to the CloverDX Support Portal.

MCP API is available at:

```
http(s)://[cloverdx-server-host]:[port]/clover/mcp/mcp
```

> [!NOTE]
> In CloverDX 7.5.0 we’ve significantly expanded the scope of the MCP Server by adding more than 40 new tools. Given this capability expansion, we are releasing the MCP APIs in CloverDX 7.5.0 as a **technology preview**.
>
> MCP Server and its tools are under active development. Tools may change in future releases, sometimes in incompatible ways, even be completely removed. **Use the MCP in dev/test environments only, not in production.** Treat it as a tool for evaluation and non-critical work, and review everything it produces before relying on it. Use it with caution since it is possible to edit files, run jobs or even read data flowing through them via MCP.
>
> Gathering feedback on how teams use the MPC Server in CloverDX is one of the goals of this technology preview. Contact your Account representative if you wish to provide feedback that could help us improve future versions of the MCP Server.

### MCP Tools Reference

The following tables list all MCP tools available in CloverDX Server, grouped by functional area. The **Access** column indicates whether a tool is available in read-only mode. To configure permissions for various tools, see [MCP tools permissions configuration](../admin/server-config-mcp.md#mcp-tools-permissions).

#### Sandbox Tools

Tools for browsing and managing files inside CloverDX sandboxes.

| Tool | Description | Access |
| --- | --- | --- |
| `sandbox_list` | List all sandboxes accessible to the current user. | Read |
| `sandbox_get_detail` | Get detailed information about a specific sandbox — root path, owner, distribution type, and suspension state. | Read |
| `sandbox_list_files` | List files and folders inside a sandbox directory. | Read |
| `sandbox_find_file` | Recursively search for files in a sandbox using wildcard patterns (`*`, `?`). | Read |
| `sandbox_read_file` | Read the text content of a file stored in a sandbox. Supports optional line range and encoding detection. | Read |
| `sandbox_analyze_file` | Extract or profile content from binary and structured files: extract text from PDF documents (`extract_pdf`), read Excel sheets (`extract_excel`), or profile CSV files for data-quality statistics (`profile_csv`). | Read |
| `sandbox_list_assets` | List reusable shared assets in a sandbox: metadata definitions (`.fmt`), connection configurations (`.cfg`), lookup tables (`.lkp`), CTL files, sequences, and parameter files. | Read |
| `sandbox_get_workspace_parameters` | Resolve sandbox workspace parameter values such as `${DATAIN_DIR}` and `${CONN_DIR}` with server-side defaults and system property overlays. | Read |
| `sandbox_grep_files` | Search file contents across one or more sandboxes using literal strings or regular expressions. | Read |
| `sandbox_write_file` | Create or update a file in a sandbox. Supports overwrite, append, insert, and line-range replace modes. | Write |
| `sandbox_patch_file` | Apply targeted anchor-based patches to a text file in a sandbox without replacing the whole file. Preferred for editing CTL, SQL, and properties files. | Write |
| `sandbox_copy_file` | Copy a file within or across sandboxes. Overwrites the destination if it already exists. | Write |
| `sandbox_rename_file` | Rename a file within its current directory in a sandbox. | Write |
| `sandbox_delete_file` | Delete a file from a sandbox. This operation is irreversible. | Write |
| `sandbox_create_directory` | Create a new directory in a sandbox. | Write |
| `sandbox_delete_directory` | Delete a directory from a sandbox, including all its contents. This operation is irreversible. | Write |
| `sandbox_git` | Perform git version-control operations on a sandbox repository: commit, log, diff, status, branch management, stash, and more. | Write |

#### Job Tools

Tools for running, monitoring, and debugging graph and jobflow executions.

| Tool | Description | Access |
| --- | --- | --- |
| `job_list` | List recent graph and jobflow executions from the execution history, with optional filtering by sandbox, job file, and status. | Read |
| `job_get_status` | Get the current execution status of a job run without fetching the full log. | Read |
| `job_get_log` | Retrieve the full execution log for a job run (up to 1 MiB). | Read |
| `job_get_tracking` | Get per-phase, per-node, and per-port execution tracking data, including record and byte counts for each component. | Read |
| `job_get_edge_debug_data` | Fetch sample records that flowed through a specific graph edge during a debug-enabled run. | Read |
| `job_await` | Wait for a running job to reach a terminal state (finished, error, or aborted). Safe to re-call on timeout. | Read |
| `job_validate` | Validate a graph or jobflow file using the server-side configuration checker. Reports errors, warnings, and info messages. | Read |
| `job_plan` | Record a structured graph design plan and validate its internal consistency before writing any XML. | Read |
| `job_run` | Submit a graph or jobflow for asynchronous execution. Returns a run ID immediately. | Write |
| `job_abort` | Abort a running graph or jobflow execution. Also terminates any child jobs it spawned. | Write |

#### Graph Editing Tools

Tools for inspecting and modifying CloverDX graphs (`.grf`), jobflows (`.jbf`), and subgraphs (`.sgrf`) via the XML DOM.

| Tool | Description | Access |
| --- | --- | --- |
| `graph_resolve_edge_schemas` | Resolve the record schema (field names, types, nullability) that would flow along each edge of a graph at runtime, including propagated schemas. | Read |
| `graph_list_elements` | List specific element types defined in a job file: metadata records, lookup tables, dictionaries, or sequences. | Read |
| `graph_edit_properties` | Set or update attribute values, CTL transformation code, or metadata record definitions on existing graph elements. Supports bulk edits and dry-run preview. | Write |
| `graph_edit_structure` | Add, delete, or move whole structural elements in a job — nodes, edges, phases, metadata definitions, connections, and more. Supports dry-run preview. | Write |

#### Component Tools

Tools for discovering and understanding CloverDX component types.

| Tool | Description | Access |
| --- | --- | --- |
| `component_list` | Browse and search available CloverDX component types by name, category, or keyword. | Read |
| `component_get_info` | Get detailed configuration information for a component type: input/output ports, properties, required settings, and metadata propagation rules. | Read |
| `component_get_guide` | Fetch the in-depth reference guide for a component, including configuration examples, CTL mapping syntax, and known pitfalls. | Read |

#### Server Tools

Tools for inspecting CloverDX Server state, logs, and internal system database.

| Tool | Description | Access |
| --- | --- | --- |
| `server_deployment` | Get a snapshot of the running CloverDX Server environment — JVM, OS, memory, cluster topology, and configuration. Can also return the official support matrix. | Read |
| `server_logs_search` | Search server log entries by time range and regular expression pattern. Supports multiple log appenders: main server log, cluster, user actions, job queue, data services, and others. | Read |
| `server_perf_logs_query` | Execute SQL queries (Apache Calcite dialect) against the server performance log. Returns time-series CPU, memory, GC, and I/O metrics sampled every 3 seconds. | Read |
| `server_db_get_schema` | Retrieve the table and column schema of the CloverDX internal system database (execution history, users, sandboxes, schedules, and other server-managed records). | Read |
| `server_db_execute_query` | Execute a read-only SQL SELECT query against the CloverDX internal system database. | Read |

#### External Database Tools

Tools for interacting with external databases accessible via JDBC.

| Tool | Description | Access |
| --- | --- | --- |
| `db_get_schema` | Query schemas, tables, or columns of any database accessible via JDBC — using either a saved connection configuration file or inline connection properties. Supports all major databases (PostgreSQL, Oracle, MSSQL, MySQL, and others). | Read |
| `db_execute_query` | Execute SQL (SELECT, DML, or DDL) against any database accessible via JDBC. Results are returned as JSON or delimited text. | Write |

#### Knowledge Tools

Tools for accessing the built-in CloverDX knowledge library and managing project-scoped knowledge entries.

| Tool | Description | Access |
| --- | --- | --- |
| `knowledge_list_resources` | List all static reference documents exposed as MCP resources by the installed CloverDX knowledge library, including graph XML reference, CTL language reference, and component guides. | Read |
| `knowledge_read_resource` | Fetch the content of a specific knowledge resource by its URI. | Read |
| `knowledge_base_read` | Read a specific entry from the CloverDX knowledge base by name or scoped pointer (e.g. `cdx:component/csv-file`). | Read |
| `knowledge_base_search` | Search the read-only CloverDX knowledge base (guides, recipes, troubleshooting articles) by keyword. | Read |
| `knowledge_project_read` | Read a project-local knowledge entry or the auto-generated index of all entries for a project. | Read |
| `knowledge_project_search` | Search project-local knowledge entries by keyword. | Read |
| `knowledge_project_store` | Store or update a project-local knowledge entry. Used by AI agents to persist project-specific facts (business rules, conventions, validated findings) across sessions. | Write |
| `knowledge_project_delete` | Delete a project-local knowledge entry. | Write |

#### Agent Utility Tools

Tools used by AI agents to manage session state and workflow guidance.

| Tool | Description | Access |
| --- | --- | --- |
| `note_read` | Read notes from the session-scoped working memory. | Read |
| `think` | Log explicit reasoning before taking an action. Helps AI agents plan component selection, graph edits, and error diagnostics. | Read |
| `task_workflow_get` | Get step-by-step procedural instructions for a CloverDX task type: creating a graph, editing a graph, creating a jobflow, or validating and running a job. | Read |
| `note_add` | Append a note to a named section in session-scoped working memory. Notes are lost when the MCP session ends. | Write |
| `note_clear` | Clear notes from session-scoped working memory — either a specific section or all sections. | Write |
| `report_support_issue` | Report a problem to the CloverDX Support Portal. Optionally attaches a diagnostic support package containing logs and configuration details. | Write |
