<!-- Development > Component reference > Writers > Common properties of Writers > Supported file URL formats for Writers -->

#### Supported file URL formats for Writers

The **File URL** attribute lets you type in the file URL directly, or open the [URL file dialog](common-dialogs.md#url-file-dialog).

The URL shown below can also contain placeholders – a dollar sign or hash sign.
> [!IMPORTANT]
> Dollar and hash signs serve for different purposes.
>
> - **Dollar sign** should be used when each of multiple output files contains only a specified number of records based on the **Records per file** attribute.
> - **Hash sign** should be used when each of multiple output files only contains records corresponding to the value of specified **Partition key**.
>
> To ensure graph portability, forward slashes must be used when defining the path in URLs (even on Microsoft Windows).

Below are examples of possible URLs for **Writers**:

##### Writing to local files

- `/path/filename.out`
  Writes specified file on disk.
- `/path1/filename1.out;/path2/filename2.out`
  Writes two specified files on disk.
- `/path/filename$.out`
  Writes a number of files on disk. The dollar sign represents one digit. Thus, the output files can have the name range from `filename0.out` to `filename9.out`. The dollar sign is used when **Records per file** is set.
- `/path/filename$$.out`
  Writes a number of files on disk. Two dollar signs represent two digits. Thus, the output files can have the name range from `filename00.out` to `filename99.out`. The dollar sign is used when **Records per file** is set.
- `/path/filename#.out`
  Writes a number of files on disk. If **Partition file tag** is set to **Key file tag**, the hash sign in the file name is replaced with **Partition key** field value. Otherwise, the hash sign is replaced with number.
- `zip:(/path/file$.zip)`
  Writes a number of compressed files on disk. The dollar sign represents one digit. Thus, the compressed output files can have the names from `file0.zip` to `file9.zip`. The dollar sign is used when **Records per file** is set.
- `zip:(/path/file$.zip)!innerfolder/filename.out`
  Writes a specified file inside the compressed files on disk. The dollar sign represents one digit. Thus, the compressed output files containing the specified `filename.out` file can have the name range from `file0.zip` to `file9.zip`. The dollar sign is used when **Records per file** is set.
> [!NOTE]
> Path separator character `!` is supported since **CloverDX version 6.4**, and should be used instead of old separator character `#`. The old separator character is still supported for backward compatibility.

- `gzip:(/path/file$.gz)`
  Writes a number of compressed files on disk. The dollar sign represents one digit. Thus, the compressed output files can have the name ranges from `file0.gz` to `file9.gz`. The dollar sign is used when **Records per file** is set.
> [!NOTE]
> Although **CloverDX** can read data from a `.tar` file, writing to a `.tar` file is not supported.

##### Writing to remote files

- `ftp://user:password@server/path/filename.out`
  Writes a specified `filename.out` file on a remote server connected via an FTP protocol using username and password.
- `sftp://user:password@server/path/filename.out`
  Writes a specified `filename.out` file on a remote server connected via an SFTP protocol using a username and password.
  If a certificate-based authentication is used, certificates are placed in the `${PROJECT}/ssh-keys/` directory. For more information, see [SFTP certificate in CloverDX](common-dialogs.md#sftp-certificate-private-key).
  The certificate-based authentication has a URL without a password:
  `sftp://username@server/path/filename.txt`
- `zip:(ftp://username:password@server/path/file.zip)!innerfolder/filename.txt`
  Writes a specified `filename.txt` file compressed in the `file.zip` file on a remote server connected via an FTP protocol using username and password.
- `zip:(ftp://username:password@server/path/file.zip)!innerfolder/filename.txt`
  Writes a specified `filename.txt` file compressed in the `file.zip` file on a remote server connected via an FTP protocol.
- `zip:(zip:(ftp://username:password@server/path/name.zip)!innerfolder/file.zip)!innermostfolder/filename.txt`
  Writes a specified `filename.txt` file compressed in a `file.zip` file that is also compressed in a `name.zip` file on a remote server connected via an FTP protocol using username and password.
- `gzip:(ftp://username:password@server/path/file.gz)`
  Writes the first file compressed in a `file.gz` file on a remote server connected via an FTP protocol.
- `http://username:password@server/filename.out`
  Writes a specified `filename.out` file on a remote server connected via a WebDAV protocol using username and password.
- `s3://access_key_id:secret_access_key@s3.amazonaws.com/bucketname/path/filename.out`
  Writes to `path/filename.out` object located in the Amazon S3 web storage service in a bucket `bucketname` using an access key ID and secret access key.
  See [Amazon S3 URL](common-dialogs.md#amazon-s3-specific-url).
  It is recommended to connect to S3 via a *region-specific* S3 URL: `s3://s3.eu-central-1.amazonaws.com/bucket.name/`. A region-specific URL have much better performance than a generic one (`s3://s3.amazonaws.com/bucket.name/`).
  See recommendation on [Amazon S3 URL](common-dialogs.md#amazon-s3-specific-url).
- `az-blob://account:account_key@account.blob.core.windows.net/containername/path/filename.txt`
  Writes to `path/filename.out` object located in the Azure Blob Storage service in the specified container.
  Connects using the specified Account Key. See [Azure Blob Storage](common-dialogs.md#azure-blob-storage) for other authentication options.
- `hdfs://CONN_ID/path/filename.dat`
  Writes a file on a Hadoop distributed file system (HDFS). To which HDFS NameNode to connect to is defined in a [*Hadoop connection*](hadoop-connections.md) with `CONN_ID`. This example file URL writes a file with `/path/filename.dat` absolute HDFS path.
- `smb://domain%3Buser:password@server/path/filename.txt`
  Writes a file to a Windows share (Microsoft SMB version 1/CIFS protocol). The `server` part may be a DNS name, an IP address or a NetBIOS name. The Userinfo part of the URL (`domain%3Buser:password`) is not mandatory and any URL reserved character it contains should be escaped using the %-encoding similarly to the semicolon `;` character with `%3B` in the example (the semicolon is escaped because it collides with the default **CloverDX** file URL separator). Also note that the dollar sign `$` in the URL path (e.g. in the case of writing to an Administrative share) is reserved for the file partitioning feature so it too needs be escaped (with `%24`).
  The SMB protocol is implemented in the JCIFS library which may be configured using Java system properties. For a list of all configurable properties, see [Setting client properties](http://jcifs.samba.org/src/docs/api/overview-summary.html#scp) in JCIFS documentation.
- `smb2://domain%3Buser:password@server/path/filename.txt`
  Writes a file to a Windows share (Microsoft SMB version 2 and 3).
  The SMB version 2 and 3 protocol is implemented in the SMBJ library.
> [!NOTE]
> Due to the upgrade of the SMBJ library in **CloverDX version 6.2**, anonymous access using SMB protocol version 2 or 3 will no longer work unless your Samba server is configured to stop requiring message signing. If turning off message signing is not an option, you can create a user without a password to use in the URL as a workaround. See below for example URLs:
> `smb2://domain%3Buser@server/path/filename.txt`
> `smb2://domain%3Buser:@server/path/filename.txt`

##### Writing to output port

- `port:$0.FieldName:discrete`
  If this URL is used, the output port of the **Writer** must be connected to another component. Output metadata must contain a `FieldName` of one of the following data types: `string`, `byte` or `cbyte`. Each data record that is received by the **Writer** through the input port is processed according to the input metadata, sent out through the optional output port, and written as the value of the specified field of the metadata of the output edge. Next records are parsed in the same way as described here.

##### Using proxy in Writers

- `http:(direct:)//seznam.cz`
  Without proxy.
- `http:(proxy://user:password@212.93.193.82:443)//seznam.cz`
  Proxy setting for HTTP protocol.
- `ftp:(proxy://user:password@proxyserver:1234)//seznam.cz`
  Proxy setting for ftp protocol.
- `ftp:(proxy://proxyserver:443)//server/path/file.dat`
  Proxy setting for FTP protocol.
- `sftp:(proxy://66.11.122.193:443)//user:password@server/path/file.dat`
  Proxy setting for SFTP protocol.
- `s3:(proxy://user:password@66.11.122.193:443)//access_key_id:secret_access_key@s3.amazonaws.com/bucketname/path/filename.out`
  Proxy setting for S3 protocol.

##### Writing to dictionary

- `dict:keyName:source`
  Writes data to a file URL specified in dictionary. Target file URL is retrieved from the specified dictionary entry.
- `dict:keyName:discrete`[[1]](examples-of-file-url-in-writers.md#common-of-writers-footnote1)
  Writes data to dictionary. Creates `ArrayList<byte[]>`
- `dict:keyName:stream`[[2]](examples-of-file-url-in-writers.md#common-of-writers-footnote2)
  Writes data to dictionary. Creates `WritableByteChannel`

##### Sandbox resource as data source

A sandbox resource, whether it is a shared, local or partitioned sandbox, is specified in the graph under the fileURL attributes as a so called sandbox URL like:

`sandbox://data/path/to/file/file.dat`

where `data` is a code for sandbox and `path/to/file/file.dat` is the path to the resource from the sandbox root. The URL is evaluated by CloverDX Server during graph execution and a component (Reader or Writer) obtains the opened stream from the Server. This may be a stream to a local file or to some other remote resource. Thus, a graph does not have to run on the node which has local access to the resource. There may be more sandbox resources used in the graph and each of them may be on a different node. In such cases, CloverDX Server would choose the node with the most local resources to minimize remote streams.

The sandbox URL has a specific use for parallel data processing. When the sandbox URL with the resource in a *partitioned sandbox* is used, that part of graph/phase runs in parallel, according to the node allocation specified by the list of partitioned sandbox locations. Thus, each worker has its own local sandbox resource. CloverDX Server evaluates the sandbox URL on each worker and provides an open stream to a local resource to the component.

##### See also

| [Supported file URL formats for Readers](examples-of-file-url-in-readers.md) |
| --- |
| [URL file dialog](common-dialogs.md#url-file-dialog) |

| 1 | The `discrete` processing type uses a byte array for storing data. |
| --- | --- |

| 2 |  The `stream` processing type uses an output stream that must be created before running a graph (from Java code). |
| --- | --- |
