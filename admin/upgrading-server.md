<!-- Administration > Upgrade > Server manual upgrade -->

## 7. Server manual upgrade

### General notes on upgrade

- An upgrade of **CloverDX Server** requires downtime; plan a maintenance window.
- A successful upgrade requires about 30 minutes; rollback requires 30 minutes.
- Perform the steps below in a development/testing environment first before moving onto a production environment.

### Upgrade prerequisites

- Having a new **CloverDX Server** web application archive (`clover.war` appropriate for the application server used) & license files available (licenses for the version you are upgrading to or newer).
- Having [release notes](https://support.cloverdx.com/releases/) for the particular **CloverDX** version available (and all versions between current and intended version to be upgraded to).
- Having the graphs and jobs updated and tested with regards to known issues & compatibility for the particular **CloverDX** version.
- Having the **CloverDX Server** configuration properties file externalized from default location, see [Configuration sources](configuration-sources.md).
- Standalone database schema where **CloverDX Server** stores configuration, see [System database configuration](examples-db-connection-configuration.md).
- Having a separate sandbox with a test graph that can be run at any time to verify that **CloverDX Server** runs correctly and allows for running jobs.

### Upgrade instructions

1. Suspend all sandboxes, wait for running graphs to finish processing.
2. Shut down the **CloverDX Server** application (or all servers, if they run in a Cluster mode).
3. Back up the existing **CloverDX** database schema.
4. Back up the existing **CloverDX** web application archive (`clover.war`) & license files (on all nodes).
5. Back up the existing **CloverDX** sandboxes (on all nodes).
6. Re-deploy the CloverDX Server web application. Instructions how to do that are application server dependent - see [Production Server](production-server.md) for installation details on all supported application servers. After the re-deployment, your new server will be configured based on the previous version’s configuration.
7. Replace old license files with the valid ones (or you can later use the web GUI form to upload new license). The license file is shipped as a text containing a unique set of characters. If you:
   - received the new license as a file (`*.dat`), then simply use it as new license file.
   - have been sent the license text, e.g. inside an email, then copy the license contents (i.e. all text between `Company` and `END LICENSE`) into a new file called `clover-license.dat`. Next, overwrite the old license file with the new one or upload it in the web GUI.
   For details on license installation, see [Activation](production-server.md#activation).
8. Start **CloverDX Server** application; in a Cluster environment start just one of the nodes. Wait until **CloverDX Server** is accessible (i.e., you can log in).
   - If any changes to the database schema are necessary, the new server will automatically make them when you start it for the first time. Since this operation could be dangerous as there is a chance the update might fail and damage the system database, the start of the server is suspended and a confirmation dialog is displayed.

![upgrade server confirm dialog](../figures/upgrade-server-confirm-dialog.png)
*Figure 58. Confirm dialog*

- You are presented with 2 options:
  1. Make a database backup and proceed with the update by typing in "*backup completed*" and clicking on **Proceed**.
  2. Cancel the update. In this case, the database is not modified and the server fails to start. You must stop the application server the CloverDX Server is running on and deploy the previous version of CloverDX Server (clover.war).

![upgrade server cancel dialog](../figures/upgrade-server-cancel-dialog.png)
*Figure 59. Cancel dialog*
> [!TIP]
> In a cluster, the confirmation is needed only on one node.
> [!TIP]
> The approval can be skipped by setting the server property [`autoapply.sys.db.patches`](list-of-properties.md#lop-autoapply-sys-db-patches) to the version you are upgrading to or newer.

#### Postupgrade checklist

1. Review the contents of all tabs in the **CloverDX Server** Console, especially scheduling and event listeners.
2. Update graphs to be compatible with the particular version of **CloverDX Server** (this should be prepared and tested in advance).
3. Resume the test sandbox and run a test graph to verify functionality.
4. Resume all sandboxes.

#### Upgrade from 4.8.x or earlier to 4.9.x or later
> [!IMPORTANT]
> Significant architectural change in version 4.9.0
> By default since 4.9.0, jobs (graphs, jobflow, data services) are executed in a standalone JVM called [Worker](architecture.md#cloverdx-worker).
>
> To run jobs in the Server Core (i.e. in the same way as in earlier versions of **CloverDX Server**), you can disable execution in Worker for [particular jobs or sandboxes](../developer/jobconfig.md#job-config-property-worker-execution) or [disable Worker completely](list-of-properties.md#lop-worker-initialworkers).

#### Configuration changes

Worker is the executor of jobs, all jobs run in the Worker by default. It runs in a separate process (JVM), so it requires configuration in addition to the Server Core.

The Worker’s configuration relates to memory size, classpath, command line options and JNDI. For an overview of Worker related configuration, see [Introduction to Worker configuration](architecture.md#configuration). The introduction provides an overview of the new Worker specific configuration with links to details.

With Worker, [new configuration properties](list-of-properties.md#worker-configuration-properties) were introduced to set up various parameters (timeouts, heap size, etc.). These properties can be added to the [properties file](setup.md#configuration-file).

You should split the main memory used by the Server between the Server Core and Worker. Generally, Worker would require more memory than the Server Core as it runs graphs.

The command line arguments and parameters, you were used to add to the Server Core command line in earlier versions, should be added to the Worker’s command line, too.

Libraries added to the Server Core classpath should be added to the classpath of Worker. The place to copy these libraries is the `${clover.home}/worker-lib` directory.

#### Changes to jobs

If your jobs (DX graphs, jobflows, etc.) use JNDI for database or JMS connections, you need to configure JNDI on Worker (see [JNDI in worker](list-of-properties.md#worker-jndi-properties)). You might also need to update your jobs to use the new JNDI resources configured in Worker - they might be available on new JNDI paths. If you do not need these JNDI resources on the Server Core anymore, consider removing them from the Server Core.

### Rollback instructions

1. Shut down the **CloverDX Server** application.
2. Restore the **CloverDX Server** web application (`clover.war`) & license files (on all nodes).
3. Restore the **CloverDX Server** database schema.
4. Restore the **CloverDX** sandboxes (on all nodes).
5. Start the **CloverDX Server** application (on all nodes).
6. Resume the test sandbox and run a test graph to verify functionality.
7. Resume all sandboxes.
> [!IMPORTANT]
> **Evaluation version** - a mere upgrade of your license is not sufficient. When moving from an evaluation to production server, you should not use the default configuration and database. Instead, take some time to configure **CloverDX Server** so that it best fits your production environment.
