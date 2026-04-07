<!-- Administration > Configuration > Server configuration > Securing sensitive data > Securing configuration properties -->

#### Securing configuration properties

Some configuration properties can be confidential (e.g. a password to a database, mail client, etc.), so it is desirable to encrypt them. For this purpose, there is a command-line utility *secure-cfg-tool.jar*.

| [Basic utility usage](secure-configuration-properties.md#basic-utility-usage) |
| --- |
| [Advanced usage - custom settings](secure-configuration-properties.md#advanced-usage-custom-settings) |
| [Configuring application server](secure-configuration-properties.md#configuring-an-application-server) |

##### Basic utility usage

1. Download the utility archive file (`secure-cfg-tool.zip`) and unzip it.
   The utility is available in the download section of your **CloverDX** account - at the same location as the download of **CloverDX Server**.
2. Execute the script given for your operating system, `encrypt.bat` for MS Windows, `encrypt.sh` for Linux. You will be asked for inserting a value of a configuration property intended to be encrypted.
   Example:
   C:\secure-cfg-tool>encrypt.bat ************************************************************** Secure config encryption (use --help or -h option to show help) ************************************************************** ****** Config settings ****** Provider: SunJCE version 17 Algorithm: PBEWithHmacSHA512AndAES_256 ***************************** Enter text to encrypt: mypassword Text to encrypt: "mypassword" Encrypted text: conf#xLndKgzwP7DxAbWuhztvt/vHIvtUFjnB7MnL6pJIWpRw0gVJPghBr4HUnp0GE0Ym C:\secure-cfg-tool>
   If you want to configure the way the values are encrypted, see [Advanced usage - custom settings](secure-configuration-properties.md#advanced-usage-custom-settings)
3. The encrypted string has *conf#encrypted_property* format and can be used as a value of a configuration property in the properties file, `clover.xml` file or `web.xml` file (see details about configuration sources in [Configuration sources](configuration-sources.md)).
   **Example of a configuration property file with encrypted password:**
   ```properties
   jdbc.driverClassName=org.postgresql.Driver
   jdbc.url=jdbc:postgresql://127.0.0.1/clover_db?charSet=UTF-8
   jdbc.username=yourUsername
   jdbc.password=conf#xLndKgzwP7DxAbWuhztvt/vHIvtUFjnB7MnL6pJIWpRw0gVJPghBr4HUnp0GE0Ym
   jdbc.dialect=org.hibernate.dialect.PostgreSQLDialect
   ```

**Alternatively**, you can use the following command:

```properties
java -jar secure-cfg-tool.jar
```

> [!IMPORTANT]
> Values encrypted by a Secure parameter form ([Secure parameters](secure-parameters.md)) **cannot** be used as a value of a configuration property.

##### Advanced usage - custom settings

The way of encrypting configuration values described above uses default configuration settings (a default provider and algorithm). If you need to customize the settings, use the following parameters of the *secure-cfg-tool.jar* utility.

| Parameter | Description | Example |
| --- | --- | --- |
| --algorithm, -a | algorithm to encrypt | --algorithm PBEWithHMACSHA512AndAES_256 |
| --file, -f | config file location | -f C:\Users\admin\cloverServer.properties |
| --help, -h | show help | --help |
| --providerclass, -c | custom provider class | -c org.provider.ProviderClass |
| --providerlocation, -l | path to jar/folder containing a custom provider class (it will be added to the classpath) | --providerlocation C:\Users\admin\lib\customprovider.jar, -l C:\Users\admin\lib\ |
| --providers, -p | print available security providers and their algorithms | --providers |
> [!NOTE]
> To demonstrate usage of an external provider, the [Bouncy Castle](http://www.bouncycastle.org) provider is used.

To find out a list of algorithms, use **-p** or **--providers**

`C:\secure-cfg-tool>encrypt.bat -p`

If you want to find out a list of algorithms of an external provider, you must pass the provider’s class name and path to jar file(s).

`C:\secure-cfg-tool>encrypt.bat -p -c org.bouncycastle.jce.provider.BouncyCastleProvider -l C:\Users\admin\bcprov-jdk18on-<version>.jar`

The result might look like this:
***** List of available providers and their algorithms ***** Provider: SunJCE Provider class: com.sun.crypto.provider.SunJCE Algorithms: PBEWithHMACSHA512AndAES_256 PBEWithMD5AndDES PBEWithSHA1AndDESede PBEWithSHA1AndRC2_40 Provider: BC Provider class: org.bouncycastle.jce.provider.BouncyCastleProvider Algorithms: PBEWITHMD2ANDDES PBEWITHMD5AND128BITAES-CBC-OPENSSL PBEWITHMD5AND192BITAES-CBC-OPENSSL PBEWITHMD5AND256BITAES-CBC-OPENSSL
The provider class is displayed on the row starting with *Provider class*, algorithms are strings with *PBE* prefix. Both can be used to configure encryption.

###### Configuring the encryption process

The algorithm and provider can be passed to the utility in two ways.

- **Using command line arguments**
  To change the algorithm, use the argument **-a**. The provider remains default:
  `C:\secure-cfg-tool>encrypt.bat -a PBEWithMD5AndDES`
  To use an external provider, you must specify the provider’s class name (the `--providerclass` or `-c` arguments) and add jar(s) to the classpath (the `--providerlocation` or `-l` arguments). Provider location must point to a concrete jar file or directory containing the jar(s) and can be used several times for several paths:
  `C:\secure-cfg-tool>encrypt.bat -a PBEWITHSHA256AND256BITAES-CBC-BC -c org.bouncycastle.jce.provider.BouncyCastleProvider -l C:\Users\admin\bcprov-jdk18on-<version>.jar`
- **Using configuration file**
  A configuration file is a common properties file (text file with key-value pairs):
  `[property-key]=[property-value]`
  See the following example of `secure.config.example.properties` distributed within `secure-cfg-tool.zip`):
  ```properties
  security.config_properties.encryptor.providerClassName=org.bouncycastle.jce.provider.BouncyCastleProvider
  security.config_properties.encryptor.algorithm=PBEWITHSHA256AND256BITAES-CBC-BC
  security.config_properties.encryptor.providerLocation=C:\\User\\libs
  ```
  You must also set the path to the file using the **-f** argument:
  `C:\secure-cfg-tool>encrypt.bat -f path/to/secure.config.example.properties`
  > [!NOTE]
  > More jar locations can be set with the **security.config_properties.encryptor.providerLocation** property. The locations are delimited by semicolon.

###### Configuring an application server

**CloverDX Server** application needs to know how the values have been encrypted, therefore the properties must be passed to the server (see details in [Configuration](part3.md)). For example:

```properties
...
security.config_properties.encryptor.providerClassName=org.bouncycastle.jce.provider.BouncyCastleProvider
security.config_properties.encryptor.algorithm=PBEWITHSHA256AND256BITAES-CBC-BC
...
```

> [!IMPORTANT]
> If a third-party provider is used, its classes must be accessible to the application server. Property **security.config_properties.encryptor.providerLocation** will be ignored.
