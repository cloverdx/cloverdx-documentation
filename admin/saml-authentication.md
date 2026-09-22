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
| security.saml.authnrequest_signed | No | Whether the authentication request sent to the Identity Provider is signed (defaults to false). The published service provider metadata advertises this setting to the Identity Provider. |
| security.saml.logoutrequest_signed | No | Whether the logout request sent to the Identity Provider is signed (defaults to false). |
| security.saml.logoutresponse_signed | No | Whether the logout response sent to the Identity Provider is signed (defaults to false). |
| security.saml.sign_metadata | No | Whether the service provider metadata published at `/saml/metadata` is signed with the service provider private key (defaults to false). |
| security.saml.nameid_encrypted | No | Whether the NameID in the logout request sent to the Identity Provider is encrypted (defaults to false). Encryption uses the Identity Provider certificate, so `security.saml.idp_x509cert` is required when this setting is enabled. |
| security.saml.want_messages_signed | No | Whether the response, logout request and logout response received from the Identity Provider are required to be signed (defaults to false). Verification uses the Identity Provider certificate, the service provider keyStore is not needed. |
| security.saml.want_assertions_signed | No | Whether assertions received from the Identity Provider are required to be signed (defaults to false). Verification uses the Identity Provider certificate, the service provider keyStore is not needed. |
| security.saml.want_assertions_encrypted | No | Whether assertions received from the Identity Provider are required to be encrypted (defaults to false). |
| security.saml.want_nameid_encrypted | No | Whether the NameID received from the Identity Provider is required to be encrypted (defaults to false). |
| security.saml.reject_deprecated_alg | No | Whether messages signed with a deprecated algorithm, such as SHA-1, are rejected (defaults to false). The setting applies to signature verification only, the service provider keyStore is not needed. |
| security.saml.signature_algorithm | No | Algorithm used to sign the messages **CloverDX Server** sends. Defaults to `http://www.w3.org/2001/04/xmldsig-more#rsa-sha256`. |
| security.saml.digest_algorithm | No | Digest algorithm used when signing. Defaults to `http://www.w3.org/2001/04/xmlenc#sha256`. |
| security.saml.sp_keystore | Conditional | Path to the keyStore file holding the service provider private key and certificate. The property is required if any of `security.saml.authnrequest_signed`, `security.saml.logoutrequest_signed`, `security.saml.logoutresponse_signed`, `security.saml.sign_metadata`, `security.saml.want_assertions_encrypted` or `security.saml.want_nameid_encrypted` is enabled. The remaining signing and encryption properties do not use the service provider key. |
| security.saml.sp_keystore_password | Conditional | Password of the keyStore, also used to unlock the key entry. Supports [encrypted configuration properties](secure-configuration-properties.md). The property is required if `security.saml.sp_keystore` is set. |
| security.saml.sp_key_alias | Conditional | Alias of the key in the keyStore. The property is required if `security.saml.sp_keystore` is set. |

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

###### Example of signed and encrypted SAML communication

By default **CloverDX Server** neither signs the messages it sends nor requires the messages it receives to be signed. Signing what the server sends, and decrypting what it receives, needs a service provider private key and certificate, which are read from a keyStore. Verifying signatures created by the Identity Provider needs no keyStore, only `security.saml.idp_x509cert`.

Create the keyStore before configuring the properties. Use the PKCS12 format, because it keeps one password for the store and for the key entry, which is what `security.saml.sp_keystore_password` is:

```
keytool -genkeypair -alias clover-sp -keyalg RSA -keysize 2048 -sigalg SHA256withRSA \
        -validity 3650 -storetype PKCS12 -keystore saml-sp.p12 \
        -dname "CN=clover-server.example.com, O=Example, C=US"
```

The following example signs the authentication request sent to the Identity Provider and requires the assertions received from it to be both signed and encrypted. The keyStore password is stored [encrypted](secure-configuration-properties.md):

```properties
# Sign the authentication request sent to the Identity Provider
security.saml.authnrequest_signed=true
# Require the assertions received from the Identity Provider to be signed and encrypted
security.saml.want_assertions_signed=true
security.saml.want_assertions_encrypted=true
# Reject messages signed with a deprecated algorithm such as SHA-1
security.saml.reject_deprecated_alg=true
# Service provider private key and certificate
security.saml.sp_keystore=/opt/clover/conf/saml-sp.p12
security.saml.sp_keystore_password=conf#xLndKgzwP7DxAbWuhztvt/vHIvtUFjnB7MnL6pJIWpRw0gVJPghBr4HUnp0GE0Ym
security.saml.sp_key_alias=clover-sp
```

**Relation to `security.saml.strict`:** the `want_*` properties say **what** is required, while `security.saml.strict` decides **whether a message that does not meet the requirement is rejected**. With `security.saml.strict=false` the requirements are only advertised to the Identity Provider and a message that fails them is still accepted, so keep `security.saml.strict=true` (the default) whenever you enable any of them.

**Note:****CloverDX Server** publishes its service provider metadata at the `/saml/metadata` path, for example `http://clover-server:8080/clover/saml/metadata`. Once a keyStore is configured, the published metadata contains the service provider certificate and reflects the signing properties, so the Identity Provider may need the metadata re-imported for signing to work.

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
