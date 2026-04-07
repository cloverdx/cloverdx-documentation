<!-- Development > Component reference > File Operations > Common properties of File Operations components > Supported file URL formats for File Operations -->

#### Supported file URL formats for File Operations

URL attributes may be defined using the [URL file dialog](common-dialogs.md#url-file-dialog).

Unless explicitly stated otherwise, URL attributes of **File Operation** components accept multiple URLs separated with a semicolon (';').
> [!IMPORTANT]
> To ensure graph portability, forward slashes must be used when defining the path in URLs (even on Microsoft Windows).

Most protocols support wildcards: `?` (question mark) matches one arbitrary character; `*` (asterisk) matches any number of arbitrary characters. Note that wildcard support and their syntax is protocol-dependent.

Below are some examples of possible URL for **File Operations**:

##### Local files

- `/path/filename.txt`
  One specified file.
- `/path1/filename1.txt;/path2/filename2.txt`
  Two specified files.
- `/path/filename?.txt`
  All files satisfying the mask.
- `/path/*`
  All files in the specified directory.
- `/path?/*.txt`
  All `.txt` files in directories that satisfy the `path?` mask.

##### Remote files

- `ftp://username:password@server/path/filename.txt`
  Denotes the `path/filename.txt` file on a remote server connected via an FTP protocol using username and password.
  If the initial working directory differs from the server root directory, please use absolute FTP paths, see below.
- `ftp://username:password@server/%2Fpath/filename.txt`
  Denotes the `/path/filename.txt` file on a remote server - the initial slash must be escaped as `%2F`. The path is absolute with respect to the server root directory.
- `ftp://username:password@server/dir/*.txt`
  Denotes all files satisfying the mask on a remote server connected via an FTP protocol using username and password.
- `sftp://username:password@server/path/filename.txt`
  Denotes the `filename.txt` file on a remote server connected via an SFTP protocol using username and password.
- `sftp://username:password@server/path?/filename.txt`
  Denotes all files `filename.txt` in directories satisfying the mask on a remote server connected via SFTP protocol using username and password.
- `http://server/path/filename.txt`
  Denotes the `filename.txt` file on a remote server connected via an HTTP protocol.
- `https://server/path/filename.txt`
  Denotes the `filename.txt` file on a remote server connected via an HTTPS protocol.
- `s3://access_key_id:secret_access_key@s3.amazonaws.com/bucketname/path/filename.txt`
  Denotes the `path/filename.txt` object located in Amazon S3 web storage service in a bucket `bucketname`. The connection is established using the specified access key ID and secret access key.
- `az-blob://account:account_key@account.blob.core.windows.net/containername/path/filename.txt`
  Denotes the `path/filename.txt` object located in Azure Blob Storage service in a container `containername`. Connects using the specified Account Key. See [Azure Blob Storage](common-dialogs.md#azure-blob-storage) for other authentication options.
- `hdfs://CONNECTION_ID/path/filename.txt`
  Denotes the `filename.txt` file on Hadoop HDFS. The "`CONNECTION_ID`" stands for the ID of a Hadoop connection defined in a graph.
- `smb://domain%3Buser:password@server/path/filename.txt`
  `smb2://domain%3Buser:password@server/path/filename.txt`
  Denotes a file located in Windows share (Microsoft SMB/CIFS protocol). The URL path may contain wildcards (both * and ? are supported). The `server` part may be a DNS name, an IP address or a NetBIOS name. The Userinfo part of the URL (`domain%3Buser:password`) is not mandatory and any URL reserved character it contains should be escaped using the %-encoding similarly to the semicolon `;` character with `%3B` in the example (the semicolon is escaped because it collides with the default **CloverDX** file URL separator).
  The SMB version 1 protocol is implemented in the JCIFS library which may be configured using Java system properties. See [Setting client properties](http://jcifs.samba.org/src/docs/api/overview-summary.html#scp) in JCIFS documentation for a list of all configurable properties.
  The SMB version 2 and 3 protocol is implemented in the SMBJ library.
> [!NOTE]
> Due to the upgrade of the SMBJ library in CloverDX version 6.2, anonymous access using SMB protocol version 2 or 3 will no longer work unless your Samba server is configured to stop requiring message signing. If turning off message signing is not an option, you can create a user without a password to use in the URL as a workaround. See below for example URLs:
> `smb2://domain%3Buser@server/path/filename.txt`
> `smb2://domain%3Buser:@server/path/filename.txt`

##### Sandbox resources

A sandbox resource, whether it is a shared, local or partitioned sandbox, is specified in a graph under the fileURL attributes as a so called sandbox URL like this:

`sandbox://data/path/to/file/file.dat`

where `data` is a code for sandbox and `path/to/file/file.dat` is the path to the resource from the sandbox root. A graph does not have to run on the node which has local access to the resource.

##### List files in archives

To list the archive contents with the **ListFiles** component, archive scheme must be used in a so called archive URL like this:

- `zip:(archive.zip)`
- `tar:(archive.tar)`
- `tgz:(archive.tar.gz)`
- `gzip:(file.gz)`

Use local or remote URL for the archive file itself inside the parentheses.

- `zip:(ftp://username:password@server/path/archive.zip)`
- `tar:(sandbox://data/path/to/archive.tar)`

For `zip`, `tar`, and `tgz` schemes, use `!` to denote a path inside the archive, possibly with a wild card mask like this:

- `zip:(http://server/path/file.zip)!innerfolder/filename.txt`
  Denotes a specified `filename.txt` file compressed in the `file.zip` file on a remote server connected via an HTTP protocol.
- `tar:(/path/file????.tar)!innerfolder??/filename*.txt`
  Denotes all files from the archive file(s) that satisfy the specified mask. Wild cards (? and *) may be used in the compressed file names, inner folder and inner file names.
> [!NOTE]
> Path separator character `!` is supported since **CloverDX version 6.4**, and should be used instead of old separator character `#`. The old separator character is still supported for backward compatibility.

Use archive URL for inner archives (archives inside other archives). Wrap the archive URL of the outer archive file (with path to the inner archive file) in the archive URL of the inner archive. For example:

- `zip:(tgz:(data-in/outerfile.tar.gz)!tgzfolder/innerfile.zip)!zipfolder/`
  Denotes outer tar.gz archive file `data-in/outerfile.tar.gz` which has inner zip archive file `tgzfolder/innerfile.zip` which has folder `zipfolder/`.
- `zip:(tar:(/path/name?.tar)!innerfolder/file*.zip)!innermostfolder?/`
  Denotes files in the folder satisfying the path mask from all compressed zip files satisfying the specified zip mask from all compressed tar files satisfying the specified tar mask.
