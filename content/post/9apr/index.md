---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Accessing MongoDb with Pymongo"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-09T10:27:05+08:00
lastmod: 2020-04-09T10:27:05+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Center"
  placement: 2
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []

---

In the midst of looking for a job in such situation, I took some time to pick up new knowledge which I think it's useful. One of them is **MongoDB**.

**So what is MongoDB**? 

MongoDB is a document-oriented NoSQL database used for high volume data storage. MongoDB is a database which came into light around the mid-2000s. It falls under the category of a NoSQL database. Traditional RDBMS uses SQL syntax to store and retrieve data for further insights. Instead, a NoSQL database system encompasses a wide range of database technologies that can store structured, semi-structured, unstructured and polymorphic data. 



**What is NoSQL?**

NoSQL is a non-relational database that does not require a fixed schema,avoid joins and is easy to scale. NoSQL database stands for "Not Only SQL" or "Not SQL." 



**Why NoSQL?**

Structured SQL is difficult to scale as database grows. Unstructured databases do not need to follow predefined format.

There are several ways of installing MongoDB on the machine. 

1. I have chose to install them using HomeBrew and largely uses Command Line to interact with MongoDB. There are some things you may need to watch out like Os version of your Mac. You may wish to follow this installation guide. This guide makes it easy to understand and follow like [creating a connection on local machine](https://zellwk.com/blog/local-mongodb/).
2. There is also another way which is to install MongoDB Compass on the local machine. You may wish to follow this [guide](https://docs.mongodb.com/compass/master/install/). 

## Python with MongoDB

In python, in order to connect to MongoDB, we will need a package call PyMongo. Assuming installation is done correctly, now we will move on to Python to connect to our database. MongoDB works in the key value pair metholody.

Below snippet is the basic of connecting to the database. The package "pprint" is called pretty printer which allows user to print data in a more readable way.

```python
import pymongo 
import pprint
mongo_uri = "mongodb://localhost:27017/"  
client = pymongo.MongoClient(mongo_uri)
```

To see available databases:

```python
client.list_database_names()

```

**Creating Database and collection**

It is simple to create a database and a collection in python with the following syntax.

```python
mydb=client['sample']
mytable=mydb['table']
```

However, this database and collection will not be shown if we run list_database_names() module. This is because MongoDB does not show any empty databases. We will need to insert arbitrary data into the collection. 

```python
testInsert=mytable.insert_one({"country":'India'}).inserted_id

```

We can also use pandas to load a csv and transform into MongoDB.

```python
df=pd.read_csv('sampleMongoData.csv') 
#create empty array
listofDocs=[]
for i in df.index:
    listofDocs.append(dict(df.iloc[i]))

myfinal = mytable.insert_many(listofDocs)

```

Reading from MongoDB and transfer to a dataframe

```python
# transfering to dataframe
sample=table.find()
df=pd.DataFrame(sample)
df.head()

```

**Inserting mutliple observations into MongoDB**

```python
mport datetime
new_posts = [{"name": "newMike",
            "username": "latestpost!",
            "date": datetime.datetime(2009, 11, 12, 11, 14)},
            {"name": "Eliot",
            "title": "onceAgain",
            "text": "and pretty easy too!",
            "date": datetime.datetime(2009, 11, 10, 10, 45)}]

final = mytable.insert_many(new_posts)

final.inserted_ids
```

Upon successful data entry, this will be shown. 

```python
[ObjectId('5e8c2ebc6057435b48b52886'), ObjectId('5e8c2ebc6057435b48b52887')]
```

**Filtering entry**

In order to filter an entry of document, you will need to use find_one method

```python
mytable.find_one({"name":'Same'})
```

**Delete entry** 

To delete entry, you will just need to use delete_one method

```
mytable.delete_one({'name':'Mike'})

```

**Update entry**

To update entry, you will to use the update_one method

```
myquery = { "address": "Valley 345" }
newvalues = { "$set": { "address": "Canyon 123" } }

mytable.update_one(myquery, newvalues)
```



## Conclusion

I hope the resources and this post willl be able to show you the basics of MongoDB and how you can try to integrate Python with MongoDB.



## References

- https://www.analyticsvidhya.com/blog/2020/02/mongodb-in-python-tutorial-for-beginners-using-pymongo/
- https://www.guru99.com/create-read-update-operations-mongodb.html
- https://zellwk.com/blog/install-mongodb/