<!-- Administration > Installation > Server installation > System database configuration > JNDI configuration and encryption -->

#### JNDI configuration and encryption

| [JNDI DB Datasource](jndi-datasource-config.md#jndi-db-datasource) |
| --- |
| [JNDI datasource troubleshooting](jndi-datasource-config.md#jndi-datasource-troubleshooting) |
| [Encrypted JNDI](jndi-datasource-config.md#encrypted-jndi) |

##### JNDI DB datasource

**CloverDX Server** can connect to a database using JNDI Datasource which is configured in an application server.
> [!NOTE]
> Worker JNDI Configuration
> Note that the following configuration applies to [*Server Core*](architecture.md#cloverdx-core) only. Graphs running in [*Worker*](architecture.md#cloverdx-worker) cannot use JNDI as defined in the application container of the Server Core, because Worker is a separate JVM process. Worker provides its own [*JNDI configuration*](list-of-properties.md#worker-jndi-properties).

###### Example for Apache Tomcat and PostgreSQL database:

- **JNDI Datasource Definition**
  First you need to **define a JNDI Datasource** in an application server. The following context resource configuration may be added to the `[Tomcat_home]/conf/server.xml` file to the `<Host>` element.
  **Note:** Do not put the code into the `<GlobalNamingResources>` element, since the resource would not be visible by the **CloverDX** webapp.
  ```xml
  <Context path="/clover">
    <Resource name="jdbc/clover_server"
              auth="Container"
              type="javax.sql.DataSource"
              factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
              driverClassName="org.postgresql.Driver"
              url="jdbc:postgresql://127.0.0.1:5432/clover_db"
              username="clover"
              password=""
              maxTotal="20"
              maxIdle="10"
              maxWaitMillis="-1"/>
  </Context>
  ```
- **JNDI Connection Configuration**
  Now that the Datasource is defined, you should **configure the connection**.
  The following parameters may be set in the same way as other parameters (in the properties file or the Tomcat context file). You can also set the parameters in the *[Database](setup.md#system-database)* tab of the *[Setup](setup.md)* GUI.
  ```properties
  # The type of Datasource; must be set, because the default value is JDBC. #
  datasource.type=JNDI
  # JNDI location of DB Datasource; the default value is java:comp/env/jdbc/clover_server #
  datasource.jndiName=java:comp/env/jdbc/clover_server
  # Set the dialect according to DB which DataSource is connected to. #
  # The correct dialect can be found in the examples of DB configuration. #
  jdbc.dialect=org.hibernate.dialect.PostgreSQLDialect
  ```
  Since the DB connection contains sensitive information (e.g. username, password, etc.), **CloverDX** provides the *[JNDI Encryption](jndi-datasource-config.md#encrypted-jndi)* feature.
> [!TIP]
> The resource configuration may also be added to the context file `[Tomcat_home]/conf/Catalina/localhost/clover.xml`.
> [!IMPORTANT]
> Special characters typed in the context file have to be specified as XML entities, e.g. ampersand "&" as "&amp;", etc.

For a detailed list of parameters which can be set up in the configuration file, see [List of configuration properties](list-of-properties.md).

##### JNDI datasource troubleshooting

###### JNDI and SQL query metadata on worker

When using JNDI and [SQL query metadata](../developer/metadata-types.md#sql-query-metadata), JNDI must be configured on both **Server Core** and **Worker**. Otherwise, the `Cannot open DB connection from JNDI data source` error will occur.

##### Encrypted JNDI

The encryption feature allows you to protect your sensitive data defined in the Datasource definition (e.g. username, password, etc.), which are by default stored in plain text. The configuration differs between particular application servers.

| [Encrypted JNDI on Tomcat](jndi-datasource-config.md#encrypted-jndi-on-tomcat) |
| --- |

###### Encrypted JNDI on Tomcat

You need `secure-cfg-tool` to encrypt the passwords. Use the version of `secure-cfg-tool` corresponding to the version of **CloverDX Server**. Usage of the tool is described in [Secure Configuration Properties](secure-configuration-properties.md).

Use `encrypt.sh` or `encrypt.bat` for password encryption. Place the encrypted password into a configuration file, and put `cloverdx-secure-jndi-resource-{version}.jar` and `jasypt-1.9.0.jar` files on the classpath of the application server. The `.jar` files can be found in the `tomcat-secure-jndi-resource` directory packed in secure-cfg-tool.

The `tomcat-secure-jndi-resource` directory contains a useful `README` file with further details on encrypted JNDI.
Example of encrypted JNDI connection for PostgreSQL
Encrypt the password:

1. `./encrypt.sh -a PBEWithSHA1AndDESede`
2. The configuration is placed in `${CATALINA_HOME}/conf/context.xml`. Note that the encryption algorithm PBEWithSHA1AndDESede is not default.
   ```xml
   <Resource name="jdbc/clover_server"
             auth="Container"
             factory="com.cloveretl.secure.tomcatresource.Tomcat8SecureDataSourceFactory"
             secureAlgorithm="PBEWithSHA1AndDESede"
             type="javax.sql.DataSource"
             driverClassName="org.postgresql.Driver"
             url="jdbc:postgresql://127.0.0.1:5432/clover_db?charSet=UTF-8"
             username="conf#rPz5Foo7HPn4dFTRV5Ourg=="
             password="conf#4KlNp8/FVDR+rTWX0dEqWA=="
             maxTotal="20"
             maxIdle="10"
             maxWaitMillis="-1"/>
   ```
   If you use other JCE (e.g. Bouncy Castle), it has to be added to the classpath of the application server (`${CATALINA_HOME}/lib`). The encrypt command requires the path to directory with JCE, too.
   `./encrypt.sh -l ~/lib/ -c org.bouncycastle.jce.provider.BouncyCastleProvider -a PBEWITHSHA256AND256BITAES-CBC-BC`
   ```xml
   <Resource name="jdbc/clover_server"
             auth="Container"
             factory="com.cloveretl.secure.tomcatresource.Tomcat8SecureDataSourceFactory"
             secureProvider="org.bouncycastle.jce.provider.BouncyCastleProvider"
             secureAlgorithm="PBEWITHSHA256AND256BITAES-CBC-BC"
             type="javax.sql.DataSource"
             driverClassName="org.postgresql.Driver"
             url="jdbc:postgresql://127.0.0.1:5432/clover_db?charSet=UTF-8"
             username="conf#Ws9IuHKo9h7hMjPllr31VxdI1A9LKIaYfGEUmLet9rA="
             password="conf#Cj1v59Z5nCBHaktn6Ubgst4Iz69JLQ/q6/32Xwr/IEE="
             maxTotal="20" maxIdle="10"
             maxWaitMillis="-1"/>
   ```
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [Activation](production-server.md#activation)
