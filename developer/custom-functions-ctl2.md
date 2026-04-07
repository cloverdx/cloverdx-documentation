<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Custom CTL functions -->

### Custom CTL functions

In addition to prepared CTL functions, you can create your own CTL functions. To do that, you need to write your own code defining the custom CTL functions and specify its plugin.

Each custom CTL function library must be derived/inherited from:

`org.jetel.interpreter.extensions.TLFunctionLibrary` class.

Each custom CTL function must be derived/inherited from:

`org.jetel.interpreter.extensions.TLFunctionPrototype` class.

These classes have some standard operations defined and several abstract methods which need to be defined so that the custom functions may be used. Within the custom functions code, an existing context must be used or some custom context must be defined. The context serves to store objects when the function is to be executed repeatedly, in other words, on more records.

Along with the custom functions code, you also need to define the custom functions plugin. Both the library and the plugin will be used in **CloverDX**.
> [!TIP]
> For a more in-depth guide on creating and using custom CTL functions, including a sample source code, visit this [Tech Blog article](https://www.cloverdx.com/tech-blog/extending-ctl-with-java-functions).
