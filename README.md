<h1 align="center">DOCUMENTACI脫N MONGODB 馃摎</h1> 

<p align="justify">Documentaci贸n realizada con el objetivo de recordar algunas funcionalidades que nos permite realizar el lenguaje de MongoDB. A continuaci贸n se mostrar谩n los comandos b谩sicos de CRUD (Create, Read, Update, Delete) y algunas funciones primitivas de MongoDB. Este repositiorio es de proposito educativo.</p>

<p align="justify">

### Usar una base de datos espec铆fica	
	
```md
USE *DB*
```

<hr>

### Crear Base de Datos

En MongoDB no existe ning煤n comando estilo create database, ni nada as铆, lo que hace mongodb es crear una colecci贸n (base de datos) en el momento que se le inserta un objeto o documento(registro de una tabla por llamarlo de alguna forma) a dicha colecci贸n.

<hr>

### Crear una Colecci贸n

Las colecciones son conjuntos de (normalmente) documentos relacionados. Su base de datos puede tener tantas colecciones como desee. 

```md
db.createCollection('*NAME*')
```

<hr>

### Mostrar Bases de Datos y/o Colecciones

```md
show dbs
show collections
```

<hr>

### Insertar Documentos en una Colecci贸n

Los documentos son objetos JSON que viven dentro de una colecci贸n. Pueden tener cualquier formato JSON v谩lido, con la salvedad de que no pueden contener funciones.

```md
db.*COLECCION*.insert({*LLAVE*: *VALOR*})
```

<hr>

### Encontrar un Documento

```md
db.*COLECCION*.find()
```

A todos nuestros documentos se les crea un ID a la hora de insertar valores. Podemos hacer multiples funciones con el ID, una de estas es filtrar, veamos:

```md
db.*COLECCION*.find(ObjectId("*ID*"))
```

Tambi茅n podemos filtrar por sus llaves, ejemplo:

```md
db.*COLECCION*.find({
  name: "dave",
  email: "davey@aol.com"
})
```

<hr>

### Proyecciones

Tambi茅n podemos filtrar por un segundo campo donde en este ejemplo nuestra colecci贸n desayunos, nos devolver谩 todos los desayunos que contengan huevos y lime.

```md
db.breakfast.find({}, {
  eggs: true,
  lime: true
})
```

<hr>

### CRUDS EJEMPLOS

#### Create

```md
db.people.insert({name: "Tony Stark", occupation: "Billionaire, playboy, philantropist..."})
```

#### Read

Tenemos muchas opciones para encontrar. Ya hemos visto db.collection.find(). Tambi茅n podemos usar db.collection.findOne() que devolver谩 como m谩ximo un resultado.

#### Update

Filtramos por el nombre y donde coincida, actualizamos el campo

```md
db.people.update({name: 'dave'}, {name:'brunhilde'})
```

#### Delete

Remueve todos los registros con el nombre "Dave", veamos:

```md
people = db.people.remove({name:'Dave'})
```

<hr>

### Metodos Primitivos

#### Exists
Tambi茅n podemos filtrar si existe o no un documento, ejemplo, nos traera todos los desayunos que tengan huevos incluidos. Todas las funciones van con un signo $, veamos:

```md
db.breakfast.find({
  eggs: {
    $exists: true
  }
})
```

#### $gt y $lt

Podemos usar $gt y $lt para buscar documentos que tengan campos que sean mayores o menores que un valor:

```md
db.breakfast.find({
  starRating: {
    $gt: 5
  }
})
```

#### $where

Incluso podemos filtrar usando una expresi贸n de JavaScript arbitraria usando $where. Esto nos permitir谩 comparar dos campos en un solo documento.

```md
db.sandwiches.find({
  $where: "*EXPRESION*"
})
```

#### Contar

Count convertir谩 nuestro conjunto de resultados en un n煤mero. Podemos usarlo de dos maneras. Podemos encadenarlo:

```md
db.people.find({sharks: 3}).count()
```

O podemos usarlo en lugar de find:

```md
db.people.count({sharks: 3})
```

#### Limitar y Saltar

Limit nos permitir谩 limitar los resultados en el conjunto de salida. Saltar nos permitir谩 compensar el inicio. Entre ellos nos dan paginaci贸n, veamos:

```md
db.biscuits.find().limit(5)
```

Nos dar谩 las primeras 5 galletas. Si queremos los siguientes 5 podemos saltarnos los primeros 5.

```md
db.biscuits.find().limit(5).skip(5)
```

#### Ordenar

Podemos ordenar los resultados usando el operador de ordenaci贸n. Esto ordenar谩 las ara帽as en orden ascendente de vellosidad, as铆:

```md
db.spiders.find().sort({hairiness: 1})
```

<hr>

### Cursores

Podemos crear una variable cursor, el cual, podemos iterar sobre el cursor usando un ciclo while simple. Podemos verificar si el cursor tiene un valor siguiente y podemos llamar a cursor.next para obtener el valor.

```md
var people = db.people.find();
while (people.hasNext()) {
   print(tojson(people.next()));
}
```

<hr>

- Para mayor informaci贸n sobre las funciones y metodos primitivos pueden visitar el sitio web: 

<a href="http://nicholasjohnson.com/mongo/course/workbook/">馃憠 MongoDB Documentation</a>

