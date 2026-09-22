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
http(s)://[cloverdx-server-host]:[port]/clover/mcp/all/v1
```

Besides this main endpoint, each tool group has an endpoint of its own. They all serve the same tools; what differs is how much of the catalogue a client connected to them sees:

| Endpoint | Serves |
| --- | --- |
| `/clover/mcp/all/v1` | Everything the caller is allowed to use, from both groups. |
| `/clover/mcp/diagnostic/v1` | The diagnostic group only. |
| `/clover/mcp/authoring/v1` | The authoring group only. |
> [!NOTE]
> The older URL `/clover/mcp/mcp` still works and serves the same as `/clover/mcp/all/v1`, but it is deprecated. Configure new clients with the versioned one.

### MCP Tools Reference

The following tables list all MCP tools available in CloverDX Server, grouped by functional area. The **Access** column indicates whether a tool is available in read-only mode, the **Permission** column names the permission a caller needs to use the tool. To configure which tools the Server exposes, see [MCP tools permissions configuration](../admin/server-config-mcp.md#mcp-tools-permissions). Tools that work with sandbox files additionally honour the [sandbox file access](../admin/server-config-mcp.md#sandbox-file-access) configuration, which can restrict them to files matching administrator-defined patterns.

#### Tool groups and permissions

Independently of the functional areas below, every tool belongs to a tool group, and the group decides which permission its caller needs:

- **Use AI Diagnostic MCP tools** covers the tools for looking into a running Server – listing jobs, their status, logs and tracking, server and performance logs, the system database, and reporting an issue to CloverDX support. These tools need no seat.
- **Use AI Authoring MCP tools** covers the tools that build or change a solution – sandbox files, graph editing, job execution, the component reference and the knowledge base. A user holding this permission occupies one AI Authoring seat – the same seat that licenses the AI Assistant in the Designer.

Granting **Use all MCP tools** grants both. See [MCP permissions and AI Authoring seats](../admin/server-config-mcp.md#mcp-permissions-and-ai-authoring-seats) for the whole model.

The authoring group is not available through an [MCP proxy](../admin/server-config-mcp.md#configuration-for-cloverdx-60-to-72).

#### Sandbox Tools

Tools for browsing and managing files inside CloverDX sandboxes.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `sandbox_list` | List all sandboxes accessible to the current user. | Read | Use AI Authoring MCP tools |
| `sandbox_get_detail` | Get detailed information about a specific sandbox — root path, owner, distribution type, and suspension state. | Read | Use AI Authoring MCP tools |
| `sandbox_list_files` | List files and folders inside a sandbox directory. | Read | Use AI Authoring MCP tools |
| `sandbox_find_file` | Recursively search for files in a sandbox using wildcard patterns (`*`, `?`). | Read | Use AI Authoring MCP tools |
| `sandbox_read_file` | Read the text content of a file stored in a sandbox. Supports optional line range and encoding detection. | Read | Use AI Diagnostic MCP tools |
| `sandbox_analyze_file` | Extract or profile content from binary and structured files: extract text from PDF documents (`extract_pdf`), read Excel sheets (`extract_excel`), or profile CSV files for data-quality statistics (`profile_csv`). | Read | Use AI Authoring MCP tools |
| `sandbox_list_assets` | List reusable shared assets in a sandbox: metadata definitions (`.fmt`), connection configurations (`.cfg`), lookup tables (`.lkp`), CTL files, sequences, and parameter files. | Read | Use AI Authoring MCP tools |
| `sandbox_get_workspace_parameters` | Resolve sandbox workspace parameter values such as `${DATAIN_DIR}` and `${CONN_DIR}` with server-side defaults and system property overlays. | Read | Use AI Authoring MCP tools |
| `sandbox_grep_files` | Search file contents across one or more sandboxes using literal strings or regular expressions. | Read | Use AI Authoring MCP tools |
| `sandbox_write_file` | Create or update a file in a sandbox. Supports overwrite, append, insert, and line-range replace modes. | Write | Use AI Authoring MCP tools |
| `sandbox_patch_file` | Apply targeted anchor-based patches to a text file in a sandbox without replacing the whole file. Preferred for editing CTL, SQL, and properties files. | Write | Use AI Authoring MCP tools |
| `sandbox_copy_file` | Copy a file within or across sandboxes. Overwrites the destination if it already exists. | Write | Use AI Authoring MCP tools |
| `sandbox_rename_file` | Rename a file within its current directory in a sandbox. | Write | Use AI Authoring MCP tools |
| `sandbox_delete_file` | Delete a file from a sandbox. This operation is irreversible. | Write | Use AI Authoring MCP tools |
| `sandbox_create_directory` | Create a new directory in a sandbox. | Write | Use AI Authoring MCP tools |
| `sandbox_delete_directory` | Delete a directory from a sandbox, including all its contents. This operation is irreversible. | Write | Use AI Authoring MCP tools |
| `sandbox_git` | Perform git version-control operations on a sandbox repository: commit, log, diff, status, branch management, stash, and more. | Write | Use AI Authoring MCP tools |

#### Job Tools

Tools for running, monitoring, and debugging graph and jobflow executions.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `job_list` | List recent graph and jobflow executions from the execution history, with optional filtering by sandbox, job file, and status. | Read | Use AI Diagnostic MCP tools |
| `job_get_status` | Get the current execution status of a job run without fetching the full log. | Read | Use AI Diagnostic MCP tools |
| `job_get_log` | Retrieve the full execution log for a job run (up to 1 MiB). | Read | Use AI Diagnostic MCP tools |
| `job_get_tracking` | Get per-phase, per-node, and per-port execution tracking data, including record and byte counts for each component. | Read | Use AI Diagnostic MCP tools |
| `job_get_edge_debug_data` | Fetch sample records that flowed through a specific graph edge during a debug-enabled run. | Read | Use AI Authoring MCP tools |
| `job_await` | Wait for a running job to reach a terminal state (finished, error, or aborted). Safe to re-call on timeout. | Read | Use AI Authoring MCP tools |
| `job_validate` | Validate a graph or jobflow file using the server-side configuration checker. Reports errors, warnings, and info messages. | Read | Use AI Authoring MCP tools |
| `job_plan` | Record a structured graph design plan and validate its internal consistency before writing any XML. | Read | Use AI Authoring MCP tools |
| `job_run` | Submit a graph or jobflow for asynchronous execution. Returns a run ID immediately. | Write | Use AI Authoring MCP tools |
| `job_abort` | Abort a running graph or jobflow execution. Also terminates any child jobs it spawned. | Write | Use AI Diagnostic MCP tools |

#### Graph Editing Tools

Tools for inspecting and modifying CloverDX graphs (`.grf`), jobflows (`.jbf`), and subgraphs (`.sgrf`) via the XML DOM, and for validating the CTL code that goes into them.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `graph_resolve_edge_schemas` | Resolve the record schema (field names, types, nullability) that would flow along each edge of a graph at runtime, including propagated schemas. | Read | Use AI Authoring MCP tools |
| `graph_list_elements` | List specific element types defined in a job file: metadata records, lookup tables, dictionaries, or sequences. | Read | Use AI Authoring MCP tools |
| `ctl_validate` | Validate standalone CTL2 code against explicit port metadata, without a job file. Reports compilation and metadata problems with their position in the code, and checks the entry functions the given component type requires. | Read | Use AI Authoring MCP tools |
| `graph_edit_properties` | Set or update attribute values, CTL transformation code, or metadata record definitions on existing graph elements. Supports bulk edits and dry-run preview. | Write | Use AI Authoring MCP tools |
| `graph_edit_structure` | Add, delete, or move whole structural elements in a job — nodes, edges, phases, metadata definitions, connections, and more. Supports dry-run preview. | Write | Use AI Authoring MCP tools |
| `graph_layout` | Re-arrange every component of a job file into a deterministic left-to-right layout. Job files are laid out automatically on every write, keeping the positions a human set; this tool re-arranges the whole file regardless. Supports dry-run preview. | Write | Use AI Authoring MCP tools |

#### Component Tools

Tools for discovering and understanding CloverDX component types.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `component_list` | Browse and search available CloverDX component types by name, category, or keyword. | Read | Use AI Authoring MCP tools |
| `component_get_info` | Get detailed configuration information for a component type: input/output ports, properties, required settings, and metadata propagation rules. | Read | Use AI Authoring MCP tools |
| `component_get_guide` | Fetch the in-depth reference guide for a component, including configuration examples, CTL mapping syntax, and known pitfalls. | Read | Use AI Authoring MCP tools |

#### Server Tools

Tools for inspecting CloverDX Server state, logs, and internal system database.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `server_deployment` | Get a snapshot of the running CloverDX Server environment — JVM, OS, memory, cluster topology, and configuration. Can also return the official support matrix. | Read | Use AI Diagnostic MCP tools |
| `server_logs_search` | Search server log entries by time range and regular expression pattern. Supports multiple log appenders: main server log, cluster, user actions, job queue, data services, and others. | Read | Use AI Diagnostic MCP tools |
| `server_perf_logs_query` | Execute SQL queries (Apache Calcite dialect) against the server performance log. Returns time-series CPU, memory, GC, and I/O metrics sampled every 3 seconds. | Read | Use AI Diagnostic MCP tools |
| `server_db_get_schema` | Retrieve the table and column schema of the CloverDX internal system database (execution history, users, sandboxes, schedules, and other server-managed records). | Read | Use AI Diagnostic MCP tools |
| `server_db_execute_query` | Execute a read-only SQL SELECT query against the CloverDX internal system database. | Read | Use AI Diagnostic MCP tools |

#### External Database Tools

Tools for interacting with external databases accessible via JDBC.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `db_get_schema` | Query schemas, tables, or columns of any database accessible via JDBC — using either a saved connection configuration file or inline connection properties. Supports all major databases (PostgreSQL, Oracle, MSSQL, MySQL, and others). | Read | Use AI Authoring MCP tools |
| `db_execute_query` | Execute SQL (SELECT, DML, or DDL) against any database accessible via JDBC. Results are returned as JSON or delimited text. | Write | Use AI Authoring MCP tools |

#### Knowledge Tools

Tools for accessing the knowledge space – the built-in CloverDX knowledge library, the customer’s own company entries and the project-scoped entries – and for managing the project-scoped ones.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `knowledge_list_resources` | List all static reference documents exposed as MCP resources by the installed CloverDX knowledge library, including graph XML reference, CTL language reference, and component guides. | Read | Use AI Authoring MCP tools |
| `knowledge_read_resource` | Fetch the content of a specific knowledge resource by its URI. | Read | Use AI Authoring MCP tools |
| `kb_search` | Search the whole knowledge space by keyword: the entries shipped in the CloverDX knowledge library (`platform/`), the customer’s own entries (`company/`) and the project entries (`project/`). Hits are filtered by the agent role the caller declares and each one carries the path to read it with. | Read | Use AI Authoring MCP tools |
| `kb_read` | Read the body of one knowledge entry by its `<subtree>/[<topic>/]<name>` path, e.g. `platform/guides/joiner-selection`. | Read | Use AI Authoring MCP tools |
| `kb_store` | Store or update a knowledge entry in the `project/` subtree, the only writable one. Used by AI agents to persist project-specific facts (business rules, conventions, validated findings) across sessions. Requires `sandboxCode` and `projectName`. | Write | Use AI Authoring MCP tools |
| `kb_delete` | Delete one entry from the `project/` subtree. Requires `sandboxCode` and `projectName`. | Write | Use AI Authoring MCP tools |
| `knowledge_context_get` | Return what one agent role sees of the knowledge space: the pinned rules addressed to that role and the index of entries visible to it. The assistant host calls it when it composes a system prompt; other clients can call it to preview a role’s view. | Read | Use AI Authoring MCP tools |

#### Agent Utility Tools

Tools used by AI agents to manage session state and workflow guidance.

| Tool | Description | Access | Permission |
| --- | --- | --- | --- |
| `note_read` | Read notes from the session-scoped working memory. | Read | Use AI Authoring MCP tools |
| `think` | Log explicit reasoning before taking an action. Helps AI agents plan component selection, graph edits, and error diagnostics. | Read | Use AI Authoring MCP tools |
| `task_workflow_get` | Get step-by-step procedural instructions for a CloverDX task type: creating a graph, editing a graph, creating a jobflow, or validating and running a job. | Read | Use AI Authoring MCP tools |
| `note_add` | Append a note to a named section in session-scoped working memory. Notes are lost when the MCP session ends. | Write | Use AI Authoring MCP tools |
| `note_clear` | Clear notes from session-scoped working memory — either a specific section or all sections. | Write | Use AI Authoring MCP tools |
| `report_support_issue` | Report a problem to the CloverDX Support Portal. Optionally attaches a diagnostic support package containing logs and configuration details. | Write | Use AI Diagnostic MCP tools |
