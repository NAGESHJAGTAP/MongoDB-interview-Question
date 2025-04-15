# MongoDB-interview-Question


# MongoDB Operations for Students Database

# SECTION A: Core Database and Collection Operations

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



# SECTION B: Data Modeling & Relationships in MongoDB

This section explains different types of relationships in MongoDB and how to model them using embedded documents and references.

---

## 1. One-to-Many Relationship Using Embedded Documents

Example: One student has many courses.

```js
db.students.insertOne({
  name: "John Doe",
  age: 20,
  courses: [
    { name: "Math", grade: "A" },
    { name: "Physics", grade: "B+" }
  ]
})
```

## 2. One-to-Many Relationship Using References

Example: One student has many course references.

### Students Collection:
```js
db.students.insertOne({
  name: "Alice",
  age: 21,
  course_ids: [ObjectId("607d95eb2f1b2c6c7c8d1b1e"), ObjectId("607d95eb2f1b2c6c7c8d1b1f")]
})
```

### Courses Collection:
```js
db.courses.insertMany([
  { _id: ObjectId("607d95eb2f1b2c6c7c8d1b1e"), name: "Biology" },
  { _id: ObjectId("607d95eb2f1b2c6c7c8d1b1f"), name: "Chemistry" }
])
```

## 3. Many-to-Many Relationship Using References

Example: Students and Courses (many students can enroll in many courses).

### Students Collection:
```js
db.students.insertOne({
  name: "Bob",
  course_ids: [
    ObjectId("607d95eb2f1b2c6c7c8d1b21"),
    ObjectId("607d95eb2f1b2c6c7c8d1b22")
  ]
})
```

### Courses Collection:
```js
db.courses.insertMany([
  {
    _id: ObjectId("607d95eb2f1b2c6c7c8d1b21"),
    name: "History",
    student_ids: [ObjectId("607d95eb2f1b2c6c7c8d1b10")]
  },
  {
    _id: ObjectId("607d95eb2f1b2c6c7c8d1b22"),
    name: "Geography",
    student_ids: [ObjectId("607d95eb2f1b2c6c7c8d1b10")]
  }
])
```

## 4. Embedding vs Referencing: Which to Choose?

| Embedding                            | Referencing                                |
|--------------------------------------|--------------------------------------------|
| Better for fast reads                | Better for large data or frequent updates  |
| Useful for one-to-few relationships  | Useful for one-to-many or many-to-many     |
| All data stored in one document      | Data spread across multiple documents      |
| Data duplication possible            | No data duplication                        |
| Not suitable if sub-documents grow   | More flexible and scalable                 |

**Example Decision:**  
If courses are small and always accessed with students → use embedding.  
If courses are shared across many students → use referencing.

## 5. Using `$lookup` for Joins (Aggregation)

Join `students` with `courses` using `$lookup`:

```js
db.students.aggregate([
  {
    $lookup: {
      from: "courses",
      localField: "course_ids",
      foreignField: "_id",
      as: "enrolled_courses"
    }
  }
])
```

## (Optional) Using `.populate()` in Mongoose

```js
Student.find().populate("course_ids").exec((err, students) => {
  console.log(students);
});
```

---



# SECTION C: Aggregation Framework in MongoDB

This section explains how to use MongoDB's powerful Aggregation Framework to analyze and transform data.

---

## 1. Use `$group` to Count How Many Students Are in Each Course

```js
db.students.aggregate([
  { $unwind: "$course_ids" },
  {
    $group: {
      _id: "$course_ids",
      studentCount: { $sum: 1 }
    }
  }
])
```

---

## 2. Use `$avg` to Calculate the Average Marks of Students

```js
db.students.aggregate([
  {
    $group: {
      _id: null,
      averageMarks: { $avg: "$marks" }
    }
  }
])
```

---

## 3. Use `$sum` to Find Total Marks Scored Per Course

```js
db.students.aggregate([
  { $unwind: "$courses" },
  {
    $group: {
      _id: "$courses.name",
      totalMarks: { $sum: "$courses.marks" }
    }
  }
])
```

---

## 4. Use `$match` to Filter Documents Before Aggregation

```js
db.students.aggregate([
  { $match: { age: { $gte: 18 } } },
  {
    $group: {
      _id: "$age",
      count: { $sum: 1 }
    }
  }
])
```

---

## 5. Use `$sort` to Sort Results of an Aggregation

```js
db.students.aggregate([
  {
    $group: {
      _id: "$age",
      count: { $sum: 1 }
    }
  },
  { $sort: { count: -1 } }
])
```

---

## 6. Use `$project` to Reshape Documents in Aggregation

```js
db.students.aggregate([
  {
    $project: {
      _id: 0,
      name: 1,
      age: 1,
      "firstCourse": { $arrayElemAt: ["$courses", 0] }
    }
  }
])
```

---

## 7. Use `$limit` and `$skip` Inside an Aggregation Pipeline

```js
db.students.aggregate([
  { $sort: { name: 1 } },
  { $skip: 5 },
  { $limit: 5 }
])
```

---

## 8. Use `$lookup` to Perform a Join Between Students and Courses

```js
db.students.aggregate([
  {
    $lookup: {
      from: "courses",
      localField: "course_ids",
      foreignField: "_id",
      as: "enrolled_courses"
    }
  }
])
```

---

## 9. Use `$unwind` to Flatten an Array Field During Aggregation

```js
db.students.aggregate([
  { $unwind: "$courses" },
  {
    $project: {
      name: 1,
      courseName: "$courses.name",
      marks: "$courses.marks"
    }
  }
])
```

---

