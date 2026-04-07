<!-- Administration > Installation > Server installation > System requirements -->

### System requirements

#### Hardware requirements

This section outlines the hardware requirements for deploying CloverDX Server in standalone and cluster configurations.

##### Standalone Server environment

The following table shows hardware requirements for standalone **CloverDX Server** environments.

| Hardware | Minimum | Recommended |
| --- | --- | --- |
| RAM | 8 GB | 32 GB |
| Processors | 2 cores [[1]](system-requirements-for-cloverdx-server.md#system-requirements-fn-cores) | 8 cores [[1]](system-requirements-for-cloverdx-server.md#system-requirements-fn-cores) |
| Disk space (installation) | 2 GB |  |
| Disk space (temp space) | > 25 GB [[2]](system-requirements-for-cloverdx-server.md#system-requirements-fn02) |  |
| Disk space (data) | > 50 GB [[2]](system-requirements-for-cloverdx-server.md#system-requirements-fn02) |  |

| 1 | A CPU core in this context is a **logical core**. Most modern processors use simultaneous multi-threading (called Hyper-Threading by Intel) and the number of logical cores is double the number of physical cores. See [CPU recommendations](system-requirements-for-cloverdx-server.md#cpu-recommendations) below for more information. |
| --- | --- |

| 2 | Minimum value, the disk space requirements depend on data and the processes you run on CloverDX Server. High-volume processes may require more storage even though their compute requirements may be the same. |
| --- | --- |

##### Server cluster environment

The hardware requirements for standalone Server environments also apply to individual **Server nodes in a cluster**. When [setting up a cluster](cluster-setup-index.md), ensure that all cluster nodes have the same hardware configuration and each node has at least 50 GB of disk space reserved for [shared sandboxes](cluster-setup-index.md#shared-sandbox). Additionally, keep in mind that the total number of CPUs specified in the Server license represents the combined total of logical CPUs across all server nodes.

##### CPU recommendations

**Non-production environments** with low job volumes or no resource-demanding tasks can often suffice with a minimum of **2 logical CPU cores**. This configuration can provide adequate performance for development, testing, or staging purposes.

However, for **production environments** or those **handling heavy workloads**, **8 logical CPU cores** are generally recommended as a baseline. This configuration offers more processing power, allowing for efficient execution of demanding tasks and maintaining optimal system performance.

It’s important to note that these are general guidelines. The ideal number of CPU cores can vary significantly based on specific factors such as:

- *Job complexity*: The nature and resource requirements of the tasks being processed.
- *Workload intensity*: The volume and frequency of jobs.
- *Other system resources*: The availability of memory, storage, and network bandwidth.

To determine the optimal number of CPU cores for your environment, carefully evaluate your specific needs and consider factors such as performance benchmarks, historical data, and future projections. Consulting with system experts or using performance monitoring tools can also provide valuable insights.

Note that your CloverDX Server license includes information regarding the maximum number of CPU cores that the Server can utilize. This **licensing restriction** is an additional factor to consider when determining the appropriate number of CPU cores for your deployment. Please refer to your licensing agreement for specific details or reach out to your account manager for further information.

#### Software requirements

**CloverDX Server** requires a compatible operating system, an application server, Java Development Kit (JDK) and a database to run. Together, these requirements are called a **stack**. Not all combinations of supported vendors or software product versions are supported by **CloverDX Server**. This section provides details about the supported configurations of software dependencies for **CloverDX Server**.

At the same time, **CloverDX Server** can be deployed in different circumstances - either as a production instance, as a test/non-production instance, or as an evaluation instance. Production instances must follow software stacks as described below to ensure full support and maximum stability of the platform.
> [!NOTE]
> Using unsupported configurations may lead to unexpected behavior, errors, or instability within your **CloverDX** deployment. Adhering to the officially supported stacks and database versions ensures a reliable and functional **CloverDX** environment.
>
> Note that **CloverDX Server** requires a Java Development Kit (JDK) to run. JRE is not supported.

##### Production deployment

###### Operating system, application server and Java

For production deployments, CloverDX supports following basic configurations - one is fully open-source, while others are built on top of commercial software:

| Operating system | Application server | JDK vendor and version |
| --- | --- | --- |
| **Ubuntu 22 LTS or Ubuntu 24 LTS** | [**Apache Tomcat 10.1.x (64 bit)**](production-server.md#apache-tomcat) | [**Eclipse Temurin JDK 21**](https://adoptium.net/temurin/releases/?arch=x64&package=jdk&version=21&os=linux&mode=filter) or [Eclipse Temurin JDK 17](https://adoptium.net/temurin/releases/?arch=x64&package=jdk&version=17&os=linux&mode=filter) |
| Red Hat Enterprise Linux 9 | Red Hat JBoss Web Server 6.0 | [Red Hat OpenJDK 21 or 17](https://developers.redhat.com/products/openjdk/) |
| Microsoft Windows Server 2025 Standard | [Apache Tomcat 10.1.x (64 bit)](production-server.md#apache-tomcat) | [Eclipse Temurin JDK 21](https://adoptium.net/temurin/releases/?arch=x64&package=jdk&version=21&os=windows&mode=filter) or [Eclipse Temurin JDK 17](https://adoptium.net/temurin/releases/?arch=x64&package=jdk&version=17&os=windows&mode=filter) |

Note that other combinations of JDK and application servers may not work at all or produce unexpected results.
> [!NOTE]
> When building a cluster of CloverDX Servers, we recommend using Linux as the base platform. Cluster performance may be lower on Microsoft Windows when SMB shares are used as shared drive for cluster nodes since it is required to disable caching on SMB to ensure all cluster nodes get consistent view of the file system.

###### System database

A system database stores CloverDX Server’s configuration and variety of logs. You can pick any of the databases mentioned in the list below (recommended option in bold). **We support only the listed major versions for each database below, but you can pick a different minor/bugfix version of each**. We use the exact version listed in our test environment.
> [!IMPORTANT]
> CloverDX Server relies critically on the integrity of its system database to ensure stable and reliable operation. Modifications to this database can lead to severe issues, including data corruption, data loss, feature disruptions, and upgrade failures. Such changes fall outside the scope of supported configurations and may limit the level of assistance our support team can provide. If you encounter database-related issues, contact [CloverDX Support](https://support.cloverdx.com/hc/request/new) before making any changes.

| Database provider | Supported major version | Tested version |
| --- | --- | --- |
| [**PostgreSQL**](postgresql.md) | **15** | **15.5** |
| [MySQL](mysql.md) | 8 | 8.0.25 |
| [Oracle](oracle.md) | 23 | 23.4.0 |
| [MS SQL Server](mssql.md) | 2022 | 16.0.4215.2 |

As you can see from the above, the preferred stack to use is **Ubuntu + Apache Tomcat + Temurin JDK 21 + PostgreSQL 15**. This stack uses open-source components and is, therefore, simple to install and run.

Other stacks use commercial components, which have additional commercial support available. Having both open-source and commercial stacks allows you to deploy CloverDX instances in a way that matches your organizational policies and requirements. Note that the above-mentioned commercial components come with their own support policies, outside of CloverDX policies. Ensure that you understand these additional policies before selecting any of the commercial stacks.

##### Non-production deployment

For your non-production deployments, you should generally follow the same configuration as for your production instances. This will ensure maximum compatibility between your instances. This is especially important during promotion of code from dev/test environments to your production.

Same technology requirements hold for non-production deployments as for production deployments. Usually, the non-production instances are smaller (e.g., 4 cores instead of 8) or do not have as high redundancy (e.g., 2-node cluster instead of 4).

##### Evaluation deployment

[Evaluation deployments](evaluation-server.md) are useful when you are trying new version of CloverDX Server to try a new feature, when evaluating CloverDX platform for the first time or during trainings etc.

To make the evaluation as simple as possible, we offer one more way of installing CloverDX Server - you can use it without an external system database. In such a case, CloverDX Server will use its own instance of Apache Derby database.

Additionally, evaluation instances can also be installed on other operating systems - Microsoft Windows 10 (64-bit), Microsoft Windows 11 (64-bit) or macOS 13 Ventura (*Apple Silicon* - M1, M2 or M3 CPUs only) and newer.

To make the installation as easy as possible, we offer a "bundle" which contains Apache Tomcat with already deployed CloverDX Server instance which is configured to use embedded Derby instance as its system database.

#### Supported web browsers for CloverDX web interfaces

CloverDX Server provides multiple different web interfaces - such as **Server Console** to manage the Server instance or various interfaces in **Business Tools** suite like Wrangler or Data Manager. These web apps are supported on following browsers (recommended option in bold):

- **Google Chrome** (latest)
- Mozilla Firefox (latest)

Using other recent browsers (e.g., Microsoft Edge or Apple Safari) should work but is not supported or recommended.
