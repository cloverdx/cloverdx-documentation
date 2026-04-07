<!-- Administration > Configuration > Server configuration > Configuration properties and sources > Example configuration file -->

#### Example configuration file

Below is an example configuration file including the most commonly used configuration properties. You can use this configuration file as a template and uncomment and modify the desired properties. See [Properties details](example-configuration-file.md#properties-details) below for more information on the properties used in this file. For a full list of all configuration properties, see [List of configuration properties.](list-of-properties.md) For cluster-specific properties, see [Mandatory Cluster Properties](cluster-setup-index.md#mandatory-cluster-properties) and [Optional cluster properties.](cluster-setup-index.md#optional-cluster-properties)
> [!NOTE]
> Changes in the configuration file will take effect after CloverDX Server is restarted.

```properties
##The following properties are primarily used in the sandboxes root path specification.
#sandboxes.home=${clover.home}/sandboxes
#sandboxes.home.local=${clover.home}/sandboxes-local
#sandboxes.home.partitioned=${clover.home}/sandboxes-partitioned

##CloverDX libraries home
#libraries.home=${sandboxes.home}/libraries

##CloverDX Wrangler workspaces home
#workspaces.home=${sandboxes.home}

## Uncomment and modify the properties below to change the default user lockout values.

## Number of failed login attempts after which a next failed login attempt will lock the user.
## 0 means feature is switched off
## Default value is 5
#security.lockout.login.attempts=5

## Period of time during which the failed login attempts are counted.
## Default value is 300s (5 min)
#security.lockout.reset.period=300

## Period of time after which a successful login attempt will unlock a previously locked user.
## Default value is 300s (5 min)
#security.lockout.unlock.period=300

## Comma separated list of emails which will be notified when a user is locked out.
#security.lockout.notification.email=

## Uncomment lines bellow to enable the cluster mode.
#cluster.enabled=true
#cluster.node.id=node01
#cluster.jgroups.bind_address=localhost
#cluster.jgroups.start_port=7800
#cluster.http.url=http://localhost:8083/clover
#cluster.grpc.port=10600
#cluster.group.name=cloverCluster

## Instance indicator
## Modify the color and label of your environment. Colors can be: green, blue, yellow, or red.
#webGui.instance.color=blue
#webGui.instance.label=DEV

## Uncomment and tweak one of the following sections to use a
## separate database instead of the embedded Derby. This is
## recommended practice for production deployments.

## Example configuration for MySQL database.
## Modify the url, username and password for your environment.
#jdbc.driverClassName=com.mysql.cj.jdbc.Driver
#jdbc.url=jdbc:mysql://hostname:3306/clover?useUnicode=true&characterEncoding=utf8
#jdbc.username=user
#jdbc.password=pass
#jdbc.dialect=org.hibernate.dialect.MySQLDialect

## Example configuration for Oracle database.
## Modify the url, username and password for your environment.
#jdbc.driverClassName=oracle.jdbc.OracleDriver
#jdbc.url=jdbc:oracle:thin:@hostname:1521:db
#jdbc.username=user
#jdbc.password=pass
#jdbc.dialect=org.hibernate.dialect.OracleDialect

## Example configuration for MSSQL database.
## Modify the url, username and password for your environment.
#jdbc.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
#jdbc.url=jdbc:sqlserver://hostname:1433;databaseName=clover
#jdbc.username=user
#jdbc.password=pass
#jdbc.dialect=org.hibernate.dialect.SQLServerDialect

## Example configuration for PostgreSQL database.
## Modify the url, username and password for your environment.
#jdbc.driverClassName=org.postgresql.Driver
#jdbc.url=jdbc:postgresql://hostname/clover?charSet=UTF-8
#jdbc.username=user
#jdbc.password=pass
#jdbc.dialect=org.hibernate.dialect.PostgreSQLDialect
```

##### Properties details

| Property | Description |
| --- | --- |
| [sandboxes.home](list-of-properties.md#lop-sandboxes-home) | Directory where sandbox contents are stored. |
| sandboxes.home.local | Used in [cluster environments](cluster-setup-index.md) only; path to a [local sandbox](../admin/cluster-setup-index.md#local-sandbox) which is to be accessible only to a certain cluster node. |
| sandboxes.home.partitioned | Used in [cluster environments](cluster-setup-index.md) only; path to a [partitioned sandbox](../admin/cluster-setup-index.md#partitioned-sandbox) directory. |
| [libraries.home](list-of-properties.md#lop-libraries-home) | Directory for installed [libraries](../operations/libraries.md). |
| [workspaces.home](list-of-properties.md#lop-workspaces-home) | Directory for [Wrangler workspaces](wrangler-administration.md#workspaces). |
| [security.lockout.login.attempts](list-of-properties.md#lop-security-lockout-login-attempts) | Number of login attempts until a user is locked. See [user lockout](user-lockout.md) for more information. |
| [security.lockout.reset.period](list-of-properties.md#lop-security-lockout-reset-period) | Period during which login attempts are counted. See [user lockout](user-lockout.md) for more information. |
| [security.lockout.unlock.period](list-of-properties.md#lop-security-lockout-unlock-period) | Period after which a successful login releases the lock. See [user lockout](user-lockout.md) for more information. |
| [security.lockout.notification.email](list-of-properties.md#lop-security-lockout-notification-email) | Comma separated list of emails which will be notified when a user is locked out. |
| cluster.enabled  cluster.node.id  cluster.jgroups.bind_address  cluster.jgroups.start_port  cluster.http.url  cluster.grpc.port  cluster.group.name | Mandatory properties to enable clustering. See [Cluster mandatory properties](cluster-setup-index.md#mandatory-cluster-properties) for more information. |
| [webGui.instance.color](list-of-properties.md#webgui-instance-color) | Changes the color of the instance indicator in the left upper corner in CloverDX console. See [server instance indicator](server-instance-indicator.md) for more information. |
| [webGui.instance.label](list-of-properties.md#webgui-instance-label) | Changes the label of the instance indicator in the left upper corner in CloverDX console. See [server instance indicator](server-instance-indicator.md) for more information. |
| system database connection examples | For more information on system database installation and configuration, see [system database configuration.](examples-db-connection-configuration.md) When setting up a connection to a system database, remember to place the appropriate JDBC driver in the application server classpath (e.g., for Tomcat: <TOMCAT_INSTALL_DIR>/LIB). |
