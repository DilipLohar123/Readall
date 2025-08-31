## MongoDB Learning TODO List (Beginner to Pro)

- [ ] **Introduction to MongoDB**
	- [ ] What is MongoDB?

		**Answer:**
		MongoDB is a popular open-source NoSQL database that stores data in flexible, JSON-like documents. Unlike traditional relational databases (SQL), MongoDB does not use tables and rows. Instead, it uses collections and documents, making it easy to store and query complex data structures.

		**Example:**
		A document in MongoDB might look like this:
		```json
		{
			"name": "Alice",
			"age": 25,
			"skills": ["Python", "MongoDB"]
		}
		```

	- [ ] NoSQL vs SQL databases

		**Answer:**
		- **SQL (Relational Databases):** Use tables, rows, and columns. Data is structured and relationships are defined using foreign keys. Example: MySQL, PostgreSQL.
		- **NoSQL (MongoDB):** Uses collections and documents. Data is flexible, can be nested, and does not require a fixed schema. Good for handling unstructured or semi-structured data.

		**Example:**
		- SQL Table:
			| id | name  | age |
			|----|-------|-----|
			| 1  | Alice | 25  |

		- MongoDB Document:
			```json
			{ "name": "Alice", "age": 25 }
			```

	- [ ] Installing MongoDB (Windows, Mac, Linux)

		**Answer:**
		1. **Windows:**
			 - Download from https://www.mongodb.com/try/download/community
			 - Run the installer and follow the setup wizard.
			 - Add MongoDB to your system PATH for easy command-line access.
		2. **Mac:**
			 - Use Homebrew: `brew tap mongodb/brew` then `brew install mongodb-community`
		3. **Linux (Ubuntu):**
			 - Import the public key: `wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -`
			 - Create a list file: `echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list`
			 - Update and install: `sudo apt-get update && sudo apt-get install -y mongodb-org`

		**Example:**
		After installation, run `mongod` to start the MongoDB server, and `mongosh` to open the shell.

	- [ ] MongoDB Atlas (Cloud)

		**Answer:**
		MongoDB Atlas is a cloud-based MongoDB service. It allows you to create, manage, and scale MongoDB clusters without installing anything locally.

		**Example:**
		1. Go to https://www.mongodb.com/cloud/atlas and sign up.
		2. Create a free cluster.
		3. Connect to your cluster using the connection string provided (e.g., in MongoDB Compass or your application code).
		4. Example connection string:
		```
		mongodb+srv://<username>:<password>@cluster0.mongodb.net/myFirstDatabase?retryWrites=true&w=majority
		```

- [ ] **Basic MongoDB Operations**
	- [ ] MongoDB Shell (mongosh) basics

	**Answer:**
	The MongoDB shell (`mongosh`) is an interactive JavaScript interface to MongoDB. You use it to run commands, queries, and scripts.

	**Example:**
	```
	mongosh
	> show dbs
	> use mydb
	> db
	```

	- [ ] Creating and listing databases

	**Answer:**
	Use `use <dbname>` to switch/create a database. List all databases with `show dbs`.

	**Example:**
	```
	> use shop
	> show dbs
	```

	- [ ] Creating and listing collections

	**Answer:**
	Collections are like tables. Create with `db.createCollection('name')`. List with `show collections`.

	**Example:**
	```
	> db.createCollection('products')
	> show collections
	```

	- [ ] Inserting documents

	**Answer:**
	Use `insertOne()` or `insertMany()` to add documents.

	**Example:**
	```
	> db.products.insertOne({ name: "Pen", price: 10 })
	> db.products.insertMany([{ name: "Book", price: 50 }, { name: "Pencil", price: 5 }])
	```

	- [ ] Querying documents (find, findOne)

	**Answer:**
	Use `find()` to get multiple documents, `findOne()` for a single document.

	**Example:**
	```
	> db.products.find({ price: { $gt: 5 } })
	> db.products.findOne({ name: "Pen" })
	```

	- [ ] Updating documents

	**Answer:**
	Use `updateOne()`, `updateMany()`, or `replaceOne()`.

	**Example:**
	```
	> db.products.updateOne({ name: "Pen" }, { $set: { price: 12 } })
	> db.products.updateMany({}, { $inc: { price: 1 } })
	```

	- [ ] Deleting documents

	**Answer:**
	Use `deleteOne()` or `deleteMany()`.

	**Example:**
	```
	> db.products.deleteOne({ name: "Pencil" })
	> db.products.deleteMany({ price: { $lt: 10 } })
	```

- [ ] **Data Modeling**
	- [ ] Documents and Collections

		**Answer:**
		- **Document:** A record in MongoDB, stored as BSON (binary JSON).
		- **Collection:** A group of documents, similar to a table in SQL.

		**Example:**
		```json
		// Document
		{ "name": "Alice", "age": 25 }
		// Collection: users
		```

	- [ ] Embedding vs Referencing

		**Answer:**
		- **Embedding:** Store related data in the same document. Good for data that is accessed together.
		- **Referencing:** Store related data in separate documents and link with IDs. Good for large or shared data.

		**Example:**
		- Embedding:
			```json
			{ "name": "Alice", "address": { "city": "NY", "zip": "10001" } }
			```
		- Referencing:
			```json
			{ "name": "Alice", "address_id": ObjectId("...") }
			// Address is in another collection
			```

	- [ ] Schema design best practices

		**Answer:**
		- Design for how your app queries data.
		- Embed for one-to-few relationships, reference for one-to-many.
		- Avoid deeply nested documents.
		- Use indexes for frequently queried fields.

- [ ] **Advanced Queries**
	- [ ] Query operators ($gt, $lt, $in, etc.)

	**Answer:**
	MongoDB provides operators for advanced queries:
	- `$gt`: Greater than
	- `$lt`: Less than
	- `$in`: In array

	**Example:**
	```
	> db.products.find({ price: { $gt: 10, $lt: 100 } })
	> db.products.find({ name: { $in: ["Pen", "Book"] } })
	```

	- [ ] Aggregation framework (pipeline, stages)

	**Answer:**
	Aggregation processes data records and returns computed results. Use stages like `$match`, `$group`, `$sort`.

	**Example:**
	```
	> db.products.aggregate([
		{ $match: { price: { $gt: 10 } } },
		{ $group: { _id: "$name", total: { $sum: "$price" } } }
	  ])
	```

	- [ ] Indexes (single field, compound, text, geospatial)

	**Answer:**
	Indexes speed up queries. Types:
	- Single field: `db.products.createIndex({ price: 1 })`
	- Compound: `db.products.createIndex({ name: 1, price: -1 })`
	- Text: `db.products.createIndex({ name: "text" })`
	- Geospatial: `db.places.createIndex({ location: "2dsphere" })`

- [ ] **Performance and Security**
	- [ ] Indexing for performance

		**Answer:**
		Use indexes on fields you query often. Avoid too many indexes as they slow down writes.

		**Example:**
		```
		> db.products.createIndex({ price: 1 })
		```

	- [ ] Data validation

		**Answer:**
		Use schema validation to enforce rules on documents.

		**Example:**
		```
		db.createCollection("users", {
			validator: {
				$jsonSchema: {
					bsonType: "object",
					required: ["name", "email"],
					properties: {
						name: { bsonType: "string" },
						email: { bsonType: "string" }
					}
				}
			}
		})
		```

	- [ ] User authentication and roles

		**Answer:**
		MongoDB supports user accounts and roles for security. Create users with specific permissions.

		**Example:**
		```
		use admin
		db.createUser({
			user: "myUser",
			pwd: "myPassword",
			roles: [ { role: "readWrite", db: "shop" } ]
		})
		```

	- [ ] Backup and restore

		**Answer:**
		Use `mongodump` to back up and `mongorestore` to restore data.

		**Example:**
		```
		mongodump --db shop --out ./backup
		mongorestore --db shop ./backup/shop
		```

- [ ] **Working with Drivers**
	- [ ] MongoDB with Node.js

	**Answer:**
	Use the `mongodb` npm package to connect and interact with MongoDB.

	**Example:**
	```js
	const { MongoClient } = require('mongodb');
	const uri = 'mongodb://localhost:27017';
	const client = new MongoClient(uri);
	async function run() {
	  await client.connect();
	  const db = client.db('shop');
	  const products = db.collection('products');
	  await products.insertOne({ name: 'Pen', price: 10 });
	  const result = await products.find().toArray();
	  console.log(result);
	  await client.close();
	}
	run();
	```

	- [ ] MongoDB with Python (PyMongo)

	**Answer:**
	Use the `pymongo` library to connect and interact with MongoDB.

	**Example:**
	```python
	from pymongo import MongoClient
	client = MongoClient('mongodb://localhost:27017')
	db = client['shop']
	products = db['products']
	products.insert_one({'name': 'Pen', 'price': 10})
	for product in products.find():
		print(product)
	client.close()
	```

	- [ ] MongoDB with other languages

	**Answer:**
	MongoDB provides drivers for Java, C#, Go, PHP, and more. See the official docs for language-specific examples.

- [ ] **Deployment and Scaling**
	- [ ] Replica sets (high availability)

	**Answer:**
	A replica set is a group of MongoDB servers that maintain the same data, providing redundancy and high availability.

	**Example:**
	Start three mongod instances with different ports and data paths, then initiate a replica set:
	```
	mongod --replSet rs0 --port 27017 --dbpath /data/rs0-0
	mongod --replSet rs0 --port 27018 --dbpath /data/rs0-1
	mongod --replSet rs0 --port 27019 --dbpath /data/rs0-2
	mongosh
	> rs.initiate()
	```

	- [ ] Sharding (horizontal scaling)

	**Answer:**
	Sharding splits data across multiple servers for scalability. Each shard holds part of the data.

	**Example:**
	Set up config servers, shard servers, and a mongos router. Enable sharding on a database:
	```
	mongosh
	> sh.enableSharding('shop')
	> sh.shardCollection('shop.products', { _id: 1 })
	```

	- [ ] Monitoring and tools (Compass, Atlas, CLI)

	**Answer:**
	- **MongoDB Compass:** GUI for exploring data and running queries.
	- **Atlas:** Cloud dashboard for monitoring, scaling, and backups.
	- **CLI tools:** `mongostat`, `mongotop` for server stats.

- [ ] **Project: Build a Real-World App**
	- [ ] Design schema for a sample app

	**Answer:**
	Example: For an e-commerce app, design collections for users, products, and orders.
	```json
	// users
	{ "_id": ObjectId(), "name": "Alice", "email": "alice@mail.com" }
	// products
	{ "_id": ObjectId(), "name": "Pen", "price": 10 }
	// orders
	{ "_id": ObjectId(), "user_id": ObjectId(), "items": [{ "product_id": ObjectId(), "qty": 2 }] }
	```

	- [ ] Implement CRUD operations

	**Answer:**
	Use insert, find, update, and delete commands to manage data in your app.

	**Example:**
	```
	// Insert a user
	db.users.insertOne({ name: "Bob", email: "bob@mail.com" })
	// Find all products
	db.products.find()
	// Update a product price
	db.products.updateOne({ name: "Pen" }, { $set: { price: 12 } })
	// Delete an order
	db.orders.deleteOne({ _id: ObjectId("...") })
	```

	- [ ] Use aggregation and indexing

	**Answer:**
	Use aggregation for analytics and indexes for performance.

	**Example:**
	```
	// Total sales by product
	db.orders.aggregate([
	  { $unwind: "$items" },
	  { $group: { _id: "$items.product_id", total: { $sum: "$items.qty" } } }
	])
	// Create index on product name
	db.products.createIndex({ name: 1 })
	```

	- [ ] Deploy to MongoDB Atlas

	**Answer:**
	Create a free cluster on MongoDB Atlas, import your data, and connect your app using the provided connection string.
    
	**Example:**
	- Use `mongoimport` to upload data:
	  ```
	  mongoimport --uri "<your-atlas-uri>" --collection products --file products.json
	  ```

---
_Check off each item as you progress!_
