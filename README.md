# Ejecuta la aplicacion

Primeramente tenemos que clonar el siguiente repositorio con el comando git clone seguido de la url del repositorio.
=> 
```shell
git clone https://github.com/EminatarenX/prisma-api-act2.git

```

Dentro de la carpeta de este proyecto debemos abrir una terminal y ejecutar el comando 
```shell 
npm install
```
para instalar todas las dependencias que esten dentro del package json para que el programa funcione correctamente.

Despues tenemos que agregar un archivo .env en la raiz del proyecto con una variable de entorno llamada DATABASE_URL, el valor de esta url es de una base de datos de mysql en la nube:
```.dotenv
DATABASE_URL="mysql://root:ckfTON5f436ZZ66OVVzT@containers-us-west-65.railway.app:7642/act2"
```


una vez hecho todos estos pasos podemos ejecutar el comando :
```shell
npx prisma generate
```
en nuestra terminal ubicados en la raiz del proyecto. para que prisma pueda leer los modelos de nuestra base de datos.

para correr el servidor podemos usar el comando disponible en nuestro package json:
```shell
 npm run dev
```

para poder ver y editar el codigo de este proyecto necesitamos un entorno de desarrollo o un editor de codigo.

# Comprobar funcionamiento, ( Consutas GET )

Despues de ejecutar npm run dev, en la consola deberia aparecer un mensaje diciendo: ```servidor corriendo en el puerto 4000 ```.
Para verificar su funcionaiento ingrese a ```http://localhost:4000/api/clientes``` dentro de este enlace podra ver los siguentes datos:
```json
{
    "clientes": [
        {
            "id": 1,
            "nombre": "Juan",
            "apellidos": "Gomez",
            "created_At": "2023-09-09T04:06:40.000Z",
            "email": "juan@correo.com"
        },
        {
            "id": 2,
            "nombre": "Maria",
            "apellidos": "Sanchez",
            "created_At": "2023-09-09T04:06:40.000Z",
            "email": "Maria@correo.com"
        },
        {
            "id": 3,
            "nombre": "Marco",
            "apellidos": "Torres",
            "created_At": "2023-09-09T04:06:40.000Z",
            "email": "marco@mail.com"
        }

    ]
}
```
Tambien puede consultar los productos haciendo un get desde su navegador consultando el siguente link: ```http://localhost:4000/api/productos```
obtenra una respuesta como esta: 
```json
[
    {
        "id_producto": 1,
        "nombre": "Tenis",
        "precio": "120.5",
        "cantidad_en_stock": 10,
        "marcas": {
            "nombre": "Nike"
        }
    },
    {
        "id_producto": 2,
        "nombre": "Pantalon",
        "precio": "80.99",
        "cantidad_en_stock": 15,
        "marcas": {
            "nombre": "Adidas"
        }
    },
    {
        "id_producto": 3,
        "nombre": "Camiseta",
        "precio": "25.5",
        "cantidad_en_stock": 20,
        "marcas": {
            "nombre": "Adidas"
        }
    }
]
```

Puede hacer consultas para consultar un id en especifico tando de productos como de clientes añadiendo un /:id 
ejemplo de productos: 
```shell
http://localhost:4000/api/productos/4
```

obtendra la siguiente respuesta: 
```json
{
    "productoEncontrado": {
        "id_producto": 4,
        "nombre": "Bolso",
        "precio": "50.99",
        "cantidad_en_stock": 8,
        "marca_id": 1
    }
}
```
ejemplo de clientes:
```shell
http://localhost:4000/api/clientes/6
```
obtendra la siguiente respuesta:
```json
{
    "cliente": {
        "id": 6,
        "nombre": "Camila",
        "apellidos": "Lopez",
        "created_At": "2023-09-09T04:06:40.000Z",
        "email": "camila@mail.com"
    }
}
```

puede hacer consultas POST, DELETE y PUT con ayuda de aplicaciones como Postman o ThunderClient.

# Consultas POST, DELETE y PUT


## POST de clientes
Empezando con clientes, puede insertar un nuevo cliente mandando una peticion o solicitud POST a la siguiente url
```shell
http://localhost:4000/api/clientes
```
Dentro del body debe escribir un objeto json con los valores: nombre, apellidos, email.
Ejemplo: 
```json
{
  "nombre": "Julian",
  "apellidos": "Vicente",
  "email": "julionpro@correo.com"
}
```
al hacerlo recibira la siguiente respuesta:
```json
{
  "nuevoCliente": {
    "id": 16,
    "nombre": "Julian",
    "apellidos": "Vicente",
    "created_At": "2023-09-09T04:51:44.000Z",
    "email": "julionpro@correo.com"
  }
}
```

## PUT clientes ( modificar ) 

Para modificar los datos de un cliente existente se requiere hacer una consulta tipo PUT al siguiente url:
```shell
http://localhost:4000/api/clientes/16
```
toma en cuenta que en este caso queremos modificar al cliente con id = 16

para completar esta accion tenemos que agregar un body con los datos que deseamos modificar ( objeto json )
en este caso:
```json
{
  "nombre": "Jose",
  "apellidos": "Perez",
  "email": "jose@correo.com"
}
```
Despues de realizar la solicitud recibiremos una respuesta con el cliente actualizado:
```json
 {
  "cliente": {
    "id": 16,
    "nombre": "Jose",
    "apellidos": "Perez",
    "created_At": "2023-09-09T04:51:44.000Z",
    "email": "jose@correo.com"
  }
}
```

## Delete clientes 

Para eliminar a un cliente tenemos que hacer una consulta de tipo DELETE hacia el siguiente endpoint /:id para indicar al cliente que deseamos eliminar en este caso el 16
```shell
http://localhost:4000/api/clientes/16
```
Donde id = 16.
seguido de esto podemos hacer la peticion, y recibiremos una respuesta como esta:
```json
{
  "msg": "Cliente eliminado",
  "cliente": {
    "id": 16,
    "nombre": "Jose",
    "apellidos": "Perez",
    "created_At": "2023-09-09T04:51:44.000Z",
    "email": "jose@correo.com"
  }
}
```
si intenta consultar ese cliente en la direccion ```http://localhost:4000/api/clientes/16``` recibira la siguiente respuesta:
```json
{
    "msg": "El cliente no existe"
}
```

