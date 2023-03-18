### Instrucciones
En un entorno inicial como administrador de base de datos cree colecciones y Indexes, como un usuario admin, administre usuarios y como un usuario con privilegios limitados (developer, por ejemplo) lea y escriba datos en las bases de datos que haya creado.

### Creando un contenedor
```bash
docker run -d --name db -p 27017:27017 --mount src=dbdata,dst=/data/db mongo
```

### 1.- Creado bases de datos e indexes

```m
use recordGame

db.players.insertOne({name: "Paco el Chato", age: 29})

db.games.insertOne({name: "FIFA 2022"})

db.records.insertOne({playerName: "Pacho el Chato", game: "FIFA 2022", record: NumberInt(20500)})

db.records.createIndex({"record": 1})

db.players.createIndex({"name": 1})

db.createUser({user: "admin1", pwd: "admin1mdb", roles:["userAdmin"]})
```
### 2.- Creando usuarios con privilegios de solo lectura y escritura en mongosh
```m
Please enter a MongoDB connection string (Default: mongodb://localhost/): admin1:admin1mdb@localhost

use recordGame

db.createUser({user: "recordGameDev3", pwd: "r3c0$66am3", roles: [{role: "readWrite", db: "recordGame"}]})
```

### 3.- Escribiendo y leyendo en la BD recordGame en mongosh
```m
Please enter a MongoDB connection string (Default: mongodb://localhost/): mongodb://recordGameDev3:r3c0$66am3@localhost:27017/recordGame

recordGame> db.players.find()
[
  {
    _id: ObjectId("6415f8ae229e34b64565ffee"),
    name: 'Paco el Chato',
    age: 29
  },
  {
    _id: ObjectId("6415fc39229e34b64565fff1"),
    name: 'Diego Bonetta',
    age: 36
  },
  {
    _id: ObjectId("6415fc8c229e34b64565fff2"),
    name: 'Manuel Chan',
    age: 36
  },
  {
    _id: ObjectId("6415fdd0229e34b64565fff3"),
    name: 'Victor Chan',
    age: 36
  }
]
recordGame> db.players.insertOne({name: "Camilo Vargas", age: NumberInt(35)})
{
  acknowledged: true,
  insertedId: ObjectId("641606959f9af89b683a6f92")
}
```


### Lectura recomendada
- [Drop all users](https://www.mongodb.com/docs/manual/reference/method/db.dropAllUsers/)

