<!-- Automation and operations > Server management APIs > SOAP WebService API -->

## 12. SOAP WebService API

The **CloverDX Server** SOAP Web Service is an advanced API that provides an automation alternative to the Simple HTTP API. While most of the HTTP API operations are available in the SOAP interface too, the SOAP API provides additional operations for manipulating sandboxes, monitoring, etc.

The SOAP API service is accessible on URL:

```
http://[host]:[port]/clover/webservice
```

The SOAP API service descriptor is accessible on URL:

```
http://[host]:[port]/clover/webservice?wsdl
```

Protocol HTTP can be changed to secured HTTPS based on the web server configuration.

### SOAP WS Client

Exposed service is implemented with the most common binding style "document/literal", which is widely supported by libraries in various programming languages.

To create a client for this API, only WSDL document (see the URL above) is needed together with some development tools according to your programming language and development environments.

JavaDoc of the WebService interface with all related classes is accessible in a running **CloverDX Server** instance on URL `http://[host]:[port]/[contextPath]/javadoc-ws/index.html`

If the web server has an HTTPS connector configured, the client must also meet the security requirements according to web server configuration, i.e. client trust + key stores configured properly.

### SOAP WS API Authentication/Authorization

Since exposed service is stateless, an authentication "sessionToken" has to be passed as a parameter to each operation. The client can obtain the authentication sessionToken by calling the `login` operation.
