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

##Usuario
* ID
* Nombre
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

#RESTful API

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

* Usand total and being:

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
* ID: id del evento a modificar
* date: fecha del evento y hora (definir formato) 
* description: string con la definicion del evento 
* url: url con el evento 
* image: json con los urls, ejemplo {"thumbnail":<url1>,"descriptive":<url2>} 
* contact: json con la info, ejemplo {"correo":<>,"telefono":<>,...}
* tags: array con strings, ejemplo ["tecnologia","emprendedurismo",...]
* user_id: id del usuario que lo creo

**Ejemplo de uso**

<base_url>/event?id=<>&date=<>&description=<>&url=<>&image={"thumbnail":<url1>,"descriptive":<url2>}&contact={"correo":<>,"telefono":<>,...}&tags=[]&user_id=<>

**Ejemplo del retorno**
{"response":{"id":<>}, "success": true}
