# Basics

- **Date:** Wednesday, June 29, 2022
- **Time:** 8:43 AM
- **Tutorial:** [MongoDB Query Document](https://www.tutorialspoint.com/mongodb/mongodb_query_document.htm)

1. **Create a collection:**
    - `db.createCollection("newCollection")`
    - In MongoDB, a collection is automatically created when a document is inserted.

2. **Insert a document into the collection:**
    - `db.BudgetCollection.insert({"date":new Date(2022,29,06),"category":"Grocery","amount":4.99})`
    - `db.BudgetCollection.insert([{"date":new Date(2022,29,06),"category":"Dress","amount":20.99},{"date":new Date(2022,29,06),"category":"Snacks","amount":3.99}])` (for multiple documents in array form)
    - Use the above array with `insertMany`.
    - For single inserts, `insertOne` can also be used.
    - **Note:** `insert` is usually deprecated for many drivers. Use `insertOne` or `insertMany` in that case.

3. **Drop a collection:**
    - `db.BudgetCollection.drop()`

4. **Retrieving documents:**
    - `db.getCollection('BudgetCollection').find({})` (returns all documents)
    - `db.getCollection('BudgetCollection').find({"category" : "Dress"})` (filtered list)
    - `db.getCollection('BudgetCollection').findOne({"category":"Groceries"})` (returns one record)
    - `db.getCollection('BudgetCollection').find({"amount":{$lte: 20}})` (relational operations refer next sections for more)
    - `db.getCollection('BudgetCollection').find({$and:[{"amount":{$lte: 20}},{"category":"Snacks"}]})` (And condition)
    - `db.getCollection('BudgetCollection').find({$or:[{"amount":{$lte: 20}},{"category":"Snacks"}]})` (OR condition)

5. **Update Document:**
    - `db.getCollection('BudgetCollection').update({"category":"Grocery"},{$set:{"category":"Groceries"}})`
    - `db.getCollection('BudgetCollection').update({"category":"Grocery"},{$set:{"category":"Groceries"}},{"multi":true})` (Default only updates one, for multiple updates set `multi:true`)
    - `db.empDetails.findOneAndUpdate({First_Name: 'Radhika'},{ $set: { Age: '30',e_mail: 'radhika_newemail@gmail.com'}})` (updates one based on condition)
    - `db.empDetails.updateOne({First_Name: 'Radhika'},{ $set: { Age: '30',e_mail: 'radhika_newemail@gmail.com'}})`
    - `db.empDetails.updateMany({Age:{ $gt: "25" }},{ $set: { Age: '00'}})`

6. **Delete Documents:**
    - `db.getCollection('BudgetCollection').remove({"_id":ObjectId("62bc63b0b6ac2fc45880b7cb")})` (deletes all records that match criteria)
    - `db.getCollection('BudgetCollection').remove({"_id":ObjectId("62bc63b0b6ac2fc45880b7cb")},1)` (deletes one record that matches criteria)
    - `db.getCollection('BudgetCollection').remove({})` (truncates collections)

7. **Projection:**
    - `db.BudgetCollection.find({},{"_id":0,"date":1,"amount":1})` (displays date and amount)
    - `db.mycol.find({},{"title":1,_id:0}).limit(1).skip(1)` (for skipping the first element and returning one document)

8. **Sorting:**
    - `db.BudgetCollection.find({},{"_id":0,"date":1,"amount":1}).sort({"amount":1})` (ascending order)
    - `db.BudgetCollection.find({},{"_id":0,"date":1,"amount":1}).sort({"amount":-1})`
