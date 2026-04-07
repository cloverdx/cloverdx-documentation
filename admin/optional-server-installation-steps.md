<!-- Administration > Installation > Server installation > Manual installation > Optional installation steps -->

#### Optional installation steps

| [Adding libraries to worker classpath](optional-server-installation-steps.md#adding-libraries-to-worker-classpath) |
| --- |
| [Advanced memory configuration](optional-server-installation-steps.md#advanced-memory-configuration) |

This chapter covers optional installation steps that allow you to further customize your CloverDX Server setup. In most cases, the default settings are sufficient for typical deployments. However, if you need to extend the environment with additional libraries or fine-tune memory management for advanced use cases, the instructions in this section will help you adjust the configuration.

##### Adding libraries to worker classpath

Worker may need additional libraries, e.g. a JDBC driver library or the Bouncy Castle cryptographic library. There are two ways to add the libraries.

###### Using default worker classpath directory

Create a `worker-lib` directory in the `${clover.home}` directory and place the libraries there. The path set by [clover.home](list-of-properties.md#lop-clover-home) can be found in **Server GUI** under **Configuration** ****CloverDX Info** ****Server Properties**.

###### Configuration property

Create a directory containing the libraries and set the `worker.classpath` configuration property to the path to this directory.

##### Advanced memory configuration

This section describes advanced memory configuration options for CloverDX Server. In most cases, the default settings are sufficient and require no changes. However, if you encounter memory-related issues or want to fine-tune your environment for better performance or stability, the options below allow you to set appropriate limits and adjust JVM behavior for specific use cases.

See [JVM configuration guidelines for Core and Worker processes](postinstallation-configuration.md#jvm-configuration-guidelines-for-core-and-worker-processes) for more information on CloverDX Server architecture and configuration.

###### Metaspace

In Java, **Metaspace** is the memory space used to store class metadata and is separate from the heap. By default, there is no limit, but you can specify a reasonable upper limit to prevent excessive memory use. The limit is set by adding the `-XX:MaxMetaspaceSize` JVM argument. Use a suitably high limit, such as `512 MB`, which is typically sufficient.

This argument is **passed from the Core to Worker and it is recommended to keep the values the same in both JVMs**.

To set the limit on the Core process, add the argument in the following place and **make sure to restart CloverDX Server for the change to take effect**:

| JVM | OS | Config location | Example |
| --- | --- | --- | --- |
| **Core** | Linux | *setenv.sh* | `export CATALINA_OPTS="$CATALINA_OPTS -XX:MaxMetaspaceSize=512m"` |
| Windows - manual | *setenv.bat* | `set "CATALINA_OPTS=%CATALINA_OPTS% -XX:MaxMetaspaceSize=512m"` |  |
| Windows - service | *Apache Commons Daemon Service Manager* | Add `-XX:MaxMetaspaceSize=512m` to the *Java Options* section on the *Java* tab. |  |

###### Maximum cached buffer size

Java NIO uses direct ByteBuffers for efficient I/O operations, especially when working with native libraries. To improve performance, each thread maintains a small cache of recently used direct buffers in direct memory, known as *the temporary buffer cache*. By default, this cache has no limit on the size of buffers it can retain, which can lead to excessive off-heap memory usage in multi-threaded applications like CloverDX.

Setting a limit helps reduce memory retention and improve control over off-heap memory use. That is why we, by default, hardcode the **limit on the Worker process to `262,144`** bytes, which should be sufficient in most environments.

If you need to fine-tune the limit on the Worker process, or add it to the Core process, you can do so by using the `-Djdk.nio.maxCachedBufferSize` JVM argument. For more information about the argument, refer [here](https://www.oracle.com/java/technologies/javase/9-enhancements.html).

Add the argument in the following place and **make sure to restart CloverDX Server or Worker for the changes to take effect**:

| JVM | OS | Config location | Example |
| --- | --- | --- | --- |
| **Core** | Linux | *setenv.sh* | `export JAVA_OPTS="$JAVA_OPTS -Djdk.nio.maxCachedBufferSize=262144"` |
| Windows - manual | *setenv.bat* | `set JAVA_OPTS=%JAVA_OPTS% "-Djdk.nio.maxCachedBufferSize=262144"` |  |
| Windows - service | *Apache Commons Daemon Service Manager* | Add `-Djdk.nio.maxCachedBufferSize=262144` to the *Java Options* section on the *Java* tab. |  |
| **Worker** | Add `-Djdk.nio.maxCachedBufferSize=<new size>` to the **JVM Arguments** section in the CloverDX Console under **Configuration > Setup > [Worker](setup.md#worker)**. |  |  |

###### Code cache size

Some CloverDX Server installations may experience severe performance slowdowns, sometimes over 100× slower than normal. One possible cause is the **JVM code cache** becoming full.

The **code cache** is a special memory area where the JVM stores compiled versions of frequently used parts of the program. When this cache is full, the JVM can no longer compile new code for faster execution and instead must run it in a slower, interpreted mode. This shift can dramatically reduce performance. The reserved code cache size is platform-dependent and can be too small for **CloverDX Server**.

The limit is controlled by the the `-XX:ReservedCodeCacheSize` argument. Refer [here](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html) for more information.

If you hit the code cache limit, you can increase the code cache size by adding the argument on the Core or Worker process in the following places and **restarting CloverDX Server or Worker for the changes to take effect**:

| JVM | OS | Config location | Example |
| --- | --- | --- | --- |
| **Core** | Linux | *setenv.sh* | `export JAVA_OPTS="$JAVA_OPTS -XX:ReservedCodeCacheSize=512m"` |
| Windows - manual | *setenv.bat* | `set JAVA_OPTS=%JAVA_OPTS% "-XX:ReservedCodeCacheSize=512m"` |  |
| Windows - service | *Apache Commons Daemon Service Manager* | Add `-XX:ReservedCodeCacheSize=512m` to the *Java Options* section on the *Java* tab. |  |
| **Worker** | Add `-XX:ReservedCodeCacheSize=512m` to the **JVM Arguments** section in the CloverDX Console under **Configuration > Setup > [Worker](setup.md#worker)**. |  |  |
