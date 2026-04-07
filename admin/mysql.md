<!-- Administration > Installation > Server installation > System database configuration > MySQL -->

#### MySQL

| [Creating database](mysql.md#creating-database) |
| --- |
| [CloverDX Server setup](mysql.md#cloverdx-server-setup) |

**CloverDX Server** supports MySQL 8.

##### Creating database

The following steps will create a `clover_db` database and the `clover` user with `clover` password.

1. Create database `clover_db`, set charset and collate.
   ```sql
   CREATE SCHEMA clover_db CHARACTER SET utf8 COLLATE utf8_unicode_ci;
   ```
2. Use clover_db as the current database.
   ```sql
   USE clover_db;
   ```
3. Create a new user with password and host.
   ```sql
   CREATE USER 'clover'@'%' IDENTIFIED BY 'clover';
   ```
4. Add all privileges to user 'clover' in DB clover_db.
   ```sql
   GRANT ALL ON clover_db.* TO 'clover'@'%';
   ```
5. Reload privileges.
   ```sql
   FLUSH privileges;
   ```

##### CloverDX Server setup

Example of a properties file configuration:

```properties
jdbc.driverClassName=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://127.0.0.1:3306/clover_db?useUnicode=true&characterEncoding=utf8
jdbc.username=clover
jdbc.password=clover
jdbc.dialect=org.hibernate.dialect.MySQLDialect
```

Add a JDBC 4 compliant driver on the classpath. A JDBC Driver which doesn’t meet JDBC 4 won’t work properly.
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [Encrypted JNDI](jndi-datasource-config.md#encrypted-jndi) or [Activation](production-server.md#activation)
