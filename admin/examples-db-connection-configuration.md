<!-- Administration > Installation > Server installation > System database configuration -->

### System database configuration

The **CloverDX Server** license, as well as user’s information, event listeners and other services, are saved in a database. For stability and performance reasons, the default Apache Derby database is **not** supported for production environment, it is supported for evaluation purposes with Tomcat 10.1 application container only; therefore, you should choose one of the supported DB systems.
> [!IMPORTANT]
> Since **CloverDX Server** stores important data in a database, you should create a system database and set up a working connection **before** you activate the Server with license and configure it.

For details on how to set up a connection to an external system database, see the list of examples below. The examples contain details on creating databases in DB systems supported by **CloverDX Server** and configuring a working connection between the database and the Server.

It is possible to specify common **JDBC** DB connection properties (see below) or a **JNDI** location of DB Datasource.

**Clustered Deployment**

In a Clustered deployment, each node must have a direct connection to a shared database specified. For more information, see [Cluster configuration](cluster-setup-index.md#cluster-configuration).

#### Setting up a CloverDX Server’s system database

1. **Create a database**
   - Choose one of the supported database systems and create a database dedicated to **CloverDX Server**. Add a user/role for Clover and grant it required rights/privileges.
2. **Configure common JDBC connection properties**
   - Some JDBC connection properties are common for all supported database systems. If you use a **properties file** for configuration, specify these properties:
     | **jdbc.driverClassName** | Class name for JDBC driver name. |
     | --- | --- |
     | **jdbc.url** | JDBC URL used by **CloverDX Server** to store data. |
     | **jdbc.username** | JDBC database username. |
     | **jdbc.password** | JDBC database password. |
     | **jdbc.dialect** | Hibernate dialect to use in Object-relational mapping (ORM). |
3. **Add a JDBC 4 compliant driver on the classpath.**
   - As the last step, add a JDBC 4 compliant driver on the classpath. A JDBC Driver which doesn’t meet JDBC 4 won’t work properly.

Below is a list of examples of individual database systems configurations.

##### Examples of database configurations

- [Embedded Apache Derby](embedded-apache-derby.md)
- [MySQL](mysql.md)
- [Oracle](oracle.md)
- [Microsoft SQL Server](mssql.md)
- [PostgreSQL](postgresql.md)
- [JNDI DB Datasource](jndi-datasource-config.md#jndi-db-datasource)

For officially supported versions of particular database systems, see [Supported stacks](system-requirements-for-cloverdx-server.md#software-requirements).
