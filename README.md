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
* ID del usuario que lo creo
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
* ID del usuario que lo creo
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

