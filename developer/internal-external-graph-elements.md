<!-- Development > Job types > Graphs & development basics > Internal/external graph elements -->

### Internal/external graph elements

This chapter applies to [Metadata](metadata.md), [Connections](connections.md), [Lookup Tables](lookup-tables.md), [Sequences](sequences.md), and [Parameters](parameters.md).

There are some properties which are common for all mentioned graph elements.

Each element can be internal or external (shared).

#### Internal graph elements

Internal elements are part of the graph. They are contained in the graph and you can find them in the **Source** tab in the **Graph Editor**.

#### External (shared) graph elements

External (shared) elements are located outside the graph in an external file (in the `meta`, `conn`, `lookup`, `seq` subfolders, or in the `project` itself, by default).

In the **Source** tab, you can only see a link to the external file where the elements are described.

#### Working with graph elements

In case you have multiple graphs that use the same data files or the same database tables or any other data resource, you can have the same metadata, connection, lookup tables, sequences, or parameters for each such graph. These resources can be defined either in each of these graphs separately, or shared by all of the graphs.

In addition to metadata, the same is valid for connections (database connections, JMS connections, and QuickBase connections), lookup tables, sequences, and parameters. Connections, sequences and parameters can be internal and external (shared), as well.

#### Advantages of external (shared) graph elements

It is simpler and more convenient to have one external (shared) definition for multiple graphs in one location, i.e. to have one external file (shared by all of these graphs) that is linked to these various graphs that use the same resources.

It would be very difficult if you worked with these shared elements across multiple graphs separately in case you wanted to make some changes to all of them. In such a case, you would have to change the same characteristics in each of the graphs. As you can see, it is much better to be able to change the desired property in only one location - in an external (shared) definition file.

You can create external (shared) graph elements directly, or you can export or externalize internal elements.

#### Advantages of internal graph elements

On the other hand, if you want to transfer graphs between computers, you must transfer all linked information, as well. In such a case, it is much simpler to have these elements contained in your graph.

You can create internal graph elements directly, or you can internalize external (shared) elements after they have been linked to the graph.

#### Changing form of graph elements

Below are examples of when to use internal or external (shared) elements:

- **Linking external graph elements to the graph**
  If you have some elements defined in a file or multiple files outside a graph, you can link them to it. You can see these links in the **Source** tab of the **Graph Editor** pane.
- **Internalizing external graph elements into the graph**
  If you have some elements defined in a file or multiple files outside the graph but linked to the graph, you can internalize them. The files still exist, but new internal graph elements appear in the graph.
- **Externalizing internal graph elements in the graph**
  If you have some elements defined in the graph, you can externalize them. They will be converted to the files in corresponding subdirectories and only links to these files will appear in the graph instead of the original internal graph elements.
- **Exporting internal graph elements outside the graph**
  If you have some elements defined in the graph, you can export them. New files outside the graph will be created (non-linked to the graph) and the original internal graph elements will remain in the graph.
