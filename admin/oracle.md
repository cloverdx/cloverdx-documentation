<!-- Administration > Installation > Server installation > System database configuration > Oracle -->

#### Oracle

| [Creating database](oracle.md#creating-database) |
| --- |
| [CloverDX Server setup](oracle.md#cloverdx-server-setup) |

##### Creating database

Run the following script to create a role (`cloverRole`), user (`cloverUser`) with password (`cloverPassword`) and tablespace for **CloverDX Server**:

```sql
-- Create a new role and grant it privileges.
CREATE ROLE cloverRole NOT IDENTIFIED;

GRANT CREATE SESSION TO cloverRole;
GRANT ALTER SESSION TO cloverRole;
GRANT CREATE TABLE TO cloverRole;
GRANT CREATE SEQUENCE TO cloverRole;
GRANT CREATE TRIGGER TO cloverRole;

-- Create a new database user with password.
CREATE USER cloverUser IDENTIFIED BY cloverPassword;

-- Set quota on tablespace.
GRANT UNLIMITED TABLESPACE TO cloverUser;

-- Connect a new role to a new user.
GRANT cloverRole TO cloverUser;
```

##### CloverDX Server setup

Example of a properties file configuration:

```properties
jdbc.driverClassName=oracle.jdbc.OracleDriver
jdbc.url=jdbc:oracle:thin:@host:1521:db
jdbc.username=cloverUser
jdbc.password=cloverPassword
jdbc.dialect=org.hibernate.dialect.OracleDialect
```

Add a JDBC 4 compliant driver on the classpath. A JDBC driver which doesn’t meet the JDBC 4 specifications won’t work properly.

**These are the privileges which have to be granted to a schema used by CloverDX Server:**

```sql
CONNECT
CREATE SESSION
CREATE/ALTER/DROP TABLE
CREATE/ALTER/DROP SEQUENCE

QUOTA UNLIMITED ON <user_tablespace>;
QUOTA UNLIMITED ON <temp_tablespace>;
```

> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [Encrypted JNDI](jndi-datasource-config.md#encrypted-jndi) or [Activation](production-server.md#activation)
