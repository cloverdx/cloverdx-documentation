<!-- Development > Component reference > AI Components > AIClient -->

### AIClient

![AIClient 64x64](../figures/AIClient-64x64.png)

| [Short description](aiclient.md#short-description) |
| --- |
| [Ports](aiclient.md#ports) |
| [Metadata](aiclient.md#metadata) |
| [AIClient attributes](aiclient.md#aiclient-attributes) |
| [Connection](aiclient.md#connection) |
| [CTL interface](aiclient.md#ctl-interface) |
| [Compatibility](aiclient.md#compatibility) |
| [See also](aiclient.md#see-also) |
> [!NOTE]
> This component is currently in the **incubation phase**. Although it is available for use, it is under active development and may be subject to changes. We welcome feedback and encourage users to explore its capabilities.

#### Short description

The **AIClient** component lets you compose and send queries to various online language models and processes the responses.

You can define control logic which either refines your query based on assistant’s response, or moves to the next record. This is great in situations when you’re not happy with assistant’s response and want to continue “chatting about the same input record”, until you’re satisfied with the results.

**Warning** Make sure the queries you generate and send to the assistant only contain data you are willing to share with their service. Make sure you conform to your data security, privacy and governance standards.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 1 | **⨯** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 1 | **✓** | Input prompts for the assistant | Any |
| Output | 1 | **✓** | Generated responses | At least one `string` or `variant` field |

#### Metadata

**AIClient** propagates input metadata to output.

#### AIClient attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| **Basic** |  |  |  |
| Connection | yes | Configuration of the AI provider, usually set via API key, model name, and temperature. See [Connection](aiclient.md#connection). |  |
| System message URL | no | An URL or relative path to a .txt file containing a system message. Used to load longer system prompts from external files. |  |
| System message | no | A instruction message that is sent to the GPT model as context. Can help shape the tone or style of the response. |  |
| Query and response processor | yes | CTL transformation script to fully control the GPT interaction workflow (input → query → response → output). See [CTL interface](aiclient.md#ctl-interface). |  |
| Output field | yes | The name of the field in the output record where the GPT response will be stored. |  |
| **Error handling** |  |  |  |
| Request timeout |  | How long the component waits to get a response. If it does not receive a response within a specified limit, the execution of the component fails. The AIClient has one minute request timeout by default.  Request timeout is in milliseconds. Different time units can be used. See [Time intervals](components.md#time-intervals). | 1 minute (default) |
| Retry count |  | How many times should the component retry a request in the case of a failure. The retry count specifies the number of times the component will attempt to re-send a failed request. A failure is considered to occur when the component encounters an error processing the request or response.  If **Query and response processor** specifies the `sendRequestOnError` function, this function is called only after all retries have failed, using the last exception. | 0 (default) |
| Retry delay |  | Specifies the time intervals between retry attempts. It is a comma-separated list of integers, where each integer represents the delay time in seconds for the corresponding retry. For example, a delay of `2, 5, 10` means the component will wait 2 seconds for the first retry, 5 seconds for the second, and 10 seconds for subsequent retries. If the number of retries exceeds the number of specified delays, the last delay in the list will be used for all subsequent retries. | 0 (default) |
| Rate limit: time interval |  | Limits the number of allowed requests defined by the **Rate limit: max results** property per time period (*seconds, minutes, hours, days*). When a limit is set and reached, the component waits until the defined time interval passes to continue sending requests. | 1s (default), 1m, 1h, 1d |
| Rate limit: max requests |  | Limits the total number of requests per time period defined by the **Rate limit: time interval** property. By default, the number of requests is unlimited. When a limit is set and reached, the component waits until the defined time interval passes to continue sending requests. |  |

#### Connection

**Connection** represents provider-specific configuration of connection to assistant:

- **Anthropic** ([https://www.anthropic.com/](https://www.anthropic.com/)) connects to Claude models such as Opus or Sonnet, focusing on AI safety and alignment.
- **Google AI** ([https://gemini.google.com/](https://gemini.google.com/)) connects to Gemini models provided by Google AI.
- **Microsoft Foundry (Azure OpenAI)** ([https://azure.microsoft.com/en-us/products/ai-foundry/models/openai](https://azure.microsoft.com/en-us/products/ai-foundry/models/openai)) provides OpenAI models via Microsoft Azure AI Foundry with enterprise security and compliance features.
- **Microsoft Foundry via Azure AI Gateway** ([https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities)) connects to Microsoft Foundry models via API endpoints provided by Azure API Management.
- **OpenAI** ([https://openai.com/api/](https://openai.com/api/)) connects to GPT models provided by OpenAI or to any OpenAI-compatible tools such as Ollama, vLLM and others. The **base URL** attribute defines the base URL for API requests and defaults to `https://api.openai.com/v1`.
- **OpenAI-compatible via Azure AI Gateway** ([https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities](https://learn.microsoft.com/en-us/azure/api-management/genai-gateway-capabilities)) uses Azure-hosted endpoints to connect to OpenAI-compatible APIs hosted by non-Microsoft providers.

The following attributes are shared across multiple providers:

The **model name** is represented by a combo box. When you open the connection dialog, available models are fetched dynamically from the provider; you can also type any model name manually.

The **temperature** controls the creativity or randomness of the model’s output. Lower values make the output more deterministic, higher values more random. The lowest possible value is 0.0; the upper bound is model-dependent, usually 1.0 or 2.0. Some models might not support temperature at all.

The **API key header name** is the name of the HTTP header used to pass your API / Subscription key to Azure AI Gateway (e.g. `Ocp-Apim-Subscription-Key`). Defaults to `api-key` if not set.

The **API version** is the Azure REST API version to use in requests to the Azure AI Gateway. Defaults to `2025-03-01-preview` if not set.

#### CTL interface

**AIClient** requires a CTL transformation (named *Query and response processor*).

Its function `newChat()` is called once for each input record. Consequently, the functions `prepareQuery()` and `processResponse()` are called repeatedly for each input record until assistant response is either accepted or skipped, or the processing is stopped.

Most of the functions use the `ChatMessage` data type which is **globally available**, so that the transformation can be externalized. Besides `role` and `content`, the type contains four additional fields that are only relevant for assistant messages:

- `cachedInputTokenCount`: number of cached input tokens used
- `totalInputTokenCount`: total number of input tokens, including the cached ones
- `totalOutputTokenCount`: total number of output tokens
- `totalTokenCount`: total number of tokens, both input and output

If not available for particular provider or model, these statistics may be *null*. Namely, `cachedInputTokenCount` is only available for Anthropic and OpenAI. For Azure AI Gateway providers, it may also be available if the gateway exposes the information.

##### CTL template

| CTL Template Functions |  |
| --- | --- |
| **boolean newChat()** |  |
| Required | Yes |
| Description | Prepares the component for a new input record. The return value signifies whether the chat history (messages for previous input records) shall be preserved or reset; reset clears the history but keeps the component-level system message. |
| Invocation | Called once for each input record. |
| Returns | `true` – reset the chat context \| `false` – preserve it |
| **boolean newChatOnError(string errorMessage, string stackTrace)** |  |
| Required | No |
| Description | An optional fallback function to handle possible errors in `newChat()`. The purpose is otherwise identical to the base function. |
| Invocation | Called if `newChat()` throws an exception. |
| Input Parameters | `string errorMessage` – message of the thrown exception |
| `string stackTrace` – stack trace of the thrown exception |  |
| Returns | `true` – reset the chat context \| `false` – preserve it |
| Example | ```ctl function integer newChatOnError(string errorMessage, string stackTrace) {     printErr("Resetting chat because newChat failed: " + errorMessage);     return true; } ``` |
| **string prepareQuery(list[ChatMessage] chatContext, integer iterationIndex)** |  |
| Required | Yes |
| Description | Prepare a new query. The returned string will be added to the chat context as user message; if `null` is returned, the method shall modify the context on its own. |
| Invocation | Called repeatedly for each input record, after `newChat()` and before `processResponse()`. |
| Input Parameters | `list[ChatMessage] chatContext` – modifiable chat context, a list of previous messages |
| `integer iterationIndex` – number of calls of this method for the current input record (0 for the first call) |  |
| Returns | `string` – a new user message, or `null` if none shall be added |
| Example | ```ctl function string prepareQuery(         list[ChatMessage] chatContext,         integer iterationIndex) {     if (iterationIndex == 0) {         return $in.0.message;     } else {         return "Try it once more.";     } } ``` |
| **boolean prepareQueryOnError(string errorMessage, string stackTrace, list[ChatMessage] chatContext, integer iterationIndex)** |  |
| Required | No |
| Description | An optional fallback function to handle possible errors in `prepareQuery()`. The purpose is otherwise identical to the base function. |
| Invocation | Called if `prepareQuery()` throws an exception. |
| Input Parameters | `string errorMessage` – message of the thrown exception |
| `string stackTrace` – stack trace of the thrown exception |  |
| `list[ChatMessage] chatContext` – modifiable chat context, a list of previous messages |  |
| `integer iterationIndex` – number of calls of `prepareQuery()` for the current input record (0 for the first call) |  |
| Returns | `string` – a new user message, or `null` if none shall be added |
| Example | ```ctl function integer prepareQueryOnError(         string errorMessage,         string stackTrace,         list[ChatMessage] chatContext,         integer iterationIndex) {     printErr("Using unmodified prompt because prepareQuery failed: " + errorMessage);     return $in.0.prompt; } ``` |
| **boolean sendRequestOnError(string errorMessage, string stackTrace, list[ChatMessage] chatContext, integer iterationIndex)** |  |
| Required | No |
| Description | An optional function to handle possible errors in communication with the assistant. |
| Invocation | Called if an exception is thrown during communication with the assistant.  If the **Retry count** attribute is specified, this function is called only after all retries have failed, using the last exception. |
| Input Parameters | `string errorMessage` – message of the thrown exception |
| `string stackTrace` – stack trace of the thrown exception |  |
| `list[ChatMessage] chatContext` – modifiable chat context, a list of previous messages |  |
| `integer iterationIndex` – number of calls of `prepareQuery()` for the current input record (0 for the first call) |  |
| Returns | `integer` – a code indicating whether an output record shall be generated, see `processResponse()` |
| Example | ```ctl function integer sendRequestOnError(         string errorMessage,         string stackTrace,         list[ChatMessage] chatContext,         integer iterationIndex) {     if (iterationIndex < 3) {         printErr("Retrying because communication with assistant failed: " + errorMessage);         return CONTINUE;     } else {         $out.0.prompt = $in.0.prompt;         $out.0.error = "Failed to send request: " + errorMessage;         return OK;     } } ``` |
| **integer processResponse(list[ChatMessage] chatContext, integer iterationIndex, string assistantResponse)** |  |
| Required | Yes |
| Description | Process assistant response: write it to output, repeat a query with additional instructions, or ignore it. |
| Invocation | Called repeatedly for each input record when assistant response is received, as long as it returns `CONTINUE`. |
| Input Parameters | `list[ChatMessage] chatContext` – modifiable chat context, including the current assistant response (at the last position) |
| `integer iterationIndex` – number of calls of this method for the current input record (0 for the first call) |  |
| `string assistantResponse` – the current assistant response, just for convenience |  |
| Returns | `integer` – a code indicating whether an output record shall be generated:  - `OK` – An output record is generated and next input record is processed. - `CONTINUE` – No output is generated, `prepareQuery()` is called again with incremented iteration index. - `SKIP` – The response is ignored and next input record is processed. - `STOP` – Processing (of all records) is stopped, an exception is thrown. |
| Example | ```ctl function integer processResponse(         list[ChatMessage] chatContext,         integer iterationIndex,         string assistantResponse) {     try {         $out.0.response = parseJson(assistantResponse);         return OK;     } catch (CTLException e) {         if (iterationIndex < 3) {             ChatMessage message;             message.role = "USER";             message.content = "Answer with a valid JSON.";             push(chatContext, message);             return CONTINUE;         } else {             return SKIP;         }     } } ``` |
| **boolean processResponseOnError(string errorMessage, string stackTrace, list[ChatMessage] chatContext, integer iterationIndex)** |  |
| Required | No |
| Description | An optional fallback function to handle possible errors in `processResponse()`. The purpose is otherwise identical to the base function. |
| Invocation | Called if `processResponse()` throws an exception. |
| Input Parameters | `string errorMessage` – message of the thrown exception |
| `string stackTrace` – stack trace of the thrown exception |  |
| `list[ChatMessage] chatContext` – modifiable chat context, including the current assistant response (at the last position) |  |
| `integer iterationIndex` – number of calls of this method for the current input record (0 for the first call) |  |
| Returns | `integer` – a code indicating whether an output record shall be generated, see `processResponse()` |
| Example | ```ctl function integer processResponseOnError(         string errorMessage,         string stackTrace,         list[ChatMessage] chatContext,         integer iterationIndex) {     if (iterationIndex < 3) {         printErr("Retrying because processing of assistant response failed: " + errorMessage);         ChatMessage message;         message.role = "USER";         message.content = "Reply again, I cannot use your response: " + errorMessage;         push(chatContext, message);         return CONTINUE;     } else {         $out.0.prompt = $in.0.prompt;         $out.0.error = "Failed to process assistant response: " + errorMessage;         return OK;     } } ``` |

#### Compatibility

| Version | Compatibility notice |
| --- | --- |
| 7.1.0 | *AIClient* was introduced in CloverDX version 7.1 as *OpenAIClient* – it only supported OpenAI. |
| 7.3.0 | The component was renamed to *AIClient* and gained support for additional providers: Anthropic (Claude models), Azure OpenAI, and Google Gemini. |
| 7.5.0 | The component gained support for 2 additional providers: Microsoft Foundry via Azure AI Gateway and OpenAI-compatible via Azure AI Gateway. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
