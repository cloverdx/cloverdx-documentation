<!-- Administration > Installation > Server installation > Manual installation > Troubleshooting -->

#### Troubleshooting

Since **CloverDX Server** is considered a universal JEE application running on various application servers, databases and JVM implementations, problems may occur during the installation. These can be solved with a proper configuration of the Server environment. This section contains tips for the configuration.

| [Memory issues on Derby](possible-installation-problems.md#memory-issues-on-derby) |
| --- |
| [JAVA_HOME environment variable is not defined](possible-installation-problems.md#java-home-environment-variable-is-not-defined) |
| [Tomcat log file catalina.out is missing on Windows](possible-installation-problems.md#tomcat-log-file-catalinaout-is-missing-on-windows) |
| [Derby.system.home cannot be accessed](possible-installation-problems.md#derbysystemhome-cannot-be-accessed) |
| [Environment variables and more than one CloverDX Server instances running on single machine](possible-installation-problems.md#environment-variables-and-more-than-one-cloverdx-server-instances-running-on-single-machine) |
| [Special characters and slashes in path](possible-installation-problems.md#special-characters-and-slashes-in-path) |
| [File system permissions](possible-installation-problems.md#file-system-permissions) |
| [JMS API and JMS third-party libraries](possible-installation-problems.md#jms-api-and-jms-third-party-libraries) |

##### Memory issues on Derby

If your Server suddenly starts consuming too much resources (CPU, memory) despite having been working well before, it might be caused by a running internal Derby DB. Typically, causes are incorrect/incomplete shutdown of Apache Tomcat and parallel (re)start of Apache Tomcat.

Solution: move to a standard (standalone) database.

How to fix this? Redeploy **CloverDX Server**:

1. Stop Apache Tomcat and verify there are no other instances running. If so, kill them.
2. Backup the configuration file, if you configured any.
3. Delete the `webapps/clover` directory.
4. Start the Apache Tomcat server. It will automatically redeploy **CloverDX Server**.
5. Verify you can connect from Designer and from web.
6. Shutdown Apache Tomcat.
7. Restore the configuration file and point it to your regular database.
8. Start Apache Tomcat.

##### JAVA_HOME environment variable is not defined

If you are getting this error message during an attempt to start your application server (mostly Tomcat), perform the following actions.

**Linux:**

This command sets the path to the variable on the server. `[clover@server /] export JAVA_HOME=/usr/local/jdk17`

Then restart the application server.

**Windows OS:**

Set `JAVA_HOME` to your JDK installation directory, e.g. `C:\Program Files\java\jdk17`.
> [!IMPORTANT]
> CloverDX Server requires a Java Development Kit (JDK). Running with just JRE is not supported.

##### Tomcat log file catalina.out is missing on Windows

Tomcat start batch files for Windows aren’t configured to create the `catalina.out` file which contains the standard output of the application. The `catalina.out` file may be vital when Tomcat isn’t started in the console and an issue occurs. Or even when Tomcat is executed in the console, it may be closed automatically just after the error message appears in it.

Please follow these steps to enable `catalina.out` creation:

- Modify `[Tomcat_home]/bin/catalina.bat` and add the parameter `/B` to the lines where the `_EXECJAVA` variable is set. There should be two such lines:
  `set _EXECJAVA=start /B [the rest of the line]`
  Parameter `/B` causes the "start" command to not open a new console window, but run in its own console window instead.
- Create a new startup file, e.g. `[Tomcat_home]/bin/startupLog.bat`, containing a single line:
  `catalina.bat start > ..\logs\catalina.out 2<&1`
  It executes Tomcat in the usual way, but the standard output isn’t put to the console, but to the `catalina.out` file.

Then use the new startup file instead of `[Tomcat_home]/bin/startup.bat`.

##### Derby.system.home cannot be accessed

If the Server cannot start and the following message is in the log:

*java.sql.SQLException: Failed to start database 'databases/cloverserver'*

then see the next exception for details. After that, check settings of the `derby.system.home` system property. It may point to an unaccessible directory, or files may be locked by another process. We suggest you set a specific directory as the system property.

##### Environment variables and more than one CloverDX Server instances running on single machine

If you are setting environment variables like `clover_license_file` or `clover_config_file`, remember you should not be running more than one **CloverDX Server**. Therefore, if you ever need to run more instances at once, use other ways of setting parameters (see [Configuration](part3.md) for description of all possibilities). The reason is the environment variables are shared by all applications in use causing them to share configurations and fail unexpectedly. Instead of the environment variables, you can use system properties (passed to the application container process using parameter with -D prefix: `-Dclover_config_file`).

##### Special characters and slashes in path

When working with servers, be sure to follow the folder naming rules. Do not use any special characters in the server path, e.g. spaces, accents, diacritics are not recommended. It can produce issues which are hard to find. If you are experiencing weird errors and cannot trace the source of them, install the application server in a safe destination like:

`C:\Tomcat10\`

Similarly, use slashes but never backslashes in paths inside the `*.properties` files, e.g. when pointing to the **CloverDX Server** license file. If you incorrectly use a backslash, it will be considered an escape character and the Server may not work properly (this applies to Windows OS, as well). This is an example of a correct path:

`license.file=C:/CloverDX/Server/license.dat`

##### File system permissions

The application server must be executed by an OS user with proper read/write permissions on file system. Problem may occur, if app-server is executed by a root user for the first time, so log and other temp files are created by root user. When the same app-server is executed by another user, it will fail because it cannot write to root’s files.

##### JMS API and JMS third-party libraries

Missing JMS libraries do not cause failure of the Server startup, but it is an issue of deployment on an application server, thus it is still related to this chapter.

`clover.war` itself does not contain `jms.jar`, so it has to be on an application server’s classpath. Most of the application servers have `jms.jar` by default, but Tomcat, for example, does not. So if the JMS features are needed, the `jms.jar` has to be added explicitly.

If the "JMS Task" feature is used, there must be third-party libraries on a Server’s classpath as well. The same approach is recommended for JMS Reader/Writer components, even if these components allow to specify external libraries. It is due to common memory leak in these libraries which causes `OutOfMemoryError: Metaspace`.
