<!-- Administration > Configuration > Server configuration > User management and access control > SAML authentication -->

#### SAML authentication

**CloverDX Server** supports Single Sign-on (SSO) by the SAML 2.0 protocol. Available since version 5.2.

Authorization is still handled by the **CloverDX Server** security module, so the user must be registered as a [CloverDX user](users.md) and their username must be the same as the username on Identity Provider’s (IdP) side. Since version 5.4 user accounts can be created automatically on the first time login and users can also be assigned to a default group.

The automatic account creation on the first time login is controlled by the `security.saml.user_autocreate` property, which defaults to `false`. Since users have no access to the server console by default, you need to also automatically assign them to a group. This can be achieved using the `security.saml.default_user_group` property. The expected value of the property is the code of the user group you want new users to be assigned to. If the property is not set or no user group with the given code is found, the login operation will fail and an error message is logged.

##### Example of SAML configuration using metadata file

By default, **CloverDX Server** allows only its own internal mechanism for authentication, under the default `clover` domain. To enable authentication with SAML, add `SAML` to the list of allowed authentication domains e.g.: `security.authentication.allowed_domains = clover,SAML`

**Note:** if the property is set as in the example above and you want to log in using the **CloverDX Server** credentials, use the `noSSO` parameter in the **CloverDX Server** URL, for example: `http://localhost:8083/clover?noSSO=true`

In order to set up the SAML authentication, **CloverDX Server** has to be configured as a Service Provider. First you need to configure a unique identifier using `security.saml.sp_entity_id` property. This ID is acquired from the Identity Provider when configuring it for **CloverDX Server** access. Then you have to configure the address where the **CloverDX Server** is reachable using `security.saml.sp_assertion_consumer_url` property.

Next you need to set up the configuration properties relating to the Identity Provider so that the **CloverDX Server** can connect to it. The recommended way of doing this is to use the SAML metadata file provided by the Identity Provider. Set the property `security.saml.idp_metadata_url` to the URL pointing to this file.

```properties
# Enable SAML SSO by adding SAML to allowed authentication domains
security.authentication.allowed_domains=clover,SAML
# Configure CloverDX Server running at http://clover-server:8080/clover as a Service Provider.
security.saml.sp_entity_id=https://example.com/example-app
security.saml.sp_assertion_consumer_url=http://clover-server:8080/clover
# Setting metadata URL automatically configures the Identity Provider to be used for SAML SSO
security.saml.idp_metadata_url=https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml
```

For more advanced examples, see the [SAML Examples section](saml-authentication.md#saml-configuration-examples).

SAML authentication can be set up in the [configuration file](configuration-sources.md#configuration-file-on-specified-location), using the following properties:

| Name | Required | Description |
| --- | --- | --- |
| **security.saml.sp_entity_id** | Yes | Unique identifier to be used by **CloverDX Server** as a Service Provider. Acquired from the Identity Provider when setting up access for new Service Providers. In case of Microsoft Azure it’s called `Application ID`. |
| **security.saml.sp_assertion_consumer_url** | Yes | The URL where **CloverDX Server** is reachable by the Identity Provider as a Service Provider. It is the target for redirect after a successful Single Sign-on. |
| **security.saml.idp_metadata_url** | Recommended | URL pointing to the metadata file of the Identity Provider. The metadata file provides required properties for setting up SAML authentication. We recommend to use this property to download the values of `security.saml.idp_*` properties automatically. |
| security.saml.idp_entity_id | Conditional | The identifier of the Identity Provider, must be a **URI**. Acquired from metadata file if `security.saml.idp_metadata_url` is configured. |
| security.saml.idp_sso_service_url | Conditional | The URL of the Identity Provider where the server will send the authentication request (for Single Sign-on). Acquired from metadata file if `security.saml.idp_metadata_url` is configured. |
| security.saml.idp_x509cert | Conditional | The public X509 certificate of the Identity Provider. Acquired from metadata file if `security.saml.idp_metadata_url` is configured. |
| security.saml.idp_x509cert_multi.0 | No | Additional public certificate. Multiple additional certificates can be added by incrementing the integer at the end of the property, e.g.: `security.saml.idp_x509cert_multi.1` |
| security.saml.idp_slo_service_url | No | The URL of the Identity Provider where the server will send the logout request (for Single Logout). Acquired from metadata file if `security.saml.idp_metadata_url` is configured. |
| security.saml.strict | No | If set to `true` the **CloverDX Server** will reject unsigned or unencrypted SAML messages if it expects them signed or encrypted. It will also reject messages that do not strictly follow the SAML 2.0 protocol. Default value is `true`. |
| security.saml.send_logout_response | No | Whether the **CloverDX Server** should send a logout response after an IdP-initiated logout request (defaults to true). |
| security.saml.metadata.idp_entity_id | No | The preferred Identity Provider ID if the metadata file contains more than one Identity Provider IDs. |
| security.saml.metadata.name_id_format | No | Name ID format to use, if available in the metadata file. Possible values: urn:oasis:names:tc:SAML:2.0:nameid-format:persistent urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified urn:oasis:names:tc:SAML:2.0:nameid-format:transient For more information see [the Oasis SAML Specification](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf) |
| security.saml.sp_nameid_format | No | Specifies constraints on the name identifier used to represent the requested subject. For more information see [the Oasis SAML Specification](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf) |
| security.saml.user_autocreate | No | Enablement of automatic user account creation on first time login using SAML (defaults to false). |
| security.saml.default_user_group | Conditional | The group to which automatically created user accounts should be assigned to. Expected value is the `code` of the group. The property is required if `security.saml.user_autocreate` is set to true. |

##### SAML configuration examples

###### Example of SAML configuration without using metadata file

If your Identity Provider does not provide a SAML Metadata file or you want to manually configure the feature, you will need to configure the following properties:
security.saml.idp_entity_id security.saml.idp_sso_service_url security.saml.idp_x509cert
While not a required property, in order for the Single Logout functionality to work you also need to configure service URL of it using: `security.saml.idp_slo_service_url`

```properties
# Enable SAML SSO by adding SAML to allowed authentication domains
security.authentication.allowed_domains=clover,SAML
# Configure clover server running at http://clover-server:8080/clover as a Service Provider.
security.saml.sp_entity_id=https://example.com/example-app
security.saml.sp_assertion_consumer_url=http://clover-server:8080/clover
# Set Identity Provider ID
security.saml.idp_entity_id=https://sts.windows.net/{tenantid}/
# Set the Single Sign-on service URL
security.saml.idp_sso_service_url=https://login.microsoftonline.com/common/saml2
# Set the X509 certificates (Base64-encoded DER format)
# required
security.saml.idp_x509cert=MIIDBTCCAe2gAw ... SryT2SUk
# optional
security.saml.idp_x509cert_multi.0=MIIDBTCCAe2gAw ... SryT2SUk
security.saml.idp_x509cert_multi.1=MIIC8TCCAdmgAw ... 5432GA==
# Set the Single Logout service URL
# optional
security.saml.idp_slo_service_url=https://login.microsoftonline.com/common/saml2
```

*# Do not send LogoutResponse back to Azure AD, it does not expect it*  **security.saml.send_logout_response**=false

###### Example of overriding SAML configuration acquired from metadata file

The following properties have priority and override the SAML configuration acquired from the metadata file.
security.saml.idp_entity_id security.saml.idp_sso_service_url security.saml.idp_x509cert security.saml.idp_slo_service_url

```properties
# Enable SAML SSO by adding SAML to allowed authentication domains
security.authentication.allowed_domains=clover,SAML
# Configure clover server running at http://clover-server:8080/clover as a Service Provider.
security.saml.sp_entity_id=https://example.com/clover-local
security.saml.sp_assertion_consumer_url=http://clover-server:8080/clover
# Setting metadata URL automatically configures the Identity Provider to be used for SAML SSO
security.saml.idp_metadata_url=https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml
# Override the Identity Provider ID
security.saml.idp_entity_id=https://sts.windows.net/{46-id-example}/
# Do not send LogoutResponse back to Azure AD, it does not expect it
security.saml.send_logout_response=false
```

##### SAML troubleshooting

Configuring SAML authentication might be a quite challenging task. Sometimes it does not work but there is no clear reason why. To detect problems we can configure **Log4j 2** to intercept communication between CloverDX Server and Identity Provider, write it to a log file and examine the log to find the problems.

###### How to configure Log4j 2 to log SAML authentication

1. Create a copy of `[clover.war]/WEB-INF/log4j2.xml` file.
2. Uncomment fragments in the file with **samlAppender** and loggers referring to the appender.
   ```xml
   <RollingFile name="samlAppender"
          fileName="${sys:clover.clover.home}/cloverlogs/saml.log"
          filePattern="${sys:clover.clover.home}/cloverlogs/saml.log.%i">
          <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p %X{IP} %m%n" charset="UTF-8" />
          <Policies>
          <SizeBasedTriggeringPolicy size="5MB" />
          </Policies>
          <DefaultRolloverStrategy max="10" />
   </RollingFile>
   ```
   ```xml
   <Logger name="com.cloveretl.server.auth.SamlServlet" level="debug" additivity="false">
          <AppenderRef ref="samlAppender" />
   </Logger>
   <Logger name="org.codelibs.saml2" level="debug" additivity="false">
          <AppenderRef ref="samlAppender" />
   </Logger>
   ```
3. Define a new system property **log4j.configurationFile** with the full path to the file:
   -Dlog4j.configurationFile=file:///C:/path/to/log4j2.xml
4. Start the CloverDX Server.
5. The communication is logged into `saml.log` file (located (by default) in the directory specified by the `java.io.tmpdir` system property in the `cloverlogs` subdirectory).
