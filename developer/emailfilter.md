<!-- Development > Component reference > Data Quality > EmailFilter -->

### EmailFilter

![EmailFilter 64x64](../figures/EmailFilter-64x64.png)

| [Short description](emailfilter.md#short-description) |
| --- |
| [Ports](emailfilter.md#ports) |
| [Metadata](emailfilter.md#metadata) |
| [EmailFilter attributes](emailfilter.md#emailfilter-attributes) |
| [Details](emailfilter.md#details) |
| [See also](emailfilter.md#see-also) |

#### Short description

**EmailFilter** filters input records according to a specified condition.

| Same input metadata | Sorted inputs | Inputs | Outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 1 | 0-2 | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | For input data records | Any |
| Output | 0 | **⨯** | For valid data records | Input 0 |
| 1 | **⨯** | For rejected data records | Any[[1]](emailfilter.md#emailfilter-footnote1) |  |

| 1 |  Metadata on the output port 0 contain any of the input data fields plus up to two additional fields. Fields whose names are the same as those in the input metadata are filled in with input values of these fields. |
| --- | --- |

#### Metadata

Metadata cannot be propagated through this component.

Metadata on the output port 0 contain any of the input data fields plus up to two additional fields. Fields whose names are the same as those in the input metadata are filled in with input values of these fields.

| Field number | Field name | Data type | Description |
| --- | --- | --- | --- |
| FieldA | the **Error field** attribute value | string | Error field |
| FieldB | the **Status field** attribute value | integer[[1]](emailfilter.md#emailfilter-footnote2) | Status field |

| 1 |  The following error codes are the most common:  - **0**`No error` - email address accepted. - **1**`Syntax error` - any string that does not conform to email address format specification is rejected with this error code. - **2**`Domain error` - verification of domain failed for the address. Either the domain does not exist or the DNS system can not determine a mail exchange server. - **3**`SMTP handshake error` - at `SMTP` level, this error code indicates that a mail exchange server for specified domain is either unreachable or the connection failed for other reason (e.g. server too busy, etc.). - **4**`SMTP verify error` - at `SMTP` level, this error code means that the server rejected the address as being invalid using the VRFY command. The address is officially invalid. - **5**`SMTP recipient error` - at `SMTP` level, this error code means the server rejected the address for delivery. - **6**`SMTP mail error` - at `MAIL` level, this error indicates that although the server accepted the test message for a delivery, an error occurred during send. |
| --- | --- |

#### EmailFilter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Field list | yes | A list of selected input field names whose values should be verified as valid or non-valid email addresses. Expressed as a sequence of field names separated by a colon, semicolon, or pipe. |  |
| Level of inspection |  | Various methods used for the email address verification can be specified. Each level includes and extends its predecessor(s) on the left. For more information, see [Level of inspection](emailfilter.md#level-of-inspection). | SYNTAX \| DOMAIN (default) \| SMTP \| MAIL |
| Accept empty |  | By default, even an empty field is accepted as a valid address. This can be switched off by setting to `false`. For more information, see [Accept conditions](emailfilter.md#accept-conditions). | true (default) \| false |
| Error field |  | The name of the output field to which an error message can be written (for rejected records only). |  |
| Status field |  | The name of the output field to which an error code can be written (for rejected records only). |  |
| Multi delimiter |  | A regular expression that serves to split an individual field value to multiple email addresses. If empty, each field is treated as a single email address. | [,;] (default) \| other |
| Accept condition |  | By default, a record is accepted even if at least one field value is verified as a valid email address. If set to `STRICT`, a record is accepted only if all field values from all fields of the **Field list** are valid. For more information, see [Accept conditions](emailfilter.md#accept-conditions). | LENIENT (default) \| STRICT |
| Advanced |  |  |  |
| E-mail buffer size |  | Maximum number of records that are read into memory after which they are bulk processed. For more information, see [Buffer and cache size](emailfilter.md#buffer-and-cache-size). | 2000 (default) \| 1-N |
| E-mail cache size |  | The maximum number of cached email address verification results. For more information, see [Buffer and cache size](emailfilter.md#buffer-and-cache-size). | 2000 (default) \| 0 (caching is turned off) \| 1-N |
| Domain cache size |  | Maximum number of cached DNS query results. Is ignored at `SYNTAX` level. | 3000 (default) \| 0 (caching is turned off) \| 1-N |
| Domain retry timeout (ms) |  | The timeout in millisecond for each DNS query attempt. Thus, maximum time in milliseconds spent to resolving equals to **Domain retry timeout** multiplied by **Domain retry count**. | 800 (default) \| 1-N |
| Domain retry count |  | The number of retries for failed DNS queries. | 2 (default) \| 1-N |
| Domain query A records |  | By default, according to the SMTP standard, if no MX record could be found, the A record should be searched. If set to `false`, DNS query is two times faster; however, this SMTP standard is broken. | true (default) \| false |
| SMTP connect attempts (ms,…​) |  | Attempts for connection and HELO. Expressed as a sequence of numbers separated by a comma. The numbers are delays between individual attempts to connect. | 1000,2000 (default) |
| SMTP anti-graylisting attempts (s,…​) |  | Anti-graylisting feature. Attempts and delays between individual attempts expressed as a sequence of number separated by a comma. If empty, anti-graylisting is turned off. For more information, see [SMTP graylisting attempts](emailfilter.md#smtp-graylisting-attempts). | 30,120,240 (default) |
| SMTP request timeout (s) |  | The TCP timeout in seconds after which a SMTP request fails. | 300 (default) \| 1-N |
| SMTP concurrent limit |  | The maximum number of parallel tasks when anti-graylisting is on. | 10 (default) \| 1-N |
| Mail From |  | The `From` field of a dummy message sent at `MAIL` level. | CloverDX <[clover@cloverdx.com](mailto:clover@cloverdx.com)> (default) \| other |
| Mail Subject |  | The `Subject` field of a dummy message sent at `MAIL` level. | Hello, this is a test message (default) \| other |
| Mail Body |  | The `Body` of a dummy message sent at `MAIL` level. | Hello,\nThis is CloverDX text message.\n\nPlease ignore and don’t respond. Thank you, have a nice day! (default) \| other |

#### Details

**EmailFilter** receives incoming records through its input port and verifies specified fields for valid email addresses. Data records that are accepted as valid are sent out through the optional first output port, if connected. Specified fields from the rejected inputs can be sent out through the optional second output port, if it is connected to other component. Metadata on the optional second output port may also contain up to two additional fields with information about an error.

##### Buffer and cache size

Increasing **E-mail buffer size** avoids unnecessary repeated queries to DNS system and SMTP servers by processing more records in a single query. On the other hand, increasing **E-mail cache size** might produce even better performance since addresses stored in cache can be verified in an instant. However, both parameters require extra memory so set it to the largest values you can afford on your system.

##### Accept conditions

By default, even an empty field from input data records specified in the **List of fields** is considered to be a valid email address. The **Accept empty** attribute is set to `true` by default. If you want to be more strict, you can switch this attribute to `false`.

In other words, this means that at least one valid email address is sufficient for considering the record accepted.

On the other hand, if **Accept condition** is set to `STRICT`, all email addresses in the **List of fields** must be valid (either including or excluding empty values depending on the **Accept empty** attribute).

Thus, be careful when setting these two attributes: **Accept empty** and **Accept condition**. If there is an empty field among fields specified in **List of fields**, and all other non-empty values are verified as invalid addresses, such record gets accepted if both **Accept condition** is set to `LENIENT` and **Accept empty** is set to `true`. However, in reality, such record does not contain any useful and valid email address, it contains only an empty string which assures that such record is accepted.

##### Level of inspection

1. **SYNTAX**
   At the first level of validation (`SYNTAX`), the syntax of email expressions is checked and even both non-strict conditions and international characters (except TLD) are allowed.
2. **DOMAIN**
   At the second level of validation (`DOMAIN`) - which is the default one a DNS system is queried for domain validity and mail exchange server information. The following four attributes can be set to optimize the ratio of performance to false-negative responses: **Domain cache size**, **Domain retry timeout**, **Domain retry count** and **Domain query A records**. The number of queries sent to a DNS server is specified by the **Domain retry count** attribute. Its default value is 2. The time interval between individual queries that are sent is defined by **Domain retry timeout** in milliseconds. By default, it is set to 800 milliseconds. Thus, the whole time during which the queries are being resolved is equal to **Domain retry count** x **Domain retry timeout**. The results of queries can be cached. The number of cached results is defined by **Domain cache size**. By default, 3,000 results are cached. If you set this attribute to 0, you turn the caching off. You can also decide whether A records should be searched, if no MX record is found (**Domain query A records**). By default, it is set to `true`. Thus, A record is searched, if MX record is not found. However, you can switch this off by setting the attribute to `false`. This way you can speed the searching two times, although this breaks the SMTP standard.
3. **SMTP**
   At the third level of validation (`SMTP`), attempts are made to connect SMTP server. You need to specify the number of attempts and time intervals between individual attempts. This is defined using the **SMTP connect attempts** attribute. This attribute is a sequence of integer numbers separated by commas. Each number is the time (in seconds) between two attempts to connect the server. Thus, the first number is the interval between the first and the second attempts, the second number is the interval between the second and the third attempts, etc. The default value is three attempts with time intervals between the first and the second attempts equal to 1,000 and between the second and the third attempts equal to 2,000 milliseconds.
   Additionally, the **EmailFilter** component, at `SMTP` and `MAIL` levels, is capable of increasing accuracy and eliminating false-negatives caused by servers incorporating graylisting. Graylisting is one of very common anti-spam techniques based on denial of delivery for unknown hosts. A host becomes known and "graylisted" (i.e. not allowed) when it retries its delivery after specified period of time, usually ranging from 1 to 5 minutes. Most spammers do not retry the delivery after initial failure just for the sake of high performance. **EmailFilter** has an anti-graylisting feature which retries each failed `SMTP/MAIL` test for specified number of times and delays. Only after the last retry fails, the address is considered as invalid.
4. **MAIL**
   At the fourth level (`MAIL`), if all have been successful, you can send a dummy message to the specified email address. The message has the following properties: **Mail From**, **Mail Subject** and **Mail Body**. By default, the message is sent from `CloverDX <clover@cloverdx.com>`, its subject is `Hello, this is a test message`. And its default body is as follows: `Hello,\nThis is CloverDX test message.\n\nPlease ignore and don’t respond. Thank you and have a nice day!`

##### SMTP graylisting attempts

To turn the anti-graylisting feature, you can specify the **SMTP gray-listing attempts** attribute. Its default value is 30,120,240. These numbers means that four attempts can be made with time intervals between them that equal to 30 seconds (between the first and the second), 120 seconds (between the second and the third) and 240 seconds (between the third and the fourth). You can change the default values by any other comma separated sequence of integer numbers. The maximum number of parallel tasks that are performed when anti-graylisting is turned on is specified by the **SMTP concurrent limit** attribute. Its default value is 10.

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Data Quality comparison](common-of-data-quality.md#data-quality-comparison) |
