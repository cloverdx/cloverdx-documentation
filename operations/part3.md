<!-- Automation and operations > Server APIs -->

# Server APIs

To effectively manage and interact with CloverDX Server, various types of APIs are available, each catering to different needs and preferences. These APIs provide flexible and robust mechanisms for performing various server operations or automating tasks. The Server provides multiple different APIs each serving different use-cases:
**REST API**
REST API is a modern management API for CloverDX Server. It offers large number of endpoints that allow you to query Server information (status, running jobs, tracking data, configuration, …​) as well as modify Server settings (import configuration, create schedules, listeners, and more).
**Data Manager API**
Data Manager API is a REST API providing access to various Data Manager functionality. You can use this API to query your data sets, their audit or even to create data sets or modify data set configuration.
**SOAP API**
SOAP API is an API that allows you detailed control of CloverDX Server. It offers wider range of methods than the REST API, however, it is intented more for internal communication between Designer and Server rather than as a generic public API. This means that its backwards compatibility is not maintained as strictly as for REST API.
**MCP (Model Context Protocol) API**
MCP API is intended for usage with MCP-compatible AI clients such as Claude, ChatGPT or others. It provides access to dozens of tools that agentic solutions can use to interact with CloverDX Server.
**Simple HTTP API - DEPRECATED**
Simple HTTP API is the original version of management API for CloverDX Server. It has been deprecated and disabled since CloverDX 6.4 (released in March 2024). Do not use this API - use REST API instead. New REST API is more consistent and more powerful providing more functionality than the old HTTP API.
