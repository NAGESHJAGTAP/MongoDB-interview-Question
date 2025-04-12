# MongoDB-interview-Question


# MongoDB Operations for Students Database

This README contains MongoDB commands for various operations related to the `students` database and `courses` collection.

## 1. Create a Database

Create a database named `students`:

```js
use students
```

## 2. Create a Collection

Create a collection named `courses`:

```js
db.createCollection("courses")
```

## 3. Insert a Single Document

Insert a single document into the `students` collection:

```js
db.students.insertOne({
  name: "John Doe",
  age: 20,
  course: "Computer Science"
})
```

## 4. Insert Multiple Documents

Insert multiple documents into the `students` collection:

```js
db.students.insertMany([
  { name: "Alice", age: 19, course: "Math" },
  { name: "Bob", age: 22, course: "Physics" },
  { name: "Charlie", age: 21, course: "Biology" }
])
```

## 5. Find All Documents

Find all documents in the `students` collection:

```js
db.students.find()
```

## 6. Find a Document with a Specific Field Value

Find a document with a specific field value:

```js
db.students.find({ name: "Alice" })
```

## 7. Find Documents Using Logical Operators

### Using `$and`:
```js
db.students.find({ $and: [ { age: { $gt: 18 } }, { course: "Math" } ] })
```

### Using `$or`:
```js
db.students.find({ $or: [ { name: "Alice" }, { age: 22 } ] })
```

### Using `$not`:
```js
db.students.find({ age: { $not: { $gt: 20 } } })
```

### Using `$in`:
```js
db.students.find({ course: { $in: ["Math", "Physics"] } })
```

### Using `$nin`:
```js
db.students.find({ course: { $nin: ["Biology"] } })
```

## 8. Find Documents Using Comparison Operators

### Greater than (`$gt`):
```js
db.students.find({ age: { $gt: 20 } })
```

### Less than (`$lt`):
```js
db.students.find({ age: { $lt: 21 } })
```

### Greater than or equal to (`$gte`):
```js
db.students.find({ age: { $gte: 19 } })
```

### Less than or equal to (`$lte`):
```js
db.students.find({ age: { $lte: 22 } })
```

## 9. Use Projection to Fetch Selected Fields

Fetch only selected fields (excluding `_id`):

```js
db.students.find({}, { name: 1, age: 1, _id: 0 })
```

## 10. Count the Number of Documents

Count the number of documents in the `students` collection:

```js
db.students.countDocuments()
```

## 11. Sort Documents Based on a Field

Sort documents in ascending or descending order based on a field:

```js
db.students.find().sort({ age: 1 })    // ascending
db.students.find().sort({ age: -1 })   // descending
```

## 12. Limit and Skip Results

Limit and skip results:

```js
db.students.find().limit(2)
db.students.find().skip(1)
db.students.find().skip(1).limit(2)
```

## 13. Update a Single Field in One Document

Update one field in one document:

```js
db.students.updateOne(
  { name: "Alice" },
  { $set: { age: 20 } }
)
```

## 14. Update Multiple Documents Using a Condition

Update multiple documents based on a condition:

```js
db.students.updateMany(
  { course: "Math" },
  { $set: { passed: true } }
)
```

## 15. Use `$inc`, `$set`, `$unset` in Update Queries

### `$inc`: Increase field value
```js
db.students.updateOne({ name: "Bob" }, { $inc: { age: 1 } })
```

### `$set`: Set new value to a field
```js
db.students.updateOne({ name: "Charlie" }, { $set: { course: "Chemistry" } })
```

### `$unset`: Remove a field
```js
db.students.updateOne({ name: "John Doe" }, { $unset: { course: "" } })
```

## 16. Delete a Single Document

Delete a single document from the `students` collection:

```js
db.students.deleteOne({ name: "Alice" })
```

## 17. Delete Multiple Documents Using a Condition

Delete multiple documents based on a condition:

```js
db.students.deleteMany({ age: { $lt: 21 } })
```

## 18. Drop a Collection

Drop the `students` collection:

```js
db.students.drop()
```

## 19. Drop a Database

Drop the entire `students` database:

```js
use students
db.dropDatabase()
```

## 20. List All Collections in the Current Database

List all collections in the current database:

```js
show collections
```

---

