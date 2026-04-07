<!-- Administration > Configuration > Server configuration > Server configuration via Setup module -->

### Server configuration via Setup module

While it is possible to configure **CloverDX Server** by modifying the [configuration file](setup.md#configuration-file) in a text editor, the **Setup** with a user-friendly GUI offers a much easier way of configuring basic properties according to your preferences and requirements. Setup is accessible from **Server Console** under **Configuration > Setup**.
> [!IMPORTANT]
> To access the Setup section, you need the [Server Setup permission](groups.md#permission-server-setup).

The Setup module consists of multiple tabs that allow you to configure the following:

| [Configuration file](setup.md#configuration-file) |
| --- |
| [License](setup.md#license) |
| [System database connection](setup.md#system-database) |
| [Worker](setup.md#worker) |
| [Data Manager connection](setup.md#data-manager) |
| [Sandbox paths](setup.md#sandboxes) |
| [Encryption](setup.md#encryption) |
| [E-mail](setup.md#e-mail) |
| [LDAP connection](setup.md#ldap) |
| [Cluster configuration](setup.md#cluster) |
| [OAuth2 authentication](setup.md#oauth2-authentication) |
> [!TIP]
> To keep your settings and data in the case of a database migration (e.g., from evaluation to production environment), see [Server Configuration Migration](server-config.md).

#### Before you start

Before using the Setup module, you must specify the path to the configuration file where Setup saves the configuration, and add the required libraries to the classpath.

1. **Specify the path to the configuration file**
   Setup uses the configuration file to save the Server’s settings. The path to the file is specified by the [`clover.config.file`](list-of-properties.md#lop-config-file) system property.
   If you used a CloverDX bundle, one of our [cloud marketplace offerings](server-in-cloud-marketplaces.md), or the [official Docker image](docker-install.md) to build your Server environment, the configuration file is already created and preconfigured with default settings.
   If you used a fresh standalone Tomcat installation, you will need to create the configuration file first and point the Server to it. Until this is done, you will not be able to make any changes in the Setup module.
   If you start the Server without configuration, you will see decorators pointing to the Setup. The decorators mark problems that require your attention. The displayed number corresponds to the number of items.
   The [**Configuration File tab**](setup.md#configuration-file) provides step-by-step instructions for creating and configuring the file.
   ![setup empty](../figures/setup-empty.png)
   *Figure 121. Setup GUI with decorators*
2. **Add libraries to the classpath**
   Next, place the libraries required for further configuration in the application server’s classpath. For Tomcat, place the files in the `<TOMCAT_INSTALL_DIR>/lib` directory. You will need:
   - A JDBC driver for the [system database connection](examples-db-connection-configuration.md).
   - If you plan to encrypt sensitive data in the configuration file using a custom encryption provider, add the provider’s `.jar` file to the classpath. See [Encryption](setup.md#encryption) for more information.
     > [!NOTE]
     > Make sure to restart the application server to load the newly added `.jar` files.
3. If you wish to encrypt the sensitive data in your configuration file, turn on the [**Encryption**](setup.md#encryption) feature.
4. **Configure individual features**
   Now, you can use the individual tabs in the Setup module to configure the desired Server features.
5. **Restart the Server (if needed)**
   Some changes require you to restart the Server. These changes are indicated by the ![cstatus RESTART REQ 24](../figures/cstatus_RESTART_REQ_24.png) icon. Other changes (e.g., License, Sandboxes, E-mail, LDAP) are applied immediately and do not require a restart.

#### Using Setup

The Setup page consists of a menu with tabs on the left, a main configuration part in the middle, and a section with configuration status and additional information on the right side.

**The main configuration part contains several buttons:**

- **Save** saves changes made to the configuration file. The changes in the configuration must be valid.
- **Save Anyway** saves the configuration even if it is invalid. For example, a database connection is considered invalid if a required library is missing.
- **Validate** validates the configuration on the current tab. If you see the **Save** button disabled, use **Validate** to validate the configuration first.
- **Discard Changes** discards unsaved changes and returns to currently used values.

If an error/warning icon appears, a status message on the right side of the Setup GUI will provide relevant details.

**The following decorators can appear in the Setup GUI:**

| Icon | Description |
| --- | --- |
| ![cstatus OK 24](../figures/cstatus_OK_24.png) | Configured tab |
| ![cstatus NOT CONFIGURED 24](../figures/cstatus_NOT_CONFIGURED_24.png) | Inactive tab |
| ![cstatus ERROR 24](../figures/cstatus_ERROR_24.png) | Error |
| ![cstatus WARNING 24](../figures/cstatus_WARNING_24.png) | Warning |
| ![cstatus RESTART REQ 24](../figures/cstatus_RESTART_REQ_24.png) | Restart required |
| ![pending changes](../figures/pending_changes.png) | Pending changes which have not been saved yet |

#### Configuration File

The **Configuration File** tab displays the content of the configuration file. For basic settings, you do not have to edit the content of the file manually. Instead, use the particular Setup tab to configure the corresponding features.

If you want to add advanced configuration properties, see [List of configuration properties](list-of-properties.md).
> [!TIP]
> Refer [here](example-configuration-file.md) for an example configuration file.

![setup configuration file](../figures/setup-configuration-file.png)
*Figure 122. Example of the Server Configuration file*

#### License

The **License** tab allows you to **view the details** of your currently loaded license(s) and to **add** or **remove** licenses as needed.

To see license details, click on the ![setup licenses dropdown arrow](../figures/setup-licenses-dropdown-arrow.png) dropdown button.

The panel on the right provides a summary of enabled features and their values (e.g., maximum number of CPU cores or Wrangler or Data Manager users) from all loaded licenses.

The license overview also displays the location of your licenses in the **Location** row:

- **Database**: licenses loaded into Server’s [system database](setup.md#system-database) display **Database**.
- **Directory**: licenses loaded from a license file or license directory display full path to the license file, e.g., `C:\Apache-Tomcat-10.1\Licenses\CLCSXCLOVE11927408SP`. See [`license.file`](list-of-properties.md#lop-license-file) and [`license.dir`](list-of-properties.md#lop-license-dir) configuration properties for more information on how to load licenses from files on a disk.
> [!IMPORTANT]
> If you load your license into the system database, when the database changes (e.g., when switching from the default Derby database used for evaluation purposes to one of the [recommended databases](system-requirements-for-cloverdx-server.md#system-database) for commercial use), you will need to load the license again into the new database.

![setup licenses](../figures/setup-licenses.gif)
*Figure 123. The License tab*

#### System database

If you used our [cloud marketplace offerings](server-in-cloud-marketplaces.md) to deploy your CloverDX Server environment, it already includes a pre-configured PostgreSQL system database.

For manual deployments, you need to create a database for CloverDX Server and add a user/role with appropriate rights before you set up the connection to the database in the server’s Setup GUI. Refer [here](system-requirements-for-cloverdx-server.md#system-database) for the list of supported databases and versions.
> [!TIP]
> CloverDX Server **requires a working database connection** to store license information. Therefore, it allows you to access the Setup and configure the connection **prior** to the Server **activation** - simply log into the Server Console and click the **Close** button. Otherwise, you would have to activate the server again after switching from the default Derby database to a new system database.

![setup server not activated](../figures/setup-server-not-activated.png)
*Figure 124. Server console without an active license*

The **Database** tab lets you configure the connection to the database. You can connect via:

- **JDBC**
  Under JDBC connection, choose your **Database** platfrom from the first drop-down list. This will enable you to choose a **Database URL** template from the second drop-down list. In this template (e.g., `jdbc:postgresql://host:5432/dbname` for PostgreSQL), replace the *host* and *dbname* keywords with proper values.
  Next, enter the **User name** and **Password** for your database.
  > [!NOTE]
  > An Apache Derby JDBC 4-compliant driver is bundled with CloverDX Server. The **Derby database** is intended for **for evaluation purposes only**. For commercial use, switch to one of the supported databases. When switching, add the appropriate JDBC-4 compliant driver to the classpath (i.e., for Tomcat, place the driver in the `<TOMCAT_INSTALL_DIR>/lib` directory) and restart the application server.

![setup database jdbc](../figures/setup-database-jdbc.png)
*Figure 125. Database connection configuration for a JDBC connection*

- **JNDI**
  With JNDI, you can access the datasource configured at the application server level. Select your **Database** platform and choose the suitable item from the JNDI tree. For more information on how to enable JNDI connections at the application server level, see [JNDI DB Datasource](jndi-datasource-config.md#jndi-db-datasource).

![setup database jndi](../figures/setup-database-jndi.png)
*Figure 126. Database connection configuration for a JNDI connection*

#### Data Manager

In this section, you can configure a Data Manager connection. For detailed instructions, see [Data Manager configuration](data-manager-administration.md#data-manager-configuration).

![DM config local](../figures/DM-config-local.png)

#### Worker

The **Worker** tab lets you configure properties for the Worker process. See [CloverDX Server architecture](architecture.md) for more information on the differences between the Server Core and Worker processes.

You can change the **Initial** and **Maximum heap size** for the Worker process, include additional **JVM arguments**, and set the **Port range** for Worker communication.

Changes in Worker configuration require a restart - click on **Finish jobs & restart** or **Restart now** to do so.

![setup worker](../figures/setup_worker.png)
*Figure 127. The Worker tab*

#### Sandboxes

The **Sandboxes** tab lets you configure a path to a directory used to store sandbox data. In a cluster environment, you can configure paths to [shared](../admin/cluster-setup-index.md#shared-sandbox), [local](../admin/cluster-setup-index.md#local-sandbox), and [partitioned](../admin/cluster-setup-index.md#partitioned-sandbox) sandboxes.

![setup sandboxes standalone](../figures/setup-sandboxes-standalone.png)
*Figure 128. Sandbox path configuration in a standalone environment*

![setup sandboxes cluster](../figures/setup-sandboxes-cluster.png)
*Figure 129. Sandbox path configuration in a cluster environment*

#### Encryption

To secure sensitive information entered in other Setup tabs, you can use the **Encryption** feature. When enabled, passwords entered in sections like *System Database* or *Email* are automatically saved in an encrypted form in the configuration file.

![setup config file encrypted](../figures/setup-config-file-encrypted.png)
*Figure 130. Configuration file with an encrypted value in jdbc.password.*

To enable encryption, select the **Enable encryption** check box and choose the desired **Encryption provider** (*SunJCE* or *Custom*) and **Encryption algorithm**. Among the default algorithms provided by SunJCE, `PBEWithHmacSHA512AndAES_256` is the strongest one. To encrypt currently unencrypted passwords, use the **Save & Encrypt** button.

Since the default algorithms are generally weaker, we **recommend** using [Bouncy Castle](https://www.bouncycastle.org/) - a free custom JCE (Java Cryptography Extension) provider offering a **higher strength of encryption**.
> [!NOTE]
> If you want to use a custom provider, the related library has to be added to the appserver classpath. For Tomcat, this means adding the file to the `<TOMCAT_INSTALL_DIR>/lib` directory.

![setup encryption](../figures/setup-encryption.png)
*Figure 131. Encryption configuration*

#### E-Mail

The **E-mail** tab lets you configure a connection to an SMTP server to allow CloverDX Server to [send email](../operations/tasks.md#send-an-email) reporting of the Server status or events on the Server, or send a notification to a newly created user.

You may authenticate the connection to an SMTP server via username and password or OAuth2. For OAuth2, you have to authorize the connection first by using the **Authorize** button.

If OAuth2 authentication is used in a cluster, all nodes must use an identical OAuth2 configuration. After the OAuth2 configuration is authorized by the **Authorize** button on any node, all cluster nodes will share the OAuth2 tokens automatically.
> [!NOTE]
> You can set the default sender address by populating the **Default sender** field.

![setup email](../figures/setup-email.png)
*Figure 132. E-mail configuration*

To make sure the configuration of the **Outgoing SMTP Server** is correct, you can send a **test email** from the **Test email** section at the bottom.

![setup email test email](../figures/setup-email-test-email.png)
*Figure 133. Test email section*

#### LDAP

The **LDAP** tab lets you use an existing LDAP database for user authentication. For detailed information on how to set up an LDAP connection, see [LDAP authentication](ldap-authentication.md).

![setup ldap](../figures/setup-ldap.png)
*Figure 134. LDAP configuration*

#### Cluster

The **Cluster** tab lets you configure clustering features. For more information on how to configure a cluster environment, see [Server cluster setup and configuration](cluster-setup-index.md).

In case your license does not allow clustering, the `Enable clustering` checkbox is grayed out, and the note `The license does not allow clustering.` appears at the top.

![setup cluster](../figures/setup-cluster.png)
*Figure 135. Cluster configuration*

#### OAuth2 authentication

The **OAuth2 authentication** tab lets you configure OAuth2 authentication for **REST API** and **Data services**. This authentication depends on a third party **Identity Provider** and information entered here contains properties of a client application created at the provider. The **REST API** and **Data services** consume access tokens which are verified with the used **Identity Provider**.

For more information on how to configure an OAuth2 authentication see [User OAuth2 authentication](oauth2-authentication.md).

If you allow OAuth2 authentication the **HTTP Basic** authentication for **REST API** and **Data services** will be disabled.

![setup oauth2](../figures/setup-oauth2.png)
*Figure 136. OAuth2 authentication*
