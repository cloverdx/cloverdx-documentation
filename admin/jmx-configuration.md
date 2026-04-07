<!-- Administration > Configuration > Server configuration > JMX configuration -->

### JMX configuration

This section describes how to configure JMX access in Tomcat for monitoring and managing the Server Core. To configure JMX monitoring of Server Worker, see [Remote JMX monitoring of Worker JVM](jmx-configuration.md#remote-jmx-monitoring-of-worker-jvm).

It’s important to note that authentication is disabled in this example configuration for demonstration purposes only. In a production environment, JMX access should always be secured with authentication and, ideally, SSL encryption. See [Password Authentication](http://java.sun.com/j2se/1.5.0/docs/guide/management/agent.html#auth) for more information.

#### How to configure JMX on Apache Tomcat

Tomcat’s JVM must be executed with these parameters:

1. `-Dcom.sun.management.jmxremote=true`
2. `-Dcom.sun.management.jmxremote.port=<port>`
3. `-Dcom.sun.management.jmxremote.ssl=false`
4. `-Dcom.sun.management.jmxremote.authenticate=false`
5. `-Djava.rmi.server.hostname=<hostname or IP address> (necessary only for remote JMX connections)`

With these values, you can use the following URL for connection to the JMX server of your JVM. No user/password is needed.

`service:jmx:rmi:///jndi/rmi://<hostname or IP address>:<port>/jmxrmi`.

##### Configuring JMX on Linux

On UNIX-like OS, set environment variable CATALINA_OPTS, for example:

```properties
export CATALINA_OPTS="-Dcom.sun.management.jmxremote=true
                      -Dcom.sun.management.jmxremote.port=<port>
                      -Dcom.sun.management.jmxremote.ssl=false
                      -Dcom.sun.management.jmxremote.authenticate=false
                      -Djava.rmi.server.hostname=<hostname or IP address>"
```

Add these paramers to file `TOMCAT_HOME/bin/setenv.sh` (if it does not exist, you may create it) or `TOMCAT_HOME/bin/catalina.sh`

##### Configuring JMX on Windows

On Windows, each parameter must be set separately:

```properties
set CATALINA_OPTS=-Dcom.sun.management.jmxremote=true
set CATALINA_OPTS=%CATALINA_OPTS% -Dcom.sun.management.jmxremote.port=<port>
set CATALINA_OPTS=%CATALINA_OPTS% -Dcom.sun.management.jmxremote.authenticate=false
set CATALINA_OPTS=%CATALINA_OPTS% -Dcom.sun.management.jmxremote.ssl=false
set CATALINA_OPTS=%CATALINA_OPTS% -Djava.rmi.server.hostname=<hostname or IP address>
```

Add these parameters to file `TOMCAT_HOME/bin/setenv.bat` (if it does not exist, you may create it) or `TOMCAT_HOME/bin/catalina.bat`

When **running Tomcat as a Windows service**, add the parameters into the "Java Options" section in the service configuration in the following format:

```properties
-Dcom.sun.management.jmxremote=true
-Dcom.sun.management.jmxremote.port=<port>
-Dcom.sun.management.jmxremote.authenticate=false
-Dcom.sun.management.jmxremote.ssl=false
-Djava.rmi.server.hostname=<hostname or IP address>
```

#### Remote JMX monitoring of Worker JVM

Add the following options to the [worker.jvmOptions](list-of-properties.md#lop-worker-jvmoptions) property:

`-Dcom.sun.management.jmxremote=true -Dcom.sun.management.jmxremote.port=8687 -Dcom.sun.management.jmxremote.rmi.port=8687 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Djava.rmi.server.hostname=example.com`

With the above options, you enable remote connection to JMX monitoring, which provides a wide range of information about the running JVM, JNDI resources, etc. Change the value of `java.rmi.server.hostname` to the hostname of your Server.
