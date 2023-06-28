# CRUD operations in MongoDB

## Create:

```js
db.collection.insertOne(data, options);
db.collection.insertMany([data], options);
```

## Read:

```js
db.collection.findOne(filter, options);
db.collection.find(filter, options);
```

## Update:

```js
db.collection.updateOne(filter, data, options);
db.collection.updateMany(filter, data, options);
db.collection.replaceOne(filter, data, options);
```

## Delete:

```js
db.collection.deleteOne(filter, options);
db.collection.deleteMany(filter, options);
```

# find() vs findOne()

findOne() return a document while find() returns a `cursor`, using which we can iterate the list.

## How can we use cursor:

```js
db.students.find().count();
db.students.find().forEach((x) => {});
db.students.find().forEach((x) => {
  printjson(x);
});
db.students.find().limit(2);
db.students.find().toArray();
```

All these methods can't be applied to findOne() as it returns a record not a cursor.

# insert() vs insertOne() vs insertMany()

insert() is deprecated, use insertOne() instead.

```js
db.students.insertOne({ name: "Ram", age: 12 });
db.students.insertMany([
  { name: "Ram", age: 12 },
  { name: "Shyam", age: 22 },
]);
```

# updateOne() vs updateMany()

```js
db.students.updateOne({ name: "Ram" }, { $set: { age: 15 } });
db.students.updateMany({ age: 15 }, { $set: { age: 13 } });
db.students.updateMany({ age: 15 }, { $set: { isEligible: false } });
db.students.updateMany({ age: { $gte: 14 } }, { $set: { isEligible: true } });
```

# deleteOne() vs deleteMany()

```js
db.students.deleteMany({ age: 13 });
db.students.deleteOne({ age: 13 });
db.students.deleteOne({ name: "nitin" });
db.students.deleteMany({});
```

# Nested documents

Every document has limit of 16MB size

```js
db.students.updateMany({}, {$set:{idCards: {hasAdhaarCard: true, hasPanCard: false}}})
db.students.updateMany({}, {$set:{hobbies: ['Anime', 'Cooking']}})
db.students.find({hobbies: 'Cooking'})
// search nested doc
// will throw error
db.students.find({idCards.hasAdhaarCard: true})
// success
db.students.find({'idCards.hasAdhaarCard': true})
```

# Projection in MongoDB

```js
db.students.find({}, { name: 1 });
db.students.find({}, { name: 1, _id: 0 });
```

# Datatypes

```js
db.companyData.insertOne({
  name: "Amazon",
  isFunded: true,
  funding: 89979879576576867,
  employees: [
    { name: "Ram", age: 12 },
    { name: "Shyam", age: 15 },
  ],
  foundedOn: new Date(),
  foundedOnTimestamp: new Timestamp(),
});
```

# Delete Database or Collection

```js
// drop database
db.dropDatabase();
// drop collection
db.students.drop();
```

# Ordered Option in Insert Command

```js
db.books.insertMany([
  { _id: "A", name: "Java" },
  { _id: "B", name: "C++" },
]);
// will give error, only _id: 'C' will be inserted
db.books.insertMany([
  { _id: "C", name: "Python" },
  { _id: "A", name: "Ruby" },
  { _id: "E", name: "Scala" },
]);
// success, 'C' and 'E' both will be inserted, by default ordered is true
db.books.insertMany(
  [
    { _id: "C", name: "Python" },
    { _id: "A", name: "Ruby" },
    { _id: "E", name: "Scala" },
  ],
  { ordered: false }
);
```
