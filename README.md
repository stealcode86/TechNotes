# TechNotes


1) Point environmental variable to bin folder in MongoDB

2)Create database path to store data
cd c:\
md data\
md data\db

3)To start server open cmd 
cd c:\
mongod

4)To start client open another cmd 
mongo

5)To test the connectivity, execute the 'db' command and if the output is 'test', your connection is successful.

6) To create a database for Zoiva, copy the below code into your cmd terminal running the MongoDB client.
use Zoiva
Type 'db' in your MongoDB client. 

The output should now say Zoiva

7) db.createCollection('product_catalog')

db.collection_name.drop()  // replace collection_name with the collection name
db.dropDatabase() 	  // Drop current database in use

---- INSERT ---------

8) Inserting documents
 One document 
 db.collection_name.insert({document})
Multiple documents 
db.collection_name.insert( 
[
{document1}, 
{document2}
]
)

db.product_catalog.insert ( 
    {
        prodid:7000010, 
        prodname:"nosql distilled", 
        publisher:"Addison-Wesley", 
        genre: {academic: "technical"},
        ISBN:1234567, 
        price:400
    }
)


db.product_catalog.insert ( [
    {
        prodid:7000012, 
        prodname:"Java for Dummies", 
        publisher:"John Wiley", 
        genre: {academic: "technical"},
        ISBN:18407806, 
        price:400
    },
    {
        prodid:7000013, 
        prodname:"Big Data: Principles and Best Practices", 
        publisher:"Dreamtech",
        genre: {academic: "technical"},
        price:700
    },
    {
        prodid: 7000001,
        prodname: "iphone 7",
        manufacturer: "apple",
        categories: {main:"electronics",sub:"smartphones"},
        year_of_launch: 2017,
        price: 60000,
        colors: ["silver","black","gold","rosegold"]
    }
] )

--- READ --------
9) You can use db.your_collection_name.find().pretty() to view the documents you have inserted.

10) db.product_catalog.find({ }, {_id: 0}).pretty() -- id will not be shown.

11) db.product_catalog.find({  }, {_id: 0, prodname: 1, price: 1}).pretty()---- prodname and price will be shown

12) db.product_catalog.find({  }, {_id: 0, prodname: 0, price: 0}).pretty() --- everything except prodname, price and id will be shown


{
        prodid: 7000001,
        prodname: "iphone 7",
        manufacturer: "apple",
        categories: {main:"electronics",sub:"smartphones"},
        year_of_launch: 2017,
        price: 60000,
        colors: ["silver","black","gold","rosegold"]
}

13) If you wanted to specifically retrieve smartphones, this is how your query would look.

db.product_catalog.find(
	{ "categories.sub":"smartphones" }
)

14) If you wanted to retrieve only the prodname of a product with black color, this is how your query would be modified.


15) we want to retrieve products that are categorized as smartphones and are manufactured by Apple
db.product_catalog.find(
	{$and:[
			{ "categories.sub": "smartphones" },
			{ manufacturer: "apple" }
	      ]
	} 
)


db.product_catalog.find(
	{ colors: "black" },
	{ prodname: 1 }
)

16) we want to find the prodname of products whose category is not electronics. 
db.product_catalog.find(
	{ "categories.main":{$ne:"electronics"} }
	{ _id: 0, prodname: 1 }
)

17) Syntax for operators


$eq - $gte -- { field:{$eq:<value>}}
$in and $nin -- {field:{$in:[value1,value2]}}


18) write the query to find the prodnames of the products having both black and silver colors.
db.product_catalog.find(
	{ colors : { $all : ["black", "silver"] } },
	{ _id: 0, prodname: 1 }
)

19) To retrieve the products whose rating field is of 'Null' datatype, either of the below commands can be used

db.product_catalog.find(
	{ rating: { $type:10 } }
)
 or 
db.product_catalog.find(
	{ rating: { $type:"null" } }
)

20) Query Projection Operator

Comparison 
Logical 
Element Query 
Array query -- $size, $elemMatch

db.employee.find( { bonus: { $exists: true} } )
db.employee.find( { salary: { $type: 1 } } ) 
db.empDetail.find({teamMates:{$size:3}}).pretty()
db.students.find(
   { scores: { $elemMatch: { $gte: 80, $lt: 85 } } }
)

----- UPDATE --------

21) Update 
db.product_catalog.update( 
	{  prodname : "nosql distilled"  }, 
	{  $set: {  "prodname" : "NoSQL Distilled - Second Edition"  } } 
)
 for updating many, use updateMany instead of update.

22) In MongoDB, if you try to update a document that does not exist, a new document is inserted with just the fields specified. 

db.product_catalog.updateMany(
      { "price" : { $gt : 80000 }, "manufacturer" : "apple" },
      { $set: { "prodname" : "iphone 7 plus" } },
      { upsert: true } 
)
we have set the attribute upsert to true. This allows a new document to be inserted if there are no documents to be updated that match the criteria specified.

23) To update many documents in one go ( { $set: { <field1>: <value1>, ... } } )
db.product_catalog.updateMany( 
	{"genre.academic": "technical"}, 
	{ $set:  {"genre.academic": "Computer Science Technology"} } 
)

db.product_catalog.updateMany(
      { "price" : { $gt : 80000 }, "manufacturer" : "apple" },
      { $set: { "prodname" : "iphone 7 plus" } },
      { upsert: true } 
)


24) This query increments the price by 50 of the book with the specified ISBN.
If the $inc operator is used on a field that does not exist, it creates the field and sets its value as the specified value.

db.product_catalog.update(
	{ ISBN: 18407806 },
	{ $inc: { price: 50 } }
)
db.product_catalog.update(
   { ISBN: 18407806 },
   {  $inc: {  quantity: 10 } }
)

25) Updating values in arrays. If colors field is not present, it will be created with the given values.
db.product_catalog.update(
	{ prodid: 7000001},
	{ $push: { colors: "white" } }
)

26) Since both the elements need to be pushed individually to the array, we need to modify the $push operator. 
Using $each ensures that both the elements are pushed individually, rather than appending an array containing the new elements.
db.product_catalog.update(
   { prodid: 7000001  },
   { $push: { colors: { $each: [ 'midnight blue', 'red' ] } } }
)

27) The below query will set the new value of the field specified as 1st parameter if the specified value is less than the existing value. 
If no such field means it will set the field with the specified value.
             
{$min: {field: <value>}}
db.students.update( {name:"Rohit"}, { $min: { mark: 70 } } )   ----  marks value will get changed to 70 if earlier marks value is > 70.

28) $max will set the value of the field specified, if the specified value is greater than the existing value. 
If no such field means it will set the field with the specified value.

{$max: {field: <value>}}
db.students.update( {name:"Anirudh"}, { $max: { mark: 90 } } ) ---  marks value will get changed to 90 if earlier marks value is < 90.

29) The query will insert the field specified if upsert: true does not found a match, else will update the field specified in $set by ignoring the field mentioned along with $setOnInsert

update({<condition>}, {$set:{field1: value }, $setOnInsert:{Field: value}}, {upsert: true})
db.customer.update({cid:"C104"},{$set:{cname:"Gautham"},$setOnInsert:{Total:678}},{upsert:true})

30)This operator can be used along with $addToSet or $push operator in order to update “multiple” values to an array field. The updating happens only if the mentioned value does not exist in the field.

            {$addToSet: {field: {$each: {[<value>]}}}}     or -- only distinct vaules will be added

            {$push: {field: {$each: {[<value>]}}}} 
$each to be used so that the values are added individually else values would be added as an array.

31)The positional operator $ will help you to update an array element without explicitly mentioning the position of the element in the array. 
            
{"arrayField.$":<newValue>} 
db.customer.update({cid:"C103",item:"Toothbrush"},{$set:{"item.$":"Cornflakes"}})

32) $[] operator will update all the elements in the mentioned array, instead of a particular element in the array. 

{"arrayField.$[]":<newValue> } 
db.students.update({studName:"Rahel"},{$set:{"marks.$[]":100}})

33) Extra update operators

$postion -- Used with $push. Specifies position in array at which $push should perform insert, else $push appends the new element to the array.
db.product_catalog.update({prodid:7000},{$push:{colors:{$each:["blue","green"],$position:0}}})

$[<identifier>] -- filtered positional operator. It identifies the array element that matches the arrayFilter.
$pullAll -- It removes all the instances of the specified from the array.
$slice -- Used to limit the number of array elements during $push operation.

--- DELETE -----

34) The deleteOne() function is used to delete a single document. By default, this function will delete only the first matching document. The syntax for this method is as shown

db.collection_name.deleteOne(
	{ <<remove criteria>> }
)
db.product_catalog.deleteOne( { prodname: "Java for Dummies"} )

db.product_catalog.deleteMany(
    {
        price: { $lt : 1000 } 
    }
)

To delete all the documents from the collection
db.collection_name.deleteMany( {} )


----- AGGREGATION ------

35) Using count() to get the total number of products categorized as 'smartphones'

db.product_catalog.count( { "categories.sub": "smartphones" })

36) This method is used to retrieve an array of the distinct values of a particular field. The query given below is used to get distinct manufacturers from the product catalog.

db.product_catalog.distinct( "manufacturer" )

37) We group by manufacturer, by specifying _id:"$manufacturer" inside $group.

We use {"$sum": "$price"} to specify that we want the sum of the prices of all the products made by each manufacturer. This value will be stored in a field called totalPrice for each manufacturer.

$project is used to specify which fields are required for performing the aggregation.

$group is used to group the fields by value and then perform some aggregation

db.product_catalog.aggregate( [
	{ $project: { _id: 0, manufacturer: 1, price: 1 } },
	{ $group: { _id: "$manufacturer", totalPrice: { $sum: "$price" } } }
] )

38) We can use $sum:1 to count the total number of documents matching the group criteria. In this case, the count of products grouped by each manufacturer.

db.product_catalog.aggregate( [
	{ $group: { _id: "$manufacturer", totalProducts: { $sum: 1 }} }
] )

39) Operators $sort, $limit and $out.

db.product_catalog.aggregate( [
	{ $sort : { price: 1 } },
	{ $limit: 5},
	{ $out: "FiveCheapestMobiles"}
] )

In line 2, $sort is used on the price to specify sort by ascending (1) or descending (-1)

In line 3, $limit is used to specify only 5 matching documents must be returned

In line 4, $out is used to specify the name of the collection in which the matching documents will be stored.

the result is returned inside the new collection specified by $out operator.

db.FiveCheapestMobiles.find().pretty()


40) $unwind is applied to the array field. It generates an output document for each array element.

Example:

db.students.insertOne({"rollno":"32","name":"Rekha","marks":[45,47,39,35,42]})

db.students.aggregate([{$unwind:"$marks"}])

41) $lookup will help you to perform join on collection or a self-join and returns a sub-array as a document.

Syntax:

{
   $lookup:
     {
       from: <collection to join>,
       collection1Field: field targeted of the input documents,
       collection2Field: <field targeted of the documents  specified in "from" collection>,
       as: <array field that is obtained as output>
     }
}

Where,

from – specifies the collection to be considered 

collection1Field – this is the field being used to carry out $lookup operation mentioned in the ‘from’ tag. $lookup checks for matching criteria between the collection1Field and collection2Field. 
If any matching condition is not fulfilled, then the match is done using the null value.

collection2Field- this is the field considered to perform the lookup on the ‘from’ tag. $lookup checks for matching criteria between the collection2Field and collection1Field. 
If any matching condition is not fulfilled, then the match is done using the null value.

as – acts as an alias where we mention the name of the new array field which will contain the newly match documents. In case of an already existing array name. It will be overwritten.

Example:

db.customer.aggregate([
   {     $lookup:       {
         from: "resident",
         localField: "cname",
         foreignField: "rname",
         as: "customer_Details"
       }
  }])

Customer details array will have resident collection details in it.

------- Map Reduce   ----- This is extreme. Learn this

42) MapReduce function
db.collection.mapReduce(
                                    function() {emit(key,value);},  //map function
                                    function(key,values) {return reduceFunction}, {
                                    out: collection,
                                    query: document,
                                    sort: document,
                                     limit: number
                                }
          )

-------- INDEXES ---------

43) The performance for queries based on indexed and non-indexed fields can be analyzed by using the explain("executionStats") 
method 

db.product_catalog.find( 
	{ price: { $gte: 5000, $lte: 20000 } } 
).explain("executionStats")

44) To create an index on a single field, we can use the createIndex() method
db.product_catalog.createIndex(
	    { price:-1 })


map()  - a function that performs mapping of value with a key and emitting a key-value pair corresponding to it. 

reduce() - a function that clubs all the documents having the identical key. 

out()  - it is used to mention the name of the new collection where the documents will be  stored

query() - acts as the specific fields filter that need to be part of the output 

sort() – needed to order the fields in a specific format (asc, desc).  

limit() -  one can choose to limit the number of documents to be added as the resultant set.  

45) Single field index
db.product_catalog.createIndex(
     { price:-1 })

46) Compound Index

db.product_catalog.createIndex(
		{ price:1, rating:-1 })

47) Text Index 

First, we can create a text index on the categories field
db.product_catalog.createIndex(
	{categories:"text"})
Now, the $text operator is used to perform text search on the indexed field to retrieve the details of 'smartphones'.
db.product_catalog.find(
	{ $text:{ $search:"smartphones"}})

48) Multi Key Index 

db.coll.createIndex( { <field>: < 1 or -1 > } )

49) Drop Index
 
An index on colors can be dropped using either the index name or the index field

db.collection_name.dropIndex( "colors_1" )

db.product_catalog.dropIndex( { colors:1 } )

NOTE: By default, a unique index is automatically created on the _id field that cannot be dropped.

50) Get all indexes in a collection

db.collection_name.getIndexes()

51) Delete all indexes

db.collection_name.dropIndexes()

52) Create Indexes to Support Queries

db.product_catalog.createIndex({category.main:"smartphone": 1})

Let us look at the various components of the MongoDB sharded cluster:

Shard: A shard is the subset of the actual data set. Each of these shards can be deployed separately as a replica.

Mongos: Mongos plays the role of a router in this cluster which acts as an interface between the client and the shards.

Config servers: In order to store metadata and configuration settings for the clusters we use the config servers. For the latest version of MongoDB, we must deploy the replica sets to these config servers individually.

Client: Any query request coming from the FE of an application will serve as the client.

Mongod: Multiple instance of MongoDB here represents the mongod blocks.


----------APPENDIX ------------

53) The mechanism to distribute data across multiple machines is called sharding. In order to improve the efficiency of the server, 
we apply the concept of sharding for databases having heavy structures collections with frequent queries.

54) Creating sharding cluster ---- not done


55) There are several packages available to connect server side to MongoDB database. Some popular packages which are used to communicate are 

MongoDB client
Mongoose
Mongojs


56) Node JS connection with MongoDB   ------ Nodejs should be installed beforehand

56.1)	Let us learn how to connect to MongoDB client

Step 1: Installing MongoDB driver.

npm install mongodb

Step 2: Create a file by the name “demo-mongodb.js”. Add the below lines of code to it.

var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/mydb";
MongoClient.connect(url, function(err, db) {
  if (err) throw err;
  console.log("Database created!");
  db.close();
});

Step 3: Run the command

C:\Users\Your Name>node demo-mongodb.js
This will give the result as: Database created

56.2) Mongoose

To use this module, we need to install it using the below command.

npm install mongoose

Steps to connect to MongoDB from Node.js using mongoose:

Step 1: Import mongoose module.

var mongoose = require("mongoose");

Step 2:  Connect to 'mydb' database with the mongoose.connect() method.

Syntax: mongoose.connect(uri, options);

mongoose.connect("mongodb://localhost:27017/mydb", { useNewUrlParser: true });

Step 3:  Create a 'users' schema. Each schema in mongoose maps to a MongoDB collection and defines the structure of the documents within that collection.

var userSchema = mongoose.Schema({
  username: String,
  password: String
});
String, Number, Date, Buffer, Boolean, Mixed, ObjectId, Array, Decimal128, Map are valid SchemaTypes.

Step 4: To use the schema definition, we need to convert the schema into a model so that we can work with it.

Syntax: mongoose.model(modelName, schema):

Pass the biodataSchema as a parameter to mongoose.model() method as below:

var User = mongoose.model("User", userSchema);


56.3) Connecting to MongoDB from an express application using mongo.js package

Using mongojs, which is a node package that allows accessing MongoDB database using an API which is very similar to MongoDB’s javascript shell.

This driver helps in communicating with the database and helps to perform operations like saving documents or retrieving them.

For installing mongojs module, use the node package manager.

npm install mongojs
Once the mongojs driver is installed, start the MongoDB server.

var mongojs = require('mongojs');
var db = mongojs('db', ['WalletUsers']);
The mongojs driver is imported into the application and then connected to the database by-passing the connection string 'db' and the collection 'WalletUsers'.


--------Concepts -----------

The second parameter, or the second document is for the projection. 
This parameter specifies which fields are to be returned in the documents that match the query selection criteria. 
{ field1: <value>, field2: <value> ... }
The <value> is always written as 0 or 1.

0 means omit this field and 1 means include this field. --  (10)--(12)

----Operators---------  (17)
$eq, $lt, $gt, $lte, $gte, $in, $nin, $all, $size and $elemMatch.

------various datatypes supported in BSON and their corresponding number and string alias that can be used while querying the documents  --------- (19)
1,"double"
2,"string"
3,"object"
4,"array"
5,"binData"
7,"objectId"
8,"bool"
9,"date"
10,"null"
11,"regex"
16,"int"


Complex query 
db.product_catalog.find({ $or:[{ $and:[{price:{$gte:1000}},{price:{$lte:20000}}]}, {manufactures:{$in:["nike","reebok"]}}]}).pretty() 

Operators in update query -- (24)
$inc
$mul
$set
$unset
$rename

Array operators in update query -- (25)
$addToSet
$pull
$pullAll
$pop


Update Operators ---- (27) -- (29)
$min
$max
$setOnInsert

$ should not be used with upsert as $ will be considered as the field name. 

$, if used with queries that travers nested arrays, will result in error as the replacement for the $ is a single value. 

If $ is used within $unset instead of removing the matching element, it will be set to null. 

Extra update operators
$postion
$[<identifier>]
$pullAll -- requires an array argument
$slice

{ $arrayElemAt: [ <array>, <indx> ] }


----- Miscellaneous ----

1) To check collections in a DB 
use Zoiva
show collections 

2) To rename exisiting field
db.collection_name.updateMany({},{$rename:{fieldname:"value"}})

3) To remove field from a collection 
db.collection_name.update({},{$unset:{fieldname:""}})

4) Map Reduce Query
db.runCommand({
   mapReduce:"userDetail",
   map:function()
   {
     
     emit(this.name,this.age)
   },
   reduce:function(name,counters)
   {
     
      return Array.sum(counters);
     }
   ,out:"SumOfAges"
 })

5) To get smarphones using aggregate query 

db.product_catalog.aggregate({$match:{"categories.sub":"smartphones"}}).pretty()

6) Aggregate query to display the count of smartphones only under the electronics category having price greater than 20000.

db.product_catalog.aggregate( [{$match:{"categories.sub":"smartphones"}},{$match:{price:{$gt:20000}}},{$count:"test"} ])

------- Complex Queries --------

1) We need to get the teamMate(empid’s)  and for those empid’s in the teammate array, we need to aggregate the SMEin and their count.

db.employees.aggregate([{
  $match: {
    empid: 1011,
  }
}, {
  $unwind: '$teamMates',
}, {
  $lookup: {
    from: 'employees',
    localField: 'teamMates',
    foreignField: 'empid',
    as: 'tm',
  }
}, {
  $project: {
    tm: {
      $arrayElemAt: ['$tm', 0]
    }
  }
}, {
  $unwind: '$tm.SMEin'
}, {
  $group: {
    _id: '$tm.SMEin',
    count: {
      $sum: 1
    }
  }
}]);

2) db.employees.aggregate([
{   $match: {     empid: 1011,   } }, {   $unwind: '$teamMates', }
])
i.e. it will expand each element in teammate array of empid:1011.

3) db.employees.aggregate([{   
    $match: {     empid: 1011,   } },
    {   $unwind: '$teamMates', },
    {   $lookup: {     from: 'employees',   
                       localField: 'teamMates',
                       foreignField: 'empid',     
                       as: 'tm',   } 
    }])

4) db.employees.aggregate([{   
    $match: {     empid: 1011,   } }, 
    {   $unwind: '$teamMates', }, 
    {   $lookup: {  from: 'employees',     
                    localField: 'teamMates',     
                    foreignField: 'empid',     
                    as: 'tm',   } }, 
    {   $project: { tm: { $arrayElemAt: ['$tm', 0]}}
 }]);

5) db.employees.aggregate([{   
    $match: {     empid: 1011,   } }, 
    {   $unwind: '$teamMates', }, 
    {   $lookup: {  from: 'employees',     
                    localField: 'teamMates',     
                    foreignField: 'empid',     
                    as: 'tm',   } }, 
    {   $project: { tm: { $arrayElemAt: ['$tm', 0]} } }, 
    { $unwind: '$tm.SMEin' }
]);


----------unfinished task -------------

To create sharding cluster in MongoDB --- (54)





