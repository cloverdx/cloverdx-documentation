<!-- Development > Component reference > Deprecated > MongoDBExecute -->

### MongoDBExecute

Deprecated Component

![MongoDBExecute 64x64](../figures/MongoDBExecute-64x64.png)

| [Short description](mongodbexecute.md#short-description) |
| --- |
| [Ports](mongodbexecute.md#ports) |
| [Metadata](mongodbexecute.md#metadata) |
| [MongoDBExecute attributes](mongodbexecute.md#mongodbexecute-attributes) |
| [Details](mongodbexecute.md#details) |
| [Examples](mongodbexecute.md#examples) |
| [See also](mongodbexecute.md#see-also) |

#### Short description

**MongoDBExecute** executes JavaScript commands on the **MongoDB**™ database. [[1]](mongodbexecute.md#mongodb-execute-footnote1)

| Same input metadata | Sorted inputs | Inputs | Outputs | Each to all outputs | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| - | **⨯** | 0-1 | 0-2 | - | **⨯** | **⨯** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **⨯** | Input data records to be mapped to component attributes. | any |
| Output | 0 | **⨯** | Results | any |
| 1 | **⨯** | Errors | any |  |

#### Metadata

**MongoDBExecute** does not propagate metadata from left to right or from right to left.

This component has metadata templates available. The templates are described in [Details](mongodbexecute.md#details). See general details on [metadata templates](components.md#metadata-templates).

#### MongoDBExecute attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | **✓** | ID of the [MongoDB connection](mongodb-connections.md) to be used. |  |
| Command | **✓**  [[1]](mongodbexecute.md#mongodbexecute-required-attribute) | JavaScript code to be executed on the MongoDB database. Mirrors the syntax used in the [mongo](http://docs.mongodb.org/manual/mongo/) shell. |  |
| Input mapping | [[2]](mongodbexecute.md#mongodbexecute-mapping-required) | Defines mapping of input records to component attributes. |  |
| Output mapping | [[2]](mongodbexecute.md#mongodbexecute-mapping-required) | Defines mapping of results to the standard output port. |  |
| Error mapping | [[2]](mongodbexecute.md#mongodbexecute-mapping-required) | Defines mapping of errors to the error output port. |  |
| Redirect error output |  | If enabled, errors will be sent to the output port instead of the error port. | false (default) \| true |
| Advanced |  |  |  |
| Stop processing on fail |  | By default, a failure causes the component to skip all subsequent command executions and send the information about skipped executions to the error output port. This behavior can be turned off by this attribute. **Note:** this function works only if an edge is connected to the component’s error port. | true (default) \| false |
| No lock |  | By default, MongoDB [eval](http://docs.mongodb.org/manual/reference/command/eval/#eval) command takes a global write lock before evaluating the JavaScript function. As a result, the execution blocks all other read and write operations to the database while the operation runs. Set **No lock** to `true` to prevent the component from taking the global write lock before evaluating the JavaScript. **No lock** does not impact whether operations within the JavaScript code itself take a write lock. | false (default) \| true |
| Field pattern |  | Specifies the format of placeholders that can be used within the **Command** attribute. The value of the attribute must contain "`field`" as substring, e.g. "`<field>`", "`#{field}`", etc.  During the execution, each placeholder is replaced using a simple string substitution with the value of the respective input field, e.g. the string "`@{name}`" will be replaced with the value of the input field called "`name`" (assuming the default format of the placeholders). | @{field} (default) \| any string containing "`field`" as a substring |

| 1 | The attribute is required, unless specified in the **Input mapping**. |
| --- | --- |

| 2 |  Required if the corresponding edge is connected. |
| --- | --- |

#### Details

| [Input mapping](mongodbexecute.md#input-mapping) |
| --- |
| [Output mapping](mongodbexecute.md#output-mapping) |
| [Error mapping](mongodbexecute.md#error-mapping) |

**MongoDBExecute** executes JavaScript code against a MongoDB database connected using the Java driver. Input parameters can be received through the single input port and command results are sent to the first output port. Error information can be sent to the second output port.

The syntax of **MongoDBExecute** commands is similar to the [mongo](http://docs.mongodb.org/manual/mongo/) shell.

The component can be used to perform administrative operations that are not supported by the **MongoDBReader** or **MongoDBWriter**, e.g. to drop a collection, create an index, etc.

In general, you shouldn’t use **MongoDBExecute** for reading or writing data to the database if you can avoid it. Please use the **MongoDBReader** for reading from the database and the **MongoDBWriter** for inserting, updating or removing data.
> [!WARNING]
> **MongoDBExecute** internally uses the [eval](http://docs.mongodb.org/manual/reference/command/eval/) command to execute the JavaScript code on the server, which has several limitations and implications:
>
> - By default, `eval` takes a global write lock before evaluating the JavaScript function. As a result, `eval` blocks all other read and write operations to the database while the operation runs. Set the **No lock** attribute to `true` to prevent the `eval` command from taking the global write lock before evaluating the JavaScript. **No lock** does not impact whether operations within the JavaScript code itself take a write lock.
> - Do not use **MongoDBExecute** for long running operations, as the `eval` command blocks all other operations.
> - **MongoDBExecute** should not be used to retrieve large amounts of data, as there is no streaming support. In particular, transferring long arrays may lead to high memory requirements.
> - You can not use **MongoDBExecute** with sharded data. In general, you should avoid using `eval` in sharded Cluster; nevertheless, it is possible to use it with non-sharded collections and databases stored in a sharded Cluster.
> - With authentication enabled, `eval` will fail during the operation if you do not have the permission to perform a specified task.
>   Furthermore, since version 2.4 you must have [full admin access](http://docs.mongodb.org/manual/reference/user-privileges/#combined-access) (`readWriteAnyDatabase`, `userAdminAnyDatabase`, `dbAdminAnyDatabase` and `clusterAdmin` privileges on the `admin` database) to run the `eval` command.

Editing any of the **Input**, **Output** or **Error mapping** opens the [Transform Editor](transformations.md#transform-editor).

##### Input mapping

The editor allows you to override selected attributes of the component with the values of the input fields.

| Field Name | Attribute | Type | Possible values |
| --- | --- | --- | --- |
| command | Command | string |  |

##### Output mapping

The editor allows you to map the results and the input data to the output port.

If output mapping is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| success | boolean | True if the execution has succeeded (can be false when **Redirect error output** is enabled). |
| errorMessage | string | If the execution has failed, the field contains the error message (used when **Redirect error output** is enabled). |
| stackTrace | string | If the execution has failed, the field contains the stack trace of the error (used when **Redirect error output** is enabled). |
| stringResult | string | Conditional. If available, contains the return value of a successful execution serialized to a string. |
| booleanResult | boolean | Conditional. Contains the return value of a successful execution, if it is a boolean. |
| integerResult | integer | Conditional. If the return value of the execution is a number, contains its value as an integer. |
| longResult | long | Conditional. If the return value of the execution is a number, contains its value as a long. |
| numberResult | number | Conditional. If the return value of the execution is a number, contains its value as a floating point number. |
| dateResult | date | Conditional. Contains the return value of a successful execution, if it is a date. |
| stringListResult | string[] | Conditional. If the return value of the execution is iterable, contains the serialized elements as a list. |
| mapResult | map[string, string] | Conditional. Contains the return value of a successful execution, if it is a map. The values of the map are serialized to strings. |
| resultType | string | Conditional. Contains the canonical class name of the execution return value, if available. |

##### Error mapping

The editor allows you to map errors and input data to the error port.

If error mapping is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| success | boolean | Will always be set to `false`. |
| errorMessage | string | The error message. |
| stackTrace | string | The stack trace of the error. |

#### Examples

The following command drops the collection named "orders":

```javascript
db.orders.drop()
```

The following snippet creates indices on two fields of the collection named "orders" - "myField1" (ascending order of the keys) and "myField2" (descending order of the keys):

```javascript
db.orders.createIndex({myField1 : 1});
db.orders.createIndex({myField2 : -1});
```

The following command returns the names of collections in the database as a list:

```javascript
db.getCollectionNames()
```

#### Compatibility

| Version | Compatibility Notice |
| --- | --- |
| 5.5.0 | **MongoDBExecute** was deprecated because it does not work with MongoDB 4.2 and newer. |

#### See also

| [Common properties of components](components.md#common-properties-of-components) |
| --- |
| [Specific attribute types](components.md#specific-attribute-types) |
| [MongoDB connections](mongodb-connections.md) |
| [Deprecated](deprecated.md) |

| 1 | MongoDB is a trademark of MongoDB Inc. |
| --- | --- |
