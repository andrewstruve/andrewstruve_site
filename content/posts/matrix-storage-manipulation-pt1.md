---
title: "Matrix Storage and Manipulation Pt 1"
date: 2020-10-10T13:08:09-08:00
draft: true
tags: ["matrix", "math", "python", "DB", "Mongo", "Front-End"]
---
When I took linear algrebra, one of the most frustrating experiences I had was watching my professor
enter long matrices in the calculator. Frequently he would use examples from the book and they would commonly
use the same matrices for this example. This got me thinking... why can't this be easier? There seems to be 
solutions to this problem but they are not free. What if you could enter the matrices you need once,
store them in a database, and then perform the operations you need to with them right on a web page?

This project will involve many parts including:
- Data Entry
- Ajax Calls
- Data Storage
- Data Manipulation

The technologies that will be used to accomplish this goal will be:
React - Front End
Flask - Back End
MongoDB - Database

All of this will be wrapped up using docker so that any user can deploy this application.
- https://www.digitalocean.com/community/tutorials/how-to-set-up-flask-with-mongodb-and-docker

What data will we have to enter and store?

A matrix will have the following properties
- id
- name 
- rows
- columns
- the numbers in the matrix

So if we have a 2 by 2 matrix, this could be entered as a json object
```
{
    _id: 1
    name: "basic",
    rows: 2,
    columns: 2,
    content: "[[1, 2], [3, 4]]"
}
```
Using mongo db image
https://phoenixnap.com/kb/docker-mongodb

To connect to the data base we will use pymongo
I often end up back at the following site for examples on how to use pymongo:
- https://www.w3schools.com/python/python_mongodb_getstarted.asp

```
import pymongo
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["matrices"]

mydict = { "_id": 1, "name":"basic_2by2", "rows": 2, "columns": 2, "Content": [ [1,2],[3,4]] }
x = mycol.insert_one(mydict)

# print all entries
for x in mycol.find():
	print(x)
```

we can also insert many at a time. This will be useful for testing our matrices with different operations.

```
import pymongo
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["matrices"]

mylist = [{ "_id": 1, "name":"a", "rows": 2, "columns": 2, "Content": [ [1,2], [3,4]] },
	  { "_id": 2, "name":"b", "rows": 2, "columns": 2, "Content": [ [2,3], [4,5]] },
	  { "_id": 3, "name":"c", "rows": 2, "columns": 2, "Content": [ [4,5], [6,7]] }]

x = mycol.insert_many(mydict)
inserted_ids = x.inserted_ids
print(inserted_ids)

# print all entries
for x in mycol.find():
        print(x)
``` 

We will be able to take the "Content" of an array and set it to the content of a numpy array (which is basically a matrix)
```
>>> import numpy as np
>>> a = { "_id": 1, "name":"a", "rows": 2, "columns": 2, "Content": [ [1,2], [3,4]] }
>>> arr = a["Content"]
>>> print(arr)
[[1, 2], [3, 4]]
>>> b = np.array(arr)
>>> print(b)
[[1 2]
 [3 4]]
>>> b.ndim
2
```

Next Steps:
Delete what is in the database.
Create scripts to test out setting matrices, creating matrices, then deleteing them all at the end.

test
