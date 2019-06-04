# MongoDB

So, what are the uses of MongoDB?
* Storing customer or client information
* Storing best scores or other numerical values in a video game associated to an account.
* Essentially, the premise here is that it is a database that you can store values into from user-side interaction and then retrieve those values later.

NoSQL - a movement where you can save data to a database without using tables, which are traditionally used in SQL. Benefits to performance, speed, program flexibility. 

Install from [MongoDB website](https://www.mongodb.com/)

### 1. Basic Server Access on Mac.

Type in mongod into a terminal window. The server will run in the terminal window.

Then, open up a new terminal window and type in mongo, this will create a connection to the server that we just opened. Type in db to display the list of existing dbs (should just have the sample test.db)

Remember that at this point you will have two terminals open.

### 2. Basic commands in MongoDB

**A. How to create a new database**

Whenever you create a new website or new project, you'll want to create a new database for it - it's a container for all the data on your website.

A database is made of different collections, or similar data. For instance, all of the user's basic info or posts would go into separate collections, in the context of a social media network.

**db**

* Check what current database you are in.

**use**

* Checks if there is a database.
* If database exists, it will switch to the database.
* If the database does not exist, it will create then switch into the database.

**db.dropDatabase()**
* Deletes the database.

Anytime new info is inserted, it must go into a collection.

**db.[collections].insert()**

Collections should be the name of your collection. In this example it is players, so the command is db.players.insert().

You can insert data as entries one-by-one by putting the data entry in as an argument for insert.

You can bulk insert via: **db.collections.insert([a,b,c])** where a, b, and c denote separate entries, where the [] denotes a bulk insert, and where commas denote distinct entries.

The result of a bulk insert is show here. 
![Preview](https://i.imgur.com/KP9OgoK.png)

In the above, nInserted indicates the number of new entries inserted.

**show collections**

If you want to see all the collections within a database, use this command.

**db.[collections].find()**

Remember that collections is the name of the collection you want to query the entries (also known as documents) for.

![Preview](https://i.imgur.com/EhSMOD9.png)

If you want to format the entries in a collection, you can use the following command.

**db.[collections].find().pretty()**

![Preview](https://i.imgur.com/BHuQsgD.png)

**db.[collections].findOne()**

Finds the first entry.


Remember:
Inside a database, you have collections, inside collections you have entries or documents.


### 3. Creating Databases and Inserting Data