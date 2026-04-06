# Road to MVP II

- **Problema central**: Necesidad de backend para persistencia y coordinación.
- **Cambio de mentalidad**: Pasar de prototipo a sistema real.
- **Arquitectura mínima**: Frontend ↔ Backend ↔ Base de datos.
- **Herramientas recomendadas**: Supabase (backend) y Vercel (hosting).
- **Seguridad y autenticación**: Autenticación progresiva y control de acceso.
- **IA**: Implementada en el backend para protección y control.
- **Errores comunes**: Lógica en frontend, falta de seguridad y pruebas.
- **Cierre conceptual**: Persistencia y reglas en backend son esenciales.

---

| Tema | Punto clave |
|------|-------------|
| Problema central | Necesidad de backend para persistencia y coordinación |
| Cambio de mentalidad | Pasar de prototipo a sistema real |
| Arquitectura mínima | Frontend ↔ Backend ↔ Base de datos |
| Herramientas | Supabase + Vercel |
| Seguridad | Autenticación y control de acceso |
| IA | Se implementa en backend |
| Errores comunes | Lógica en frontend, falta de seguridad |
| Cierre conceptual | Persistencia y reglas en backend son esenciales |


## Haciendo que Funcione: Backend para Sistemas Reales


## 1. El problema central

### Idea clave

Una aplicación solo frontend **no es un sistema**.

### Qué ocurre sin backend

* Los datos viven en el navegador
* Se pierden al refrescar
* No hay coordinación entre usuarios
* No existen reglas compartidas
* No hay memoria del sistema

### Caso introductorio

**App de reservas de espacios comunes**

* Un usuario reserva un horario
* Otro usuario puede reservar el mismo horario
* Ambos reciben confirmación
* El sistema no tiene forma de decidir

### Ejercicio

Preguntas para el grupo:

* ¿Dónde vive una reserva?
* ¿Quién valida la disponibilidad?
* ¿Qué pasa si dos usuarios actúan al mismo tiempo?

---

## 2. Cambio de mentalidad: de pantallas a sistemas

### Comparación esencial

| Prototipo          | Sistema real         |
| ------------------ | -------------------- |
| Datos temporales   | Datos persistentes   |
| Usuario aislado    | Usuarios coordinados |
| Sin reglas         | Reglas de negocio    |
| Vive en el momento | Vive en el tiempo    |

### Mensaje clave

No construimos pantallas, **construimos sistemas**.

---

## 3. Arquitectura mínima de un MVP real

### Trilogía esencial

```
Frontend ↔ Backend ↔ Base de Datos
```

#### Frontend

* Muestra información
* Captura acciones
* No decide reglas
* No guarda estado crítico

#### Backend

* Aplica reglas de negocio
* Valida acciones
* Gestiona permisos
* Coordina procesos

#### Base de datos

* Memoria persistente
* Fuente de verdad
* Estados e historial
* Timestamps

### Ejercicio práctico

Caso “reservar un espacio”:

* ¿Qué hace el frontend?
* ¿Qué valida el backend?
* ¿Qué se guarda en la base?

---

## 4. Herramientas para un MVP funcional

### Backend recomendado: Supabase

Motivos:

* PostgreSQL listo para usar
* Autenticación integrada
* Storage
* Seguridad con Row Level Security
* Menos infraestructura, más foco en producto

### Hosting

* Vercel para frontend y funciones serverless(siempre y cuando sea necesario)

### Control de versiones

* main como versión estable
* branches para experimentar
* commits como historial del sistema

### Ejercicio

Definir la tabla `reservas`:

* id
* user_id
* espacio
* fecha_hora
* estado
* created_at

---

## 5. Seguridad y autenticación

### Pregunta clave

¿Estos datos pertenecen a alguien?

### Cuándo usar autenticación

* Hay un dueño del dato
* Existen consecuencias reales
* El uso es recurrente
* Se necesita control o personalización

### Autenticación progresiva

1. Explorar sin login
2. Identificarse al generar impacto
3. Ejemplo:

   * Ver disponibilidad sin login
   * Reservar con login

### Idea central

Si hay usuarios y datos, la seguridad es parte del diseño inicial.

---

## 6. IA en el producto

### Regla fundamental

La IA vive en el backend.

### Razones

* Protección de claves
* Control de costos
* Aplicación de permisos
* Persistencia de contexto

### Flujo básico

1. Frontend envía input
2. Backend arma contexto
3. Backend llama a la IA
4. Backend valida con la base
5. Respuesta al frontend

### Caso simple

IA que sugiere horarios disponibles o explica reglas al usuario.

---

## 7. Errores comunes en MVP

* Poner toda la lógica en el frontend
* Dejar la seguridad para después
* Obligar a login para todo
* Consumir APIs externas desde el navegador
* Confundir MVP con demo visual

### Frase clave

El frontend propone, el backend dispone.

---

## 8. Ejercicio integrador

### Caso completo

Sistema de reservas de espacios comunes.

Definir:

1. Entidades principales
2. Reglas de negocio
3. Responsabilidades del frontend
4. Responsabilidades del backend
5. Qué se persiste en la base

### Resultado esperado

Un sistema simple pero real:

* Usuarios identificados
* Reservas persistentes
* Horarios bloqueados
* Reglas claras y compartidas

---

## 9. Cierre conceptual

### Ideas para llevarse

* Sin base de datos no hay producto
* MVP no es prototipo
* Persistencia convierte ideas en sistemas
* Las reglas viven en el backend
* Las herramientas aceleran el desarrollo
