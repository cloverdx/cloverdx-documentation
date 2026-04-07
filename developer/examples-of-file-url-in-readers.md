<!-- Development > Component reference > Readers > Common properties of Readers > Supported file URL formats for Readers -->

#### Supported file URL formats for Readers

The **File URL** attribute may be defined using the [URL File Dialog](common-dialogs.md#url-file-dialog).
> [!IMPORTANT]
> To ensure graph portability, forward slashes must be used when defining the path in URLs (even on Microsoft Windows).

Below are examples of possible URL for **Readers**:

##### Reading of local files

- `/path/filename.txt`
  Reads a specified file.
- `/path1/filename1.txt;/path2/filename2.txt`
  Reads two specified files.
- `/path/filename?.txt`
  Reads all files satisfying the mask.
- `/path/*`
  Reads all files in a specified directory.
- `zip:(/path/file.zip)`
  Reads the first file compressed in the `file.zip` file.
- `zip:(/path/file.zip)!innerfolder/filename.txt`
  Reads a specified file compressed in the `file.zip` file.
> [!NOTE]
> Path separator character `!` is supported since **CloverDX version 6.4**, and should be used instead of old separator character `#`. The old separator character is still supported for backward compatibility.

- `gzip:(/path/file.gz)`
  Reads the first file compressed in the `file.gz` file.
- `tar:(/path/file.tar)!innerfolder/filename.txt`
  Reads a specified file archived in the `file.tar` file.
- `zip:(/path/file??.zip)!innerfolder?/filename.*`
  Reads all files from the compressed zip file(s) that satisfy the specified mask. Wild cards (`?` and `*`) may be used in the compressed file names, inner folder and inner file names.
- `tar:(/path/file????.tar)!innerfolder??/filename*.txt`
  Reads all files from the archive file(s) that satisfy the specified mask. Wild cards (`?` and `*`) may be used in the compressed file names, inner folder and inner file names.
- `gzip:(/path/file*.gz)`
  Reads all files that has been gzipped into the file that satisfy the specified mask. Wild cards may be used in the compressed file names.
- `tar:(gzip:/path/file.tar.gz)!innerfolder/filename.txt`
  Reads a specified file compressed in the `file.tar.gz` file.
> [!NOTE]
> Although **CloverDX** can read data from a `.tar` file, writing to `.tar` files is not supported.

- `tar:(gzip:/path/file??.tar.gz)!innerfolder?/filename*.txt`
  Reads all files from the gzipped `tar` archive file(s) that satisfy the specified mask. Wild cards (`?` and `*`) may be used in the compressed file names, inner folder and inner file names.
- `zip:(zip:(/path/name?.zip)!innerfolder/file.zip)!innermostfolder?/filename*.txt`
  Reads all files satisfying the file mask from all paths satisfying the path mask from all compressed files satisfying the specified zip mask. Wild cards (`?` and `*`) may be used in the outer compressed files, innermost folder and innermost file names. They cannot be used in the inner folder and inner zip file names.

##### Reading of remote files

- `ftp://username:password@server/path/filename.txt`
  Reads a specified `filename.txt` file on a remote server connected via an FTP protocol using username and password.
- `sftp://username:password@server/path/filename.txt`
  Reads a specified `filename.txt` file on a remote server connected via an SFTP protocol using a username and password.
  If a certificate-based authentication is used, certificates are placed in the `${PROJECT}/ssh-keys/` directory. For more information, see [SFTP certificate in CloverDX](common-dialogs.md#sftp-certificate-private-key).
  The certificate-based authentication has a URL without a password:
  `sftp://username@server/path/filename.txt`
- `http://server/path/filename.txt`
  Reads a specified `filename.txt` file on a remote server connected via an HTTP protocol.
- `https://server/path/filename.txt`
  Reads a specified `filename.txt` file on a remote server connected via an HTTPS protocol.
- `zip:(ftp://username:password@server/path/file.zip)!innerfolder/filename.txt`
  Reads a specified `filename.txt` file compressed in the `file.zip` file on a remote server connected via an FTP protocol using username and password.
- `zip:(http://server/path/file.zip)!innerfolder/filename.txt`
  Reads a specified `filename.txt` file compressed in the `file.zip` file on a remote server connected via an HTTP protocol.
- `tar:(ftp://username:password@server/path/file.tar)!innerfolder/filename.txt`
  Reads a specified `filename.txt` file archived in the `file.tar` file on a remote server connected via an FTP protocol using username and password.
- `zip:(zip:(ftp://username:password@server/path/name.zip)!innerfolder/file.zip)!innermostfolder/filename.txt`
  Reads a specified `filename.txt` file compressed in the `file.zip` file that is also compressed in the `name.zip` file on a remote server connected via an FTP protocol using username and password.
- `gzip:(http://server/path/file.gz)`
  Reads the first file compressed in the `file.gz` file on a remote server connected via an HTTP protocol.
- `http://server/filename*.dat`
  Reads all files from a WebDAV server which satisfy specified mask (only * is supported).
- `s3://access_key_id:secret_access_key@s3.amazonaws.com/bucketname/filename*.out`
  Reads all objects which satisfy the specified mask from an Amazon S3 web storage service from a given bucket using access key ID and a secret access key.
  It is recommended to connect to S3 via *region-specific* S3 URL: `s3://s3.eu-central-1.amazonaws.com/bucket.name/`. The region-specific URL has much better performance than the generic one (`s3://s3.amazonaws.com/bucket.name/`).
  See recommendation on [Amazon S3 URL](common-dialogs.md#amazon-s3-specific-url).
  > [!NOTE]
  > s3:// URL protocol is available since **CloverETL 4.1**. More information about the deprecated http:// S3 protocol can be found in **CloverDX 4.0 User Guide**.
- `az-blob://account:account_key@account.blob.core.windows.net/containername/path/filename*.txt`
  Reads all objects matching the specified mask from the specified container in Microsoft Azure Blob Strage service.
  Connects using the specified Account Key. See [Azure Blob Storage](common-dialogs.md#azure-blob-storage) for other authentication options.
- `hdfs://CONN_ID/path/filename.dat`
  Reads a file from the Hadoop distributed file system (HDFS). To which HDFS NameNode to connect to is defined in a [Hadoop connection](hadoop-connections.md) with `CONN_ID`. This example file URL reads a file with the `/path/filename.dat` absolute HDFS path.
- `smb://domain%3Buser:password@server/path/filename.txt`
  Reads files from Windows share (Microsoft SMB/CIFS protocol) version 1. The URL path may contain wildcards (both * and ? are supported). The `server` part may be a DNS name, an IP address or a NetBIOS name. The Userinfo part of the URL (`domain%3Buser:password`) is not mandatory and any URL reserved character it contains should be escaped using the %-encoding similarly to the semicolon `;` character with `%3B` in the example (the semicolon is escaped because it collides with the default **CloverDX** file URL separator).
  The SMB protocol is implemented in the JCIFS library which may be configured using Java system properties. See [Setting client properties](http://jcifs.samba.org/src/docs/api/overview-summary.html#scp) in the JCIFS documentation for the list of all configurable properties.
- `smb2://domain%3Buser:password@server/path/filename.txt`
  Reads files from Windows share (Microsoft SMB/CIFS protocol) version 2 and 3.
  The SMB2 protocol is implemented in the SMBJ library.
> [!NOTE]
> Due to the upgrade of the SMBJ library in **CloverDX version 6.2**, anonymous access using SMB protocol version 2 or 3 will no longer work unless your Samba server is configured to stop requiring message signing. If turning off message signing is not an option, you can create a user without a password to use in the URL as a workaround. See below for example URLs:
> `smb2://domain%3Buser@server/path/filename.txt`
> `smb2://domain%3Buser:@server/path/filename.txt`

##### Reading from input port

- `port:$0.FieldName:discrete`
  Each data record field from input port represents one particular data source.
- `port:$0.FieldName:source`
  Each data record field from an input port represents a URL to be loaded in and parsed.
- `port:$0.FieldName:stream`
  Input port field values are concatenated and processed as an input file(s); `null` values are replaced by the `eof`.

See also [Input port reading](input-port-reading.md).

##### Using proxy in Readers

- `http:(direct:)//seznam.cz`
  Without proxy.
- `http:(proxy://user:password@212.93.193.82:443)//seznam.cz`
  Proxy setting for HTTP protocol.
- `ftp:(proxy://user:password@proxyserver:1234)//seznam.cz`
  Proxy setting for FTP protocol.
- `sftp:(proxy://66.11.122.193:443)//user:password@server/path/file.dat`
  Proxy setting for SFTP protocol.
- `s3:(proxy://user:password@66.11.122.193:443)//access_key_id:secret_access_key@s3.amazonaws.com/bucketname/filename*.dat`
  Proxy setting for S3 protocol.

##### Reading from dictionary

- `dict:keyName:discrete`[[1]](examples-of-file-url-in-readers.md#common-of-readers-footnote1)
  Reads data from dictionary.
- `dict:keyName:source`[[1]](examples-of-file-url-in-readers.md#common-of-readers-footnote1)
  Reads data from dictionary in the same way as the `discrete` processing type, but expects that the dictionary values are input file URLs. The data from this input passes to the **Reader**.

##### Sandbox resource as data source

A sandbox resource, whether it is a shared, local or partitioned sandbox, is specified in the graph under the **fileURL** attributes as a so called sandbox URL like this:

`sandbox://data/path/to/file/file.dat`

where `data` is a code for sandbox and `path/to/file/file.dat` is the path to the resource from the sandbox root. The URL is evaluated by CloverDX Server during graph execution and a component (reader or writer) obtains the opened stream from the Server. This may be a stream to a local file or to some other remote resource. Thus, a graph does not have to run on the node which has local access to the resource. There may be more sandbox resources used in the graph and each of them may be on a different node. In such cases, CloverDX Server would choose the node with the most local resources to minimize remote streams.

The sandbox URL has a specific use for parallel data processing. When the sandbox URL with the resource in a *partitioned sandbox* is used, that part of the graph/phase runs in parallel, according to the node allocation specified by the list of partitioned sandbox locations. Thus, each worker has its own local sandbox resource. CloverDX Server evaluates the sandbox URL on each worker and provides an open stream to a local resource to the component.

##### See also

| [Supported file URL formats for Writers](examples-of-file-url-in-writers.md) |
| --- |
| [URL file dialog](common-dialogs.md#url-file-dialog) |

| 1 | Reader finds out the type of source value from a dictionary and creates a readable channel for a parser. Reader supports the following type of sources: `InputStream, byte[], ReadableByteChannel, CharSequence, CharSequence[], List<CharSequence>, List<byte[]>, ByteArrayOutputStream`. |
| --- | --- |
