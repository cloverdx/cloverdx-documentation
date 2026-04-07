<!-- Development > Component reference > Writers > MongoDBWriter -->

### MongoDBWriter

![MongoDBWriter 64x64](../figures/MongoDBWriter-64x64.png)

| [Short description](mongodbwriter.md#short-description) |
| --- |
| [Ports](mongodbwriter.md#ports) |
| [Metadata](mongodbwriter.md#metadata) |
| [MongoDBWriter attributes](mongodbwriter.md#mongodbwriter-attributes) |
| [Details](mongodbwriter.md#details) |
| [Mapping](mongodbwriter.md#mapping) |
| [Error handling in bulk operations](mongodbwriter.md#error-handling-in-bulk-operations) |
| [Examples](mongodbwriter.md#examples) |
| [See also](mongodbwriter.md#see-also) |

#### Short description

**MongoDBWriter** stores, removes, or updates data in the MongoDB database using the Java driver.

**MongoDBWriter** can manipulate with documents in a MongoDB collection. New documents can be inserted, existing documents can be updated or removed.

| Data output | Input ports | Output ports | Transformation | Transf. required | Java | CTL | Auto-propagated metadata |
| --- | --- | --- | --- | --- | --- | --- | --- |
| database | 1 | 0-2 | **✓** | **✓** | **⨯** | **✓** | **✓** |

#### Ports

| Port type | Number | Required | Description | Metadata |
| --- | --- | --- | --- | --- |
| Input | 0 | **✓** | Input data records to be mapped to component attributes. | any |
| Output | 0 | **⨯** | Results | any |
| 1 | **⨯** | Errors | any |  |

#### Metadata

**MongoDBWriter** does not propagate metadata.

This component has metadata templates. The templates are described in the documentation of [MongoDBReader](mongodbreader.md) in the section [Metadata](mongodbreader.md#metadata).

#### MongoDBWriter attributes

| Attribute | Req | Description | Possible values |
| --- | --- | --- | --- |
| Basic |  |  |  |
| Connection | **✓** | The ID of the [MongoDB connection](mongodb-connections.md) to be used. |  |
| Collection name | **✓**  [[1]](mongodbwriter.md#mongodbwriter-required-attribute) | The name of the target collection. |  |
| Operation |  | The operation to be performed. **MongoDBWriter** can perform:  - **Bulk write operations (recommended)**   [insertOne](mongodbwriter.md#mongodbwriter-insertone), [updateOne](mongodbwriter.md#mongodbwriter-updateone), [updateMany](mongodbwriter.md#mongodbwriter-updatemany), [replaceOne](mongodbwriter.md#mongodbwriter-replaceone), [deleteOne](mongodbwriter.md#mongodbwriter-deleteone), [deleteMany](mongodbwriter.md#mongodbwriter-deletemany) - **Basic operations**   [insert](mongodbwriter.md#mongodbwriter-insert), [remove](mongodbwriter.md#mongodbwriter-remove), [save](mongodbwriter.md#mongodbwriter-save), [update](mongodbwriter.md#mongodbwriter-update), [update_multi](mongodbwriter.md#mongodbwriter-update-multi), [upsert](mongodbwriter.md#mongodbwriter-upsert) | See the description. |
| Query |  | Selects a subset of documents from a collection. The selection criteria may contain *[query operators](http://docs.mongodb.org/manual/reference/operator/#query-selectors)*.  Ignored by the `insertOne`, `insert` and `save` operations. | [BSON document](http://docs.mongodb.org/manual/core/document/) |
| New value | **✓**  [[1]](mongodbwriter.md#mongodbwriter-required-attribute) | Specifies the document to be stored in the database.  Ignored by delete operations (`deleteOne`, `deleteMany` and `remove`).  For update operations, **New value** may contain *[update operators](https://docs.mongodb.com/manual/reference/operator/update/)*. | [BSON document](http://docs.mongodb.org/manual/core/document/) |
| Input mapping | **✓** | Defines the mapping of input records to component attributes. |  |
| Output mapping |  | Defines mapping of results to standard output port. |  |
| Error mapping |  | Defines the mapping of errors to the error output port. |  |
| Advanced |  |  |  |
| Batch size |  | Number of records that can be sent to database in one batch.  [Bulk write operations](mongodbwriter.md#bulk-write-operations) may significantly increase performance. However, the whole batch is stored in memory, so increasing **Batch size** also increases memory requirements. | bulk write: 100 (default) \| basic: 1 (default) |
| Stop processing on fail |  | If `true`, a failure causes the component to skip all subsequent operations and send the information about skipped executions to the error output port. **Note:** this function works only if the edge is connected to the component’s error port. | true (default) \| false |
| Field pattern |  | Specifies the format of placeholders that can be used within the **Query** and **New value** attributes. The value of the attribute must contain "`field`" as a substring, e.g. "`<field>`", "`#{field}`", etc.  During the execution, each placeholder is replaced using a simple string substitution with the value of the respective input field, e.g. the string "`@{name}`" will be replaced with the value of the input field called "`name`" (assuming the default format of the placeholders). | @{field} (default) \| any string containing "`field`" as a substring. |

| 1 | The attribute is required, unless specified in the **Input mapping**. |
| --- | --- |

#### Details

| [Operations](mongodbwriter.md#operations) |
| --- |
| [Mapping](mongodbwriter.md#mapping) |
| [Error handling in bulk operations](mongodbwriter.md#error-handling-in-bulk-operations) |
| [Notes and limitations](mongodbwriter.md#notes-and-limitations) |
| [Format of the Date field value](mongodbwriter.md#format-of-the-date-field-value) |

##### Operations

There are two types of operations available for this component: *[bulk write](https://docs.mongodb.com/manual/reference/method/db.collection.bulkWrite/)* and basic operations. Bulk write operations are supported since driver and DB version 3.2.

| Operation | Description |
| --- | --- |
| **Bulk write operations (recommended)** |  |
| `insertOne` | Adds the value of the **New value** attribute as a new document to the target **Collection**. If the document does not contain the `_id` field, a generated one will be added.  See also [db.collection.insertOne()](https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/). |
| `updateOne` | Updates a single document matching the **Query**, with the values specified in the **New value** attribute, which must contain [update operators](https://docs.mongodb.com/manual/reference/operator/update/).  The `Upsert` parameter is available for this operation.  See also [db.collection.updateOne()](https://docs.mongodb.com/manual/reference/method/db.collection.updateOne/). |
| `updateMany` | Updates multiple documents matching the **Query**, with the values specified in the **New value** attribute, which must contain [update operators](https://docs.mongodb.com/manual/reference/operator/update/).  The `Upsert` parameter is available for this operation.  See also [db.collection.updateMany()](https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/). |
| `replaceOne` | Replaces a single document matching the **Query**.  The `Upsert` parameter is available for this operation.  See also [db.collection.replaceOne()](https://docs.mongodb.com/manual/reference/method/db.collection.replaceOne/). |
| `deleteOne` | Removes a single document matching the **Query**.  See also [db.collection.deleteOne()](https://docs.mongodb.com/manual/reference/method/db.collection.deleteOne/). |
| `deleteMany` | Removes all documents matching the **Query**.  See also [db.collection.deleteMany()](https://docs.mongodb.com/manual/reference/method/db.collection.deleteMany/). |
| **Parameters for bulk write operations** |  |
| Upsert | Only applicable to [`updateOne`](mongodbwriter.md#mongodbwriter-updateone), [`updateMany`](mongodbwriter.md#mongodbwriter-updatemany) and [`replaceOne`](mongodbwriter.md#mongodbwriter-replaceone). If enabled, the operation inserts a new document into the collection if no document matches the **Query**.  Generated object IDs for upserted documents will be returned as the `objectId` field in the output mapping. |
| Ordered | Executes operations in the order they arrive within every batch. If enabled, the first error causes the following operations in the same batch to be skipped. |
| **Basic operations** |  |
| `insert` | Adds the value of the **New value** attribute as a new document to the target **Collection**. If the document does not contain the `_id` field, a generated one will be added.  See also [db.collection.insert()](https://docs.mongodb.com/manual/reference/method/db.collection.insert/#db.collection.insert). |
| `remove` | Removes objects that match the **Query** from the **Collection**.  See also [db.collection.remove()](https://docs.mongodb.com/manual/reference/method/db.collection.remove/#db.collection.remove). |
| `save` | Similar to `insert`. Adds the document specified as the **New value** attribute to the **Collection** or replaces an existing document with the same `_id`.  See also [db.collection.save()](https://docs.mongodb.com/manual/reference/method/db.collection.save/#db.collection.save). |
| `update` | Updates at most *one* document that matches the **Query**, with the values specified in the **New value** attribute which may contain [update operators](https://docs.mongodb.com/manual/reference/operator/update/).  See also [db.collection.update()](https://docs.mongodb.com/manual/reference/method/db.collection.update/#definition). |
| `update_multi` | Updates multiple documents matching the **Query** with the values specified in the **New value** attribute which must contain [update operators](https://docs.mongodb.com/manual/reference/operator/update/).  See also [db.collection.update() - multi](https://docs.mongodb.com/manual/reference/method/db.collection.update/#multi-parameter). |
| `upsert` | If no existing document matches the **Query**, inserts a new document into the **Collection**, otherwise performs an update. The **New value** attribute may contain [update operators](https://docs.mongodb.com/manual/reference/operator/update/).  See also [db.collection.update() - upsert](https://docs.mongodb.com/manual/reference/method/db.collection.update/#upsert-option). |

##### Mapping

Editing any of the **Input**, **Output** or **Error mapping** opens the [Transform Editor](transformations.md#transform-editor).

###### Input mapping

The editor allows you to override selected attributes of the component with the values of the input fields.

| Field Name | Attribute | Type | Possible values |
| --- | --- | --- | --- |
| collection | Collection | string |  |
| query | Query | string |  |
| newValue | Projection | string |  |

###### Output mapping

The editor allows you to map the results and the input data to the output port.

If **Output mapping** is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| numAffected | integer | The number of affected documents, only set by the `update`, `update_multi` and `upsert` operations. |
| objectId | string | The object ID of the document.  **Bulk write operations:** set by the `insertOne` operation, and the `updateOne`, `updateMany` and `replaceOne` operations for `upsert`.  **Basic operations:** set by the `insert` and `save` operations. (Not populated in the bulk insert mode.) |
| batchNumber | long | The sequence number of the current batch, starting from 0. |
| deletedCount | integer | The number of documents deleted by the current batch. |
| insertedCount | integer | The number of documents inserted by the current batch. |
| matchedCount | integer | The number of documents matched by the current batch. |
| modifiedCount | integer | The number of documents modified by the current batch. |

###### Error mapping

The editor allows you to map the errors and the input data to the error port.

If **Error mapping** is empty, fields of input record and result record are mapped to output by name.

| Field Name | Type | Description |
| --- | --- | --- |
| errorMessage | string | The error message. |
| stackTrace | string | The stack trace of the error. |
| batchNumber | long | The sequence number of the current batch, starting from 0. |
| deletedCount | integer | The number of documents deleted by the current batch. |
| insertedCount | integer | The number of documents inserted by the current batch. |
| matchedCount | integer | The number of documents matched by the current batch. |
| modifiedCount | integer | The number of documents modified by the current batch. |

##### Error handling in bulk operations

Each input record produces one output record either on the standard, or error output port. A record is sent to the error output port if an error occurs or the operation is skipped. In such a case, see the **errorMessage** field in **Error mapping** for details and possible solution.

##### Notes and limitations

**MongoDBWriter** does not write maps and lists. It converts maps and lists to string and writes the string.

##### Format of the date Field Value

A `date` value is in an [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) date format.

```json
{
    withTZ : { "$date": "2018-11-22T14:25:11.541+02:00" },
    millis: { "$date": "2018-11-22T14:25:11.541" },
    seconds: { "$date": "2018-11-22T14:25:11" },
    dateLocal: { "$date": "2018-11-22" },
    dateUTC: { "$date": "2018-11-22+00:00" }
}
```

![mongodb date format](../figures/mongodb-date-format.png)

#### Examples

##### Writing records to MongoDB

Insert records (productID, productName, description) to collection `newProducts`.

###### Solution

Create MongoDB Connection to target database.

Set up the following attributes:

| Attribute | Value |
| --- | --- |
| Connection | MyMongoDBConnection |
| Collection name | newProducts |
| Operation | insertOne |
| New value | { productID : @{productID}, productName : "@{productName}", description: "@{description}"} |

#### See also

| [MongoDBReader](mongodbreader.md) |
| --- |
| [MongoDBExecute](mongodbexecute.md) |
| [Common properties of components](components.md#common-properties-of-components) |
| [Specific attribute types](components.md#specific-attribute-types) |
| [Common properties of Writers](common-of-writers.md) |
| [Writers comparison](common-of-writers.md#writers-comparison) |
| [MongoDB connections](mongodb-connections.md) |
