# EPS · API de gestión de citas médicas

API REST para una EPS: administra doctores, pacientes, especialidades, consultorios, horarios y **citas médicas**, con permisos por rol y **notificaciones push** a la app móvil.

App móvil: [Eps_React](https://github.com/CristianGarcia7/Eps_React)

## 👥 Roles

| Rol | Qué puede hacer |
|---|---|
| **Paciente** | Registrarse, ver doctores disponibles con sus horarios y consultorios, solicitar citas y ver su historial |
| **Doctor** | Ver sus citas, aprobarlas, rechazarlas o completarlas, gestionar sus horarios y ver su consultorio |
| **Admin** | CRUD de usuarios, roles, doctores, pacientes, especialidades y consultorios |

## ✨ Funcionalidades

- Autenticación con **JWT** (`tymon/jwt-auth`) y middleware propio que maneja varios *guards* y roles.
- Flujo de citas con estados: *Por aprobar* → *Programada* o *Rechazada* → *Completada* o *Cancelada*.
- **Notificaciones push con Expo** cuando una cita cambia de estado.
- Correos para **solicitud de cita** y **restablecimiento de contraseña**.

## 🧱 Stack

Laravel 12 · PHP 8.2 · JWT Auth · SQLite / MySQL · Expo Push API

## 🚀 Cómo correrlo

```bash
composer install
cp .env.example .env        # SQLite por defecto; configura el correo (MAIL_*)
php artisan key:generate
php artisan jwt:secret
php artisan migrate
php artisan serve
```

## 📡 Endpoints destacados

| Método | Ruta | Rol |
|---|---|---|
| `POST` | `/api/login` · `/api/register` · `/api/reset-password` | Público |
| `POST` | `/api/solicitar-cita` | Paciente |
| `GET` | `/api/doctores-disponibles` · `/api/horarios-disponibles/{doctor}` | Paciente |
| `PUT` | `/api/doctor/aprobar-cita/{id}` · `/rechazar-cita/{id}` · `/completar-cita/{id}` | Doctor |
| `GET` `POST` `PUT` `DELETE` | `/api/doctor/...Horario` | Doctor |
| CRUD | `/api/doctores` · `/pacientes` · `/Especialidades` · `/users` · `/roles` | Admin |

La lista completa está en [`routes/api.php`](routes/api.php).
