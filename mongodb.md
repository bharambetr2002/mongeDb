# MongoDB Notes

MongoDB is mostly used with Express.JS.

## The Shell

1. `mongosh` - Start MongoDB shell/server.
2. `use db_name` - Create and use a new database called `db_name`.
3. `cmd+k` - Clear the shell.
4. `help` - Get all MongoDB commands.
5. `show dbs` - Show all the databases in the system.
6. `quit` - Exit the shell/server.

MongoDB shell is a JavaScript-based shell. It recognizes JavaScript commands, though not all, and allows running a subset of JavaScript commands.

### Notes:

- **`test` database**: A temporary database created by default. If you switch to a different database, its name will replace `test` in the shell prompt.
- **Saving a database**: To save a database permanently, insert some data into it. Databases without stored data are temporary in MongoDB.
- `db`: Displays the current database in use.

### BSON (Binary JSON)

MongoDB uses BSON (Binary JSON) for data storage.

#### Drawbacks of JSON:

1. It's a text-based format.
2. It's space-inefficient.
3. It supports fewer data types.

Refer to the JSON and BSON pages on [mongodb.com](https://www.mongodb.com) for more details.

## Collections and Documents

- **Document**: MongoDB stores data in the form of documents (key-value pairs).
- **Collection**: A collection is a group of documents. A database can have multiple collections, and each collection can include multiple documents.

### Inserting Data

- `insertOne()` - Inserts a single document.
- `insertMany()` - Inserts multiple documents.
- Example:
  ```javascript
  db.collection_name.insertOne({ key: "value" });
  db.collection_name.insertMany([
    { key1: "value1" },
    { key2: "value2" },
    { key3: "value3" },
  ]);
  ```
- `show collections` - Displays the collections in the database.

> **Note**: If a collection does not exist, MongoDB creates it automatically when you insert data.

### Finding Data

- `db.collection.find()` - Displays all data in the collection.
- For specific queries:
  ```javascript
  db.collection.find({ key: value, key2: value2 });
  ```
- `db.collection.findOne({ key: value })` - Displays only one matching document.

#### Cursor:

- The `find()` method returns a reference (cursor) to the original documents.
- The `findOne()` method returns the actual document.

#### Query Operators:

- `$gt`: Greater than.
- `$gte`: Greater than or equal to.
- **More operators**: Check MongoDB's official documentation for a complete list.

### Nested Objects:

To find data within nested objects:

```javascript
db.collection.find({ "key.innerKey": value });
```

## Updating Data

- Syntax:
  ```javascript
  db.collection.updateOne(<filter>, <update>, <options>);
  ```
- **Update operator**: `$set` (used to specify fields to update).

### Example:

```javascript
db.collection.updateOne(
  { key: "value" },
  { $set: { keyToUpdate: "newValue" } }
);
```

## Deleting Data

- `db.collection.deleteOne({ key: value })` - Deletes a single document matching the condition.
- `db.collection.deleteMany({ key: value })` - Deletes all documents matching the condition.
- **Warning**: To delete all documents in a collection:
  ```javascript
  db.collection.deleteMany({});
  ```
