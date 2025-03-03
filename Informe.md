# Sistema de Información de Notas y Asistencias para Colegios

Este proyecto tiene como objetivo desarrollar un **Sistema de Información de Notas y Asistencias** para colegios, que permita gestionar de manera eficiente la información académica de los estudiantes, incluyendo notas, asistencias, asignaturas, cursos y noticias escolares. El sistema está diseñado para ser utilizado por administradores, docentes, estudiantes y editores de noticias, cada uno con roles y permisos específicos.

---

## Requisitos del Sistema

### Requisitos Funcionales

1. **Gestión de Usuarios**:
   - Inicio y cierre de sesión para todos los usuarios.
   - Cambio de contraseña.
   - Creación, modificación y eliminación de usuarios por parte de los administradores.
   - Asignación de roles y permisos.
   - Registro de estudiantes a cursos y grupos.
   - Actualización de información personal por parte de docentes y estudiantes.
   - Consulta de información de estudiantes por parte de administradores y docentes.

2. **Gestión de Asignaturas y Cursos**:
   - Registro de asignaturas y asignación de docentes.
   - Consulta de asignaturas por curso para administradores, docentes y estudiantes.

3. **Gestión de Notas**:
   - Registro, edición y actualización de notas por parte de los docentes.
   - Consulta de notas según el rol del usuario.
   - Generación de reportes de notas por parte de administradores.

4. **Gestión de Asistencia**:
   - Registro, edición y actualización de asistencias por parte de los docentes.
   - Consulta de asistencias por parte de administradores, docentes y estudiantes.

5. **Gestión de Noticias Escolares**:
   - Publicación, edición y eliminación de noticias por parte del editor de noticias.
   - Consulta de noticias por parte de todos los usuarios.

---

### Requisitos de Comportamiento

1. **Reglas de Negocio**:
   - Un estudiante solo puede estar asignado a un único curso y grupo.
   - Un docente solo puede ingresar notas y asistencias para sus asignaturas asignadas.
   - Las notas no pueden ser modificadas después del cierre del período académico, salvo autorización del administrador.
   - Solo el administrador puede publicar, editar o eliminar noticias.
   - Un estudiante solo puede ver sus propias notas y asistencias.

2. **Validaciones y Restricciones**:
   - Las notas deben estar dentro del rango permitido (no negativas ni superiores al límite establecido).
   - Solo los administradores pueden generar reportes de notas.
   - Un estudiante solo puede tener un estado de asistencia por día y asignatura.
   - Las noticias solo pueden ser editadas o eliminadas por su autor.

---

## Casos de Uso

El sistema incluye los siguientes casos de uso:

1. **Gestión de Usuarios**:
   - UC-01: Iniciar sesión.
   - UC-02: Cerrar sesión.
   - UC-03: Cambiar contraseña.
   - UC-04: Crear usuarios (Administrador).
   - UC-05: Gestionar roles (Administrador).
   - UC-06: Eliminar usuarios (Administrador).
   - UC-07: Registrar estudiante a un curso (Administrador).
   - UC-08: Registrar estudiante a un grupo (Administrador).
   - UC-09: Modificar información de estudiantes (Administrador).
   - UC-10: Solicitar actualización de información (Docentes y estudiantes).
   - UC-11: Consultar información de estudiantes (Administradores y docentes).

2. **Gestión de Asignaturas y Cursos**:
   - UC-12: Registrar asignaturas (Administrador).
   - UC-13: Asignar docentes a asignaturas y grupos (Administrador).
   - UC-14: Consultar asignaturas por curso (Administradores, docentes y estudiantes).

3. **Gestión de Notas**:
   - UC-15: Registrar notas de los estudiantes (Docentes).
   - UC-16: Editar notas (Docentes).
   - UC-17: Consultar notas (Docentes y estudiantes).
   - UC-18: Generar reportes de notas (Administradores y docentes).

4. **Gestión de Asistencia**:
   - UC-19: Registrar asistencia de los estudiantes (Docentes).
   - UC-20: Editar asistencias (Docentes).
   - UC-21: Consultar asistencia (Administradores, docentes y estudiantes).

5. **Gestión de Noticias Escolares**:
   - UC-22: Publicar noticias del colegio (Editor de Noticias).
   - UC-23: Editar noticias (Editor de Noticias).
   - UC-24: Eliminar noticias (Editor de Noticias).

---

## Modelo de Dominio

El modelo de dominio del sistema se representa mediante diagramas UML que describen las relaciones entre las entidades principales, como **Usuario**, **Administrador**, **Docente**, **Estudiante**, **Curso**, **Asignatura**, **Grupo**, **Nota**, **Asistencia**, **Noticia** y **Horario**.

![Modelo de Dominio]("https://github.com/AlbeiroBurbanoTobar/SINAC/Imágenes/Modelo_de_dominio.png")
```plantuml
@startuml
class Usuario {}
class ReporteNotas{}
class HistorialNotas{}
class HistorialAsistencias{}
class Administrador {}
class Docente {}
class Estudiante {}
class Curso {}
class Asignatura {}
class Grupo {}
class Nota {}
class Asistencia {}
class Noticia {}
class Horario{}

Usuario <|-- Administrador
Usuario <|-- Docente
Usuario <|-- Estudiante

Noticia --o Administrador
Noticia o-- Usuario

Grupo o-- Estudiante
Curso <|-- Grupo
Grupo o-- Horario
Horario o-- Asignatura
Asignatura o-- Docente

Docente o-- Nota
Nota o-- Estudiante
Estudiante o-- HistorialNotas
HistorialNotas o-- Nota

Administrador o-- Curso
Administrador o-- Usuario
Administrador o-- ReporteNotas

ReporteNotas o-- HistorialNotas
ReporteNotas o-- HistorialAsistencias

Docente o-- Asistencia
Asistencia o-- Estudiante
Estudiante o-- HistorialAsistencias
Asistencia --o HistorialAsistencias
@enduml