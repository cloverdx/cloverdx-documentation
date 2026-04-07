<!-- Administration > Configuration > Server configuration > Configuration properties and sources > Configuration sources -->

#### Configuration sources

| [Configuration file on specified location](configuration-sources.md#configuration-file-on-specified-location) |
| --- |
| [Alternative configuration sources](configuration-sources.md#alternative-configuration-sources) |
| [Priorities of configuration sources](configuration-sources.md#priorities-of-configuration-sources) |
| [Specifying path to configuration file](configuration-sources.md#specifying-path-to-configuration-file) |

Once installed, **CloverDX Server** requires the configuration of essential ([database connection](examples-db-connection-configuration.md), [license](production-server.md#activation), [sandboxes](setup.md#sandboxes)) and optional ([SMTP](list-of-properties.md#lop-smtp), [LDAP authentication](ldap-authentication.md), [SAML](saml-authentication.md), etc.) features. The configuration is done by specifying *[configuration properties](list-of-properties.md)* in a `[property-key]=[property-value]` format.
> [!IMPORTANT]
> The configuration might contain sensitive data; therefore, **CloverDX Server** enables you to encrypt the configuration properties (for more information, see [Securing configuration properties](secure-configuration-properties.md)).

**CloverDX** can load the configuration properties from several sources. We **recommend** the easiest, most convenient way:

##### Configuration file on specified location

The `cloverServer.properties` configuration file is a text file which contains all **CloverDX** settings. You can edit the file either manually, or using a **simple and intuitive***[Setup GUI](setup.md)*.
> [!TIP]
> For an example configuration file, see [Example configuration file.](example-configuration-file.md)

The path to the file can be specified by system property, context parameter or environment variable.

**We recommend** specifying the path with the `clover.config.file` system property.

**Example for Apache Tomcat:**

Edit `bin/setenv.sh` (or `bin\setenv.bat`) and add `-Dclover.config.file=/absolute/path/to/cloverServer.properties` to `CATALINA_OPTS`.

For more information and examples on the supported application containers, see [Specifying path to configuration file](configuration-sources.md#specifying-path-to-configuration-file).

##### Alternative configuration sources

There are other sources of configuration properties, as well. Each source containing the configuration data has a different priority. If a property isn’t set, application’s default setting is used.
> [!WARNING]
> Combining configuration sources could lead to a confusing configuration which would make maintenance much more difficult.

- **Environment Variables**
  Environment variables are variables configured by means of your operating system (e.g. `$PATH` is an environment variable).
  There are two ways of configuration via environment variables:
  - **direct override** - using environment variables with the same name as the configuration properties and adding the `clover.` prefix. For example, the environment variable `clover.sandboxes.home` will override the configuration property `sandboxes.home`.
    Some operating systems may not use a dot (`.`) character, so underlines (`_`) may be used instead of dots. So the `clover_config_file` name works as well.
  - **placeholders** - configuration properties can reference environment variables using the `${env:ENVIRONMENT_VARIABLE}` syntax. For instance, `sandboxes.home=${env:SANDBOXES_ROOT}`.
    Placeholders can be used in all **CloverDX Server** properties. If placeholder must not be resolved, use doubled '$' character, e.g. `security.ldap.user_search.filter=(sn=$${username})`.
- **System Properties**
  System properties are configured by means of JVM, i.e. with the `-D` argument (`-Dclover.config.file`).
  Set a system property with the `clover.` prefix, i.e. (`clover.config.file`).
  Underlines (`_`) may be used instead of dots (`.`) so the `clover_config_file` name works as well.
  System properties can also be referenced from within placeholders in all **CloverDX Server** properties. For instance, `sandboxes.home=${sys:user.home}/sandboxes`.
- **Configuration File on Default Location**
  A text file containing configured **CloverDX** properties. By default, **CloverDX** searches for the file on the `[AppServerDir]/cloverServer.properties` path.
- **Modification of Context Parameters in web.xml**
  This way **isn’t recommended**, since it requires a modification of the WAR file, but it may be useful when none of the approaches above are possible.
  Unzip `clover.war` and modify the `WEB-INF/web.xml` file. Add the following piece of code into the file:
  ```xml
  <context-param>
      <param-name>[property-name]</param-name>
      <param-value>[property-value]</param-value>
  </context-param>
  ```
- **Context Parameters (Available on Apache Tomcat)**
  Some application servers allow you to set context parameters without modification of the WAR file.
  This way of configuration is possible, but it is **not recommended**, as Apache Tomcat may ignore some context parameters in some environments. Using the configuration file is almost as convenient and much more reliable.
  **Example for Apache Tomcat:**
  On Tomcat, it is possible to specify context parameters in a context configuration file `[Tomcat_home]/conf/Catalina/localhost/clover.xml` which is created automatically just after deployment of the CloverDX Server web application.
  You can specify a property by adding this element:
  ```xml
  <Parameter name="[propertyName]" value="[propertyValue]" override="false" />
  ```
  (Note: by setting the `override` attribute to `false`), the context parameter does not override the default setting associated with the owning host.)

##### Priorities of configuration sources

Configuration sources have the following priorities (from the highest to lowest):

1. **Context parameters**
   Context parameters are specified in an application server or directly in a `web.xml` file (**not recommended**).
2. **External configuration file**
   The path to the external configuration file can be specified in several ways. CloverDX Server attempts to find the file in this order (only one of them is loaded):
   1. the path specified with a `config.file` context parameter;
   2. the path specified with a `clover_config_file` or `clover.config.file` system property (**recommended**);
   3. the path specified with a `clover_config_file` or `clover.config.file` environment variable;
   4. the default location (`[AppServerDir]/cloverServer.properties`).
3. **System properties**
4. **Environment variables**
5. **Default values**

##### Specifying path to configuration file

*[Setup](setup.md)* uses the configuration file to save the Server’s settings. The path to the file is specified by the `clover.config.file` system property. Each application server has a different way to configure the path:

- **Apache Tomcat**
  Edit `bin/setenv.sh` (or `bin/setenv.bat`) and add `-Dclover.config.file=/absolute/path/to/cloverServer.properties` to `CATALINA_OPTS`.
  See also [Apache Tomcat](production-server.md#apache-tomcat).
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [System database configuration](examples-db-connection-configuration.md)
