<!-- Administration > Installation > Server installation > Manual installation > Post-installation configuration -->

#### Post-installation configuration

| [JVM configuration guidelines for Core and Worker processes](postinstallation-configuration.md#jvm-configuration-guidelines-for-core-and-worker-processes) |
| --- |
| [Memory settings](postinstallation-configuration.md#memory-settings) |
| [JVM memory areas overview](postinstallation-configuration.md#jvm-memory-areas-overview) |
| [Configuring heap memory](postinstallation-configuration.md#configuring-heap-memory) |
| [Recommended Server Core and Worker heap memory configuration](postinstallation-configuration.md#recommended-server-core-and-worker-heap-memory-configuration) |
| [Reflective access](postinstallation-configuration.md#reflective-access) |
| [Garbage collector for Worker](postinstallation-configuration.md#garbage-collector-for-worker) |
| [Maximum number of open files](postinstallation-configuration.md#maximum-number-of-open-files) |
| [Maximum number of processes or threads](postinstallation-configuration.md#maximum-number-of-processes-or-threads) |
| [Firewall exceptions](postinstallation-configuration.md#firewall-exceptions) |
| [Reverse proxy configuration](postinstallation-configuration.md#reverse-proxy-configuration) |
| [Redirecting the OAuth2 discovery documents](postinstallation-configuration.md#redirecting-the-oauth2-discovery-documents) |

##### JVM configuration guidelines for Core and Worker processes
> [!NOTE]
> CloverDX Server consists [of two standalone JVMs](architecture.md): the **Core** and the **Worker**. While the Worker inherits some properties from the Core, others must be explicitly configured for the Worker. For a comprehensive overview of the properties that are inherited and those requiring separate configuration, refer to [Properties on Worker’s command line](list-of-properties.md#properties-on-workers-command-line).

###### Core process configuration

To configure the **Core process**, the following are the recommended options, depending on your operating system and how Apache Tomcat is run:

- **Unix/Linux**: Add the required arguments to the `setenv.sh` file located in the `bin` directory of your Tomcat installation.
- **Windows** (Tomcat run manually from `startup.bat`): Add the arguments to the `setenv.bat` file located in the `bin` directory of your Tomcat installation.
- **Windows** (Tomcat run as a service): Use the *Apache Commons Daemon Service Manager* to configure the arguments. This is done via the executable named `<service name>w.exe` (e.g., `Tomcat10w.exe`) found in the `bin` directory of your Tomcat service installation.

**Note**: While other configuration methods may exist depending on your server setup and deployment preferences, they are not included here as they are platform-specific and outside the scope of this guide.

###### Worker configuration

For the **Worker process**, the recommended approach is to add the arguments in **Configuration > Setup > [Worker](setup.md#worker)** in the Server Console. When added through this interface, the arguments are automatically translated and saved into the Server [configuration file](configuration-sources.md#configuration-file-on-specified-location).

##### Memory settings

The current implementation of the Java Virtual Machine (JVM) allows only a global memory configuration per JVM process. In the CloverDX Server architecture, the **Core** process and the **Worker** process **each run in their own separate JVM instance**. Within each of these JVMs, the memory space is shared—so all components running inside a single JVM, operate within the same memory allocation. As a result, memory configuration should be tailored to the specific role and expected workload of each process.

The default JVM memory settings are **too low** for running an application container with CloverDX Server. The **optimal memory limits** depend on many conditions, including the nature and complexity of the transformations that CloverDX Server is expected to execute. Please note that the maximum limit isn’t the amount of permanently allocated memory, but rather the limit which can’t be exceeded. If the limit is exhausted, the `OutOfMemoryError` is raised.

###### JVM memory areas overview

JVM memory consists of several areas: **heap memory**, **Metaspace**, **direct memory**, and **stack memory**.

Configuring the **heap sizes** for the Core and Worker processes is essential for stable and efficient operation and should be the primary focus of memory tuning. Since JVM memory is not just **heap** memory, **you should not set the heap limit too high**, as this can lead to the JVM exhausting the available system RAM. If the heap consumes too much of the total RAM, the JVM may struggle to allocate sufficient direct memory or stack space for new threads, potentially causing performance issues or application crashes. See [Recommended Server Core and Worker heap memory configuration](postinstallation-configuration.md#recommended-server-core-and-worker-heap-memory-configuration) for more information.

Other areas affecting memory—such as **Metaspace, direct memory**, or the **code cache**—are typically well-handled by default settings. However, depending on the complexity of your jobs, the amount of custom Java code, or specific performance requirements, you may benefit from reviewing and adjusting these areas as well. For example, you might choose to limit **Metaspace** to control its size, adjust the **maximum cached buffer** size to better manage direct memory, or tune the **code cache size**—especially if running extensive custom Java code, as an undersized code cache can lead to noticeable performance issues. For more information, see the [Advanced memory configuration](optional-server-installation-steps.md#advanced-memory-configuration) section.

| Type | Description |
| --- | --- |
| **Heap memory** | Heap is an area of memory used by JVM for dynamic memory allocation. Required heap memory size depends on various factors (e.g. complexity of graphs, number of graphs running in parallel, type of used components, etc.).  Configuring the **correct heap sizes for both the Core and Worker processes is crucial for stable and efficient operation**. Insufficient heap space can lead to performance issues or memory-related errors, especially under high or complex workloads. To configure heap limits, see [Configuring heap memory](postinstallation-configuration.md#configuring-heap-memory).  The current heap memory usage can be observed in [CloverDX Server Console](../operations/monitoring.md). |
| **Metaspace** | Separate memory space containing class definitions and related metadata. By default, metaspace is not limited. If you want to set a limit to it, see [Advanced memory configuration](optional-server-installation-steps.md#advanced-memory-configuration). |
| **Direct memory** | Memory used for faster I/O operations, such as reading from files or communicating over a network. It is managed through direct buffers. Java maintains a small per-thread cache of these buffers to enhance performance. In most cases, the default caching behavior is sufficient and does not require adjustment. However, when working with particularly large datasets or high thread counts, reviewing buffer management may help optimize memory usage. See [Advanced memory configuration](optional-server-installation-steps.md#advanced-memory-configuration) for more information. |
| **Stack memory** | Contains local, method-specific variables and references to other objects in the method. Each thread has its own stack; therefore, the memory usage depends on the number of components running in parallel. |

###### Configuring heap memory

You can set the minimum and maximum memory heap sizes by adjusting the `-Xms` and `-Xmx` JVM arguments. Since CloverDX Server consists [of two standalone JVMs](architecture.md): the **Core** and the **Worker**, the heap limits need to be configured individually for each. The recommended maximum heap values are included in the [Recommended Server Core and Worker heap memory configuration](postinstallation-configuration.md#recommended-server-core-and-worker-heap-memory-configuration) section below.

To set the initial and maximum limits for the **Core** and **Worker** processes, add the arguments in the following places, and **make sure to restart CloverDX Server or Worker for the changes to take effect:**

| JVM | OS | Config location | Example |
| --- | --- | --- | --- |
| **Core** | Linux | *setenv.sh* | `export CATALINA_OPTS="$CATALINA_OPTS -Xms8192m -Xmx15g"` |
| Windows - manual | *setenv.bat* | `set "CATALINA_OPTS=%CATALINA_OPTS% -Xms8192m -Xmx15g"` |  |
| Windows - service | *Apache Commons Daemon Service Manager* | Populate the **Initial memory pool** and **Maximum memory pool** fields at the bottom of the *Java* tab. |  |
| **Worker** | Populate the **Initial heap size** (MB) and **Maximum heap size (MB)** amounts under **Configuration > Setup > [Worker](setup.md#worker)** in the Server Console. |  |  |

###### Recommended Server Core and Worker heap memory configuration

The optimal distribution of main memory between the Server Core and Worker depends on the nature of executed tasks. The recommended defaults of Server Core heap size and Worker heap size for different RAM sizes are in the table below.
> [!NOTE]
> To ensure optimal performance and reliability, the server hosting CloverDX Server should be fully dedicated to this purpose. No other applications, such as databases, web servers, or third-party services, should be installed or running on this server. This approach helps prevent resource competition, where multiple applications demand critical CPU, memory, and disk I/O simultaneously, which can lead to performance bottlenecks, increased latency, or may cause CloverDX Server to stop running or become unresponsive.

It is important to note that the heap limit is *not* a limit of the full memory used by the JVM. Additional memory is required for other areas such as [direct memory](optional-server-installation-steps.md#maximum-cached-buffer-size) or [Metaspace](optional-server-installation-steps.md#metaspace). **We recommend that the combined maximum heap sizes of both the Core and Worker processes do not exceed 75% of the system’s total memory**, to leave space for the operating system and other JVM memory spaces.

| RAM Size | Max Server Core Heap | Max Worker Heap | Remaining for OS (estimated) |
| --- | --- | --- | --- |
| 4 GB | 1 GB | 1 GB | 1 GB |
| 8 GB | 2 GB | 3 GB | 2 GB |
| 16 GB | 4 GB | 7 GB | 3 GB |
| 32 GB | 7 GB | 15 GB | 5 GB |
| 64 GB | 8 GB | 40 GB | 8 GB |
| 128 GB | 8 GB | 95 GB | 16 GB |

While we do not prescribe specific `-Xms` values (initial heap size), the general recommendation is to set `-Xms` equal to `-Xmx`. This approach avoids dynamic heap resizing during runtime, which can reduce garbage collection overhead and lead to more stable and predictable performance. However, setting a large initial heap size can also increase memory usage, limit flexibility, or delay startup time. Therefore, this setting should be evaluated in the context of your specific workload, resource availability, and performance requirements. If you’re unsure what value to use, a practical starting point is to set `-Xms` to half of `-Xmx` and observe how the application behaves under the expected load. You can then adjust as needed based on performance and memory utilization.

##### Reflective access

Some libraries require reflective access to function properly. Reflective access needs to be enabled by command-line arguments. For the **Worker, these arguments are added automatically**. However, for the **Core**, they need to be enabled manually by adding the following arguments:

**Linux:**

- Add the arguments below to the the `setenv.sh` file, located in the `bin` directory of your Tomcat installation.
  export JAVA_OPTS="$JAVA_OPTS \ --add-opens=jdk.management/com.sun.management.internal=ALL-UNNAMED \ --add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED \ --add-opens=java.base/javax.net.ssl=ALL-UNNAMED \ --add-opens=java.base/java.lang=ALL-UNNAMED \ --add-opens=java.base/java.lang.reflect=ALL-UNNAMED \ --add-opens=java.base/java.nio=ALL-UNNAMED \ --add-opens=java.base/java.nio.file=ALL-UNNAMED \ --add-opens=java.base/sun.nio.fs=ALL-UNNAMED"

**Windows:**

- Add the arguments below to the `setenv.bat` file, located in the `bin` directory of your Tomcat installation.
   set JAVA_OPTS=%JAVA_OPTS% ^ "--add-opens=jdk.management/com.sun.management.internal=ALL-UNNAMED" ^ "--add-opens=java.xml/com.sun.org.apache.xerces.internal.dom=ALL-UNNAMED" ^ "--add-opens=java.base/javax.net.ssl=ALL-UNNAMED" ^ "--add-opens=java.base/java.lang=ALL-UNNAMED" ^ "--add-opens=java.base/java.lang.reflect=ALL-UNNAMED" ^ "--add-opens=java.base/java.nio=ALL-UNNAMED" ^ "--add-opens=java.base/java.nio.file=ALL-UNNAMED" ^ "--add-opens=java.base/sun.nio.fs=ALL-UNNAMED"

**Windows service:**

- Add all the arguments to the *Java Options* section on the *Java tab* in the *Apache Commons Daemon Service Manager* individually, one argument per line.

##### Garbage collector for Worker

We recommend using the G1 garbage collector for the Worker process. No configuration is necessary thanks to G1 being the default JVM garbage collector.

If you want to configure the garbage collector yourself, you can do so using the [worker.jvmOptions](list-of-properties.md#lop-worker-jvmoptions) property.

See also [Enabling GC logging](../operations/diagnostics.md#tweaking-garbage-collection-logging).

##### Maximum number of open files

When using resource-demanding components, such as **FastSort**, or when running a large number of graphs concurrently, you may reach the system limit on simultaneously open files. This is usually indicated by the `java.io.IOException: Too many open files` exception.

The default limit is fairly low in many Linux distributions (e.g. 4,096 in Ubuntu). Such a limit can be easily exceeded, considering that one **FastSort** component can open up to 1,000 files when sorting 10 million records. Furthermore, some application containers recommend increasing the limit themselves.

Therefore, it is recommended to increase the limit for production systems. Reasonable limits vary from 10,000 to about 100,000, depending on the expected load of **CloverDX Server** and the complexity of your graphs.

The current limit can be displayed in most UNIX-like systems using the `ulimit -Sn` command.

The exact way of increasing the limit is OS-specific and is beyond the scope of this manual.

##### Maximum number of processes or threads

If you run graphs with many subgraphs containing many components, you may reach the limit on the number of threads per user or per system. In this case, you can find `java.lang.OutOfMemoryError: unable to create new native thread` in a graph’s log.

The current limit on number of processes/threads per user can be displayed in most UNIX-like systems using the `ulimit -Su` command. Note that the documentation on `ulimit` may not distinguish between processes and threads. The limit on number of threads per system can be displayed using the `sysctl kernel.threads-max` command. The exact way of increasing the limit is OS-specific and is beyond the scope of this manual.

##### Firewall exceptions

In order to function properly, **CloverDX Server** requires both incoming and outcoming communication. Please, configure your firewall exceptions accordingly.

| Traffic | Communication | Description & Components |
| --- | --- | --- |
| **Incoming** | HTTP(S) | Communication between Designer and Server |
| JMX | Tracking and debugging information |  |
| **Outgoing (depending on actual usage)** | JDBC | Connection to databases (DatabaseReader, DatabaseWriter, DBExecute) |
| JMS | Receiving and sending JMS messages (JMSReader, JMSWriter, JMS Listener) |  |
| HTTP(S) | Requesting and receiving responses from servers (Readers, WebserviceClient, HTTPConnector) |  |
| SMTP | Sending data converted into emails (EmailSender) |  |
| IMAP/POP3 | Receiving emails (EmailReader) |  |
| FTP/SFTP | Remote file reading and writing (readers, writers) |  |

##### Reverse proxy configuration

CloverDX Server instance can run behind an HTTP proxy that provides services such as logging, SSL termination, caching, load balancing, access control, etc. However, the proxy may interfere with some parts of the CloverDX Server Console. For instance, the endpoint URL for Data Services will not show the public URL used in the web browser, but the internal URL of the CloverDX Server instance, as seen by the proxy. That is because the Data Service endpoint URL is constructed from the incoming request and the request no longer comes from the client but from the proxy.

As a workaround, you may configure the proxy to override the URL using the following HTTP headers:
`X-Forwarded-Proto`
URL scheme (protocol), e.g. "https"
`X-Forwarded-Host`
the hostname (and optionally, the port), e.g. "my-proxy-host:80"
`X-Forwarded-Port`
the port number, overrides X-Forwarded-Host, e.g. "80"
`X-Forwarded-Prefix`
the context path including the leading slash, e.g. "/mycontext"

The following snippets show configuration examples for commonly used proxy servers.
Example 1. Apache HTTP Server proxy configuration

```apacheconf
# Requires mod_proxy module
<Location "/mycontext">
    # Enable proxy
    ProxyPass "http://cloverdx-svc:8080/clover"
    # Pass "Host" header value; alternatively, set X-Forwarded-Host
    ProxyPreserveHost On
    # Fix "Location" response headers in redirects
    ProxyPassReverse "http://cloverdx-svc:8080/clover"

    # Add "X-Forwarded-Proto" header when running as a SSL terminator
    #RequestHeader set X-Forwarded-Proto "https"

    ### Only necessary when changing the context path from "/clover" to something else:
    # Add "X-Forwarded-Prefix" header to override the context path
    RequestHeader set X-Forwarded-Prefix "/mycontext"
    # Fix path in "Set-Cookie" headers
    ProxyPassReverseCookiePath "/clover" "/mycontext"
</Location>
```

Example 2. NGINX proxy configuration

```nginx
events {
}

http {

  server { # simple reverse-proxy
    listen       80;

    location /mycontext {
        # Enable proxy
        proxy_pass          http://cloverdx-svc:8080/clover;
        # Pass "Host" header value; alternatively, set X-Forwarded-Host
        proxy_set_header    Host $http_host;
        # Fix "Location" response headers in redirects
        proxy_redirect      http://$http_host/clover http://$http_host/mycontext;

        # Add "X-Forwarded-Proto" header when running as a SSL terminator
        #proxy_set_header   X-Forwarded-Proto https

        ### Only necessary when changing the context path from "/clover" to something else:
        # Override context path
        proxy_set_header    X-Forwarded-Prefix /mycontext;
        # Fix path in "Set-Cookie" headers
        proxy_cookie_path   /clover /mycontext;
    }

  }

}
```

###### Overwriting the headers at the proxy

Have the proxy **set**`X-Forwarded-Host` and `X-Forwarded-Prefix` rather than pass on whatever arrived with the request, as the examples above do with `RequestHeader set` and `proxy_set_header`.

Proxies and load balancers commonly manage `X-Forwarded-For` and `X-Forwarded-Proto` by themselves while leaving these two alone, so a value the client sent reaches the application untouched. Most applications ignore it; CloverDX Server does not. Besides the URLs shown in the Console, it builds the OAuth2 callback and the address that identifies the [MCP Server](server-config-mcp.md) in the access tokens it issues from the same request, so whoever sets the header decides more than what a URL looks like on screen.

##### Redirecting the OAuth2 discovery documents

A client of the [CloverDX MCP Server](server-config-mcp.md) works out where to authenticate from the endpoint URL alone. It derives the address of the authorization server metadata and looks for it at the **root of the host**, above the servlet context CloverDX is deployed under – `https://your-server.example.com/.well-known/oauth-authorization-server/clover/mcp`. A web application cannot answer above its own context, so the container, or the reverse proxy in front of it, has to redirect such a request into the context. Without that redirect, discovery stops at the first step and no MCP client connects.

A Server installed from the CloverDX Tomcat bundle or from the Designer+Server installer, and a Server run from the CloverDX Docker image, answer there with nothing configured by hand. Set the redirect up yourself only when you deploy `clover.war` into a container of your own, or when a reverse proxy stands in front.
> [!TIP]
> To check a deployment, request `http://your-server.example.com:8080/.well-known/oauth-authorization-server/clover/mcp`. It should answer `302` pointing at `/clover/mcp/.well-known/oauth-authorization-server`, and that address should return the metadata document.

###### In your own Tomcat

1. Take `rewrite.config` from the Server distribution you downloaded – it ships alongside `clover.war`, so the rules are never written by hand.
2. Copy it into `[Tomcat_home]/conf/Catalina/localhost/` – the **Engine** and **Host** names of a default Tomcat installation.
3. Declare the valve on that **Host** in `[Tomcat_home]/conf/server.xml`:
   ```xml
   <Valve className="org.apache.catalina.valves.rewrite.RewriteValve" />
   ```
4. Restart Tomcat.

The valve has to sit on the **Host**, not on the web application: the request never reaches a servlet context, so a context-level valve would not run. The rules take the context out of the request, so nothing in the copied file is edited – the same file serves any context, `/clover` and a Server deployed as the root application alike.

###### On a reverse proxy

A deployment behind a reverse proxy can put the redirect there instead, and then the container needs neither the valve nor the file. Reproduce the two rules CloverDX ships:

```ctl
RewriteRule ^/\.well-known/(oauth-authorization-server|oauth-protected-resource)((?:/.+?)?/mcp)(/.+)$ $2/.well-known/$1$3 [R=302,L]
RewriteRule ^/\.well-known/(oauth-authorization-server|oauth-protected-resource)((?:/.+?)?/mcp)$ $2/.well-known/$1 [R=302,L]
```

> [!CAUTION]
> Match the two OAuth2 documents by name, as the rules above do. A blanket rule over the whole `/.well-known/` namespace also captures the ACME challenge and breaks certificate renewal on any host that renews its certificates automatically.
> [!NOTE]
> ![arrow](../figures/arrow.png) Continue with: [System database configuration](examples-db-connection-configuration.md)
