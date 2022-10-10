
# 1.- Relación Uno a Uno embebida

Una fuerte relación **Uno a Uno** embebido se estructura de la siguiente manera:

~~~json
[
  {
    _id: ObjectId("633d6eddec3f4e626baec02e"),
    firstName: 'John',
    lastName: 'Sarmiento',
    age: 21,
    diseaseSummary: [
      { disease: 'Chronic Repiratory', treatment: 'Antibiotics' },
      { disease: 'Infectious bursitins', treatment: 'Vaccination' }
    ],
    name: 'Louis John'
  }
]
~~~

Donde un paciente tiene un resumen medico.

# 2.- Relación Uno a Uno usando referencias

Una relación **Uno a Uno** usando referencias se usan dos collecciones, en una se registra la entidad a la que le pertenece algo y la segunda almacena la pertenencia, por ejemplo:

Un **médico**
~~~json
[
  {
    _id: ObjectId("63439894782e256f36cc71d6"),
    firstName: 'Tania',
    lastName: 'Puc Sarmiento',
    age: 28
  }
]
~~~
Le pertenece un **consultorio**
~~~json
[
  {
    _id: ObjectId("634398c7782e256f36cc71d7"),
    name: 'Consultorio A',
    owner: ObjectId("63439894782e256f36cc71d6")
  }
]
~~~

# 3.- Relación Uno a Muchos embebido

La relación **Uno a Muchos** incrustado o embebido se puede estructurar de una manera similar a una relación **Uno a Uno** de un **Paciente** al cual le pertenece un **Historial médico**, solo que se recomienda seguir esta estructura si las reglas del próblema a resolver no interfieren con las restricciones del documento, recordemos que en un documento de MongoDB podemos almancenar hasta 16 MB.

# 4.- Relación Uno a Muchos usando referencias

Para una relación **Uno a Muchos** donde el próblema a resolver puede ser el registro de ciudadanos de una ciudad sería de la siguiente manera:

En una **ciudad**
~~~json
[
  {
    _id: ObjectId("63439c7b782e256f36cc71d8"),
    name: 'New York City',
    coordinates: { lat: 21, lng: 55 }
  }
]
~~~

Habitan los siguientes ciudadanos:
~~~json
[
  {
    _id: ObjectId("63439e17782e256f36cc71d9"),
    name: 'Luis Puc Sarmiento',
    cityId: ObjectId("63439c7b782e256f36cc71d8")
  },
  {
    _id: ObjectId("63439e17782e256f36cc71da"),
    name: 'Thiago Jota',
    cityId: ObjectId("63439c7b782e256f36cc71d8")
  }
]
~~~

# 5.- Relación Muchos a Muchos embebido

En un problema de ejemplo donde un cliente puede tener varias ordenes de compra, podemos estructurar los documentos de tal manera que en un solo documento tengamos toda la informació, pero una vez más si usa este enfoque puede que en el futuro para un problema como el del ejemplo, puede tener conflictos por lo que se recomienda usar un enfoque usando referencias.

# 6.- Relación Muchos a Muchos usando referencias

Un problema donde se puede usar una relación **Muchos a Muchos** es un registro de **Libros**, cada libro puede tener uno o más **Autores** y esos autores puede que escriban otros libros más. Entonces una estructura bajo el enfoque de uso de referencias pudiera verse así:

**Autores**
~~~json
[
  {
    _id: ObjectId("6343a3ed782e256f36cc71db"),
    name: 'Stephen King',
    age: 75,
    address: { city: 'Portland', country: 'USA' }
  },
  {
    _id: ObjectId("6343a3ed782e256f36cc71dc"),
    name: 'Howard Phillps',
    age: 47,
    address: { city: 'Rhode Island', country: 'USA' }
  }
]
~~~
**Libros**
~~~json
[
  {
    _id: ObjectId("6343a41e782e256f36cc71dd"),
    name: 'Ficti Book',
    authors: [
      ObjectId("6343a3ed782e256f36cc71db"),
      ObjectId("6343a3ed782e256f36cc71dc")
    ]
  }
]
~~~