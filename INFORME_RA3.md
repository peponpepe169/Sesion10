# Informe RA3 - Administración de gestores de contenidos

## Sección 1. Roles, capacidades y perfiles de usuario

* **Capacidad para publicar entradas:** `publish_posts`
* **Capacidad para subir ficheros:** `upload_files`

| Usuario | Rol | Qué puede hacer | Qué NO puede hacer |
| :--- | :--- | :--- | :--- |
| `javier_wp` | Administrador | Control total: ajustes, plugins, temas, usuarios y contenidos. | Sin restricciones. |
| `coord.web` | Editor | Publicar y editar entradas/páginas de cualquiera, moderar comentarios y gestionar categorías. | Instalar/gestionar plugins, temas, usuarios o ajustes del sitio. |
| `profe.redes` | Autor | Escribir, publicar y borrar sus propias entradas; subir imágenes/archivos. | Editar o borrar entradas de otros usuarios ni crear páginas. |
| `alumna.fct` | Colaborador | Escribir sus propias entradas y enviarlas a revisión. | Publicar directamente ni subir imágenes o ficheros. |
| `familia.garcia` | Suscriptor | Leer contenido y editar su propio perfil de usuario. | Escribir, subir ni publicar ningún contenido. |
| `revisor.fp` | Revisor (a medida) | Revisar, editar y publicar entradas/páginas propias y de otros usuarios. | Borrar entradas o páginas (no tiene opción de Papelera) ni gestionar categorías, plugins o ajustes. |

## Sección 2. Selección y configuración de módulos (plugins)

* **R1. Formulario de contacto con almacenamiento en BD:**
  * **Comparativa:** *Contact Form 7 + Flamingo* vs *WPForms Lite*. La versión gratuita de WPForms no guarda los envíos en la base de datos de WordPress (requiere licencia Pro), mientras que Contact Form 7 junto con Flamingo almacena todos los mensajes entrantes en BD de forma gratuita.
  * **Elección:** **Contact Form 7 + Flamingo** (con `skip_mail: on` para evitar errores al no disponer de servidor SMTP en el contenedor).
* **R2. Aviso de cookies (LSSI y RGPD):**
  * **Comparativa:** *Complianz | GDPR/CCPA Cookie Consent* vs *CookieYes | GDPR Cookie Consent*. Ambos cuentan con cientos de miles de instalaciones activas, actualizaciones recientes, compatibilidad con WordPress 7.1 y asistente en español.
  * **Elección:** Plugin configurado con botones de **Aceptar** y **Rechazar** al mismo nivel visual y enlace a la página de política de cookies.
* **R3. Registro de actividad de los usuarios:**
  * **Comparativa:** *Simple History* vs *WP Activity Log*. Simple History es más ligero, muestra el registro directamente en el Escritorio de WordPress sin sobrecargar la interfaz y cubre los eventos de inicio de sesión, publicaciones y cambios de plugins.
  * **Elección:** **Simple History**.
