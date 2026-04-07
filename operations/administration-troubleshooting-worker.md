<!-- Automation and operations > Operations > Server logs & troubleshooting > Troubleshooting worker issues -->

### Troubleshooting worker issues

#### Worker logs

When investigating issues with Worker itself or jobs running in Worker, there are several logs with useful information:

Logs found in the **Monitoring** ****Server Logs** section of the Server Console.

- **COMMON** log - the main Server log contains also information related to Worker. This log contains the full command line used to start Worker, this allows you to check the command line arguments. Additionally, standard output of the Worker process is redirected to this log - this is useful especially if the Worker process crashes during startup.
  The COMMON log file is located in `${java.io.tmpdir}/cloverlogs/all.log`
- **WORKER** log - the main Worker log provides information about Worker startup, initialization, executed jobs, runtime activities, etc. The initialization details contain information about Worker’s JNDI resources, etc.
  The WORKER log file is located in `${java.io.tmpdir}/cloverlogs/worker_[nodeID].log`
  You can also open this log via the **Go to logs** action in the **Worker** section of the **Monitoring** page.

#### Worker command line

The full command line that was used to start the Worker process can be found in:

- Monitoring section, use the **Show command line** action on Worker. For more details, see [Showing worker command line arguments](monitoring.md#4-showing-worker-command-line-arguments).
- The COMMON log of the Server (found in the **Monitoring** ****Server Logs** page). See section above for more details.

Investigate the command line options in case Worker does not correctly start or if the configuration of the running Worker is not correct.

#### Performance logging

CloverDX regularly collects performance metrics and stores them in the performance log. The metrics are such as CPU load, garbage collector activity, used heap, thread counts etc. The performance log is an additional tool to analyze an incident, see [Performance log](logging.md#performance-log) for more details.

#### Worker does not start

If Worker does not start, check the following:

- Server’s COMMON log and the WORKER log, see [above](administration-troubleshooting-worker.md#worker-logs). Look for errors during Worker startup and initialization.
- Worker’s command line arguments, see [above](administration-troubleshooting-worker.md#worker-command-line). Look for invalid command line arguments. Additionally, check the custom JVM arguments set on Worker, in the [Worker](../admin/setup.md#worker) tab of [Setup](../admin/setup.md) or via the [worker.jvmOptions](../admin/list-of-properties.md#lop-worker-jvmoptions) configuration property.

#### Restarting worker

If Worker gets into an unrecoverable state (e.g. out of heap memory, etc.) and you fix the source issue, you can restart it from the Monitoring section (For more details, see [Restarting the worker](monitoring.md#2-restarting-worker).):

- restart immediately, which will abort jobs currently running in Worker;
- restart after running jobs finish, in case the currently running jobs are crucial.

#### Worker does not start

In case Worker does not start (i.e. remains in the `STARTING` status), check the COMMON log first.

#### Worker crashes

If common log (`all.log` file) contains row similar to the following one, the worker crashed due to exhausted heap space.

```
2018-03-22 16:08:29,008[s StdOut reader] WorkerProcess    INFO      [worker0@N1:10500]: java.lang.OutOfMemoryError: Java heap space
```

You can configure it to generate heap dump for further investigation. To do so, add `-XX:+HeapDumpOnOutOfMemoryError` to JVM arguments in Worker configuration (**Configuration** > **Setup** > **Worker**). The generated file can be investigated with tools like `jvisualvm` or `jhat`.

Another cause of the crash can be swapped Worker’s main memory. If there is insufficient free space in the main memory and the pages of Worker process are swapped on the hard drive, Worker is slowed down, it does not receive heart beat from the Server in time and it kills itself. Lower the maximum heap size of Worker to avoid swapping. Note that Java process uses also non-heap memory, e.g. metaspace or direct memory.

To investigate usage of direct memory, add `-XX:NativeMemoryTracking=summary` to Worker’s JVM arguments (**Configuration** > **Setup** > **Worker**). The details on native memory usage can be displayed with **jcmd <pid> VM.native_memory summary**. See *[https://docs.oracle.com/en/java/javase/11/vm/native-memory-tracking.html](https://docs.oracle.com/en/java/javase/11/vm/native-memory-tracking.html)* for details on native memory tracking.

#### Worker hangs

Usually, it is caused by garbage collector. Try tweaking the garbage collection.

Another cause can be swapping of worker process pages on hard drive.

#### Issues with classloading

To debug issues with classloading, add `-verbose:class` to **JVM arguments** of Worker. Loaded and unloaded classes will be printed to the output. The output can be seen in the common log.
