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
//modify the  blog data to change the way it is being stored

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