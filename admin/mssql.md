<!-- Administration > Installation > Server installation > System database configuration > Microsoft SQL Server -->

#### Microsoft SQL Server

It is recommended to use the **SQL Server Authentication** for connection to the system database. This section details the steps to create a new MS SQL database with an **SQL Server Authentication** account and how to set up **CloverDX Server** to use it as its system database.

##### Prerequisites

###### Version compatibility

Ensure the version of your MS SQL Server is supported. See [Software requirements](system-requirements-for-cloverdx-server.md#software-requirements) for more information.

###### Enabling SQL Server Authentication

If your MS SQL Server does not currently allow **SQL Server Authentication**, enable it: Select the server instance in **Microsoft SQL Server Management Studio**, right-click and go to **Properties > Security > Server authentication**. Select the **SQL Server and Windows Authentication mode** and restart the server instance afterwards.

###### TCP connections and port

Ensure you have the following configured in **SQL Server Configuration Manager**:

- **TCP/IP** is set to `Enabled` in **SQL Server Network Configuration** > **Protocols**
- **TCP Port** is set to `1433` in **TCP/IP Properties** under **IP Addresses > IPAll**.
> [!NOTE]
> While port `1433` is the default for MS SQL databases, you can use any unused port. This guide uses port `1433` for demonstration purposes.

##### Creating database

The following commands can be used to create a system database and user configuration.
> [!NOTE]
> Remember to modify the script according to your specific needs. This includes replacing the following:
>
> - *clover_db*: Choose a desired name for your database.
> - *clover*: Replace with your preferred username for database access.
> - *clover*: Set a strong password for the database user.

```sql
-- Create the database 'clover_db'
CREATE DATABASE clover_db;

-- Enable READ COMMITTED SNAPSHOT isolation level on 'clover_db'
ALTER DATABASE clover_db SET READ_COMMITTED_SNAPSHOT ON;
GO

-- Create a login named 'clover' with password 'clover'
-- and set the default database to 'clover_db'
CREATE LOGIN clover WITH PASSWORD = 'clover', DEFAULT_DATABASE = clover_db;

-- Connect to the database 'clover_db'
USE clover_db;

-- Create a user named 'clover' mapped to the login 'clover'
CREATE USER clover FOR LOGIN clover;

-- Grant 'db_owner' role membership to the user 'clover'
EXEC sp_addrolemember 'db_owner', 'clover';
```

##### CloverDX Server setup

This section describes how to set up a JDBC connection to a MS SQL database. If you want to set up a JNDI connection, refer to [JNDI configuration and encryption](jndi-datasource-config.md).

###### JDBC driver

Place an appropriate JDBC 4 compliant driver on your application server’s classpath (for Tomcat this would be `TOMCAT_HOME/lib`). If you want to validate your connection (see JDBC connection configuration below), make sure to restart your Server environment first.

###### Import database certificates into truststore

If your MS SQL Server is configured to require encryption for connections, you will need to import the server certificate into a truststore used by **CloverDX Server** core. This means to import the certificate into either:

- The default JDK `cacerts` truststore (located in `$JAVA_HOME/jre/lib/security/cacerts`, default password is `changeit`).
- You custom truststore. To tell **CloverDX Server** core to use this truststore, add the following environment variables to your application server configuration (`setenv.sh` or `setenv.bat` depending on your operating system). Alternatively, if running Tomcat as a service on Windows, you can add these variables to the "Java options" section on the Java tab in the service configuration.

```properties
JAVA_OPTS="$JAVA_OPTS -Djavax.net.ssl.trustStore=path/to/certificate/truststore.ks -Djavax.net.ssl.trustStorePassword=truststorePassword"
```

> [!NOTE]
> Remember to restart **CloverDX Server** after importing the certificate and configuring the custom truststore.

###### JDBC connection configuration

The easiest way to set up a JDBC database connection is to navigate to **Configuration > Setup > System database**.

1. Select the **JDBC connection** option.
2. Select **MS SQL Server** in the database type.
3. Enter the connection URL, e.g. `jdbc:sqlserver://host:1433;database=clover_db` (see the warning box at the bottom for more information on possible issues).
4. Specify credentials.
5. You can use the **Validate** option to see if the connection can be successfully established. The connection can be validated only when there is an appropriate JDBC driver placed in the server’s classpath and the Server environment has been restarted afterwards.
6. Make sure to click on the **Save** button to save your changes.
7. Restart the Server to use the database as the system database.

Changes performed in this section are automatically reflected in the Server configuration file. You can also set up the connection directly in the [CloverDX Server configuration file](configuration-sources.md#configuration-file-on-specified-location) by adding the following properties (or enabling and modifying the relevant sections, if you use our [example configuration file](example-configuration-file.md)). Make sure to change the connection string and credentials accordingly.

```properties
jdbc.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
jdbc.url=jdbc:sqlserver://hostname:1433;database=clover_db
jdbc.username=clover
jdbc.password=clover
jdbc.dialect=org.hibernate.dialect.SQLServerDialect
```

> [!CAUTION]
> Starting with **MS SQL JDBC driver version 10.2, TLS encryption is enabled by default**.
>
> This means the connection URL in the example above might not work if your SQL Server isn’t set up to require encryption.
>
> For maximum security, enabling encryption in production environments is highly recommended. However, for non-production use cases, you can temporarily bypass this requirement by adding either of the following properties to your connection URL:
>
> - `trustServerCertificate=true` (ignores server certificate validation - use with caution)
> - `encrypt=false` (disables encryption entirely - not recommended for sensitive data)
>
> Refer to Microsoft’s documentation for recommended security practices when connecting to SQL Server.
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [Encrypted JNDI](jndi-datasource-config.md#encrypted-jndi) or [Activation](production-server.md#activation)
