<!-- Administration > Installation > Server installation > System database configuration > Embedded Apache Derby -->

#### Embedded Apache Derby

The Apache Derby embedded DB is used with a default **CloverDX Server** installation. It uses the working directory as a storage for data persistence by default. This may be a problem on some systems. If a problem occurs with connecting to Derby DB, we recommend you configure a connection to external DB or at least specify the Derby home directory:

Configure the `derby.system.home` system property to set path which is accessible for application server. You can specify this system property with this JVM execution parameter:

`-Dderby.system.home=[derby_DB_files_root]`

Example of a properties file configuration:

```properties
jdbc.driverClassName=org.apache.derby.jdbc.EmbeddedDriver
jdbc.url=jdbc:derby:databases/cloverDb;create=true
jdbc.username=user
jdbc.password=password
```

Take a closer look at the `jdbc.url` parameter. The `databases/cloverDb` part means a subdirectory for DB data. This subdirectory will be created in the directory which is set as `derby.system.home` (or in the working directory if `derby.system.home` is not set). You may change the default value `databases/cloverDb`.

A Derby JDBC 4 compliant driver is bundled with **CloverDX Server**, thus there is no need to add it on the classpath.
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [Encrypted JNDI](jndi-datasource-config.md#encrypted-jndi) or [Activation](production-server.md#activation)
