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

A continuación, se enumeran los componentes necesarios para la correcta ejecución del laboratorio:

| Tecnología | Versión / Especificación | Icono |
|------------|--------------------------|-------|
| **PHP** | 8.5 (requerido por phpMyAdmin, se desinstaló versión 7.4) | <img src="https://img.shields.io/badge/PHP-8.5-777BB4?style=flat&logo=php&logoColor=white" alt="PHP 8.5"/> |
| **Composer** | Última versión estable | <img src="https://img.shields.io/badge/Composer-latest-885630?style=flat&logo=composer&logoColor=white" alt="Composer"/> |
| **Laravel Installer** | Versión 13 | <img src="https://img.shields.io/badge/Laravel%20Installer-13-E53D2F?style=flat&logo=laravel&logoColor=white" alt="Laravel Installer"/> |
| **Servidor Web Local** | WampServer (carpeta `www`) | <img src="https://img.shields.io/badge/WampServer-Apache%20%2B%20MySQL-DC5A2E?style=flat&logo=wampserver&logoColor=white" alt="WampServer"/> |
| **Servidor Web** | Apache (incluido en WampServer) | <img src="https://img.shields.io/badge/Apache-2.4-D22128?style=flat&logo=apache&logoColor=white" alt="Apache"/> |
| **Base de Datos** | MySQL / MariaDB (vía phpMyAdmin) | <img src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat&logo=mysql&logoColor=white" alt="MySQL"/> |
| **Editor de Código** | Visual Studio Code (VS Code) | <img src="https://img.shields.io/badge/VS%20Code-007ACC?style=flat&logo=visual-studio-code&logoColor=white" alt="VS Code"/> |
| **Sistema Operativo** | Windows (con CMD en modo administrador) | <img src="https://img.shields.io/badge/Windows-11-0078D6?style=flat&logo=windows&logoColor=white" alt="Windows"/> |
| **NPN** | No aplicó (dejado en blanco) | — |

> **Nota**: Se requirió desinstalar PHP 7.4 para evitar conflictos y poder utilizar PHP 8.5, compatible con la versión de phpMyAdmin disponible en WampServer.

---

## 2. Proceso de Instalación de Laravel

### 2.1. Instalación de Composer y Laravel Installer

1. Se abrió el **CMD de Windows en modo administrador**.
2. Se navegó hasta la carpeta donde WampServer aloja los proyectos web:
   ```bash
   cd C:\wamp64\www
