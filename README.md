# MongoIntro

//SET UP DB ##################
//drop all previous 50 blogs
db.blogs.drop()
//insert 10 sample blogs
db.blogs.insertMany({
[
"createdAt":{date},
"title":{string},
"text":{string},
"author":{string},
"lastModified":{date}, "categories":{string[]},
"id":{string},
"ObjectId":{Number}
]
})
//modify the blog data to change the way it is being stored

db.blogs.updateMany({},{$set:{"categories":[]}})
db.blogs.updateMany({},{$set:{"ObjectId":ObjectId()}})
db.blogs.updateMany({},{$set:{"createdAt":new Date()}})
db.blogs.updateMany({},{$set:{"lastModified":new Date()}})
//set objectId to a number
db.blogs.updateMany({},{$set:{"objectId":NumberInt()}})
//reassign new numbers to all objects in the database for the objectId
let number = 1
db.blogs.find().forEach(function(doc){
doc.objectId = (number)
db.blogs.save(doc)
number++
})

//QUERYING DB ##################
//find one blog by author
db.blogs.findOne({author:"Brett Wolf"})
//find all blogs whose object id is greater than 5
db.blogs.find({objectId:{$gt:5}})
//find all blogs whose createdAt is after April 1, 2022
db.blogs.find({createdAt:{$gt:new Date("April 1, 2022")}})
//find all blogs where the field lastModified exists
db.blogs.find({lastModified:{$exists:true}})
//find all blogs where the createdAt type is a date
db.blogs.find({createdAt:{$type:"date"}})

MORE QUERIES ##################
//Find all blogs in which the lastModified does not exist and set it ###DONE PREIVOUSLY IN ABOVE CODE

### From now on, all the following queries should update lastModified to be the current datetime

//Find all blogs created after May 2022 and add "lorem" as a new category in the categories array

db.blogs.updateMany({createdAt:{$gt:new Date("May 1, 2022")}},{$push:{categories:"lorem"},$set:{lastModified:new Date()}})

//Find all blogs that have the category "voluptas" and pull "voluptas" from the categories
db.blogs.updateMany({categories:"voluptas"},{$pull:{categories:"voluptas"},$set:{lastModified:new Date()}})

//Find all blogs with "corrupti" in the categories and delete those blogs
db.blogs.deleteMany({categories:"corrupti"})

- Stretch ##completed
  //Find a blog with a specific phrase in the text
  db.blogs.find({text:{$regex:"phrase"}})
//Find all blogs that have "qui" in the categories array
  db.blogs.find({categories:{$regex:"qui"}})

//what is "regex"?
//https://docs.mongodb.com/manual/reference/operator/query/regex/

//basically, -q and $regex are the same thing.
