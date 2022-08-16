<h1 align="center">DOCUMENTACIÓN MONGODB</h1>

<p align="justify">Documentación realizada con el objetivo de recordar algunas funcionalidades que nos permite realizar el lenguaje de MongoDB. A continuación se mostrarán los comandos básicos de CRUD (Create, Read, Update, Delete) y algunas funciones primitivas de MongoDB. Este repositiorio es de proposito educativo.</p>

<p align="justify">

### Usar una base de datos específica	
	
```md
USE *DB*
```

<hr>

### Crear Base de Datos

En MongoDB no existe ningún comando estilo create database, ni nada así, lo que hace mongodb es crear una colección (base de datos) en el momento que se le inserta un objeto o documento(registro de una tabla por llamarlo de alguna forma) a dicha colección.

<hr>

### Crear una Colección

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

### Insertar Documentos en una Colección

Los documentos son objetos JSON que viven dentro de una colección. Pueden tener cualquier formato JSON válido, con la salvedad de que no pueden contener funciones.

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

También podemos filtrar por sus llaves, ejemplo:

```md
db.*COLECCION*.find({
  name: "dave",
  email: "davey@aol.com"
})
```

<hr>

### Proyecciones

También podemos filtrar por un segundo campo donde en este ejemplo nuestra colección desayunos, nos devolverá todos los desayunos que contengan huevos y lime.

```md
db.breakfast.find({}, {
  eggs: true,
  lime: true
})
```

<hr>

### Metodos Primitivos

#### Exists
También podemos filtrar si existe o no un documento, ejemplo, nos traera todos los desayunos que tengan huevos incluidos. Todas las funciones van con un signo $, veamos:

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

Incluso podemos filtrar usando una expresión de JavaScript arbitraria usando $where. Esto nos permitirá comparar dos campos en un solo documento.

```md
db.sandwiches.find({
  $where: "*EXPRESION*"
})

```

