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
db.students.find({hobbies: 'Cooking'}) // here hobbies is an array, but we can search directly by providing value.
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

# Schema Validation

```js
db.createCollection("nonfiction");
db.nonfiction.insertOne({ name: "ABC" }); // success
db.nonfiction.insertOne({ name: 125673 }); // success
```

Here, there is no datatype validation on `name` field.

```js
db.createCollection("nonfiction", {
  validator: {
    $jsonSchema: {
      required: ["name", "price"],
      properties: {
        name: {
          bsonType: "string",
          description: "must be a string and required",
        },
        price: {
          bsonType: "number",
          description: "must be a number and required",
        },
      },
    },
  },
  validationAction: "warn",
});
// by default validationAction is error and it restrict to add the data if datatypes not matched, warn will allow to save the data but will give warning only.
```

## Modify mongo collection schema

```js
db.runCommand({
  collMod: "nonfiction",
  validator: {
    $jsonSchema: {
      required: ["name", "price", "authors"],
      properties: {
        name: {
          bsonType: "string",
          description: "must be a string and required",
        },
        price: {
          bsonType: "number",
          description: "must be a number and required",
        },
        author: {
          bsonType: "array"
          description: "must be an array and required",
          items: {
            bsonType: "object",
            required: ["name", "email"],
            properties: {
              name: {
                bsonType: "string",
                description: "must be a string and required",
              },
              email: {
                bsonType: "string",
                description: "must be a string and required",
              },
            },
          }
        },
      },
    },
  },
  validationAction: "error",
});
```

# Write concern in insertOne() and insertMany()

```js
{
  writeConcern: {
    w: <value>,
    j: <boolean>,
    wtimeout: <number>
  }
}
// w -> ack (0, 1)
// j -> journal (true, false)
// wtimeout -> write timeout in millisec
```

```js
db.nonfiction.insertOne(
  { name: "ABC" },
  {
    writeConcern: {
      w: 0,
      j: true,
      wtimeout: 1000,
    },
  }
);
```

```js
db.nonfiction.insertOne(
  { name: "ABC" },
  {
    writeConcern: {
      w: 0,
    },
  }
);
// this won't wait for acknowledgement
```

```js
db.nonfiction.insertOne(
  { name: "ABC" },
  {
    writeConcern: {
      w: 0,
      j: true,
    },
  }
);
// by default j is false
```

# Atomicity in MongoDB

Atomicity is achieved at document level. If there is very big document and is being inserted into mongoDB and some system error occurs then the document won't be inserted. It is only applied at per document level.

# Mongo import in MongoDB

Suppose we have a json file of collection and we want to import it in mongodb. We can do it by using mongo import tool.

```js
mongoimport <jsonFilePath> -d <databaseName> -c <collectionName> --jsonArray --drop

// eg: students.json file contains below json
[
  {
    name: "Ram",
    age: 12
  },
  {
    name: "Shyam",
    age: 12
  },
  {
    name: "Raghu",
    age: 12
  },
  {
    name: "Krishna",
    age: 12
  }
]

mongoimport students.json -d college -c students --jsonArray --drop
```

# Comparison operators in MongoDB

```js
$eq $ne
$lt $gt
$lte $gte
$in $nin
```

```js
db.students.find({ age: 5 });
db.students.find({ age: { $eq: 5 } });
db.students.find({ age: { $ne: 5 } });
db.students.find({ age: { $gt: 5 } });
db.students.find({ age: { $gte: 5 } });
db.students.find({ age: { $lt: 5 } });
db.students.find({ age: { $lte: 5 } });
db.students.find({ age: { $in: [5, 11, 15] } });
db.students.find({ age: { $nin: [5, 11, 15] } });
```

# Logical Operator in MongoDB

```js
$or $nor $and $not

db.students.find({$or:[{age: {$lte: 10}}, {age: {$gte: 12}}]})

db.students.find({$nor:[{age: {$lte: 10}}, {age: {$gte: 12}}]})

db.students.find({$and:[{age: {$lte: 11}}, {hobbies: "Walk"}]})
// Note: here if we run below query then also we will get the same result
db.students.find({age: {$lte: 11}, hobbies: "Walk"})
// then what is the use of and operator, Here is required because in case of json query if we give same key then mongo considers only last key value pair.
db.students.find({age: {$lte: 11}, age: {$gte: 5}})
// above query will give all the students having age greater than equal to 5, to execute above query properly means to consider less than equal to 11 as well we need to pass it in "and" operator as below
db.students.find({$and:[{age: {$lte: 11}}, {age: {$gte: 5}}]})

db.students.find({age: {$ne: 5}})
db.students.find({$and: [{age: {$not:{$lte: 5}}}, {age: {$not:{$gte: 11}}}]})
// student whose age is greater than 5 and less than 11
```

# Element Query Operators

- $exists
- $type

```js
db.students.find({ hasMacBook: { $exists: true } });
db.students.find({ hasMacBook: { $exists: true, $eq: true } });
db.students.find({ hasMacBook: { $exists: true, $type: "bool" } });
db.students.find({ hasMacBook: { $exists: true, $type: 8 } });
db.students.find({ hasMacBook: { $type: "bool" } });
```

# Evaluation Query Operators

```js
db.monthlyBudget.find({ $expr: { $gt: ["$spent", "$budget"] } });
// The following operation uses $expr to find documents where the spent amount exceeds the budget:
```

```js
// Aggregation expression to calculate discounted price

let discountedPrice = {
  $cond: {
    if: { $gte: ["$qty", 100] },
    then: { $multiply: ["$price", NumberDecimal("0.50")] },
    else: { $multiply: ["$price", NumberDecimal("0.75")] },
  },
};

// Query the supplies collection using the aggregation expression

db.supplies.find({ $expr: { $lt: [discountedPrice, NumberDecimal("5")] } });
```

Note: Even though `$cond` calculates an effective discounted price, that price is not reflected in the returned documents. Instead, the returned documents represent the matching documents in their original state.
