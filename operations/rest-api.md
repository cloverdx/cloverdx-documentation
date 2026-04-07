<!-- Automation and operations > Server management APIs > REST API -->

## 11. REST API

### Overview

The CloverDX REST API enables you to interact with CloverDX Server programmatically. You can use it to script interactions or develop various kinds of integrations with the Server. The API provides access to CloverDX Server resources by using a predefined set of stateless operations realized via HTTP calls. Requests to resource URIs, and also the received responses, use a payload formatted in JSON. The REST API uses the [standard HTTP status codes](https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes).

The Server also provides a generated REST API documentation available at:

```
http://[domain]:[port]/clover/api/rest/[api-version]/docs.html
```

for example:

```
http://example.com:8080/clover/api/rest/v1/docs.html
```

You can access this page through the **Server API** link on the Server Console login page. It serves as the primary resource for using the API, providing comprehensive details on all available resources, their operations (including URI paths and HTTP methods), parameters, and examples of both requests and responses. This interactive page also allows you to test API requests and view the corresponding responses directly.
> [!NOTE]
> Most of the examples use the sandbox `DWHExample` and resources from it. It can be deployed while completing the Server Console tutorial. Examples for libraries use some libraries from our [CloverDX Marketplace](https://marketplace.cloverdx.com/). Also note that most of the resources are identified by numerical IDs, which may be different in your use case.

#### Version and URI

This documentation is for version 1 of the REST API, which is the latest version. The URIs for resources have the following structure:

```
http://[domain]:[port]/clover/api/rest/v1/[resource-path]
```

For example:

```
http://example.com:8080/clover/api/rest/v1/dashboards/1/monitors
```

#### Authentication and authorization

Requests to the API must be authenticated, the API uses basic HTTP authentication. Regarding authorization, the user used to authenticate the request needs to have the required permissions to read or modify the specific resource.

All operations on monitors require the existing permission `Monitoring section`.

#### CSRF protection

The REST API provides protection against Cross-Site Request Forgery (CSRF) attacks. The mechanism basically requires the presence of a `X-Requested-By` header in every request to the API, same as described in chapter Simple HTTP API, in [CSRF Protection](simple-http-api.md#csrf-protection) and is also controlled globally by the same configuration property [`security.csrf.protection.enabled`](../admin/list-of-properties.md#lop-security-csrf-protection-enabled).

To put all the information together, an example API request to create a new monitor resource can look like:

```bash
curl -X POST "http://example.com:8080/clover/api/rest/v1/dashboards/1/monitors" -H "Accept: application/json" -H "Content-Type: application/json" -H "X-Requested-By: arbitrary_value" -u username:password -d "@request.json"
```

where `username:password` are the user’s credentials and `request.json` is a file containing the request body.
