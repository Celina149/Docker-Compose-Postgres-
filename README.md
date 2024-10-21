# Proyecto Docker-Compose con PostgreSQL

Este proyecto configura un contenedor de PostgreSQL utilizando Docker Compose. A continuación, se detallan los pasos para configurar y acceder a la base de datos.

## Estructura del Proyecto

## Requisitos Previos

- Docker y Docker Compose y visual studio code instalados en tu máquina.

y para empezar se tiene que estar ejecutando docker.

## Creación del Directorio del Proyecto

1. Abre una terminal y navega a tu directorio de trabajo:

   ```bash
   mkdir commpose02
   cd commpose02

    Una vez dentro del directorio poner como comando code . y se abrira visual studio code 

    -crear un archivo docker-compose.yml y copiar lo siguiente:
 
 		#version: '3.8'

        services:
        db:
            image: postgres:13
            container_name: postgres
            restart: always
            environment:
            POSTGRES_USER: postgres
            POSTGRES_PASSWORD: postgres
            POSTGRES_DB: basedatos
            ports:
            - "5432:5432"
            volumes:
            - pgdata:/var/lib/postgresql/data

        volumes:
        pgdata:

2. Levantar el Contenedor

Ejecuta el siguiente comando para iniciar el contenedor:
	
	docker-compose up -d

3. Verificar el Estado del Contenedor

Puedes verificar que tu contenedor esté corriendo con el siguiente comando:

    docker ps
Deberías ver algo similar a:


| CONTAINER ID      | IMAGE          | COMMAND               | CREATED         | STATUS         | PORTS                     | NAMES    |
|-------------------|----------------|-----------------------|------------------|----------------|---------------------------|----------|
| 26aa64ccc56f      | postgres:13    | "docker-entrypoint.s…" | X minutes ago    | Up X minutes   | 0.0.0.0:5432->5432/tcp    | postgres  |

# Acceder a PostgreSQL
1. Desde el Contenedor

Si no tienes psql instalado en tu máquina local, puedes acceder a la consola de PostgreSQL directamente desde el contenedor con el siguiente comando:

    docker exec -it postgres psql -U postgres -d basedatos

2. Ejemplo de Consultas SQL

Una vez que estés en la consola de psql, puedes ejecutar las siguientes consultas como ejemplo:

     CREATE TABLE ejemplo (
        id SERIAL PRIMARY KEY,
        nombre VARCHAR(50) NOT NULL
      );

    INSERT INTO ejemplo (nombre) VALUES ('Prueba 1'), ('Prueba 2');

    SELECT * FROM ejemplo;
3. Detener el Contenedor\

Cuando termines de trabajar, puedes detener y eliminar el contenedor con:

    docker-compose down

