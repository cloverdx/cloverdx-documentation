<!-- Development > Assistant company knowledge -->

## 3. Assistant company knowledge

Company knowledge is your own set of rules and reference material for the [CloverDX AI Assistant](designer-ai-assistant.md): naming conventions, connection standards, which sources a job may read – everything the Assistant has to respect and CloverDX cannot ship with the product. Each entry is a Markdown file in a CloverDX Server sandbox. An entry marked as pinned is copied into the agent’s prompt in full, so the rule holds without anyone repeating it in the chat.

Company knowledge is off until an administrator points the Server at a sandbox. See [Company knowledge store](../admin/server-config-mcp.md#company-knowledge-store) for that part of the setup.

### Where the entries live

The store is one folder in a sandbox and one Markdown file per entry:

```ctl
<company sandbox>/
    knowledge_company/
        connection-standards.md
        naming/
            graph-naming.md
            metadata-naming.md
```

- The name of an entry is its `name` frontmatter value, or the file name without the `.md` suffix.
- A subfolder is the topic of the entries in it. Only one level of subfolders is read; files directly in the store folder have no topic.
- Files that do not end in `.md` are ignored.
- Agents address an entry as `company/<topic>/<name>`, or `company/<name>` when it has no topic. The example above holds `company/connection-standards` and `company/naming/graph-naming`.
- Names are unique across the whole store, regardless of topic and letter case. When two files claim one name, the entry loaded first wins – store root before topics, topics in name order – and the Server log names the ignored file.

The Assistant never writes into this store. What the agents themselves learn goes into the project knowledge of the assistant project instead, which the Librarian curates.

### Writing an entry

An entry is YAML frontmatter followed by the text the agent reads:

```ctl
---
name: acme-graph-naming
description: Mandatory graph file naming convention - every graph file name starts with ACME_.
tags: [naming, convention, graph]
applies_to: [developer]
pinned: true
---
Every graph file (`.grf`) created for this company is named `ACME_<PascalCaseDescription>.grf`
- for example `ACME_CustomerExport.grf`, never `customer_export.grf`. The prefix is uppercase
`ACME_`, verbatim. This applies to every new graph, including small examples.
```

| Key | Description | Default |
| --- | --- | --- |
| `name` | Name the entry is addressed by. Keep it stable: a project override and a search result both refer to it. | the file name without `.md` |
| `description` | One line saying what the entry is for. Every agent sees this line in its knowledge index, so it decides whether the entry is ever opened. | (none) |
| `tags` | Keywords the knowledge search matches on, besides the name, the description and the body. | (none) |
| `applies_to` | Agent roles the entry is addressed to. See [Addressing an entry to an agent role](assistant-company-knowledge.md#addressing-an-entry-to-an-agent-role). | every role |
| `pinned` | `true` puts the whole body into the system prompt of every agent the entry applies to, before it starts working. Leave it out on a long entry the agent should read only when the task calls for it. | `false` |
| `disabled` | Meaningful in a project override only. See [Overriding an entry in one project](assistant-company-knowledge.md#overriding-an-entry-in-one-project). | `false` |

Each value is one line. A list is written inline, as `tags: [naming, convention]` or `tags: naming, convention`, and quoted items are accepted. A list broken over several lines is not read.

### How an entry reaches an agent

Every entry reaches the agents as one `path - description` line in their knowledge index. An agent reads the body with the `kb_read` tool when the description looks relevant to the task, and finds entries by keyword with `kb_search`.

An entry with `pinned: true` does not wait to be looked up. Its whole body goes into the system prompt of every agent the entry is addressed to, before that agent starts working, together with the instruction to apply it without being asked.

The flag decides **when** an entry arrives, not how seriously it is taken. Everything in the store is knowledge the Assistant follows once it has it; a rule left without the flag is followed when the agent reads it, which happens when the task points at it. So pin a rule when it is short and has to hold every time – a naming convention, a forbidden source. Leave the flag out on anything long: a page of reference material in every prompt costs tokens on every single call, and the agent fetches it by itself when the work needs it.
> [!CAUTION]
> A rule that must hold every time and is left without the flag is obeyed only in the turns where the agent happens to read it. Length is the reason to leave the flag out; "this is only advice" is not, because nothing tells the agent to treat an entry as advice.

Both blocks are capped at 16 KB each: the pinned rules and the index. Entries beyond the cap are left out, the block ends with a visible `ERROR:` line naming the first ten of them, and the Server log records the full list. Nothing is dropped quietly, but a store that grows past the cap stops delivering some of its rules.
> [!NOTE]
> MCP clients other than the Assistant compose their own prompts and get no such blocks. They can read the same two pieces as MCP resources: `cloverdx://knowledge/rules` for the full text of every pinned entry, and `cloverdx://knowledge/index` for the index. Both serve the platform entries and the global company entries unfiltered, because a resource URI names no role and no project. A client that passes `role`, `sandboxCode` and `projectName` in the `_meta` of its read request gets what that role sees in that project instead.

### Addressing an entry to an agent role

`applies_to` limits an entry to the [agent types](designer-ai-assistant.md#agent-types) that need it. The roles are written as codes: `master`, `architect`, `developer`, `data-inspector`, `ctl-author`, `troubleshooter` and `librarian`. A graph naming rule belongs to `developer`, a diagnostic convention to `troubleshooter`. An entry without `applies_to` applies to every role.
> [!CAUTION]
> A value that is not one of these seven codes makes the entry apply to **every** role, and the Server logs a warning naming the entry and the unknown value. A typo therefore widens a rule instead of narrowing it.

The Librarian is the exception: it searches and reads the whole knowledge space whatever `applies_to` says, so it can answer questions about entries the other agents do not see. Pinned rules reach the Librarian’s own prompt under the same rule as every other role: when they name `librarian`, or when they name no role at all.

### Overriding an entry in one project

A single project can replace a company entry or switch it off, without touching the global store. Put the file in the `assistant/<assistant project>/knowledge_company/` folder of the project’s own sandbox, next to the other files of the [assistant project](designer-ai-assistant.md#assistant-projects-and-sessions):

- An entry whose `name` matches a global entry replaces it in that project.
- An entry with `disabled: true` switches the global entry of that name off in that project. When no global entry carries the name, the Server logs a warning – usually a mistyped `name`.
- An entry with a name no global entry uses is a company entry of that project alone.

Overrides are read with the permissions of the user running the Assistant, and they are not cached, so an edit applies to the next agent turn.

### When a change takes effect

The global store is cached for 60 seconds by default, so a new or edited entry reaches the agents within a minute. An administrator can change the interval, or set it to `0` to reload the store on every call, which is what you want while you are writing the rules – see [Company knowledge store](../admin/server-config-mcp.md#company-knowledge-store).

Adding, editing and deleting entries needs no Server restart. Moving the store to another sandbox or another folder does, because that is a Server configuration property.

### See also

| [CloverDX AI Assistant](designer-ai-assistant.md) |
| --- |
| [Assistant’s knowledge base - CloverDXMCPKnowledge](designer-ai-assistant.md#assistants-knowledge-base-cloverdxmcpknowledge) |
| [Company knowledge store](../admin/server-config-mcp.md#company-knowledge-store) |
| [Knowledge Tools](../operations/server-mcp-api.md#knowledge-tools) |
