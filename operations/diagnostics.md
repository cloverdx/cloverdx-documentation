<!-- Automation and operations > Operations > Server logs & troubleshooting > Diagnostics -->

### Diagnostics

**CloverDX Server** allows you to create a thread dump or a heap dump for both Server Core and Worker. The heap and thread dumps are useful for investigation of performance and memory issues.

A **heap dump** is a content of the JVM process memory stored in a binary file. The generated heap dump file can be investigated with tools like `jvisualvm` or `jhat`.

A **thread dump** is a list of existing JVM threads with their callstacks and held locking objects (if supported). It can be viewed in a text editor.

Note that generating a heap dump requires the [Heap Memory Dump permission](../admin/groups.md#permission-heap-memory-dump).

#### Downloading heap/thread dump

In Server GUI, go to **Configuration** ****System Info** ****Diagnostics**.

To download a heap dump or thread dump of either Server Core or Worker, click on the respective button. Note that in the case of a heap dump, it may take a moment before the download is ready.
> [!IMPORTANT]
> The size of the heap dump temp file is determined by the Server Core or Worker [*heap memory size setting*](../admin/postinstallation-configuration.md#recommended-server-core-and-worker-heap-memory-configuration) - make sure there is enough free space in the [*temp directory*](../admin/tempspace.md) before downloading the file.
>
> The temporary file is automatically deleted after download, but note that it may contain sensitive information (e.g. passwords) in plain text.
>
> A garbage collection is triggered before the heap dump which may cause the Server to briefly stop responding.

The **Dump live objects only** checkbox allows you to avoid dumping of objects awaiting garbage collection.

#### Downloading heap/thread dump using jcmd command

##### Heap dump

The heap dump of Worker can be created with jcmd command: `jcmd <pidOfWorker> GC.heap_dump <filename>` You should specify the file name with full path to avoid searching for the file as `jcmd` does not always create it in the working directory.

##### Thread dump

The thread dump of Worker can be created with jcmd command: `jcmd <pidOfWorker> Thread.print`

See [details on jcmd](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr006.html).

#### Generating heap dump on out of memory errors

To generate a heap dump on Out of Memory errors, add `-XX:+HeapDumpOnOutOfMemoryError` to the [worker.jvmOptions](../admin/list-of-properties.md#lop-worker-jvmoptions) property. A dump file `java_pid.hprof` will be generated when an Out of Memory error occurs. The heap dump will be located in the working directory of the Worker’s process (same as the Server Core’s working directory). You can override the directory location with the `-XX:HeapDumpPath=/disk2/dumps` option. **Important:** the generated file can be large, its size is equal to the heap size.

#### Garbage collection logging

Some memory and performance issues can be investigated with help of garbage collection (GC) logs. By default, **CloverDX Server** enables Worker’s GC logging automatically, but the user can override these default settings, as required.

GC log files are stored in `temp/cloverlogs/gc`. The name of the file contains Worker and node identification, and a timestamp which prevents log overwriting, for example: `worker0_node1-gc-2019-07-18_15-18-58.log`. When a Worker process starts, it creates a new file name with the current timestamp. While the Worker process runs, files with this name are rotated. Log rotation amount is 10 files with the maximum size of 5MB per file.

You can analyze the log file with various tools, e.g. [http://gceasy.io/](http://gceasy.io/).

##### Tweaking garbage collection logging

GC Logging can be set up manually for both Server Core and Worker using the flags listed below. Note that if you overwrite even one of the flags for Worker, **CloverDX Server** default GC logging setting is ignored. You can change the name and path to the file (include the timestamp in the file name to prevent overwriting):

- **Java 17:**`-Xlog:gc*:file=/data/logs/gc_worker_%t.log:time:filecount=10,filesize=5M`

The flags should be added to:

- **Server core:**`JAVA_OPTS` in `$CATALINA_HOME/bin/setenv.sh`.
- **Worker:** Worker’s [JVM arguments](../admin/setup.md#worker) field in the Setup GUI, or the [worker.jvmOptions](../admin/list-of-properties.md#lop-worker-jvmoptions) property.

Restart CloverDX Server for changes to take effect.

#### Performance logging

CloverDX regularly collects performance metrics and stores them in the performance log. The metrics are such as CPU load, garbage collector activity, used heap, thread counts etc. The performance log is an additional tool to analyze an incident, see [Performance Log](logging.md#performance-log) for more details.

#### Additional diagnostic tools

Below are additional useful diagnostic tools:

#### Investigating usage of direct memory

To investigate usage of direct memory, add `-XX:NativeMemoryTracking=summary` to the [worker.jvmOptions](../admin/list-of-properties.md#lop-worker-jvmoptions) property. The details on native memory usage can be displayed with `jcmd <pid> VM.native_memory summary`. For more information, see [Native Memory Tracking tool](https://docs.oracle.com/en/java/javase/11/vm/native-memory-tracking.html).

#### JMX monitoring

If you want to set up JMX monitoring for Server Core or Worker, see [JMX configuration](../admin/jmx-configuration.md).
