<!-- Development > Designer user interface > Common dialogs -->

## 7. Common dialogs

### URL file dialog

| [Local files](common-dialogs.md#local-files) |
| --- |
| [Workspace view](common-dialogs.md#workspace-view) |
| [CloverDX Server](common-dialogs.md#cloverdx-server) |
| [Hadoop HDFS](common-dialogs.md#hadoop-hdfs) |
| [Remote files](common-dialogs.md#remote-files) |
| [Port](common-dialogs.md#port) |
| [Dictionary](common-dialogs.md#dictionary) |
| [Filtering files and tips](common-dialogs.md#filtering-files-and-tips) |

The **URL File Dialog** serves to navigate through the file system and select input or output files.

In many components, you are asked to specify the URL of some files. These files can serve to locate the sources of data that should be read, the sources to which data should be written or the files that must be used to transform data flowing through a component and some other file URL. To specify the URL of such a file, you can use the **URL File Dialog**.

The **URL File Dialog** has several tabs on it.

#### Local files

The **Local files** tab serves to locate files on a local file system. The combo contains local file system places and parameters. It can be used to specify both **CloverDX projects** and any other local files.

![file url dialog 011](../figures/file-url-dialog-011.png)
*Figure 83. URL File Dialog - Local files*
> [!NOTE]
> Best practice is to specify the path to files with **Workspace view** instead of **Local view**. **Workspace view** with help of parameters provides you with better portability of your graphs.

#### Workspace view

**Workspace view** tab serves to locate files in a workspace of a local **CloverDX** project.

![file url dialog 010](../figures/file-url-dialog-010.png)
*Figure 84. URL File Dialog - Workspace view*

##### CloverDX Server

**CloverDX Server** dialog serves to locate files of all opened **CloverDX Server****projects**. Available only for **CloverDX Server** projects.

![file url dialog 013](../figures/file-url-dialog-013.png)
*Figure 85. URL File Dialog - CloverDX Server*

#### Hadoop HDFS

**Hadoop HDFS** tab serves to locate files on Hadoop Distributed File System.

![file url dialog 014](../figures/file-url-dialog-014.png)
*Figure 86. URL File Dialog - Hadoop HDFS*

You need a working [Hadoop connection](hadoop-connections.md) to choose the particular files.

#### Remote Files

The **Remote files** tab serves to locate files on a remote computer or on the Internet. You can specify properties of connection, proxy settings, and HTTP properties.

You can type the URL directly in the format described in [Supported file URL formats for Readers](examples-of-file-url-in-readers.md) or [Supported file URL formats for Writers](examples-of-file-url-in-writers.md), or you can specify it with a help of **Edit URL Dialog**. The **Edit URL Dialog** is accessible under the icon ![edit url dialog icon](../figures/edit_url_dialog_icon.png).

##### Edit URL Dialog

**Edit URL Dialog** lets you specify connection to a remote server in an easy way. Choose the protocol, specify a host name, port, credentials, and path.

The dialog lets you specify the connection using the following protocols:

- HTTP
- HTTPS
- FTP
- SFTP - FTP over SSH
- Amazon S3
- Azure Blob Storage
- WebDav
- WebDav over SSL
- Windows Share - SMB1/CIFS
- Windows Share - SMB 2.x, SMB 3.x

Click **Save** to save the connection settings. Click **OK** to use it.

The **Load** button serves to load a session from the list for subsequent editing.

The **Delete** button serves to delete the session from the list.

###### HTTP(S), (S)FTP, WebDav, and SMB

If the protocol is HTTP, HTTPS, FTP, SFTP - FTP over SSH, WebDav, WebDav over SSL, Windows Share - SMB1/CIFS or Windows Share - SMB 2.x or 3.x, the dialog allows you to specify the host name, port, username, password, and path on the server. It allows you to connect anonymously as well, if anonymous access if configured on the provider’s side.
> [!NOTE]
> Due to the upgrade of the SMBJ library in **CloverDX version 6.2**, anonymous access using SMB protocol version 2 or 3 will no longer work unless your Samba server is configured to stop requiring message signing. If turning off message signing is not an option, you can create a user without a password to use in the URL as a workaround. See below for example URLs:
> `smb2://domain%3Buser@server/path/`
> `smb2://domain%3Buser:@server/path/`

###### SFTP certificate in CloverDX

If you are reading from or writing into remote files and are connected via an SFTP protocol using a certificate-based authorization, you should do one of the following:

**Option 1**: Create an OpenSSH configuration file and specify the path to it in the Preferences (in the Designer go to Window > Preferences) as per the screenshot below. The configuration file can hold multiple configurations for different hosts.

![configuration cloverdx 0011](../figures/configuration-cloverdx-0011.png)
*Figure 87. Configuration of OpenSSH file location*

**OPTION 2:** Create a directory named `ssh-keys` in your project, and put the private key files into this directory and choose a suitable filename with the `.key` suffix. Listed in order from the highest to lowest priority when resolving, the private key file can have the following names:

1. `username@hostname.key`
2. `hostname.key`
3. `*.key` (the files are resolved in alphabetical order).
> [!NOTE]
> CloverDX attempts to establish a connection using only the most specific key found. Other keys are ignored.
> [!TIP]
> If you want to explicitly select a certificate for a specific location, the best way is to use the name with the highest priority, i.e. `username@hostname.key`. In such a case, if the connection succeeds, other keys are ignored.

Figure below shows the format of the OpenSSH private key generated by `ssh-keygen`.

![ssh key examp](../figures/ssh_key_examp.png)
*Figure 88. Example of enerated OpenSSH private key*

###### Passphrase for OpenSSH private key

In case your SSH private key is protected by passphrase you can specify this passphrase in the **CloverDX Designer** configuration. These settings are applied when you are using **Designer** dialogs or running jobs in **Runtime**.

Each passphrase has to be specified on a separated line in a format `[key identity]=[passphrase]`. Setup of a correct key identity depends on how is your private key defined.

Option 1: If you are using OpenSSH configuration file check its content.

```bash
Port 22
Host myserver.dev
	User test
	IdentityFile ~/.ssh/private.key
```

Here the identity is `test@myserver.dev` or `myserver.dev`. If there is no user specified the identity is `myserver.dev`.

OPTION 2: If your private key is stored in project’s directory `ssh-keys` its identity is the filename without the suffix `.key`.

###### URL syntax for FTP proxy

**CloverDX** is able to connect to FTP proxy using the following URL syntax:

`ftp://username%40proxyuser%40ftphost:password%40proxypassword@proxyhost`

where:
`username`
Your login on the FTP server.
`proxyuser`
Your login on the proxy server.
`ftphost`
The hostname of the FTP server.
`password`
Your FTP password.
`proxypassword`
Your proxy password.
`proxyhost`
The hostname of the proxy server.

###### Amazon S3

In the case of the Amazon S3 protocol, the dialog allows you to fill in Access Key ID, Secret Access Key, bucket, and path. For better performance, you should fill in the corresponding region.

Having the connection specified, you can choose the particular file(s).

**Amazon S3 URL**

It is recommended to connect to S3 via *endpoint-specific* S3 URL: `s3://s3.eu-central-1.amazonaws.com/bucket.name/`. The end-point in URL should be the end-point corresponding to the bucket.

- The URL with a specific endpoint has a much better performance than the generic one (`s3://s3.amazonaws.com/bucket.name/`), but you can only access the buckets of the specific region.
- If you use the generic endpoint, the bucket region is determined automatically (cross-region access) at the cost of an extra request.

For list of regions and endpoints, see *[Amazon Simple Storage Service endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/s3.html)*.

When the S3 URL does not contain **Access Key ID** + **Secret Access Key** (e.g. `s3://s3.eu-central-1.amazonaws.com/bucket.name/path`), **CloverDX** automatically searches for credentials in the following sources (in this order):

1. **Java system properties** - `aws.accessKeyId` and `aws.secretAccessKey`
   The `aws.secretKey` property used by AWS SDK v1 is no longer recognized.
2. **Environment variables** - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`
   The short names `AWS_ACCESS_KEY` and `AWS_SECRET_KEY` are no longer recognized.
3. **Web identity token credentials** - `AWS_WEB_IDENTITY_TOKEN_FILE` and `AWS_ROLE_ARN` environment variables (or the `aws.webIdentityTokenFile` and `aws.roleArn` system properties)
4. **Credential profiles file at the default location** (`~/.aws/credentials`)
   shared by all AWS SDKs and the AWS CLI
5. **Credentials delivered through the Amazon ECS container service**
   the `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` environment variable must be set
6. **Instance profile credentials delivered through the Amazon EC2 metadata service**

For detailed information, see the [Default credentials provider chain](https://docs.aws.amazon.com/sdk-for-java/v2/developer-guide/credentials-chain.html) and [Read IAM role credentials on Amazon EC2](https://docs.aws.amazon.com/sdk-for-java/v2/developer-guide/ec2-iam-roles.html).
> [!TIP]
> These sources of credentials may be used for graph development in a local project; for example, set the `aws.accessKeyId` and `aws.secretAccessKey` Java system properties in the **VM parameters** of [Runtime configuration](../admin/designer-configuration.md#runtime-configuration) so that both graphs and the File URL dialog work in local projects when using S3 URLs without credentials.

###### Azure Blob Storage

Microsoft Azure Blob Storage is a cloud object storage service, similar to Amazon S3. **CloverDX** supports Azure Blob Storage since version 5.11.

There are multiple supported authentication schemes:

1. **Storage Shared Key**
   *[https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key](https://docs.microsoft.com/en-us/rest/api/storageservices/authorize-with-shared-key)*
   This authentication is the easiest to set up. It is similar to username/password authentication. You use the name of the storage account as the username and the Access Key as the password. The disadvantage is that all applications that use the Access Key have the same permissions.
   You can find the key here: *Azure Portal - Storage accounts - <storage account> - Access keys*
   ![azure blob access keys](../figures/azure-blob-access-keys.png)
   *Figure 89. Storage Account Access Keys*
   - `az-blob://[account]:[key]@[account].blob.core.windows.net/container/path`
     or
   - `az-blob://AccountName=[account]:AccountKey=[key]@[account].blob.core.windows.net/container/path`
     to avoid confusion with the Client Secret authentication.
     Note that the key must be URL-encoded before you can use it in the URL. The Edit URL dialog encodes the key automatically.
     **Example**
     Plain key: `XFqGQY9/FRBucrRKldxykYUp9WmnzFHR9to/w2sP9+fXoDAKoTfWvdUOAzcaS3Wnon9mIgRbPcudtlwsNPtwzQ==`
     Encoded key: `XFqGQY9%2FFRBucrRKldxykYUp9WmnzFHR9to%2Fw2sP9%2BfXoDAKoTfWvdUOAzcaS3Wnon9mIgRbPcudtlwsNPtwzQ%3D%3D`
2. **Client Secret**
   *[https://docs.microsoft.com/en-us/azure/container-registry/container-registry-authentication#service-principal](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-authentication#service-principal)*
   This authentication scheme allows fine-grained access control, because you can set different permissions for each application that uses your storage.
   First, create an "application" for your CloverDX processing in your Azure Active Directory: *Azure Portal - Azure Active Directory - App registrations*
   The authentication scheme uses three values: Tenant ID, Client ID (also called Application ID) and Client Secret.
   You can find the Tenant ID and Client ID in the **Overview** of your application.
   ![azure blob client secret 1](../figures/azure-blob-client-secret-1.png)
   *Figure 90. Tenant ID and Client ID*
   The Client Secret is in the **Certificates & secrets** section of your application.
   ![azure blob client secret 2](../figures/azure-blob-client-secret-2.png)
   *Figure 91. Certificates & secrets*
   Create a new secret and copy the **Value**, not the Secret ID.
   ![azure blob client secret 3](../figures/azure-blob-client-secret-3.png)
   *Figure 92. Client Secret*
   - `az-blob://TenantId=[TenantId]:ClientId=[ClientId]:ClientSecret=[ClientSecret]@[account].blob.core.windows.net`
     or just
   - `az-blob://[TenantId]:[ClientId]:[ClientSecret]@[account].blob.core.windows.net`
3. **Environment Variables**
   Instead of putting the authentication information into the URL, you can configure the connection using the environment variables below.
   The URL then contains only the storage account as a part of the host name:
   `az-blob://[account].blob.core.windows.net/container/path`
   - **Connection String**
     *[https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)*
     You can find the connection string next to your Access Key: *Azure Portal - Storage accounts - <storage account> - Access keys*
     - AZURE_STORAGE_CONNECTION_STRING
       **Example**`export AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;AccountName=[account];AccountKey=XFqGQY9/FRBucrRKldxykYUp9WmnzFHR9to/w2sP9+fXoDAKoTfWvdUOAzcaS3Wnon9mIgRbPcudtlwsNPtwzQ==;EndpointSuffix=core.windows.net"`
   - **Client Secret**
     See [Client Secret Authentication](common-dialogs.md#azure-blob-storage-client-secret).
     - AZURE_CLIENT_ID
     - AZURE_CLIENT_SECRET
     - AZURE_TENANT_ID
   - **Client Certificate**
     You can also set up certificates in the **Certificates & secrets** section of your application in Azure Active Directory.
     - AZURE_CLIENT_ID
     - AZURE_TENANT_ID
     - AZURE_CLIENT_CERTIFICATE_PATH
   - **Username and Password**
     - AZURE_CLIENT_ID
     - AZURE_USERNAME
     - AZURE_PASSWORD
4. **Managed Identity**
   If the application is deployed to an Azure host with *[Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview)* enabled, **CloverDX** will authenticate with that account.
   `az-blob://[account].blob.core.windows.net/container/path`
5. **Anonymous**
   If none of the above applies, **CloverDX** attempts to connect anonymously.
   Anonymous access must be explicitly enabled on the container. Clients can then read data from the container without authorization.
   `az-blob://[account].blob.core.windows.net/container/path`
   ![file url dialog 017](../figures/file-url-dialog-017.png)
   *Figure 93. URL File Dialog - Remote files*

#### Port

Serves to specify fields and processing type for port reading or writing. Opens only in components that allow such data source or target.

![file url dialog 018](../figures/file-url-dialog-018.png)
*Figure 94. URL File Dialog - Input Port*

![file url dialog 018b](../figures/file-url-dialog-018b.png)
*Figure 95. URL File Dialog - Output Port*

See also: [Input port reading](input-port-reading.md) or [Output port writing](output-port-writing.md)

#### Dictionary

**Dictionary** tab serves to specify dictionary key value and processing type for dictionary reading or writing. Opens only in components that allow such data source or target.

![file url dialog 019](../figures/file-url-dialog-019.png)
*Figure 96. URL File Dialog - Dictionary*

See also: [Using a dictionary in graphs](dictionary.md#using-a-dictionary-in-graphs)

#### Filtering Files and Tips

If you use **File URL Dialog** configured to display only some files according to the extension, you can see the **File Extension** below File URL.
> [!IMPORTANT]
> To ensure graph portability, forward slashes are used for defining the path in URLs (even on Microsoft Windows).
> [!NOTE]
> The **New Directory** action is available at the toolbar of **Workspace View** and the **Local Files** tab. F7 key can be used as a shortcut for the action. Newly created directory is selected at the dialog and its name can be edited in-line. Press F2 to rename the directory and DEL to delete it.

More detailed information of **URL**s for each of the tabs described above is provided in sections:

- [Supported file URL formats for Readers](examples-of-file-url-in-readers.md)
- [Supported file URL formats for Writers](examples-of-file-url-in-writers.md)

### Edit value dialog

The **Edit Value** dialog contains a simple text area where you can write the transformation code in **JMSReader** and **JMSWriter** components.

![edit value dialog 010](../figures/edit-value-dialog-010.png)
*Figure 97. Edit value dialog*

When you click the **Navigate** button in the upper left corner, you will be presented with the list of possible options. You can select either **Find** or **Go to line**.

![edit value dialog 020](../figures/edit-value-dialog-020.png)
*Figure 98. Find wizard*

If you click the **Find** item, you will be presented with another wizard. In it, you can type the expression you want to find (**Find** text area), decide whether you want to find the whole word only (**Whole word**), whether the cases should match or not (**Match case**) and the **Direction** in which the word will be searched - downwards (**Forward**) or upwards (**Backward**). These options must be selected by checking the respective checkboxes or radio buttons.

If you click the **Go to line** item, a new wizard opens in which you must type the number of the line you want to go to.

![edit value dialog 030](../figures/edit-value-dialog-030.png)
*Figure 99. Go to Line wizard*

### Open Type dialog

This dialog serves to select some class (**Transform** class, **Denormalize** class, etc.) that defines the desired transformation. When you open it, type the beginning of the class name for required classes to appear in this wizard and select the right one.

![open type dialog 010](../figures/open-type-dialog-010.png)
*Figure 100. Open Type dialog*
