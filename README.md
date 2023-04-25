# social-gift
SocialGift es una plataforma que permite interactuar con listas de regalos y miembros de una comunidad.

## De qué trata?

- SocialGift 1.0 es la primera versión de este nuevo proyecto transversal
- Tiene como objetivo desarrollar conocimientos full-stack
- Nace como iniciativa transversal para cohesionar conocimientos entre asignaturas
  - Desarrollo en entornos web
  - Desarrollo en dispositivos móviles I
  - Desarrollo de servicios en línea
- Se divide en: Front End y Back End
- El Front End consta de una interfaz de usuario web y una aplicación Android
- El Back End comprende una API conectada a una base de datos que sirve peticiones a los Front End

## Funcionalidades a implementar

- Crear y gestionar regalos y listas de regalos
- Buscar y reservar regalos de listas de regalos
- Conectar y hacer amigos con otros usuarios de la comunidad

## Caracteristicas

- autenticación y registro de usuarios
- navegación y filtrado del listado de listas de regalos
- creación y gestión de regalos
- reservas de los regalos
- peticion de amistad con otros usuarios
- mensajería con otros usuarios (desconectado o en tiempo real)

# Funcionalidades definidas por el cliente

## Gestion usuarios

- registrar Usuario
POST /users

- iniciar Sesión
```
❌
GET /login?login=pepito&password=menganito

✔️
POST /login
{
  login: pepito
  password: menganito
}
```

- cerrar Sesión
```
No hace falta ningún endpoint si el servidor/api es RESTful. Sólo se tiene que borrar el token de autenticación en el lado del cliente.

En el caso que mantengamos una sesión (no RESTful) en el cliente, se podría hacer vía:
POST /logout
header 
{
  Authorization: Bearer TOKEN 
}
```

- ver Perfil
```
GET /users/ID
GET /users/@me
GET /profile
```


- editar Perfil
```
PUT /users/ID <- verificar que soy
PUT /users/@me <- verificar que soy?
PUT /profile (cogeré el id del header Atuhentication: Bearer TOKEN)
```

## Interacción con usuarios

- buscar usuario por correo
```
✔️
GET /users?search=email@acme.com

<!-- 
GET /users?pageSize=10
GET /gifts?pageSize=10
GET /gifts?search=nombre_de_la_empresa&campo=empresa
-->

❌ (no es filosofía REST)
GET /users/search/email@acme.com
GET /gifts/search/nombre de la empresa

```

- ver perfil de usuario (de otro usuario)
```
GET /users/ID
```

- enviar solicitud de amistad (opcional)
- aceptar o rechazar solicitud de amistad (opcional)
- ver todas las listas de deseos del usuario
```
😐
GET /wishlists?iduser=ID
✔️
GET /users/ID/wishlists
```

- obtiene todos los regalos reservados p or el ususario
```
😐
GET /users/ID/reservedgifts 
😐
GET /users/ID/gifts/reserved <----- api oficial
✔️
GET /users/ID/gifts?reserved <----- yuri
✔️
GET /users/ID/gifts?reserved=true
```

## Gestion de la lista de regalos y regalos

- crear lista de regalos
```
😐
POST /wishlist
{
  id
  id_user
  name
  description
  created_at
  finished_at
}
```

```
✔️
POST /users/ID/wishlist
{
  name
  description
  finished_at
}
```


- editar lista de regalos
```
PUT /users/:IDU/wishlist/:IDW
{
  name: "Lista de PS5",
  //description: "---",
}
```

- eliminar lista de regalos
- visualizar listas de regalos

```
TODAS:
GET /wishlists

UNA:
GET /wishlists/ID

REGALOS DE UNA WISHLIST:
GET /wishlists/ID/gifts
```

- crear regalos
- editar regalos
- eliminar regalos
- visualizar regalos
- visualizar usuario que ha reservado regalo

## Mensajería con usuarios (opcional)

- enviar mensaje
- visualizar mensajes intercanviados
- visualizar usuarios con quien se ha comunicado
- recibir mensajes


## Casos de uso

TBD

## Base de datos

USERS
id
name
last_name
email
password
image

WISHLIST
id
id_user
name
description
created_at
finished_at

1|54|Lista con PS5 y nada más|---|hoy|25/DIC

WISHLIST_GIFT
id
id_wishlist
id_gift
quantity

1|1|5
2|1|5
3|1|5

BOOKED//RESERVATION//
id
id_user
id_gift


<!--
GIFT
id
wishlist_i
-->



