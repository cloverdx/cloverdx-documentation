<!-- Development > Component reference > Others > DBExecute -->

### DBExecute

![DBExecute 64x64](../figures/DBExecute-64x64.png)

| [Short description](dbexecute.md#short-description) |
| --- |
| [Ports](dbexecute.md#ports) |
| [Metadata](dbexecute.md#metadata) |
| [DBExecute attributes](dbexecute.md#dbexecute-attributes) |
| [Details](dbexecute.md#details) |
| [Examples](dbexecute.md#examples) |
| [Best practices](dbexecute.md#best-practices) |
| [See also](dbexecute.md#see-also) |
> [!TIP]
> If you’re interested in learning more about this subject, we offer the [Databases course](https://academy.cloverdx.com/courses/database) in our CloverDX Academy.

#### Short description

**DBExecute** executes specified SQL/DML/DDL statements against a database connected using the JDBC driver. It can execute queries, transactions, call stored procedures or functions.

Input parameters can be received through the single input port and output parameters or result set are sent to the first output port. Error information can be sent to the second output port.
> [!TIP]
> For executing INSERT/DELETE/UPDATE SQL queries operating on single records read from input port of the component, consider using [DatabaseWriter](dboutputtable.md) instead, as it is optimized for these types of queries.

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 0-1 | 0-2 | - | **⨯** | **⨯** | **⨯** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | [[1]](dbexecute.md#dbexe-inport) | Input records for stored procedure or the whole SQL commands. | any |
| Output | 0 | [[2]](dbexecute.md#dbexe-outport) | Update count and the executed statement.  Output parameters and result set of [stored procedures](dbexecute.md#dbexecute-attr-stored-procedure). | any |
| 1 | **⨯** | for error information | based on input metadata |  |

| 1 |   Input port must be connected if the **Query input parameters** attribute is specified or if the whole SQL query is received through the input port. |
| --- | --- |

| 2 | The output port must be connected if the **Query output parameters** or the **Return set output fields** attribute is specified. |
| --- | --- |

#### Metadata

**DBExecute** propagates input metadata to the first output port if not calling a [stored procedure](dbexecute.md#dbexecute-attr-stored-procedure). It adds two output fields: `updateCount` and `statement`.

**DBExecute** has no metadata template.

Metadata on both output ports may contain any number of fields from input (same names and types). Input metadata are mapped automatically according to their name(s) and type(s).

Since 5.7.0, output metadata may contain two additional fields: `updateCount` and `statement` (case insensitive, so `UpdateCount` or `UPDATE_COUNT` also works). If present, these fields are populated with the number of updated rows and the executed statement, respectively. This feature only works if the **Call as stored procedure** attribute is set to false.

The error output metadata may also contain the `statement` field and two additional fields for error information, which may have any names and can be set via [Autofilling functions](metadata-records-and-fields.md#autofilling-functions): `ErrCode` and `ErrText`.

#### DBExecute attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| DB connection | yes | ID of the DB connection to be used. |  |
| SQL query | [[1]](dbexecute.md#dbexecute-attributes-fn01) | An SQL query defined in the graph. Contains SQL/DML/DDL statement(s) that should be executed against database. If a stored procedure or function with parameters should be called or if output data set should be produced, the form of the statement must be the following: *{[? = ]call procedureName([?[,?,[…​]])}*. (Do not forget to enclose the statement in curly brackets!) At the same time, if the input and/or the output parameters are required, corresponding attributes are to be defined for them (**Query input parameters**, **Query output parameters** and/or **Result set output fields**, respectively).  If the query consists of multiple statements, they must be separated from each other by specified **SQL statement delimiter**. Statements will be executed one by one. |  |
| Query URL | [[1]](dbexecute.md#dbexecute-attributes-fn01) | One of these two options: Either the name of an external file, including path, defining the SQL query with the same characteristics as described in the **SQL query** attribute, or the **File URL** attribute string that is used for port reading. For details, see [SQL query received from input port](dbexecute.md#sql-query-received-from-input-port). |  |
| Query source charset |  | Encoding of external file specified in the**Query URL** attribute. | E.g. UTF-8 \| <other encodings> |
| SQL statement delimiter |  | A delimiter between individual SQL statements in the **SQL query** or **Query URL** attribute. Default delimiter is a semicolon. | ";" (default) \| other character |
| Print statements |  | By default, SQL commands are not printed. If set to `true`, they are sent to stdout. | false (default) \| true |
| Transaction set |  | Specifies whether the statements should be executed in transaction. For more information, see [Transaction set](dbexecute.md#transaction-set). Is applied only if the database supports transactions. | SET (default) \| ONE \| ALL \| NEVER_COMMIT |
| Advanced |  |  |  |
| Call as stored procedure |  | By default, SQL commands are not executed as stored procedure calls unless this attribute is switched to `true`. If they are called as stored procedures, `JDBC CallableStatement` is used. See [Calling stored procedures and functions](dbexecute.md#calling-stored-procedures-and-functions). | false (default) \| true |
| Query input parameters |  | Used when a stored procedure/function with input parameters is called. It is a sequence of the following type: `1:=$inputField1;…;n:=$inputFieldN`. The value of each specified input field is mapped to the corresponding parameter (whose position in **SQL query** equals to the specified number). This attribute cannot be specified if SQL commands should be received through the input port. |  |
| Query output parameters |  | Used when a stored procedure or function with output parameters or return value is called. It is a sequence of the following type: `1:=$outputField1;…;n:=$outputFieldN`. Value of each output parameter (specified by its position in the **SQL query**) will be written to the specified field. If the function returns a value, this value is represented by the first parameter. Use "result_set" to denote output parameters that return data sets, typically by returning a cursor, for example "2:=result_set". See [Calling stored procedures and functions](dbexecute.md#calling-stored-procedures-and-functions). |  |
| Result set output fields |  | If a stored procedure or function returns a set of data, its output will be mapped to given output fields. The attribute is expressed as a sequence of output field names separated from each other by a semicolon. See [Calling stored procedures and functions](dbexecute.md#calling-stored-procedures-and-functions). |  |
| Deprecated |  |  |  |
| Error actions |  | The definition of an action that should be performed when the specified query throws an SQL Exception. See [Return values of transformations](transformations.md#return-values-of-transformations). |  |
| Error log |  | The URL of the file to which error messages for specified **Error actions** should be written. If not set, they are written to **Console**. |  |

| 1 |  One of these must be set. If both are specified, **Query URL** has higher priority. |
| --- | --- |

#### Details

| [SQL query received from input port](dbexecute.md#sql-query-received-from-input-port) |
| --- |
| [Transaction set](dbexecute.md#transaction-set) |
| [Calling stored procedures and functions](dbexecute.md#calling-stored-procedures-and-functions) |

##### SQL query received from input port

SQL query can also be received from the input port.

In this case, two values of the **Query URL** attribute are allowed:

- SQL command is sent through the input edge.
  The attribute value is: `port:$0.fieldName:discrete`.
  Metadata of this edge has neither default delimiter, nor record delimiter, but **EOF as delimiter** must be set to `true`.
- The name of the file containing the SQL command, including the path, is sent through the input edge.
  The attribute value is: `port:$0.fieldName:source`.

For more details about reading data from input port, see [Input port reading](input-port-reading.md).

##### Transaction set

Options are the following:

- **One statement (no transaction)**
  The commit is performed after each query execution. This is needed in case a statement cannot be executed within transaction.
- **One set of statements**
  All statements are executed for each input record. The commit is performed after a set of statements.
  For this reason, if an error occurs during the execution of any statement for any of the records, all statements are rolled back for such a record.
- **All statements**
  The commit is performed after all statements, only.
  For this reason, if an error occurs, all operations are rolled back.
- **Never commit**
  The commit or rollback may be called from other component in a different phase. There is **no** automatic **rollback**.
  > [!IMPORTANT]
  > If no error occurs, the connection closure results in **autocommit** even if **Never commit** is selected. If you need to **rollback**, the rollback must be called before autocommit on session’s termination.
  >
  > If you want to use the **Never commit** option and perform **commit** or **rollback** from another component in another phase, set **Thread-safe connection** in advanced **Connection settings** to **false**. Otherwise, each component will have different connection and autocommit will be performed at the end of processing of particular components.

##### Calling stored procedures and functions

The following table summarizes basic configuration examples to call stored procedures, setting input parameters and obtaining output values in the form of output parameters, return values or cursors.
> [!NOTE]
> To call a stored procedure in **PostgreSQL**, use the CALL command directly, without enclosing it in curly brackets.

| SQL object Declaration | Output | SQL query For PostgreSQL, see the note above | Query input port parameters | Query output port parameters | Result set output fields |
| --- | --- | --- | --- | --- | --- |
| PROCEDURE remove_customer(id IN NUMBER) | None | { call remove_customer(?) }; | 1:=$customer_id; |  |  |
| PROCEDURE find_customer_name_by_id(id IN NUMBER, name OUT VARCHAR) | Parameter | { call find_customer_name_by_id(?, ?) }; | 1:=$customer_id; | 2:=$customer_name; |  |
| PROCEDURE get_newest_customer(c_cursor OUT SYS_REFCURSOR) | Cursor | { call get_newest_customer(?) }; |  | 1:=result_set; | customer_id;custom_name;customer_address |
| PROCEDURE get_customer(id IN NUMBER, c_cursor OUT SYS_REFCURSOR) | Cursor | { call get_customer(?, ?) }; | 1:=$customer_id; | 2:=result_set; | customer_id;custom_name;customer_address |
| FUNCTION get_customer_name_by_id(id IN NUMBER) RETURN VARCHAR | Value | { ? = call get_customer_name_by_id(?) }; | 2:=$customer_id; | 1:=$customer_name; |  |

#### Examples

| [Creating a database table with DBExecute](dbexecute.md#creating-a-database-table-with-dbexecute) |
| --- |
| [Executing multiple queries](dbexecute.md#executing-multiple-queries) |
| [Creating a stored procedure](dbexecute.md#creating-a-stored-procedure) |
| [Getting errors](dbexecute.md#getting-errors) |

##### Creating a database table with DBExecute

This example shows a basic use case of this component.

Create a database table *rivers* with two columns: *name* and *length*.

###### Solution

Create a database connection **RiversConnection**. See [Creating internal database connections](database-connections.md#creating-internal-database-connections).

Set the **DB Connection** to **RiversConnection** connection.

Enter the `CREATE` statement into the **SQL Query** attribute.

| Attribute | Value |
| --- | --- |
| DB Connection | RiversConnection |
| Query URL | ```sql CREATE TABLE rivers (     name VARCHAR(50) NOT NULL,     length INTEGER ); ``` |

If you use one graph to create a database table and insert data to it, do no forget to put **DBExecute** and the component inserting the data into different phases. **DBExecute** should be in a lower phase and [DatabaseWriter](dboutputtable.md) (or other component writing to the database) in a higher phase.

##### Executing multiple queries

**DBExecute** is not limited to execution of one SQL query.

Create table *rivers* as in the previous example. If the table exists, drop it first.

###### Solution

| Attribute | Value |
| --- | --- |
| DB Connection | RiversConnection |
| Query URL | ```sql DROP TABLE IF EXISTS rivers; CREATE TABLE rivers (     name VARCHAR(50) NOT NULL,     length INTEGER ); ``` |

Do not forget to end statements with semicolons.

Note: some databases (e.g. Oracle) do not understand the `IF EXISTS` part of the query. If you use a database that does not support `IF EXISTS`, change the first line of the query to `DROP TABLE rivers;`.

##### Creating a stored procedure

Create a stored procedure that inserts data into the *products* table. The table has been created with the following query:

```sql
CREATE TABLE products (
    product_name VARCHAR(40) NOT NULL
);
```

###### Solution

Create a database connection **ProductConnection**.

| Attribute | Value |
| --- | --- |
| DB Connection | ProductConnection |
| Query URL | ```sql CREATE OR REPLACE FUNCTION add_product(param VARCHAR(40)) RETURNS VOID AS ' BEGIN     INSERT INTO products (product_name) VALUES(param); END; ' LANGUAGE plpgsql; ``` |

The example has been tested with PostgreSQL 9.2 and 14.4.

##### Getting errors

This example shows a way to get errors related to an SQL query from the **DBExecute** component to send it to the next component for further processing.

The graph uses **DBExecute** to create a database table **bricks**. The **bricks** table contains details on products from our supplier. The table might exist or we could not have permission to create a table and we would like to receive the errors from the database.

###### Solution

Create a database connection **ProductConnection**.

| Attribute | Value |
| --- | --- |
| DB Connection | ProductConnection |
| Query URL | ```sql CREATE TABLE bricks (     id INTEGER PRIMARY KEY NOT NULL,     length integer,     width integer,     height integer,     weight integer ); ``` |

Connect an edge to the second output port of **DBExecute**.

Assign metadata to the edge. The metadata should contain a `String` field that has **Autofilling** set to `ErrCode`.

#### Best practices

##### Upload and download of data

Do not use the **DBExecute** component for INSERT and SELECT statements. For uploading data to a database, please use the [DatabaseWriter](dboutputtable.md) component. Similarly, for downloading use the [DatabaseReader](dbinputtable.md) component.

##### Transferring data within a database

The best practice to load data from one table to another in the same database is to do it inside the database. You can use the **DBExecute** component with a query like this:

`insert into my_table select * from another_table`

because pulling data out from the database and putting them in is slower as the data has to be parsed during the reading and formatted when writing.

##### Charset

If the query is specified in an external file (with **Query URL**), we recommend users to explicitly specify **Query source charset**.

#### Troubleshooting

##### Boolean and Oracle JDBC

Calling arguments or return values of the PL/SQL RECORD, BOOLEAN, or table with non-scalar elements are not supported by Oracle JDBC Drivers. See [Oracle JDBC reference](http://docs.oracle.com/cd/E11882_01/java.112/e16548/apxref.htm#JJDBC28928)

As a workaround, you can create a wrapper procedure. See [Wrapper procedures](http://docs.oracle.com/cd/E11882_01/java.112/e16548/apxtblsh.htm#JJDBC28981)

#### See also

| [DatabaseReader](dbinputtable.md) |
| --- |
| [DatabaseWriter](dboutputtable.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Others comparison](common-of-others.md#others-comparison) |
