# MongoIntro

Queries ######
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