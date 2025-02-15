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
   ```
## Paso 2: Descargar la imagen oficial de MariaDB

1. Abre una terminal o línea de comandos.

2. Ejecuta el siguiente comando para descargar la imagen oficial de MariaDB desde Docker Hub:

  ```bash
  docker pull mariadb
  ```
![image](https://github.com/user-attachments/assets/e9116967-12be-4239-9335-e82caefc88ce)

## Paso 3: Crear y ejecutar un contenedor de MariaDB

Una vez descargada la imagen, vamos a crear y ejecutar el contenedor de MariaDB. Utiliza el siguiente comando:

   ```bash
   docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=rootpassword -d mariadb
   ```
![image](https://github.com/user-attachments/assets/fec78277-c47f-4e3a-be7e-16bf1a870b4a)

# Explicación de los parámetros:

1. --name mariadb-container: Asigna un nombre al contenedor, en este caso mariadb-container.
2. -e MYSQL_ROOT_PASSWORD=rootpassword: Establece la contraseña del usuario root como rootpassword (puedes cambiarla si lo deseas).
3. -d: Ejecuta el contenedor en segundo plano.
4. mariadb: Especifica la imagen que estamos utilizando (MariaDB).
   
Para verificar que el contenedor se está ejecutando correctamente, usa el siguiente comando:

   ```bash
   docker ps
   ```
![image](https://github.com/user-attachments/assets/5e31ca42-1b2a-4c10-9490-ea79aaa6f67a)

Esto te mostrará una lista de los contenedores en ejecución. Asegúrate de que mariadb-container esté en la lista.

## Paso 4: Conectarse al contenedor de MariaDB

1. Para acceder al contenedor y comenzar a trabajar con la base de datos, ejecuta el siguiente comando:

```bash
docker exec -it mariadb-container mariadb -u root -p
```
![image](https://github.com/user-attachments/assets/1d837d36-4b9c-4284-883b-c1de34b77faf)

Esto te pedirá la contraseña de root (la que definimos previamente como rootpassword o el que hayas colocado tu).

2. Una vez que ingreses la contraseña, estarás dentro de la consola de MariaDB y podrás empezar a interactuar con la base de datos.

## Paso 5: Crear una base de datos

Ahora que estás dentro de la consola de MariaDB, vamos a crear una base de datos llamada escuela.

1. Ejecuta el siguiente comando:

```sql
CREATE DATABASE escuela;
```
![image](https://github.com/user-attachments/assets/71407e0d-6180-4233-a688-f014ff52d63a)

2. Para usar la base de datos que acabamos de crear, ejecuta:

```sql
USE escuela;
```
![image](https://github.com/user-attachments/assets/864b6209-792d-42a2-83dd-8aa34a36b8d1)

## Paso 6: Crear una tabla

1. Ahora, vamos a crear una tabla llamada Estudiantes en la base de datos escuela. Esta tabla tendrá las siguientes columnas:

      * id: un campo de tipo entero que se autoincrementa y es la clave primaria.
      * nombre: un campo de tipo texto (hasta 100 caracteres).
      * apellido: un campo de tipo texto (hasta 100 caracteres).
      * edad: un campo de tipo entero.
      * email: un campo de tipo texto (hasta 100 caracteres).

  Ejecuta el siguiente comando SQL para crear la tabla:

```sql
CREATE TABLE Estudiantes (
  id INT AUTO_INCREMENT,
  nombre VARCHAR(100),
  apellido VARCHAR(100),
  edad INT,
  email VARCHAR(100),
  PRIMARY KEY (id)
);
```
![image](https://github.com/user-attachments/assets/e2919991-53ee-4b3e-aece-286778f2b4ab)

2. Para verificar que la tabla Estudiantes se ha creado correctamente, ejecuta:

```sql
SHOW TABLES;
```
![image](https://github.com/user-attachments/assets/aa46ff3a-b6c5-49e3-92d1-965d4f54d469)

Esto mostrará todas las tablas en la base de datos escuela y deberías ver la tabla Estudiantes en la lista.

## Paso 7: Insertar datos en la tabla

1. Para insertar un registro en la tabla Estudiantes, utiliza el siguiente comando SQL:

```sql
INSERT INTO Estudiantes (nombre, apellido, edad, email) 
VALUES ('Juan', 'Pérez', 20, 'juan.perez@example.com');
```
![image](https://github.com/user-attachments/assets/5bbec700-d54f-4233-b3b2-38cc67d64a27)

2. Puedes agregar más registros utilizando el mismo formato, cambiando los valores según sea necesario.

## Paso 8: Ver los datos insertados

1. Para verificar que los datos se han insertado correctamente en la tabla, usa:

```sql
SELECT * FROM Estudiantes;
```
![image](https://github.com/user-attachments/assets/578a06a2-061c-4985-b029-9b610d04c459)

2. Esto mostrará todos los registros de la tabla Estudiantes, y deberías ver el registro de "Juan Pérez" si lo insertaste correctamente.
3. Colocar exit para salir de la base de datos.
```sql
exit;
```
![image](https://github.com/user-attachments/assets/e3a2cdb7-f1ef-4dc7-a02f-61a2bb0a1ba9)

## Paso 9: Verificación después de reiniciar el contenedor

1. Si deseas asegurarte de que los datos persisten después de reiniciar el contenedor, puedes detener el contenedor y reiniciarlo con los siguientes comandos:

Detener el contenedor:

```bash
docker stop mariadb-container
```
![image](https://github.com/user-attachments/assets/e797d868-72b3-488f-9c51-294dda8b932f)

2. Iniciar nuevamente el contenedor:

```bash
docker start mariadb-container
```
![image](https://github.com/user-attachments/assets/7c8be4a1-c320-40a5-8969-91966d90197f)

3. Luego, vuelve a conectarte al contenedor y verifica los datos:

```bash
docker exec -it mariadb-container mariadb -u root -p
```
![image](https://github.com/user-attachments/assets/1d837d36-4b9c-4284-883b-c1de34b77faf)

4. Selecciona la base de datos escuela y consulta la tabla Estudiantes:

```sql
USE escuela;
SELECT * FROM Estudiantes;
```
![image](https://github.com/user-attachments/assets/ab29b914-d51c-4390-9ce0-7eb52dd55acb)

5. Si los datos siguen estando allí después de reiniciar el contenedor, significa que los datos están siendo correctamente persistidos.

## Paso 10: Salir de la consola de MariaDB

1. Cuando hayas terminado de trabajar con la base de datos, puedes salir de la consola de MariaDB con el siguiente comando:

```sql
exit;
```
![image](https://github.com/user-attachments/assets/e3a2cdb7-f1ef-4dc7-a02f-61a2bb0a1ba9)
