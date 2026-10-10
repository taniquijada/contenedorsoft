## Ejercicio 4. Stack MySQL + phpMyAdmin

###  Confirmación de ejecución

Se completó la configuración del stack MySQL + phpMyAdmin mediante Docker Compose. Los contenedores se iniciaron correctamente y se comprobó su estado con el comando `docker compose ps`.

 Se ingresó a phpMyAdmin desde el navegador mediante la dirección `http://localhost:8081`.

### 1. Tabla comparativa: PostgreSQL + Adminer frente a MySQL + phpMyAdmin

| Característica | PostgreSQL + Adminer | MySQL + phpMyAdmin |
|---|---|---|
| Sistema de base de datos | PostgreSQL | MySQL |
| Interfaz de administración | Adminer | phpMyAdmin |
| Imagen de la base de datos | Imagen local construida a partir de `postgres:18` | `mysql:9.7.2` |
| Imagen de la interfaz web | `adminer:5.5.1` | `phpmyadmin:5.2.3` |
| Puerto de la base de datos en la máquina | 5434 | 3307 |
| Puerto de la interfaz web en la máquina | 8080 | 8081 |
| Dirección para acceder a la interfaz | `http://localhost:8080` | `http://localhost:8081` |
| Persistencia de datos | Volumen de Docker llamado `datos_db` | Volumen de Docker llamado `datos_mysql` |
| Comprobación de salud | `pg_isready` | `mysqladmin ping` |
| Propósito | Almacenar y administrar bases de datos PostgreSQL | Almacenar y administrar bases de datos MySQL |


### 2. ¿Qué es una versión LTS y qué es una versión Innovation?

**LTS (Long-Term Support)** Versión orientada a la estabilidad y la predictibilidad a largo plazo, la cual recibe únicamente parches críticos de seguridad y correcciones de errores sin modificar el comportamiento ni añadir funciones

**Innovation**  es una modalidad que permite acceder a nuevas funcionalidades, mejoras y cambios con mayor frecuencia. Está orientada a entornos que pueden probar las novedades y actualizarse de forma más frecuente. 


### 4. ¿Por qué se utiliza `mysql:9.7.2` y no `mysql:latest`?

En  `mysql:9.7.2` porque identifica explícitamente una versión concreta de MySQL perteneciente a la línea LTS 9.7. Esto permite que otros integrantes del equipo utilicen la misma versión y facilita la reproducción de la práctica.

Con la etiqueta `mysql:latest` que es dinámica que apunta únicamente a la última imagen subida al repositorio, la cual cambia sin previo aviso y puede provocar fallos inesperados al no garantizar estabilidad

Fijar una versión específica ayuda a reducir diferencias inesperadas entre entornos, facilita la identificación de errores y hace más confiable la repetición de las pruebas.

### Referencias

Gryp, K. y Lastori, A. (2023, 18 de julio). *Introducing MySQL Innovation and Long-Term Support (LTS) versions*. MySQL Blog Archive. https://dev.mysql.com/blog-archive/introducing-mysql-innovation-and-long-term-support-lts-versions/