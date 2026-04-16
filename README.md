# Laboratorio Laravel - Instalación y Configuración del Entorno

## Introducción

Este laboratorio tiene como objetivo documentar el proceso completo de instalación y configuración del framework Laravel en un entorno de desarrollo local con WAMP Server. A continuación, se detallan los pasos ejecutados, los requisitos previos, las decisiones técnicas tomadas y los comandos utilizados para dejar operativa una aplicación Laravel base.

El proyecto se estructura siguiendo el patrón MVC (Modelo-Vista-Controlador), cuyas carpetas principales en Laravel son:
- **`app/Models`**: Contiene los modelos que interactúan con la base de datos.
- **`app/Http/Controllers`**: Alberga los controladores que gestionan la lógica de la aplicación.
- **`routes/`**: Define las rutas (archivos `web.php`, `api.php`) que dirigen las peticiones HTTP.
- **`resources/views/`**: Almacena las vistas (principalmente Blade) que presenta la interfaz al usuario.

---

## 1. Prerrequisitos del Sistema

Los componentes necesarios que utilicé para el laboratorio :

| Tecnología | Versión / Especificación | Icono |
|------------|--------------------------|-------|
| **PHP** | 8.5 (requerido por phpMyAdmin) | <img src="https://img.shields.io/badge/PHP-8.5-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP 8.5"/> |
| **Composer** | Última versión estable | <img src="https://img.shields.io/badge/Composer-latest-885630?style=for-the-badge&logo=composer&logoColor=white" alt="Composer"/> |
| **Laravel Installer** | Versión 13 | <img src="https://img.shields.io/badge/Laravel%20Installer-13-E53D2F?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel Installer 13"/> |
| **Servidor Web Local** | WampServer (carpeta `www`) | <img src="https://img.shields.io/badge/WampServer-Apache%20%2B%20MySQL-DC5A2E?style=for-the-badge&logo=wampserver&logoColor=white" alt="WampServer"/> |
| **Servidor Web** | Apache (incluido en WampServer) | <img src="https://img.shields.io/badge/Apache-2.4-D22128?style=for-the-badge&logo=apache&logoColor=white" alt="Apache"/> |
| **Base de Datos** | MySQL (vía phpMyAdmin) | <img src="https://img.shields.io/badge/MySQL-9.1-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL"/> |
| **Editor de Código** | Visual Studio Code (VS Code) | <img src="https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white" alt="VS Code"/> |
| **Sistema Operativo** | Windows | <img src="https://img.shields.io/badge/Windows-11-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="Windows"/> |
| **NPM** | Paquetes Node.js y dependencias previamente instaladas | <img src="https://img.shields.io/badge/NPM-prebundled-CB3837?style=for-the-badge&logo=npm&logoColor=white" alt="NPM preinstalado"/> |

> **Nota**: Se requirió desinstalar PHP 7.4 para evitar conflictos y poder utilizar PHP 8.5, compatible con la versión de phpMyAdmin disponible en WampServer.

---

## 2. Proceso de Instalación de Laravel

### 2.1. Instalación de Composer y Laravel Installer

1. Se abrió el **CMD de Windows en modo administrador**.
2. Se navegó hasta la carpeta donde WampServer aloja los proyectos web:
   ```bash
   C:\Windows\System32>cd..
   C: \Windows>cd..
   C:\>cd wamp64
   C:\wamp64>cd www
3. Se instala en www el paquete instalador de laravel:
   ```bash
   C: \wamp64\www>composer global require laravel/installer
<img width="300" height="450" alt="Captura de pantalla 2026-04-14 211808" src="https://github.com/user-attachments/assets/4588700e-0618-42b9-a1df-39823ad119ca" />

Aparecerá la interfaz de instalación de manera automática.

## 3. Creación del Proyecto "PruebaLaravel"
Una vez instalado el Laravel Installer, se procedió a crear un nuevo proyecto ejecutando dentro de la carpeta www:
   ```bash
   laravel new PruebaLaravel
   ```
<img width="300" height="450" alt="Captura de pantalla 2026-04-14 211824" src="https://github.com/user-attachments/assets/2570f5c0-b4d5-4703-91ff-c50c08875fa3" />

Estos kits y frameworks que seleccioné determinan las herramientas adicionales que se integrarán al proyecto.

Al finalizar la creación del proyecto, el instalador solicitó la configuración de la base de datos. Se optó por MySQL, la cual se integraría posteriormente con phpMyAdmin accesible desde http://localhost/phpmyadmin gracias a WampServer.

<img width="500" height="450" alt="Captura de pantalla 2026-04-15 201717" src="https://github.com/user-attachments/assets/92a03419-de38-436a-9192-d84b479935a6" />

1.**Run default database migrations**  Ejecuta las migraciones de Laravel. Se seleccionó no ya que no habia tablas que migrar aún

2.**Run npm install && npm run build?** Instala dependencias Node.js y compila los assets del rpoyecto. Se seleccionó si para los complementos web.

Al terminar de instalar todas las dependencias el proyecto está listo para ejecutar desde nuestro editor de código, para verificar el estado de nuestro proyecto ejecutamos el siguiente comando:

````bash
Composer run dev
````

## 4. Editar variables de entorno y configurar base de datos

Una vez dentro del proyecto, edité las credenciales del archivo `.env`, las cuales permiten acceder a la base de datos:

```
DB_USERNAME=root
DB_PASSWORD=luifer123
```
<img width="1919" height="1019" alt="Captura de pantalla 2026-04-15 203317" src="https://github.com/user-attachments/assets/1a08e0d0-349a-4de3-880b-b8631267eda2" />

### 4.1. Solución de error con migraciones
Al verificar con composer run dev se detectó un error. Antes de correr las migraciones, se añadió en AppServiceProvider.php:

```
use Illuminate\Support\Facades\Schema; (clase)
Schema::defaultStringLength(191); (método)
```
<img width="1566" height="868" alt="Captura de pantalla 2026-04-14 220018" src="https://github.com/user-attachments/assets/987903e5-1fd5-42c4-a6f2-a11d7919b5d3" />

<img width="664" height="545" alt="Captura de pantalla 2026-04-14 220427" src="https://github.com/user-attachments/assets/a3169883-95b5-45d3-bb7a-4ed7c7ab5b2b" />

### 4.2. Limpieza de caché
Se ejecutaron los siguientes comandos:

```
php artisan config:clear
php artisan config:cache
```
<img width="819" height="148" alt="Captura de pantalla 2026-04-15 215833" src="https://github.com/user-attachments/assets/9dbea3c6-17a7-47f6-bd30-8d0de4ab777b" />

### 4.3. Verificación del proyecto
```
composer run dev
```
<img width="1228" height="504" alt="Captura de pantalla 2026-04-14 220034" src="https://github.com/user-attachments/assets/c72f2b59-287d-4726-90f5-e8e44be1d9e3" />
<img width="1919" height="920" alt="Captura de pantalla 2026-04-14 220802" src="https://github.com/user-attachments/assets/678ca5ad-895a-4654-93fc-69b6aba01fc5" />

Se verificó en el navegador la versión de Laravel funcionando correctamente.

### 4.4. Ejecución de migraciones
```
php artisan migrate
```
Al ejecutarlo, se confirma la creación de la base de datos PruebaLaravel en MySQL. Una vez creada, se visualiza en phpMyAdmin con todas las tablas generadas por las migraciones.
<img width="1070" height="521" alt="Captura de pantalla 2026-04-14 220715" src="https://github.com/user-attachments/assets/8e5c7997-b276-4e22-b5cf-f12f5c08348d" />

<img width="1919" height="918" alt="Captura de pantalla 2026-04-14 220826" src="https://github.com/user-attachments/assets/8c71656f-fc16-4499-88c2-cfafeac16c8b" />

<img width="1919" height="918" alt="Captura de pantalla 2026-04-14 220848" src="https://github.com/user-attachments/assets/0abc8eb9-07ba-462b-98a7-752c52a17894" />

