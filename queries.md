# Aggregation

- **Date:** Wednesday, June 29, 2022
- **Time:** 12:26 PM

1. **Sum**
    - `db.BudgetCollection.aggregate([{$group:{_id:"$category",total:{$sum:"$amount"}}}])`
2. **Average**
    - `db.BudgetCollection.aggregate([{$group:{_id:"$category",total:{$avg:"$amount"}}}])`
3. **Filter before group by**
    - `db.BudgetCollection.aggregate([ { $match : { category : "Groceries" } } ,{$group:{_id:"$category",total:{$avg:"$amount"}}}])`
    - `db.BudgetCollection.aggregate([ { $match : {$and:[{"amount":{$lte: 20}},{"category":"Snacks"}]} } ,{$group:{_id:"$category",total:{$avg:"$amount"}}}])`
4. **Only display select columns in output**
    - `db.BudgetCollection.aggregate([ {$group:{_id:"$category",total:{$avg:"$amount"}}},{ $project : { total : 1,_id:0 }}])`
5. **Sort the results**
    - `db.BudgetCollection.aggregate([ {$group:{_id:"$category",total:{$avg:"$amount"}}},{ $sort : { total : -1, }}])`
    - `db.BudgetCollection.aggregate([ {$group:{_id:"$category",total:{$avg:"$amount"}}},{ $sort : { total : -1, }},{$skip:1},{$limit:1}])`
