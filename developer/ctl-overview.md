<!-- Development > CTL2 - CloverDX Transformation Language > CTL overview -->

## 33. CTL overview

CTL is a proprietary scripting language oriented on data processing in transformation components of **CloverDX**.

It is designed to allow simple and clear notation of how data is processed and yet provide sufficient means for its manipulation.

Language syntax resembles Java with some constructs common in scripting languages. Although scripting language itself, CTL code organization into function resembles structure of Java classes with clearly defined methods designating code entry points.

CTL is a high level language in both abstraction of processed data as well as its execution environment. The language shields programmer from the complexity of overall data transformation, while refocusing him to develop a single transformation step as a set of operations applicable onto all processed data records.

Closely integrated with **CloverDX** environment, the language also benefits the programmer with uniform access to elements of data transformation located outside the executing component, operations with values of types permissible for record fields, and a rich set of validation and manipulation functions.

During transformation execution, each component running CTL code uses separate interpreter instance; thus preventing possible collisions in the heavily parallel multi-threaded execution environment of **CloverDX**.
Example 16. Example of CTL2 code

```
//#CTL2

function integer transform() {
    if ( $in.0.hasDetail ) {
        $out.0.name = $in.0.name;
        $out.0.email = $in.0.email;

        return 0;
    }

    $out.1.name = $in.0.name;

    return 1;
}
```

### Basic features of CTL

1. **Easy scripting language**
   **CloverDX** transformation language (CTL) is a very simple scripting language that can serve for writing transformations in a great number of **CloverDX** components.
   Although Java can be used in all of these components, working with CTL is much easier.
2. **Typed language**
   CTL2 is strongly typed. Each variable has its data type. The declarations of container types contain the data types as well.
3. **Arbitrary order of code parts**
   Declare your variable where you need them.
   CTL2 allows to declare variables and functions in any place of the code. Only one condition must be fulfilled - each variable must be declared before it is used. Functions and record types may even be used before the code declaring them.
   CTL2 also allows to define mapping in any place of the transformation and be followed by other code.
   Parts of CTL2 code may be interspersed almost arbitrarily.
4. **Almost as fast as Java**
   Transformations written in CTL are almost as fast as those written in Java.
   Source code of CTL2 can even be compiled into Java class.
5. **Compiled mode**
   CTL2 code can be transformed into pure Java which greatly increases speed of the transformation. This is called a "compiled mode" and **CloverDX** can do it for you transparently each time you run a graph with CTL2 code in it. The transformation into compiled form is done internally, so you do not need to be Java programmer to use it.
   To enable the CTL2 compiled mode, type `//#CTL2:COMPILE` at the beginning of the code.
   Each time you use a component with CTL2 transform and explicitly set it to work in compiled mode, **CloverDX** produces an in-memory Java code from your CTL and runs the Java natively - giving you a great speed increase.
6. **Used in many CloverDX components**
   CTL2 can be used in all of the components whose overview is provided in [Transformations Overview](transformations.md#transformations-overview), except in **JMSReader** and **JMSWriter**.
7. **Used even without knowledge of Java**
   Even without any knowledge of Java, the user can write the code in CTL2.
8. **Access to Graph elements (Lookups, Sequences, …​)**
   A strict type checking is further extended to validation of lookup tables and sequences access. For lookup tables, the actual arguments of lookup operation are validated against lookup table keys, while using the record returned by table in further type checked.
   Sequences support three possible return types explicitly set by the user: `integer`, `long` and `string`.

### CTL history

The current version of CTL is CTL2. It is available since **CloverETL 3.0**. Older version of CTL (CTL1) is deprecated since **CloverETL 4.0.0.M2**. We strongly advise to use CTL2.

In the following chapters and sections, we provide a thorough description of the current version of CTL.
