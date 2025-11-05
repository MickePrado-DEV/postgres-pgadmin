# Entorno de Desarrollo PostgreSQL + pgAdmin con Docker

Este proyecto utiliza Docker Compose para levantar rápida y fácilmente un entorno de desarrollo local que incluye:

* **`db`**: Un contenedor con la base de datos **PostgreSQL 15.1**.
* **`pgAdmin`**: Un contenedor con **pgAdmin 4**, una interfaz gráfica para administrar la base de datos.

## 🚀 Cómo Empezar

### Prerrequisitos

* Tener [Docker](https://www.docker.com/get-started) y **Docker Compose** instalados en tu máquina.

### 1. Iniciar los Servicios

1.  Clona o descarga este repositorio.
2.  Abre una terminal en la carpeta raíz del proyecto (donde se encuentra el archivo `docker-compose.yml`).
3.  Ejecuta el siguiente comando para construir e iniciar los contenedores en segundo plano (`-d`):

    ```bash
    docker-compose up -d
    ```

### 2. Acceder a pgAdmin

1.  Abre tu navegador web y ve a **`http://localhost:8080`**.
2.  Inicia sesión con las credenciales que definiste en el archivo `docker-compose.yml`:
    * **Email**: `superman@google.com`
    * **Contraseña**: `123456`

### 3. Conectar pgAdmin a la Base de Datos

Una vez dentro de pgAdmin, necesitas "registrar" tu base de datos para que pgAdmin sepa cómo conectarse a ella.

1.  En la página principal, haz clic en **"Add New Server"** (o haz clic derecho en "Servers" -> "Register" -> "Server...").
2.  **Pestaña `General`**:
    * **Name**: Escribe un nombre descriptivo (ej. `Mi DB Local`).
3.  **Pestaña `Connection`**:
    * **Host name/address**: Escribe `db`.
        > **Importante:** Usas `db` (y no `localhost` o `127.0.0.1`) porque es el nombre del servicio de la base de datos definido en el `docker-compose.yml`. Docker se encarga de resolver este nombre a la IP interna del contenedor.
    * **Port**: `5432` (es el puerto por defecto de Postgres).
    * **Maintenance database**: `postgres`
    * **Username**: `postgres` (es el usuario por defecto que crea la imagen de Postgres).
    * **Password**: `123456` (la contraseña que definiste en `POSTGRES_PASSWORD`).
4.  Haz clic en **"Save"**.

¡Y listo! Ahora deberías ver tu servidor `Mi DB Local` en el panel izquierdo y podrás empezar a crear tablas y gestionar tu base de datos.

### 4. Detener los Servicios

Para detener y eliminar los contenedores, ejecuta:

```bash
docker-compose down
```

## 📂 Persistencia de Datos

Este setup está configurado para que tus datos no se pierdan aunque detengas o elimines los contenedores.

* **Datos de PostgreSQL**: Se guardan en la carpeta `./postgres` de tu máquina.
* **Configuración de pgAdmin**: Se guarda en la carpeta `./pgadmin` de tu máquina.

Si quieres empezar de cero, simplemente detén los contenedores (`docker-compose down`) y elimina estas dos carpetas.
