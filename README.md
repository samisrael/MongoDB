# MongoDB
```
Name   : Sam Israel D
Reg No : 212222230128
```

## Aim

To perform complete CRUD (Create, Read, Update, Delete) operations and advanced MongoDB queries on a Products collection, including conditional filtering, array-based searches, logical operators, regular expressions, sorting, skipping, and aggregation functions to manage and analyze product data effectively.

## Algorithm

### 1. CREATE Operation
- Start MongoDB and select the database.
- Create a collection named `products`.
- Insert multiple product documents using `insertMany()`.
- Insert an additional product using `insertOne()`.

### 2. READ Operation
- Display all documents using `find().pretty()`.
- Filter documents based on:
  - Price conditions (`$lt`, `$gt`)
  - Category not equal (`$ne`)
  - Logical conditions using `$and` and `$or`
- Search documents by tags using array operators:
  - `$in` (match any tag)
  - `$all` (must contain all tags)
  - `$size` (exact array length)
- Use REGEX to filter names starting with a specific letter.
- Sort documents using `sort()`.
- Skip documents using `skip()`.

### 3. UPDATE Operation
- Update fields using `$set` (e.g., update price).
- Increment numeric values using `$inc` (e.g., increase stock).
- Modify array fields:
  - `$push` to add a tag
  - `$pull` to remove a tag

### 4. DELETE Operation
- Remove a specific product using `deleteOne()`.

### 5. AGGREGATION Operations
- Use `$group` to calculate:
  - Total stock across all products

---

## MongoDB Queries

```mongodb
db.products.insertMany([
  {
    _id: 1,
    name: "Laptop",
    brand: "Dell",
    price: 55000,
    category: "Electronics",
    stock: 30,
    tags: ["computer", "technology"]
  },
  {
    _id: 2,
    name: "Smartphone",
    brand: "Samsung",
    price: 30000,
    category: "Electronics",
    stock: 50,
    tags: ["mobile", "android"]
  },
  {
    _id: 3,
    name: "Headphones",
    brand: "Sony",
    price: 2500,
    category: "Accessories",
    stock: 100,
    tags: ["audio", "music"]
  },
  {
    _id: 4,
    name: "Smartwatch",
    brand: "Apple",
    price: 45000,
    category: "Electronics",
    stock: 20,
    tags: ["wearable", "ios"]
  },
  {
    _id: 5,
    name: "Keyboard",
    brand: "Logitech",
    price: 1200,
    category: "Accessories",
    stock: 80,
    tags: ["computer", "typing"]
  }
])

db.products.insertOne({
  _id: 6,
  name: "Tablet",
  brand: "Lenovo",
  price: 20000,
  category: "Electronics",
  stock: 40,
  tags: ["mobile", "touch"]
})

db.products.find().pretty()

db.products.find({ price: { $lt: 5000 } })

db.products.find({ price: { $gt: 10000 } })

db.products.find({ category: { $ne: "Electronics" } })

db.products.find({
  $and: [
    { category: "Electronics" },
    { price: { $lt: 50000 } }
  ]
})

db.products.find({
  $or: [
    { category: "Accessories" },
    { price: { $gt: 40000 } }
  ]
})

db.products.find({
  tags: { $in: ["computer", "mobile"] }
})

db.products.find({
  tags: { $all: ["audio", "music"] }
})

db.products.find({
  tags: { $size: 2 }
})

db.products.updateOne(
  { name: "Laptop" },
  { $set: { price: 52000 } }
)

db.products.updateOne(
  { name: "Keyboard" },
  { $inc: { stock: 10 } }
)

db.products.updateOne(
  { name: "Smartwatch" },
  { $push: { tags: "premium" } }
)

db.products.updateOne(
  { name: "Headphones" },
  { $pull: { tags: "music" } }
)

db.products.deleteOne({ name: "Keyboard" })

db.products.find().sort({ price: -1 })

db.products.find().skip(2)

db.products.find({ name: /^S/ })

db.products.aggregate([
  { $group: { _id: null, totalStock: { $sum: "$stock" } } }
])

db.products.aggregate([
  { $group: { _id: "$category", count: { $sum: 1 } } }
])

## Result

- CRUD operations were successfully performed on the `products` collection.  
- Advanced queries including filtering, sorting, array operations, regex, and aggregation were executed.  
- The total stock and category-wise product counts were calculated using aggregation.
