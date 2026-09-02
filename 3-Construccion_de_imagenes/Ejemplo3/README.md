# Descripción Ejemplo 3

## 🎥 Mira el video del ejemplo 3

[![Ver en YouTube](https://img.youtube.com/vi/tFdH4_Y_Gl8/0.jpg)](https://www.youtube.com/watch?v=tFdH4_Y_Gl8)

Un dockerfile mas completo para este ejemplo:

![Dockerfile](Dockerfile)

Donde corremos sobre una imagen de python slim.


### Argumentos(ARG) vs Variebles de Ambiente(ENV)

#### 🧱 `ARG` (Argumento de construcción)

#### 📌 ¿Qué es?
Una **variable disponible solo durante la construcción (`build`)** de la imagen Docker.

Se pueden utilizar unicamente a la hora de crear una imagen, si no se especifica, se utiliza la por defecto.

#### 🛠️ ¿Para qué se usa?
Sirve para **parametrizar valores** que pueden cambiar al construir, como la versión de la imagen base, etc.

# ENV en Docker

### `ENV` (Variable de Entorno)

#### 📌 ¿Qué es?

`ENV` es una instrucción del Dockerfile que permite definir **variables de entorno** dentro del contenedor. Estas variables estarán disponibles **en tiempo de ejecución** y pueden ser utilizadas por procesos o scripts en el contenedor.

Se pueden cambiar a la hora de crear un contenedor, si no se especifica, se utiliza la por defecto

---

#### 🛠️ ¿Para qué se usa?

- Configurar parámetros sin modificar el código (por ejemplo: `development`, `staging`, `production`).
- Pasar valores reutilizables como rutas o claves de configuración.
- Reutilizar en otras instrucciones como `RUN`, `CMD`, `ENTRYPOINT`.
- Permitir al usuario sobrescribirlas al momento de ejecutar el contenedor con `-e`.

---

| Característica                          | `ARG`                          | `ENV`                          |
|----------------------------------------|--------------------------------|--------------------------------|
| Disponible durante el build            | ✅ Sí                          | ✅ Sí                          |
| Disponible durante ejecución           | ❌ No                          | ✅ Sí                          |
| Persistente en la imagen final         | ❌ No                          | ✅ Sí                          |
| Se puede sobrescribir en `docker run`  | ❌ No                          | ✅ Sí con `-e`                 |
| Uso principal                          | Parametrizar builds            | Configurar entornos            |


Para generar la imagen debemos realizar la construcción del Dockerfile, lo podemos hacer de las siguientes 2 maneras:

Simple con las variables por defecto
   ```bash
   docker build -t simple-index .
 ```

ó modificando los argumentos con ***--build-arg***

   ```bash
    docker build --build-arg UBUNTU_VERSION=20.04 -t simple-index .
 ```

 Donde:
 
**docker build** es el comando para realizar la construccion de la imagen.
**-t** Flag para indicar cual es el nombre que le queremos colocar a nuestra imagen.
**simple-index** Este va a ser el numbre de nuestra imagen, esto puede variar a gusto.
**UBUNTU_VERSION=20.04** El nombre del argumento *UBUNTU_VERSION* y el dato que queremos asignarle, en este caso *20.04*
**.** Ruta donde se encuentra el archivo **Dockerfile**, en este caso se encuentra en la misma carpeta donde estamos corriendo el comando, esto lo inidcamos con el **.**

**Nota:**Revisa que estés dentro de la carpeta para poder ejecutar el comando con la ruta **.** si no tenes que modificarla.

***TIP:***Comando para moverte entre carpetas **cd /<nombre-del-directorio>** dentro de una carpeta / **cd ..** salir de la carpeta actual

Una vez creada la imagen lo podemos comprobar con:

   ```bash
   docker images
 ``` 

Ahora nosotros podemos revisar los parametros y propiedades con los que fue creada esta imagen esto es como "Ver dque hay dentro de nuestra imagen", para ver esto utilizaremos el comando:

   ```bash
   docker inspect simple-index
 ```

 Acá podemos encontrar mucha información de esta imagen, entre ellos, los **LABEL** que colocamos, unicamente son visibles de este modo, adicionalmente, podemos observar cómo cambió el argumento **UBUNTU_VERSION**

Para crear un contenedor a base de esta imagen, lo podemos hacer las siguientes maneras:

Simple con las variables por defecto

   ```bash
   docker run -d -p 80:80 --name docker-web simple-index
```

ó modificando las variables con ***-e***

   ```bash
    docker run -d -p 80:80 -e CREATOR="OSCAR" -e APP_ENVIROMENT=PRUEBAS --name docker-web simple-index 
```

Al igual que con la imagen podemos inspeccionar dentro de nuestro contenedor para observar sus parametos y ver como cambiaron las variables:

   ```bash
   docker inspect docker-web
 ```

Nota: Este ejemplo está hosteado en NGINX podes encontrar mas información en su documentación.

![Documentación NGINX](https://nginx.org/)

