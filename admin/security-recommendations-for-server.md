<!-- Administration > Installation > Server installation > Post-installation best practices -->

### Post-installation best practices

To improve security of **CloverDX Server**, you should:

- Change the default password for **clover** user. Without changing the password, everybody would be able to log in as **clover**. See [Change credentials](users.md#change-credentials).
- Create a user different from **clover** and add it to the **admin** group. If there are more administrators, create a user account for each. See [Users](users.md).
- Set the **master password**. Without the master password, you cannot use secure parameters. See [Securing job parameters in Server](secure-parameters.md).
- Run **CloverDX Server** with privileges of an ordinary user, e.g. create a system account `clover` used only for running **CloverDX Server**. Do not run **CloverDX Server** under the **root** account.
- The communication with a system database may be unencrypted. Consider encrypting the connection to system database too.
- If a database provides you with a root/admin account, do not use this account for **CloverDX Server**. Create a separate database user account, e.g. **clover**.
- [Configure **CloverDX Server** to run on HTTPS](https-server-config.html). If you communicate over HTTP, your data is sent unencrypted and eavesdroppers can easily see it.
- Disable the HTTP API if you do not need it. See [Simple HTTP API](../operations/simple-http-api.md).
- In Data Services, put KeyStores outside a sandbox and run the service on HTTPS. If you have a KeyStore in a sandbox, a user with write permissions could replace it with another KeyStore. [HTTPS Connectors](../operations/data-services.md#https-connectors).
- Enable **user lockout** after repeated failed login attempts. If you use this feature in Cluster, make sure that all Cluster nodes have the same lockout configuration. See [User lockout](user-lockout.md)
