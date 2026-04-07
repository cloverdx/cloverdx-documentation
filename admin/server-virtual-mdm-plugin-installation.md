<!-- Administration > Installation > Server installation > IBM InfoSphere MDM plugin installation -->

### IBM InfoSphere MDM plugin installation

**CloverDX IBM InfoSphere MDM Components** is an extension of CloverDX for connectivity to **IBM InfoSphere MDM** technology. The extension can be installed and used with **CloverDX Designer** and **CloverDX Server**. For installation steps into CloverDX Designer, refer [here](part-installation-instructions.md#ibm-infosphere-mdm-plugin-installation).

**CloverDX** supports IBM InfoSphere MDM 11.6 and 12.0 since version 5.11.0.

#### Downloading

**IBM InfoSphere MDM Components** for **CloverDX Server** are downloaded as a ZIP file containing the extension. The ZIP file is available for download under your account on [www.cloverdx.com](http://www.cloverdx.com) in **Downloads** area, under the **CloverDX Server Utilities & Extras** section:

- `ibm-mdm-11.6-connectors.5.x.x.zip` for IBM InfoSphere MDM 11.6
- `ibm-mdm-12.0-connectors.5.x.x.zip` for IBM InfoSphere MDM 12.0

#### Installation

The following steps are needed to install **IBM InfoSphere MDM Components** into **CloverDX Server**:

1. Download the ZIP file with **IBM InfoSphere MDM Components** for the Server and store it on the system where **CloverDX Server** is installed. For the download instructions, see [Downloading](part-installation-instructions.md#downloading).
2. The ZIP file contains a **CloverDX** plugin. Your Server installation needs to be configured to find and load the plugin from the ZIP file. This is done by setting the `engine.plugins.additional.src` Server configuration property to the absolute path of the ZIP file, e.g. `engine.plugins.additional.src=../opt/CloverDX/ibm-mdm-12.0-connectors.${version}.zip` (in case the Server is configured via property file).
   Details for setting the configuration property depend on your Server installation specifics, application server used, etc. See **CloverDX Server** documentation for details. Typically the property would be set similarly to how you set-up the properties for connection to the Server’s database. Updating the configuration property usually requires restart of the Server.
3. To verify that the plugin was loaded successfully, log into the Server’s **Reporting Console** and look in the **Configuration** ****CloverDX Info** ****Plugins** page. In the list of plugins, you should see `cloverdx.engine.initiate`.
> [!IMPORTANT]
> It is not possible to install multiple versions of IBM InfoSphere MDM plugin into one **CloverDX Server**.

#### Troubleshooting

If you get an `Unknown component` or `Unknown connection` error when running a graph with IBM InfoSphere MDM components, it means that the **IBM InfoSphere MDM Components** plugin was not loaded by the Server successfully. Please check the above steps to install the plugin, especially the path to the ZIP file.
