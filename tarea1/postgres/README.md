# Ejercicio 3. De PostgreSQL 17 a 18

## 1. Tabla comparativa PostgreSQL 17 y PostgreSQL 18

## Diferencias entre PostgreSQL 17 y PostgreSQL 18

| Categoría | Elemento | Descripción y justificación del cambio |
| :--- | :--- | :--- |
| **1. Configuración general** | **Versión de PostgreSQL** | Se cambia de `postgres:17` a una imagen basada en `postgres:18` para utilizar una versión principal más reciente. |
| | **Nombre del servicio** | El servicio pasa de llamarse `postgres` a `db`, por lo que también cambia el nombre utilizado en los comandos de Docker Compose. |
| | **Nombre del contenedor** | Se cambia de `postgres173CV231AGO2026` a `apsw_db` para facilitar su identificación. |
| | **Versión de Compose** | Se elimina `version: '3.8'` porque Docker Compose moderno considera obsoleto este atributo. |
| **2. Construcción de la imagen** | **Imagen utilizada** | PostgreSQL 17 utiliza directamente `postgres:17`; PostgreSQL 18 utiliza `build: .` para construir una imagen local. |
| | **Dockerfile** | Se utiliza `FROM postgres:18` como imagen base para construir la imagen personalizada de PostgreSQL 18. |
| **3. Base de datos y acceso** | **Variables de entorno** | Los valores fijos de base de datos, usuario y contraseña se sustituyen por variables con valores predeterminados, lo que facilita su configuración. |
| | **Puerto publicado** | PostgreSQL 17 utiliza `5432:5432`; PostgreSQL 18 utiliza por defecto `127.0.0.1:5434:5432`, para evitar conflictos de puerto y limitar el acceso publicado al equipo local. |
| | **Inicialización** | PostgreSQL 18 agrega argumentos para definir la codificación UTF-8 y la configuración regional al inicializar la base de datos. |
| **4. Almacenamiento** | **Tipo de volumen** | Se cambia la carpeta local `./data` por el volumen con nombre `datos_db`, administrado por Docker. |
| | **Ruta de datos** | Se cambia `/var/lib/postgresql/data` por `/var/lib/postgresql` para adaptarse a la estructura de almacenamiento de la imagen oficial de PostgreSQL 18. |
| | **Scripts de inicialización** | Se agrega el montaje de `./initdb` para permitir ejecutar scripts al crear una base de datos por primera vez. |
| **5. Servicios adicionales** | **Comprobación de salud** | PostgreSQL 18 incorpora `healthcheck` con `pg_isready` para comprobar si el servidor está preparado para aceptar conexiones. |
| | **Adminer** | Se agrega el servicio `adminer` para administrar la base de datos mediante una interfaz web. |
| | **Dependencias** | Adminer espera a que PostgreSQL esté saludable antes de iniciarse, reduciendo problemas de conexión durante el arranque. |
| **6. Políticas del contenedor** | **Reinicio automático** | Se conserva `restart: unless-stopped` en ambas configuraciones para permitir el reinicio automático, salvo que el contenedor se detenga manualmente. |
| | **Directorio de trabajo** | PostgreSQL 18 establece `/trabajo` como directorio de trabajo y monta la carpeta del proyecto para acceder a sus archivos. |

## 2. ¿Se usaba el Dockerfile viejo?

En PostgreSQL 17 no se utilizaba un Dockerfile propio, porque en el archivo compose.yaml se indicaba image: postgres:17. Esto significa que se usaba una imagen que ya estaba preparada.

En PostgreSQL 18 se utiliza build: ., que indica que Docker debe construir la imagen usando las instrucciones del Dockerfile. En este archivo se encuentra FROM postgres:18, que indica que se usará la imagen oficial de PostgreSQL 18 como base.

Por eso, PostgreSQL 17 utilizaba directamente una imagen preparada, mientras que PostgreSQL 18 utiliza un Dockerfile para construir su imagen.

## 3. Qué es el versionado semántico y por qué pasar de la 17 a la 18 es un cambio mayor.

El versionado semántico es una forma de organizar las versiones de un programa mediante números que indican la importancia de sus cambios.Generalmente, se utiliza el formato MAYOR.MENOR.PARCHE.

Pasar de PostgreSQL 17 a PostgreSQL 18 se considera un cambio mayor porque se cambia el número principal de la versión.

