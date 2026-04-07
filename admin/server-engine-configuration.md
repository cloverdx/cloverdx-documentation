<!-- Administration > Configuration > Server configuration > Configuration properties and sources > Engine configuration -->

#### Engine configuration

The procedure to override the default internal engine properties is similar to overriding them in **CloverDX Designer**, as described in the *Engine configuration* section in **CloverDX Designer** User’s Guide.

To override the default properties, do the following:

1. Create a file with only those properties you want to override.
2. Add the following JVM option to the Server, use the full path to the created properties file:
   `-Dclover.engine.config.file=/full/path/to/engine.properties`
   > [!NOTE]
   > Where to set this option is specific for the application server used, examples can be found in [Specifying the path to configuration file](configuration-sources.md#specifying-path-to-configuration-file).
3. Restart the Server and check the effective properties in **Configuration** ****CloverDX Info** ****Engine Properties**
