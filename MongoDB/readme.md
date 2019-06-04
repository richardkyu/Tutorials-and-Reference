# MongoDB

So, what are the uses of MongoDB?
* Storing customer or client information
* Storing best scores or other numerical values in a video game associated to an account.
* Essentially, the premise here is that it is a database that you can store values into from user-side interaction and then retrieve those values later.

NoSQL - a movement where you can save data to a database without using tables, which are traditionally used in SQL. Benefits to performance, speed, program flexibility. 

Install from [MongoDB website](https://www.mongodb.com/)

## 1. Basic Server Access on Mac.

Type in mongod into a terminal window. The server will run in the terminal window.

Then, open up a new terminal window and type in mongo, this will create a connection to the server that we just opened. Type in db to display the list of existing dbs (should just have the sample test.db)

Remember that at this point you will have two terminals open.

# 

## 2. Creating Databases and Inserting Data


**How to create a new database**

Whenever you create a new website or new project, you'll want to create a new database for it - it's a container for all the data on your website.

A database is made of different collections, or similar data. For instance, all of the user's basic info or posts would go into separate collections, in the context of a social media network.

**db**

* Check what current database you are in.

        db

**use**

* Checks if there is a database.
* If database exists, it will switch to the database.
* If the database does not exist, it will create then switch into the database.

        use players

**db.dropDatabase()**
* Deletes the database.

Anytime new info is inserted, it must go into a collection.

**db.collections.insert()**

* Collections should be the name of your collection. In this example it is players, so the command is db.players.insert().

* You can insert data as entries one-by-one by putting the data entry in as an argument for insert.

* You can bulk insert via: **db.collections.insert([a,b,c])** where a, b, and c denote separate entries, where the [] denotes a bulk insert, and where commas denote distinct entries.

The result of a bulk insert is shown here.

![Preview](https://i.imgur.com/KP9OgoK.png)

In the above, nInserted indicates the number of new entries inserted.

**show collections**

* If you want to see all the collections within a database, use this command.

**db.collections.find()**

* Remember that collections is the name of the collection you want to query the entries (also known as documents) for.

![Preview](https://i.imgur.com/EhSMOD9.png)

**db.collections.find().pretty()**

* If you want to format the entries in a collection, you can use the following command.

![Preview](https://i.imgur.com/BHuQsgD.png)

**db.collections.findOne()**

* Finds the first entry.


Remember:
Inside a database, you have collections, inside collections you have entries or documents.

# 

## 3. Updating, Removing, and Collections

"_id" : ObjectID() is mongo's way of differentiating between two entries with similar attributes.

Above, we have the player Craig Adams' unique identifier displayed as the following:

**"_id" : ObjectId("5cf69d5a2e7e76cb23287751")**

Suppose there were two players with the same name. If you wanted to delete that record from the collection, then you would end up deleting all players with that name, so you use the ObjectId to specify which only exactly should be deleted.

To remove the record, we use this command:

**db.collections.remove()**

* Takes one parameter. The selection criteria.

        db.players.remove(
            {"_id" : ObjectId("5cf6a8b23f2b2a8cc9b57c97")}
            )

Running db.players.find() will reveal that this first entry was indeed removed from the collection players.

**db.collections.update()**

* Takes two criteria. (1) The selection criteria and (2) the updated information.

        db.players.update(
            {"_id" : ObjectId("5cf6a8b23f2b2a8cc9b57c98")},
            {"position" : "Left Wing",
            "id" : 8475761,
            "weight" : 195,
            "height" : "6' 2\"",
            "imageUrl" : "http://1.cdn.nhle.com/photos/mugs/8475761.jpg",
            "birthplace" : "Gardena, CA, USA",
            "age" : 23,
            "name" : "Bob Bennett",
            "birthdate" : "November 27, 1991",
            "number" : 19}
        )

**db.collections.drop()**

* This will just drop the collection on which the drop() method is invoked.

        db.players.drop()


#

## 4. Find and Search Query

**db.collections.find({key:value})**

* Example: 
        
        db.players.find(
            {"position":"Goalie"}
            )

You can include more than one search criteria using "and" logic.
* Example: 

        db.players.find(
            {"position":"Defenseman", 
            "age":21}
            )

Using "or" criteria for more than one criteria.
* Example: 

        db.players.find({
            $or:[
                {"position":"Right Wing"},
                {"position":"Left Wing"}
            ]
        })

This statement above will find the players occupying either right wing or left wing positions.


* Example:

        db.players.find(
            {'age':{$gt:30}}
        )

Other quantitative operators: $gt, $lt, $gte, $lte, $ne


* Example:

        db.players.find(
            {'position':"Center"},
            {'name':1, _id:0}
        )

This will return all centers in the league., but just the names of the centers. 
_id, or the object's unique idea is returned on default, so it must be specified to be 0.

* Example:

        db.players.find(
            {'position':"Center"},
            {'name':1, _id:0}
        ).limit(3)

        db.players.find(
            {'position':"Center"},
            {'name':1, _id:0}
        ).skip(2)

Respectively, .limit(3) will limit the results to three.

Meanwhile .skip(2) skips the first two results of the query.

## 5. Indexing
Bank data from [this json](https://github.com/buckyroberts/Source-Code-from-Tutorials/blob/master/Other/SampleJsonData/fake_bank_data.json)

Create users collection and import data through below:

        db.users.insert(
            {[data]}
            )

Finding age of users that are 23 or younger:

        db.users.find(
            {'age':{$lte:(23)}}
        )

Execution results.

        db.users.find(
            {'age':{$lte:(23)}}
        ).explain("executionStats")

The totalDocsExamined returns 35 results, it queries the database 35 time, which is inefficient if you have 100,000 or 1 million users.

This is where indexing comes into play.

* Example:

        db.users.ensureIndex(
            {'age':1}
        )

Above, 1 means true, or create an index for that key.

        db.users.getIndexes()

        db.users.find(
            {'age':{$lte:(23)}}

        ).explain("executionStats")

Will return totalDocsExamined as 4.

To drop indexes:
        
        db.users.dropIndex(
            {'age':1}
        )

Generally, you want to only index the columns you search for frequently. 

## 6. Aggregate Functions