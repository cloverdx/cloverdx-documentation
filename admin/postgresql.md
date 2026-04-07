<!-- Administration > Installation > Server installation > System database configuration > PostgreSQL -->

#### PostgreSQL

| [Creating database](postgresql.md#creating-database) |
| --- |
| [CloverDX Server setup](postgresql.md#cloverdx-server-setup) |

##### Creating database

Advanced users can create their own table space

We are going to create a database for **CloverDX** and a user role which will own the database. This user role will be then used by the Server to access the database.

Database name: clover_db

User: clover

Password: clover

1. Optionally, you can create a new tablespace
2. Connect as postgres (default admin) to the default DB postgres and execute the following commands:
   ```sql
   CREATE USER clover ENCRYPTED PASSWORD 'clover';
   CREATE DATABASE clover_db OWNER clover;
   ```

To separate the database into its own tablespace, create a tablespace before creating the database.

and use the following command to create the database:

```sql
CREATE DATABASE clover_db OWNER clover TABLESPACE tablespace_name;
```

For more information, see the [PostgreSQL documentation](https://www.postgresql.org/docs/15/sql-createtablespace.html).

##### CloverDX Server setup

Example of a properties file configuration:

```properties
jdbc.driverClassName=org.postgresql.Driver
jdbc.url=jdbc:postgresql://localhost/clover_db?charSet=UTF-8
jdbc.username=clover
jdbc.password=clover
jdbc.dialect=org.hibernate.dialect.PostgreSQLDialect
```

Add a JDBC 4 compliant driver on the classpath. A JDBC driver which doesn’t meet the JDBC 4 specifications won’t work properly.

The JDBC driver for PostgreSQL can be downloaded from the [official PostgreSQL page](https://jdbc.postgresql.org/download/).

**Example for Apache Tomcat:** place the libraries into the `TOMCAT/lib` directory.

See also [PostgreSQL documentation on jdbc URL](https://jdbc.postgresql.org/documentation/use/#connecting-to-the-database).
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [Encrypted JNDI](jndi-datasource-config.md#encrypted-jndi) or [Activation](production-server.md#activation)
