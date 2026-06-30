<!-- Development > Job elements > Metadata > Metadata types -->

### Metadata types

#### Internal metadata

Internal metadata is a part of a graph, it is contained in a graph and can be seen in its source tab.

##### Creating internal metadata

Internal metadata can be created in the following ways:

- **Outline**
  In the **Outline** pane, you can select the **Metadata** item and open the context menu by right-clicking and selecting **New metadata**.
- **Graph Editor — Edge**
  In the **Graph Editor**, you must open the context menu by right-clicking any of the **edges**. There you can see the **New metadata** item.
- **Graph Editor — Component**
  To create metadata using a component, fill in the required properties first. After that, right click on the component and select **Extract metadata**.

See [Creating Metadata](creating-metadata.md).

###### Creating internal metadata: Outline or edge

In both cases, after selecting **New metadata**, a new submenu appears. There you can select the way how to define metadata.

Now you have three possibilities for either case mentioned above: If you want to define metadata yourself, select the **User defined** item; if you want to extract metadata from a file, select the **Extract from flat file** or **Extract from xls(x) file** items, if you want to extract metadata from a database, select the **Extract from database** item. This way, you can only create internal metadata.

If you define metadata using the context menu, the metadata is assigned to the edge as soon as it is created.

###### Creating internal metadata: Component

Many readers and writers allow to extract metadata using components' properties. Based on a type of the component, metadata is extracted from a file, database table or other sources.

Supported components are: [FlatFileReader](flatfilereader.md), [ParallelReader](parallelreader.md), [DatabaseReader](dbinputtable.md), [DBFDataReader](dbfdatareader.md), [FlatFileWriter](flatfilewriter.md), [DatabaseWriter](dboutputtable.md), [DBFDataWriter](dbfdatawriter.md), [DB2BulkWriter](db2datawriter.md), [InfobrightBulkWriter](infobrightdatawriter.md), [InformixBulkWriter](informixdatawriter.md), [MSSQLBulkWriter](mssqldatawriter.md), [MySQLBulkWriter](mysqldatawriter.md), [OracleBulkWriter](oracledatawriter.md), [PostgreSQLBulkWriter](postgresqldatawriter.md).

The **Extract metadata** context menu is available only if the required file, connection or database properties are set on the component.

##### Externalizing internal metadata

Externalization of internal metadata is a conversion from internal metadata to external metadata being linked.

After you have created internal metadata as a part of a graph, you may want to convert it to external (shared) metadata. In such a case, you would be able to use the same metadata in other graphs (other graphs would share it).

To externalize any internal metadata item into external (shared) file, right-click an internal metadata item in the **Outline** pane and select **Externalize metadata** from the context menu. After that, a new wizard will open in which the `meta` folder of your project is offered as the location for this new external (shared) metadata file; now you can click **OK**. You can also rename the offered metadata filename.

After that, the internal metadata item disappears from the **Outline** pane **Metadata** group, but, at the same location, already linked, the newly created external (shared) metadata file appears. The same metadata file appears in the `meta` subfolder of the project and it can be seen in the **Project Explorer** pane.

You can even externalize multiple internal metadata items at once. To do this, select them in the **Outline** pane and, after right-click, select **Externalize metadata** from the context menu. After doing that, a new wizard will open in which the `meta` folder of your project will be offered as the location for the first of the selected internal metadata items and then you can click **OK**. The same wizard will open for each of the selected metadata items until they are all externalized. If you want (a file with the same name may already exist), you can change the offered metadata filename.

You can choose adjacent metadata items when you press Shift and move the **Down Cursor** or the **Up Cursor** key. If you want to choose non-adjacent items, use Ctrl+Click at each of the desired metadata items instead.

##### Exporting internal metadata

Export of metadata creates new external metadata as a copy of internal metadata.

This case is somewhat similar to that of externalizing metadata. Now you create a metadata file that is outside the graph in the same way as that of externalized file, but such a file is not linked to the original graph. Only a metadata file is being created. Subsequently you can use such a file for more graphs as an external (shared) metadata file as mentioned in the previous sections.

To export internal metadata into external (shared) one, right-click some of the internal metadata items in the **Outline** pane, click **Export metadata** from the context menu, select and expand the project you want to add metadata into, select the `meta` folder, rename the metadata file, if necessary, and click **Finish**.

After that, the **Outline** pane metadata folder remains the same, but in the `meta` folder in the **Project Explorer** pane, the newly created metadata file appears.

#### External (shared) metadata

External (shared) metadata serves for more than one graph. It is located outside the graph and can be shared across multiple graphs.

##### Creating external (shared) metadata

If you want to create shared metadata, select **File** ****New** ****Other** in the main menu.

Then expand the **CloverDX** ****Metadata** item and decide whether you want to define metadata yourself (**User defined**), or extract it from one of the available sources.

##### Linking external (shared) metadata

After its creation (see previous sections), external (shared) metadata must be linked to each graph in which it is to be used. You need to right-click either the **Metadata** group or any of its items and select **New metadata** ****Link shared definition** from the context menu. After that, a **File selection** wizard displaying the project content will open. You must expand the `meta` folder in this wizard and select the desired metadata file from the files contained in this wizard.

You can even link multiple external (shared) metadata files at once. To do this, right-click either the **Metadata** group or any of its items and select **New metadata** ****Link shared definition** from the context menu. After that, a **File selection** wizard displaying the project content will open. You must expand the `meta` folder in this wizard and select the desired metadata files from the files contained in this wizard. You can select adjacent file items by pressing Shift and moving the **Down Cursor** or the **Up Cursor** key. If you want to select non-adjacent items, use Ctrl+Click at each of the desired file items instead.

##### Linking external (shared) metadata from library

You can link external metadata from [library](../operations/libraries.md) by right-clicking either the **Metadata** group or any of its items and select **New metadata** ****Link shared definition from library**. After that, File selection wizard opens and you can list all installed libraries on the **CloverDX Server**. Only public metadata is shown.

##### Internalizing external (shared) metadata

Once you have created and linked external (shared) metadata, in case you want to put it into the graph, you need to convert it to internal metadata. In such a case you would see its structure in the graph itself.

You can internalize any linked external (shared) metadata file by right-clicking the linked external (shared) metadata item in the **Outline** pane and clicking **Internalize metadata** from the context menu.

You can even internalize multiple linked external (shared) metadata files at once. To do this, select the desired external (shared) metadata items in the **Outline** pane. You can select adjacent items when by pressing Shift and moving the **Down Cursor** or the **Up Cursor** key. If you want to select non-adjacent items, use Ctrl+Click at each of the desired items instead.

After that, the selected linked external (shared) metadata items disappear from the **Outline** pane **Metadata** group, but, at the same location, newly created internal metadata items appear.

The original external (shared) metadata files still exist in the `meta` subfolder and can be seen in the **Project Explorer** pane.

#### SQL query metadata

**SQL query metadata** is generated dynamically during runtime from an SQL query. They are useful to create more generic graphs when working with databases.

The structure of SQL query metadata is generated only during the initialization phase of the graph and **does not** change during the run of the graph, i.e. the structure of the metadata can change between executions of a graph, but not during a single execution.

SQL query metadata was introduced in **CloverDX****5.3.0** and it is an improved concept of Dynamic metadata from previous versions. SQL query metadata is backward-compatible with dynamic metadata - by saving a graph in version 5.3.0 or newer, dynamic metadata is converted to an SQL query metadata.

##### SQL query metadata in CTL

SQL query metadata can be used as a type for variables in CTL code.

If a direct reference to a field is made, the Transform editor shows this warning: `Field [field_name] may not exist in record with SQL query metadata [record_name]`

##### Use case

SQL query metadata allows you to create reusable graphs thanks to parameterization of the connection and query used, allowing you to use the same graph with multiple database tables or databases.

SQL query metadata is useful in cases where the exact fields of metadata are irrelevant, such as when dumping a DB table to a file. When columns are added to a table, it breaks metadata extracted from DB as the field counts no longer match. So if you use SQL query metadata, you no longer have to go back and manually add fields.

If you want to enforce exact metadata structure, you should use [metadata extracted from a database](creating-metadata.md#extracting-metadata-from-a-database).

##### Limitations

In most aspects, the metadata behaves similarly to a non-SQL query metadata; however, there are **some limitations**:

- an SQL query metadata cannot be exported or externalized;
- it cannot be merged with a statically typed metadata;
- SQL query metadata cannot be used if the database or the table does not exist during graph initialization, i.e. if creating the DB/Table is part of a jobflow;
- the type of an SQL query metadata is always delimited.

#### Reading metadata from special sources

Similarly to the SQL query metadata mentioned in the previous section, another metadata definitions can also be used in the **Source** tab of the **Graph Editor** pane.

However, this metadata cannot be edited in **CloverDX Designer**.

In addition to the simplest form that defines external (shared) metadata (`fileURL="${META_DIR}/metadatafile.fmt"`) in the source code of the graph, you can use more complicated URLs which also define paths to other external (shared) metadata in the **Source** tab.

For example:

```xml
<Metadata fileURL="zip:(${META_DIR}/delimited.zip)!delimited/employees.fmt"
id="Metadata0"/>
```

or:

```xml
<Metadata fileURL="ftp://guest:guest@localhost:21/employees.fmt"
id="Metadata0"/>
```

Such expressions can specify the sources from which the external (shared) metadata should be loaded and linked to the graph.
