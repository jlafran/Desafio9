# Desafio9

1) ### Agregar a colección producto:
	db.productos.insert({nombre:'Aire Acondicionado',precio:1200,url:'www.pc.com'})


2) ### Agregar a colección mensaje:
	db.mensajes.insert({usuario:'juanlafranconi@hotmail.com',mensaje:'Hola'})


3) ### Listar todos los documentos en cada colección:

	db.mensajes.find()
	{ "_id" : ObjectId("614ab3b58485f68870d6b89a"), "usuario" : "juanlafranconi@hotmail.com", "mensaje" : "Hola" }
	{ "_id" : ObjectId("614ab3c38485f68870d6b89b"), "usuario" : "tomas@hotmail.com", "mensaje" : "Como va" }
	
	db.productos.find()
	{ "_id" : ObjectId("614ab09e8485f68870d6b895"), "nombre" : "Mac", "precio" : 300, "url" : "www.mac.com" }
	{ "_id" : ObjectId("614ab0c08485f68870d6b896"), "nombre" : "Iphone", "precio" : 500, "url" : "www.mac.com" }
	{ "_id" : ObjectId("614ab0d28485f68870d6b897"), "nombre" : "Pc", "precio" : 800, "url" : "www.pc.com" }
	{ "_id" : ObjectId("614ab0e18485f68870d6b898"), "nombre" : "Tv", "precio" : 1000, "url" : "www.pc.com" }
	{ "_id" : ObjectId("614ab0f38485f68870d6b899"), "nombre" : "Aire Acondicionado", "precio" : 1200, "url" : "www.pc.com" }

4) ### Mostrar la cantidad de documentos almacenados en cada una:
	db.productos.count()
	5

	db.mensajes.count()
	2

5)
  * a) Agregar un producto:
	* db.productos.insert({nombre:'Cama',precio:1500,url:'www.ya.com'})
  * b)
   	* listar productos con precio menor a 1000:
		* db.productos.find({"precio":{$lt:1000}})
		{ "_id" : ObjectId("614ab09e8485f68870d6b895"), "nombre" : "Mac", "precio" : 300, "url" : "www.mac.com" }
		{ "_id" : ObjectId("614ab0c08485f68870d6b896"), "nombre" : "Iphone", "precio" : 500, "url" : "www.mac.com" }
		{ "_id" : ObjectId("614ab0d28485f68870d6b897"), "nombre" : "Pc", "precio" : 800, "url" : "www.pc.com" }

   	* listar productos con precio menor a 1000 y mayor a 3000:
		* db.productos.find({$and:[{"precio":{$gte:1000}},{"precio":{$lte:3000}}]})
		{ "_id" : ObjectId("614ab0e18485f68870d6b898"), "nombre" : "Tv", "precio" : 1000, "url" : "www.pc.com" }
		{ "_id" : ObjectId("614ab0f38485f68870d6b899"), "nombre" : "Aire Acondicionado", "precio" : 1200, "url" : "www.pc.com" }
		{ "_id" : ObjectId("614ab64d8485f68870d6b89c"), "nombre" : "Cama", "precio" : 1500, "url" : "www.ya.com" }

   	* listar productos con precio mayor a 3000:
		* db.productos.find({"precio":{$gt:3000}})

   	* traiga solo el nombre del tercer producto mas barato:
		* db.productos.find({},{nombre:1,_id:0}).sort({"precio":1}).skip(2).limit(1)
		{ "nombre" : "Pc" }

 * c) Agregar campo stock a todos con valor=100:
	* db.productos.update({},{$set:{"stock":100}},false, true)
	WriteResult({ "nMatched" : 6, "nUpserted" : 0, "nModified" : 5 })

 * d) Cambiar el stock=0 a los de los productos de precio<1200:
	* db.productos.update({"precio":{$gt:1200}},{$set:{"stock":0}},false, true)
	WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

 * e) Borrar los productos de precio>400:
	* db.productos.deleteMany({"precio":{$lt:400}})
	{ "acknowledged" : true, "deletedCount" : 1 }

6) ### Crear un usuario ‘pepe’, clave: ‘asd456’ que solo pueda leer:
	db.createUser({user:"pepe",pwd:"asd456",roles:[{role:"read",db:"ecommerce"}]})

	Successfully added user: {
		"user" : "pepe",
		"roles" : [
			{
				"role" : "read",
				"db" : "ecommerce"
			}
		]
	}
