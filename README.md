# WordPress con Docker (nginx + PHP-FPM + MariaDB)

Proyecto de RA2: un sitio WordPress desplegado con Docker Compose, con nginx como servidor web, PHP-FPM para ejecutar WordPress y MariaDB como base de datos. Incluye medidas de seguridad, pruebas de funcionamiento y rendimiento, y publicación en la red del aula y en GitHub Codespaces.

## Requisitos

- Docker y Docker Compose (Docker Desktop en Mac y Windows)
- Git
- Puerto 8080 libre en tu equipo

## Arrancar el proyecto desde cero

1. Clona el repositorio y entra en la carpeta:

   ```bash
   git clone https://github.com/USUARIO/REPOSITORIO.git
   cd REPOSITORIO
   git switch ra2-cms
   ```

2. Crea tu fichero de variables a partir de la plantilla y edítalo con tus valores (contraseñas largas):

   ```bash
   cp .env.example .env
   nano .env
   ```

3. Arranca los servicios:

   ```bash
   docker compose up -d
   docker compose ps
   ```

   Deben aparecer `db`, `wordpress` y `nginx` en estado `Up`.

4. Crea la base de datos y el usuario (solo la primera vez, porque los volúmenes son nuevos). Usa los valores de `WP_DB_NAME`, `WP_DB_USER` y `WP_DB_PASSWORD` de tu `.env`:

   ```bash
   docker compose exec db mariadb -u root -p
   ```

   ```sql
   CREATE DATABASE IF NOT EXISTS nombre_bd;
   CREATE USER IF NOT EXISTS 'usuario'@'%' IDENTIFIED BY 'contraseña';
   GRANT ALL ON nombre_bd.* TO 'usuario'@'%';
   FLUSH PRIVILEGES;
   EXIT;
   ```

5. Abre http://localhost:8080 y completa el instalador de WordPress.

## Acceso desde otros equipos del aula

WordPress deduce su dirección de la cabecera `Host`, así que funciona con cualquier IP. Saca la tuya con `ipconfig getifaddr en0` (Mac) o `hostname -I` (Linux) y pásala a tu compañero/a: `http://TU-IP:8080`. Los dos equipos deben estar en la misma red.

## Abrirlo en GitHub Codespaces

1. En GitHub, elige la rama `ra2-cms` → **Code** → **Codespaces** → **Create codespace on ra2-cms**.
2. En la terminal del codespace, repite los pasos 2, 3 y 4 de arriba.
3. En la pestaña **PORTS**, haz clic derecho en el 8080 → **Port Visibility** → **Public**.
4. Abre la **Forwarded Address** (`https://...-8080.app.github.dev`) y completa el instalador.
5. Al terminar, para el codespace en github.com/codespaces para no gastar horas de cuota.

## Estructura de carpetas

```text
.
├── docker-compose.yml     # servicios: nginx, wordpress, db
├── .env.example           # plantilla de variables (sin secretos)
├── .gitignore             # excluye .env
├── nginx/
│   └── default.conf       # configuración endurecida de nginx
├── docs/
│   ├── seguridad.md       # medidas de seguridad, antes y después
│   └── pruebas.md         # pruebas, rendimiento y publicación
└── README.md
```

## Documentación

- [Seguridad del gestor](docs/seguridad.md)
- [Pruebas, rendimiento y publicación](docs/pruebas.md)

## Aviso

Nunca ejecutes `docker compose down -v`: borra los volúmenes `wp_data` y `db_data` y pierdes el sitio. Para parar los servicios usa `docker compose stop` o `docker compose down` (sin `-v`).
