#Tipos de objetos

## Evento
* ID
* Fecha
* Descripción
* Link oficial del evento
* Imagen:
  * Thumbnail
  * Imagen descriptiva
* Información de contacto
  * Correo
  * Teléfono
  * Otros
* Tags
* ID del usuario con permiso para modificarlo
* Comentarios
  * Comentario
  * Timestamp
* Es valido

## Concurso
* ID
* Premio:
* Fecha de inicio:
* Fecha final
* Link oficial del evento
* Descripción
* Imagen:
  * Thumbnail
  * Description Image
* Información de contacto
  * Correo
   * Teléfono
   * Otros
* Tags
* ID de usuarios con permiso para modificarlo
* Comentarios
  * Comentario
  * Timestamp
* Es valido

##Usuario
* ID
* Nombre
* Contraseña
* Email
* Temas de interés
* Links de interés:
  * Facebook
  * LinkedIn
  * Proyectos Propios
* Eventos guardados antiguos
* Nuevos eventos (use un TTL para moverlo de un lado a otro)
* Eventos creados

##Comentarios
* Comentario
* Datestamp
* id del evento
* Tipo (evento o competencia)

##Imagenes
* Image
* Description
* url

-> TODO: save events to user.

#RESTful API

##Nota
Cuando se quiera modificar o borrar un objeto compuesto utilizando un post (JSON or ARRAY). Para mantener la interface sencilla, se va a sustituir todo el objeto compuesto.

Por ejemplo si los tags en el DB son ["tecnologia","emprendimiento","medio ambiente"], si se quiere agregar "politica" y eliminar emprendimiento, se enviaria como parametro ["tecnologia","medio ambiente","politica"], es decir se tienen que reenviar todos los tags, y hacer el cambio correspondiente.

##Evento
###GET

**Uso:** Permite obtener un grupo de eventos si no se especifica el id de un evento en específico, o obtener la info de un evento específico.

**Parámetros**
* id: id del database, si se envia este no se requieren los otros parámetros

Si no se envia el ID:

* total: numero de eventos a retornar
* begin: numero del primer evento a retornar

**Ejemplo de uso**

<base_url>/event?id=1

<base_url>/event?total=20&begin=5

**Ejemplo del retorno**
* Usando un id:

{"response": {"id":<>,"date":<>,"description":<>,"url":<>,"images":{"thumbnail":<>,"descriptive":<>},"contact":{...},"tags":[],"user_id":<>,"comments":[{"comment":<>,"datestamp":<>},...]}, "success": true}

* Usand total and begin:

{"response": [{"id":<>,"date":<>,"description":<>,"url":<>,"images":{"thumbnail":<>,"descriptive":<>},"contact":{...},"tags":[],"user_id":<>,"comments":[{"comment":<>,"datestamp":<>},...]},...], "success": true}

###POST
**Uso:** Permite agregar un nuevo evento (el usuario tiene que estar loggeado)

**Parámetros**
* date: fecha del evento y hora (definir formato) [obligatorio]
* description: string con la definicion del evento [obligatorio]
* url: url con el evento 
* image: json con los urls, ejemplo {"thumbnail":<url1>,"descriptive":<url2>} [opcional, cada elemento en el image es opcional]
* contact: json con la info, ejemplo {"correo":<>,"telefono":<>,...}
* tags: array con strings, ejemplo ["tecnologia","emprendedurismo",...]

**Ejemplo de uso**

<base_url>/event?date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}

###PUT
**Uso:** Permite modificar un evento (el usuario tiene que estar loggeado). Todos los parametros son opcionales excepto el ID.

**Parámetros**
* ID: id del evento a modificar [obligatorio]
* date: fecha del evento y hora (definir formato) 
* description: string con la definicion del evento 
* url: url con el evento 
* image: json con los urls, ejemplo {"thumbnail":<url1>,"descriptive":<url2>} 
* contact: json con la info, ejemplo {"correo":<>,"telefono":<>,...}
* tags: array con strings, ejemplo ["tecnologia","emprendedurismo",...]
* user_id: id del usuario que lo creo
* is_valid: define si el usuario quiere invalidar el evento

**Ejemplo de uso**

<base_url>/event?id=<>&date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}

##Concurso
###GET

**Uso:** Permite obtener un grupo de concursos si no se especifica el id de un concurso en específico, o obtener la info de un evento específico.

**Parámetros**
* id: id del database, si se envia este no se requieren los otros parámetros

Si no se envia el ID:

* total: numero de eventos a retornar
* begin: numero del primer evento a retornar

**Ejemplo de uso**

<base_url>/competition?id=1

<base_url>/competition?total=20&begin=5

**Ejemplo del retorno**
* Usando un id:

{"response": {"id":<>,"prize":<>,"begin_date":<>,"end_date":<>,"description":<>,"url":<>,"images":{"thumbnail":<>,"descriptive":<>},"contact":{...},"tags":[],"user_id":<>,"comments":[{"comment":<>,"datestamp":<>},...]}, "success": true}

* Usand total and begin:

{"response": [{"id":<>,"prize":<>,"begin_date":<>,"end_date":<>,"description":<>,"url":<>,"images":{"thumbnail":<>,"descriptive":<>},"contact":{...},"tags":[],"user_id":<>,"comments":[{"comment":<>,"datestamp":<>},...]},...], "success": true}

###POST
**Uso:** Permite agregar una nuevo competencia (el usuario tiene que estar loggeado)

**Parámetros**
* prize: premio a los ganadores de la competencia [obligatorio]
* begin_date: fecha en que inicia la competencia (definir formato)
* end_date: fecha en que termina la competencia (definir formato) [obligatorio]
* description: string con la definicion del evento [obligatorio]
* url: url con el evento 
* image: json con los urls, ejemplo {"thumbnail":<url1>,"descriptive":<url2>} [opcional, cada elemento en el image es opcional]
* contact: json con la info, ejemplo {"correo":<>,"telefono":<>,...}
* tags: array con strings, ejemplo ["tecnologia","emprendedurismo",...]

**Ejemplo de uso**

<base_url>/event?prize=<>&begin_date=<>&end_date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}

###PUT
**Uso:** Permite modificar un evento (el usuario tiene que estar loggeado). Todos los parametros son opcionales excepto el ID.

**Parámetros**
* ID: id del evento a modificar [obligatorio]
* prize: premio a los ganadores de la competencia
* begin_date: fecha en que inicia la competencia (definir formato)
* end_date: fecha en que termina la competencia (definir formato)
* url: url con el evento 
* image: json con los urls, ejemplo {"thumbnail":<url1>,"descriptive":<url2>} 
* contact: json con la info, ejemplo {"correo":<>,"telefono":<>,...}
* tags: array con strings, ejemplo ["tecnologia","emprendedurismo",...]
* user_id: id del usuario que lo creo
* is_valid: define si el creador dejo invalido al evento.

**Ejemplo de uso**

<base_url>/event?id=<>&date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}


##USUARIO
###GET

**Uso:** Permite obtener la informacion del usuario (necesita estar loggeado)

TODO: Se podría agregar otra función para poder buscar otros usuarios, tipo social network.

**Parámetros**

No se necesita ningún parámetro.

**Ejemplo de uso**

<base_url>/user

**Ejemplo del retorno**

{"response": {"id":<>,"name":<>,"email":<>,"topics":[...],"url":{"facebook":,"linkedin":,...}, "old_events":[],"new_events":[],"own_events":[]}, "success": true}

###POST
**Uso:** Permite crear un nuevo usuario.

**Parámetros**
* name: nombre del nuevo usuario [obligatorio]
* password: password del nuevo usuario (en el frontend hay que verificarlo dos veces por si el usuario se equivoca). [obligatorio]
* email: email del usuario [obligatorio]
* topics: es un array de strings con los temas de interes del usuario
* url: es un json con los lugares de interes del usuario. E.g. {"facebook":<>,"LinkedIn":<>,...}

**Ejemplo de uso**

<base_url>/user?prize=<>&begin_date=<>&end_date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}

###PUT
**Uso:** Permite modificar la informacion de un usuario (el usuario tiene que estar loggeado.

**Parámetros** Todos los parametros son opcionales
* name: nombre del nuevo usuario [obligatorio]
* password: password del nuevo usuario (en el frontend hay que verificarlo dos veces por si el usuario se equivoca). [obligatorio]
* email: email del usuario [obligatorio]
* topics: es un array de strings con los temas de interes nuevos del usuario
* url: es un json con los lugares de interes del usuario. E.g. {"facebook":<>,"LinkedIn":<>,...}

**Ejemplo de uso**

<base_url>/event?id=<>&date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}

#Comentario

###GET

**Uso:** Permite obtener la informacion del usuario (necesita estar loggeado)

TODO: Se podría agregar otra función para poder buscar otros usuarios, tipo social network.

**Parámetros**

No se necesita ningún parámetro.

**Ejemplo de uso**

<base_url>/user

**Ejemplo del retorno**

{"response": {"id":<>,"name":<>,"email":<>,"topics":[...],"url":{"facebook":,"linkedin":,...}, "old_events":[],"new_events":[],"own_events":[]}, "success": true}

###POST
**Uso:** Permite crear un nuevo usuario.

**Parámetros**
* Comentario
* Datestamp

**Ejemplo de uso**

<base_url>/user?prize=<>&begin_date=<>&end_date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}

###PUT
**Uso:** Permite modificar la informacion de un usuario (el usuario tiene que estar loggeado.

**Parámetros** 
* id:  [obligatorio]
* Comentario
* Datestamp

**Ejemplo de uso**

<base_url>/event?id=<>&date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**

{"response":{"id":<>}, "success": true}


