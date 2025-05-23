# pkt1

# Sistema de Gestión de Tareas - CodeIgniter 3

Este proyecto es un desarrollo web usando **PHP + CodeIgniter 3**, con autenticación, sesiones, manejo de tareas, consumo de API REST y SOAP, y despliegue en **IIS**.

---

## Requisitos

- PHP 7.4 o superior
- MySQL o MariaDB
- IIS con:
  - FastCGI configurado para PHP
  - Módulo URL Rewrite instalado

---

## Instalación

1. **Clonar el proyecto:**

```bash
C:\> git clone https://github.com/vlad9508/gestion_tareas.git C:\Users\tu_usuario\Documents\proyectos\php\pkt1
```

2. **Importar la base de datos:**

En MySQL, crea una base de datos y ejecuta el script `DatabaseSQL.sql`:

```sql
CREATE DATABASE gestion_tareas;
USE gestion_tareas;
-- Ejecutar contenido del archivo SQL
```

3. **Configurar conexión a la base de datos:**

Edita `/application/config/database.php`:

```php
'hostname' => 'localhost',
'username' => 'tu_usuario',
'password' => 'tu_password',
'database' => 'gestion_tareas',
```

4. **Asegurar rutas absolutas en `index.php`:**

```php
$system_path = realpath(__DIR__ . '/system') ?: __DIR__ . '/system';
$application_folder = realpath(__DIR__ . '/application') ?: __DIR__ . '/application';
```

5. **Configurar ruta base en IIS:**

- Ruta de acceso física: `C:\Users\tu_usuario\Documents\proyectos\php\pkt1`
- Ruta virtual: `/pkt1`

6. **Asegurar reglas de reescritura en `web.config`:**

```xml
<rewrite>
  <rules>
    <rule name="CodeIgniter Clean URLs" stopProcessing="true">
      <match url="^(.*)$" />
      <conditions logicalGrouping="MatchAll">
        <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
      </conditions>
      <action type="Rewrite" url="index.php/{R:1}" />
    </rule>
  </rules>
</rewrite>
```

---

## Acceso al sistema

Navegar a:

```bash
http://localhost/pkt1/auth/register
http://localhost/pkt1/auth/login
```

---

## 🛠 Solución de errores comunes

### `session_start(): Failed to initialize storage module`

1. Edita `php.ini`:
```ini
session.save_path = "C:\\php-sessions"
```

2. Crea la carpeta `C:\php-sessions`
3. Da permisos de escritura a `IUSR`
4. Reinicia IIS:
```cmd
iisreset
```

---

## Funcionalidades

- Registro y login con contraseña encriptada
- Generación de token simulado por sesión
- CRUD de tareas por usuario
- API externa REST (jsonplaceholder)
- Servicio SOAP (Number to Words)
- Interfaz responsive con Bootstrap 5

---

## Estructura del proyecto

```
/application
├── controllers (Auth, Tareas, Panel)
├── models (Usuario_model, Tarea_model)
├── views (auth, tareas, panel)
/config
├── database.php, routes.php
index.php
web.config
```

---
