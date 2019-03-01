# Solucion problema de sistemas de streaming

Se tiene la problemática de que se requiere que diariamente se envíe una peticion a los diferentes sistemas de streaming sobre que sistema pagó los derechos de una canción para saber sí o no

# Solución propuesta

## Patrón de diseño Chain of responsability

Este patrón nos permite pasar peticiones a través de una cadena de receptores. Y dicho receptor tiene la opción de mandarlo a otro y/o procesarlo.

En este caso se va a mandar la peticion de que quiero saber si cada uno de los receptores ya pagaron, se crea una cadena de los diferentes servicios de streaming.

![alt text](https://refactoring.guru/images/patterns/diagrams/chain-of-responsibility/structure.png)

### 1 Handler
El handler será StreamingService que tendrá su método handle, y el método setNext para mandar al siguiente en la lista.

### 2 Base Handler
Esta clase es una opcional que nos permite poner código que es común entre todas las clases Handler. Aquí se podría escribir el código para poder detectar si este servicio hizo el pago o no, retornando un valor boolean con la respuesta.

### 3 Concrete Handlers
Aquí se escribe el código concreto que hace el proceso, y se especifica con un método cual es el siguiente en la cadena, en este caso sea cual sea su manera de responder si pagó o no seguirá con el siguiente sistema de streaming hasta acabar con toda la lista de sistemas

### 4 Client
El cliente, en este caso la aplicacion de la disquera va a generar una cadena que contenga los diferentes servicios de streaming