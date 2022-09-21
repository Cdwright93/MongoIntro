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