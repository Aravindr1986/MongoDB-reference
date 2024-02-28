	1. Sum
		a. db.BudgetCollection.aggregate([{$group:{_id:"$category",total:{$sum:"$amount"}}}])
	2. Average
		a. db.BudgetCollection.aggregate([{$group:{_id:"$category",total:{$avg:"$amount"}}}])
	3. Filter before group by
		a. db.BudgetCollection.aggregate([ { $match : { category : "Groceries" } } ,{$group:{_id:"$category",total:{$avg:"$amount"}}}])
		b. db.BudgetCollection.aggregate([ { $match : {$and:[{"amount":{$lte: 20}},{"category":"Snacks"}]} } ,{$group:{_id:"$category",total:{$avg:"$amount"}}}])
	4. Only display select columns in output
		a. db.BudgetCollection.aggregate([ {$group:{_id:"$category",total:{$avg:"$amount"}}},{ $project : { total : 1,_id:0 }}])
	5. Sort the results
		a. db.BudgetCollection.aggregate([ {$group:{_id:"$category",total:{$avg:"$amount"}}},{ $sort : { total : -1, }}])
db.BudgetCollection.aggregate([ {$group:{_id:"$category",total:{$avg:"$amount"}}},{ $sort : { total : -1, }},{$skip:1},{$limit:1}])![image](https://github.com/Aravindr1986/MongoDB-reference/assets/15961001/04194153-afdf-4407-be97-8458c970d0d5)
