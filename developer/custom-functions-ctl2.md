<!-- Development > CTL2 - CloverDX Transformation Language > CTL2 functions reference > Extending CTL with Java functions -->

### Extending CTL with Java functions

In addition to the built-in CTL functions provided by CloverDX, you can define your own functions directly in CTL. Such functions can implement arbitrary transformation logic and can be reused by importing CTL source files containing their definitions.

CTL can also be extended with custom functions implemented in Java. Once registered with CloverDX, these functions become available to CTL code in the same way as standard built-in functions.

Java-based custom functions are particularly useful when you want to expose existing Java functionality to CTL, integrate third-party Java libraries, or implement functionality that would be impractical to reimplement directly in CTL. Because these functions execute as native Java code, they can also be useful for performance-sensitive operations.

To create Java-based custom CTL functions, you need to implement a custom function library and register it as a CloverDX engine plugin.

Each custom CTL function library must extend:

`org.jetel.ctl.extensions.TLFunctionLibrary` class.

Individual custom CTL functions are represented by implementations of:

`org.jetel.ctl.extensions.TLFunctionPrototype` interface.

Methods exposed as CTL functions are marked with `org.jetel.ctl.extensions.TLFunctionAnnotation`. An optional initialization method can be marked with `org.jetel.ctl.extensions.TLFunctionInitAnnotation` and used to initialize resources required by the function.

Custom functions can use `org.jetel.ctl.extensions.TLFunctionCallContext` to maintain objects or initialized state across repeated function invocations. This is useful, for example, when processing multiple records and the function relies on an object that is expensive to create or initialize repeatedly.

Along with the Java implementation, you need to define a plugin that registers the custom function library with CloverDX. Once the plugin is installed, its functions can be called transparently from CTL code alongside the standard built-in function library.
> [!TIP]
> For a more in-depth guide on creating, registering, and deploying Java-based custom CTL functions, including sample source code and an example of wrapping a third-party Java library, visit this [Tech Blog article](https://www.cloverdx.com/tech-blog/extending-ctl-with-java-functions).
