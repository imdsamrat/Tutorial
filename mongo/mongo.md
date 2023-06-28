# CRUD operations in MongoDB

## Create:

```
insertOne(data, options)
insertMany(data, options)
```

## Read:

```
findOne(filter, options)
find(filter, options)
```

## Update:

```
updateOne(filter, data, options)
updateMany(filter, data, options)
replaceOne(filter, data, options)
```

## Delete:

```
deleteOne(filter, options)
deleteMany(filter, options)
```

# find() vs findOne()

findOne() return a document while find() returns a `cursor`, using which we can iterate the list.

## How can we use cursor:

```
db.students.find().count()
db.students.find().forEach((x)=> {})
db.students.find().forEach((x)=> {printjson(x)})
db.students.find().limit(2)
db.students.find().toArray()
```

All these methods can't be applied to findOne() as it returns a record not a cursor.

# insert() vs insertOne() vs insertMany()

insert() is deprecated, use insertOne() instead.

```
db.students.insertOne({name: "Ram", age: 12})
db.students.insertMany([{name: "Ram", age: 12}, {name: "Shyam", age: 22}])
```

# updateOne() vs updateMany()

```
db.students.updateOne({name: "Ram"}, {$set:{age: 15}})
db.students.updateMany({age: 15}, {$set:{age: 13}})
db.students.updateMany({age: 15}, {$set:{isEligible: false}})
db.students.updateMany({age: {$gte: 14}}, {$set:{isEligible: true}})
```

# deleteOne() vs deleteMany()

```
db.students.deleteMany({age: 13})
db.students.deleteOne({age: 13})
db.students.deleteOne({name: "nitin"})
db.students.deleteMany({})
```

# Nested documents

Every document has limit of 16MB size

```
db.students.updateMany({}, {$set:{idCards: {hasAdhaarCard: true, hasPanCard: false}}})
db.students.updateMany({}, {$set:{hobbies: ['Anime', 'Cooking']}})
db.students.find({hobbies: 'Cooking'})
# search nested doc
db.students.find({idCards.hasAdhaarCard: true}) # will throw error
db.students.find({'idCards.hasAdhaarCard': true}) # success
```

# Projection in MongoDB

```
db.students.find({}, {name: 1})
db.students.find({}, {name: 1, _id: 0})
```
