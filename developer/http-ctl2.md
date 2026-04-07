<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Data Service HTTP Library functions -->

### Data Service HTTP Library functions

#### List of functions

| [addResponseHeader](http-ctl2.html#id_ctl2_addresponseheader) |
| --- |
| [containsResponseHeader](http-ctl2.html#id_ctl2_containsresponseheader) |
| [getRequestBody](http-ctl2.html#id_ctl2_getrequestbody) |
| [getRequestClientIPAddress](http-ctl2.html#id_ctl2_getrequestclientipaddress) |
| [getRequestContentType](http-ctl2.html#id_ctl2_getrequestcontenttype) |
| [getRequestEncoding](http-ctl2.html#id_ctl2_getrequestencoding) |
| [getRequestHeader](http-ctl2.html#id_ctl2_getrequestheader) |
| [getRequestHeaderNames](http-ctl2.html#id_ctl2_getrequestheadernames) |
| [getRequestHeaders](http-ctl2.html#id_ctl2_getrequestheaders) |
| [getRequestMethod](http-ctl2.html#id_ctl2_getrequestmethod) |
| [getRequestParameter](http-ctl2.html#id_ctl2_getrequestparameter) |
| [getRequestParameterNames](http-ctl2.html#id_ctl2_getrequestparameternames) |
| [getRequestParameters](http-ctl2.html#id_ctl2_getrequestparameters) |
| [getRequestPartFilename](http-ctl2.html#id_ctl2_getrequestpartfilename) |
| [getResponseContentType](http-ctl2.html#id_ctl2_getresponsecontenttype) |
| [getResponseEncoding](http-ctl2.html#id_ctl2_getresponseencoding) |
| [setRequestEncoding](http-ctl2.html#id_ctl2_setrequestencoding) |
| [setResponseBody](http-ctl2.html#id_ctl2_setresponsebody) |
| [setResponseContentType](http-ctl2.html#id_ctl2_setresponsecontenttype) |
| [setResponseEncoding](http-ctl2.html#id_ctl2_setresponseencoding) |
| [setResponseHeader](http-ctl2.html#id_ctl2_setresponseheader) |
| [setResponseStatus](http-ctl2.html#id_ctl2_setresponsestatus) |

Functions from Data Service HTTP Library are available in context of [Data API](data-service.md) jobs.

#### addResponseHeader

```ctl
void addResponseHeader(string name, string value);
```

The `addResponseHeader` function adds an HTTP response header field. If the fuction is called multiple times, multiple headers will be added.

The `name` parameter is a header field name. See [list of header field names](https://www.iana.org/assignments/message-headers/message-headers.xml).

If `name` is `null` or empty string, the response header field is not added.

The `value` parameter is a value of the header field. If `value` is empty string, empty string is used. If `value` is `null` the header field is not added.

**Compatibility**

The `addResponseHeader(string,string)` function is available since **CloverETL 4.7.0-M1**.
Example 339. Usage of addResponseHeader
The `addResponseHeader("Content-Language", "fr")` adds an HTTP header field `Content-Language` with value `fr`

```ctl
Content-Language: fr
```

The `addResponseHeader("foo", "")` adds header field with empty value

```ctl
foo:
```

The `addResponseHeder("foo", null)` does not add an HTTP header field because of `null`.

**See also:**[containsResponseHeader](http-ctl2.html#id_ctl2_containsresponseheader)

#### containsResponseHeader

```ctl
boolean containsResponseHeader(string headerField);
```

The `containsResponseHeader()` function checks for presence of a user-added header field. It does not check existence of header fields not added by user, e.g. `Server: Apache-Coyote/1.1`. The check is case insensitive.

The `headerField` parameter is a name of HTTP header field.

**Compatibility**

The `containsResponseHeader(string)` function is available since **CloverETL 4.7.0-M1**.
Example 340. Usage of containsResponseHeader
There is no `Content-Language` header. The `containsResponseHeader("Content-Language")` returns `false`.

 

If the header was added by `setResponseHeader()` function. The function `containsResponseHeader()` returns `true`.

```ctl
setResponseHeader("Content-Language", "fr");
boolean a = containsResponseHeader("Content-Language"); // true
```

 

The `containsResponseHeader("Server")` returns `false`. The header was not added by user.

**See also:**[addResponseHeader](http-ctl2.html#id_ctl2_addresponseheader)

#### getRequestBody

```ctl
string getRequestBody();
```

The `getRequestBody()` function returns the request body.

**Compatibility**

The `getRequestBody()` function is available since **CloverETL 4.7.0-M1**.
Example 341. Usage of getRequestBody
If you query the data service with

```ctl
wget \
    --user=userName \
    --password=password \
    --method=POST \
    --body-data="Once upon a time" \
    "http://${HOST_PORT}/clover/data-service/getRequestBody"
```

the `getRequestBody()` returns *Once upon a time*.

**See also:**[getRequestEncoding](http-ctl2.html#id_ctl2_getrequestencoding)

#### getRequestClientIPAddress

```ctl
string getRequestClientIPAddress();
```

The `getRequestClientIPAddress()` function returns the IP address of client performing the request.
Compatibility
The `getRequestClientIPAddress()` function is available since **CloverETL 4.7.0-M1**.
Example 342. Usage of getRequestClientIPAddress If you run the CloverDX Server locally, the `getRequestClientIPAddress()` returns IP address corresponding to localhost: `"127.0.0.1"` or `"0:0:0:0:0:0:0:1"`.
**See also:**[getRequestBody](http-ctl2.html#id_ctl2_getrequestbody)

#### getRequestContentType

```ctl
string getRequestContentType();
```

The `getRequestContentType()` function returns the content type.

**Compatibility**

The `getRequestContentType()` function is available since **CloverETL 4.7.0-M1**.
Example 343. Usage of getRequestContentType
If you query the data service API with

```ctl
wget \
    --user=... \
    --password=... \
    --method=POST \
    --body-data="Once upon a time" \
    "http://${HOST_PORT}/clover/data-service/getRequestContentType"
```

the `getRequestContentType()` returns `application/x-www-form-urlencoded`.

**See also:**[getResponseContentType](http-ctl2.html#id_ctl2_getresponsecontenttype)

#### getRequestEncoding

```ctl
string getRequestEncoding();
```

The `getRequestEncoding()` function encoding specified in *Content-Type* header.

If the header does not exist, the function returns `null`.

**Compatibility**

The `getRequestEncoding()` function is available since **CloverETL 4.7.0-M1**.
Example 344. Usage of getRequestEncoding
If you query the data with

```ctl
wget \
    --user=... \
    --password=... \
    --header="Content-Type: text/html; charset=UTF-8" \
    "http://${HOST_PORT}/clover/data-service/getRequestEncoding"
```

the `getRequestEncoding()` function returns `UTF-8`.

**See also:**[setRequestEncoding](http-ctl2.html#id_ctl2_setrequestencoding)

#### getRequestHeader

```ctl
string getRequestHeader(string headerField);
```

The `getRequestHeader()` function returns value of the header field.

The `headerField` parameter is HTTP header field name.

If the header field does not exist, the function returns `null`.

**Compatibility**

The function `getRequestHeader(string)` is available since **CloverETL 4.7.0-M1**.
Example 345. Usage of getRequestHeader
If you query the service with

```ctl
wget \
    --user=... \
    --password=... \
    --header="Accept-Language: de" \
    "http://${HOST_PORT}/clover/data-service/getRequestHeader"
```

the `getRequestHeader("Accept-Language")` returns `de`.

**See also:**[getRequestHeaderNames](http-ctl2.html#id_ctl2_getrequestheadernames)

#### getRequestHeaderNames

```ctl
string[] getRequestHeaderNames();
```

The `getRequestHeaderNames()` function returns names of request header fields.

**Compatibility**

The function `getRequestHeaderNames()` was introduced in **CloverETL 4.7.0-M1**.
Example 346. Usage of getRequestHeaderNames
If the data service receives

```
GET /clover/data-service/getRequestHeaderNames HTTP/1.1
User-Agent: Wget/1.19.1 (cygwin)
Accept: */*
Accept-Encoding: identity
Host: 172.22.2.71:33754
Connection: Keep-Alive
Accept-Language: es
Authorization: Basic Y2xvdmVyOmNsb3Zlcg==
Cookie: JSESSIONID=AE6A63EA112A0BADD046CDE0D068DCC1
```

The `getRequestHeaderNames()` function returns `user-agent,accept,accept-encoding,host,connection,accept-language,authorization,cookie` (as a list of strings).

**See also:**[getRequestHeader](http-ctl2.html#id_ctl2_getrequestheader), [getRequestHeaders](http-ctl2.html#id_ctl2_getrequestheaders)

#### getRequestHeaders

```ctl
map[string,string] getRequestHeaders();
string[] getRequestHeaders(string param);
```

The `getRequestHeaders()` function returns a map with request headers. The header name is a key, header field value is value.

The `param` parameter is *header field name*.

**Compatibility**

The function `getRequestHeaders()` is available since **CloverETL 4.7.0-M1**.
Example 347. Usage of getRequestHeaders
If you query the data service with>

```ctl
curl.exe \
    --user clover:clover \
    --header "Accept-Language: de, en, es, fr" \
    --header "Accept: text/plain" \
    --header "Accept: text/html" \
    --header "Accept: application/xml" \
    --header "Accept: application/json" \
    http://${HOST_PORT}/clover/data-service/getRequestHeaders
```

the `getRequestHeaders()` function returns *map* with key-value pairs: `User-Agent=curl/7.54.1;Accept=application/json;Accept-Language=de, en, es, fr;…`. As the function does not return a multimap, the *Accept* header field contains only one of the received header fields values. To get all received header field values, use the `getRequestHeaders(string)` function.

The `getRequestHeaders("Accept")` function returns list of strings: `text/plain;text/html;application/xml;application/json`.

**See also:**[getRequestHeader](http-ctl2.html#id_ctl2_getrequestheader), [getRequestHeaderNames](http-ctl2.html#id_ctl2_getrequestheadernames)

#### getRequestMethod

```ctl
string getRequestMethod();
```

The `getRequestMethod()` function returns the HTTP method: GET, POST, PUT, PATCH or DELETE.

**Compatibility**

The function `getRequestMethod()` was introduced in **CloverETL 4.7.0-M1**.
Example 348. Usage of getRequestMethod
If you query the data service with:

```ctl
wget \
    --user=clover \
    --password=clover \
    --method=GET \
    "http://${HOST_PORT}/clover/data-service/getRequestMethod"
```

the `getRequestMethod()` returns `GET`.

#### getRequestParameter

```ctl
string getRequestParameter(string param);
```

The `getRequestParameter()` function returns value of GET or POST parameter.

The `param` parameter is the parameter name.

**Compatibility**

The function `getRequestParameters()` was introduced in **CloverETL 4.7.0-M1**.
Example 349. Usage of getRequestParameter
If you query the data service with:

```ctl
wget \
    --user=clover \
    --password=clover \
    "http://${HOST_PORT}/clover/data-service/getRequestParameter?id=1234&"
```

the `getRequestParameter("id")` returns `1234` (as string).

If you query data service on `.../getRequestParameter/id/{id}` URL with

```ctl
wget \
    --user=clover \
    --password=clover \
    "http://${HOST_PORT}/clover/data-service/getRequestParameter/id/123"
```

the `getRequestParameter("id")` returns `123` (as string). Note parameters in the URL in data service configuration.

If you query data service with

```ctl
wget \
    --user=clover \
    --password=clover \
    --post-data "id=234&" \
    "http://${HOST_PORT}/clover/data-service/getRequestParameter"
```

the `getRequestParameter("id")` returns `234` (as string).

**See also:**[getRequestParameters](http-ctl2.html#id_ctl2_getrequestparameters), [getRequestParameterNames](http-ctl2.html#id_ctl2_getrequestparameternames)

#### getRequestParameterNames

```ctl
string[] getRequestParameterNames();
```

The `getRequestParameterNames()` function returns names of GET or POST parameters., e.g. `http://example.com/?id=123&`

**Compatibility**

The function `getRequestParameternames()` was introduced in **CloverETL 4.7.0-M1**.
Example 350. Usage of getRequestParameterNames
If you query the data service with:

```ctl
wget \
    --user=clover \
    --password=clover \
    "http://${HOST_PORT}/clover/data-service/getRequestParameterNames?id=123&name=doe&"
```

the `getRequestParameterNames()` returns list containing `id` and `name`.

If you query data service on `/getRequestParameterNames2/id/{id}/name/{name}` with:

```ctl
wget \
    --user=clover \
    --password=clover \
    "http://${HOST_PORT}/clover/data-service/getRequestParameterNames2/id/123/name/doe"
```

the `getRequestParameterNames()` function returns list containing `id` and `name`.

If you query data service with:

```ctl
wget \
    --user=clover \
    --password=clover \
    --post-data "name=doe&" \
    "http://${HOST_PORT}/clover/data-service/getRequestParameterNames3?id=234&"
```

the `getRequestParameterNames()` returns list containing `id` and `name`.

**See also:**[getRequestParameter](http-ctl2.html#id_ctl2_getrequestparameter), [getRequestParameters](http-ctl2.html#id_ctl2_getrequestparameters)

#### getRequestParameters

```ctl
string[] getRequestParameters(string name);
map[string,string] getRequestParameters();
```

The `getRequestParameters()` function return map of GET or POST request parameters and request parameter values. The parameters are from URL: `www.example.com/getRequestParameters?id=123&name=doe&name=john&`

The `name` parameter is name of the parameter.

**Compatibility**

The function `getRequestParameters()` was introduced in **CloverETL 4.7.0-M1**.
Example 351. Usage of getRequestParameters
If you query data service with:

```ctl
wget \
    --user=clover \
    --password=clover \
    "http://${HOST_PORT}/clover/data-service/getReqPar?id=123&name=doe&name=john&"
```

The `getRequestParameters()` returns map. The key is parameter name, the value is the parameter value.

The `getRequestParameters("name")` returns list containing `doe` and `john`.

**See also:**[getRequestParameter](http-ctl2.html#id_ctl2_getrequestparameter), [getRequestParameterNames](http-ctl2.html#id_ctl2_getrequestparameternames)

#### getRequestPartFilename

```ctl
string getRequestPartFilename(string paramName);
```

The `getRequestPartFilename()` function returns name of file received in multipart entity. Usually, it is a file name from HTML form.

The `paramName` parameter is name of HTML input field containing the file.

**Compatibility**

The function `getRequestPartFileName(string)` is available since **CloverETL 4.7.0-M1**.
Example 352. Usage of getRequestPartFilename
If you query the web service with:

```ctl
curl -F name=@/tmp/filename \
    http://example.com:8080/clover/data-service/getRequestPartFilename \
    --user clover:clover
```

the `getRequestPartFilename("name")` returns `somefile`.

#### getResponseContentType

```ctl
string getResponseContentType();
```

The `getResponseContentType()` function retuns response content type - the value of `Content-Type` response header field.

**Compatibility**

The function `getResponseContentType()` is available since **CloverETL 4.7.0-M1**.
Example 353. Usage of getResponseContentType The `getResponseContentType()` returns for example `application/json`.
[getRequestContentType](http-ctl2.html#id_ctl2_getrequestcontenttype), [setResponseContentType](http-ctl2.html#id_ctl2_setresponsecontenttype)

#### getResponseEncoding

```ctl
string getResponseEncoding();
```

The `getResponseEncoding()` function returns the response encoding.

**Compatibility**

The function `getResponseEncoding()` is available since **CloverETL 4.7.0-M1**.
Example 354. Usage of getResponseEncoding E.g. the `getResponseEncoding()` returns `iso-8859-1`.
**See also:**[getRequestEncoding](http-ctl2.html#id_ctl2_getrequestencoding), [setResponseEncoding](http-ctl2.html#id_ctl2_setresponseencoding)

#### setRequestEncoding

```ctl
void setRequestEncoding(string encoding);
```

The `setRequestEncoding()` function sets the encoding to be used in POST request parsing. Call this function in `init()`.

The `encoding` parameter is encoding.

**Compatibility**

The function `setRequestEncoding(string)` is available since **CloverETL 4.7.0-M1**.
Example 355. Usage of setRequestEncoding
The `setRequestEncoding("utf-8")` sets request encoding to UTF-8.

The `setRequestEncoding("iso-8859-2")` sets request encoding to latin2.

The `setRequestEncoding("cp1250")` sets request encoding to code page 1250.

**See also:**[getRequestEncoding](http-ctl2.html#id_ctl2_getrequestencoding)

#### setResponseBody

```ctl
void setResponseBody(string body);
```

The `setResponseBody()` function sets HTTP response body. Consider setting the response body encoding explicitly.

The `body` parameter is the content of the body.

If you try to create response body with `setResponsebody()` function and with writing to `response:body`, the later one will be used. You should use only one way to create the response body.

**Compatibility**

The function `setResponseBody(string)` is available since **CloverETL 4.7.0-M1**.
Example 356. Usage of getResponseBody The `setResponseBody("The response")` sets the response body.
**See also:**[setResponseEncoding](http-ctl2.html#id_ctl2_setresponseencoding)

#### setResponseContentType

```ctl
void setResponseContentType(string contentType);
```

The `setResponseContentType()` function sets the response content type - the value of `Content-Type` response header field.

The `contentType` parameter is the value of `Content-Type` response header field.

**Compatibility**

The function `setResponseContentType(string)` is available since **CloverETL 4.7.0-M1**.
Example 357. Usage of setResponseContentType`setResponseContentType("text/plain");`
[setResponseBody](http-ctl2.html#id_ctl2_setresponsebody), [getResponseContentType](http-ctl2.html#id_ctl2_getresponsecontenttype)

#### setResponseEncoding

```ctl
void setResponseEncoding(string encoding);
```

The `setResponseEncoding()` function sets HTTP response encoding. This encoding is used if you set the response body with the `setResponseBody()` function.

The `encoding` parameter is the response body encoding.

**Compatibility**

The function `setResponseEncoding(string)` is available since **CloverETL 4.7.0-M1**.
Example 358. Usage of setResponseEncoding The `setResponseEncoding("UTF-8");` sets response body encoding to *UTF-8*.
**See also:**[getResponseEncoding](http-ctl2.html#id_ctl2_getresponseencoding), [setResponseBody](http-ctl2.html#id_ctl2_setresponsebody)

#### setResponseHeader

```ctl
void setResponseHeader(string field, string value);
```

The `setResponseHeader()` function sets the response header. If the header does not exist, it will be created.

The `field` parameter is HTTP header field name.

The `value` parameter is HTTP header field value.

**Compatibility**

The function `setResponseHeader(string,string)` is available since **CloverETL 4.7.0-M1**.
Example 359. Usage of setResponseHeader`setResponseHeader("Server", "BOA")`
**See also:**[addResponseHeader](http-ctl2.html#id_ctl2_addresponseheader)

#### setResponseStatus

```ctl
void setResponseStatus(integer statusCode);
void setResponseStatus(integer statusCode, string message);
```

The `setResponseStatus()` function sets the response status code.

The `statusCode` parameter is the returned status code.

The `message` parameter is a message.

**Compatibility**

The `setResponseStatus(string,string)` is availables since **CloverETL 4.7.0-M1**.
Example 360. Usage of setResponseStatus
The `setResponseStatus(403)` sets the response status to 403.

 

The `setResponseStatus(414, "URI Too Long")` returns a status code 414.

```ctl
HTTP/1.1 414 URI Too Long
```

**See also:***[https://en.wikipedia.org/wiki/List_of_HTTP_status_codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)*, *[https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)*
