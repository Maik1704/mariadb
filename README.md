# Guía de instalación y configuración de MariaDB con Docker

Esta guía te llevará paso a paso en la instalación de MariaDB en un contenedor Docker, creación de una base de datos, creación de una tabla, inserción de datos y verificación de la persistencia de los datos.

## Requisitos previos

- **Docker** debe estar instalado en tu sistema. Si no lo tienes, puedes descargarlo desde [aquí](https://www.docker.com/products/docker-desktop).
- Tener acceso a una terminal o línea de comandos.

---

## Paso 1: Instalar Docker

1. Descarga e instala Docker desde [Docker Desktop](https://www.docker.com/products/docker-desktop).
2. Sigue las instrucciones de instalación según tu sistema operativo.
3. Una vez instalado, abre una terminal o línea de comandos y ejecuta el siguiente comando para verificar que Docker está instalado correctamente:

   ```bash
   docker --version
  
## Paso 2: Descargar la imagen oficial de MariaDB

Abre una terminal o línea de comandos.

Ejecuta el siguiente comando para descargar la imagen oficial de MariaDB desde Docker Hub:

  ```bash
  docker pull mariadb

## Paso 3: Crear y ejecutar un contenedor de MariaDB

Una vez descargada la imagen, vamos a crear y ejecutar el contenedor de MariaDB. Utiliza el siguiente comando:

```bash
docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=rootpassword -d mariadb
