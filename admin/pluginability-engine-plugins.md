<!-- Administration > Configuration > Server configuration > Configuration properties and sources > Extensibility - CloverDX engine plugins -->

#### Extensibility - CloverDX engine plugins

**CloverDX Server** can use external engine plugins loaded from a specified source. The source is specified by the `engine.plugins.additional.src` config property.

See details about the possibilities with **CloverDX** configuration in *[Configuration](part3.md)*

This property must be the absolute path to the directory or zip file with additional **CloverDX** engine plugins. Both the directory and zip file must contain a subdirectory for each plugin. These plugins are not a substitute for plugins packed in a WAR file. Changes in the directory or the ZIP file apply only when the Server is restarted.

Each plugin has its own classloader that uses a parent-first strategy by default. The parent of plugins' classloaders is web-app classloader (content of [WAR]/WEB-INF/lib). If the plugin uses any third-party libraries, there may be some conflict with libraries on the parent-classloaders classpath. These are common exceptions/errors suggesting that there is something wrong with class loading:

- java.lang.ClassCastException
- java.lang.ClassNotFoundException
- java.lang.NoClassDefFoundError
- java.lang.LinkageError

There are several ways you can get rid of such conflicts:

- Remove your conflicting third-party libraries and use libraries on parent classloaders (web-app or app-server classloaders)
- Use a different class loading strategy for your plugin.
  - In the plugin descriptor `plugin.xml`, set attribute `greedyClassLoader="true"` in the element `plugin`
  - It means that the plugin classloader will use a self-first strategy
- Set an inverse class loading strategy for selected Java packages.
  - In the plugin descriptor `plugin.xml`, set attribute `excludedPackages` in the element `plugin`.
  - It is a comma-separated list of package prefixes, for example: `excludedPackages="some.java.package,some.another.package"`
  - In the previous example, all classes from `some.java.package`, `some.another.package` and all their sub-packages would be loaded with the inverse loading strategy, then the rest of classes on the plugins classpath.

The suggestions above may be combined. Finding the best solution for these conflicts may depend on the libraries on app-server classpath.

For more convenient debugging, it is useful to set a TRACE log level for related class-loaders.

```xml
<logger name="org.jetel.util.classloader.GreedyURLClassLoader">
        <level value="trace"/>
</logger>
<logger name="org.jetel.plugin.PluginClassLoader">
        <level value="trace"/>
</logger>
```

See [Logging](../operations/logging.md) for details about overriding the Server’s Log4j configuration.
