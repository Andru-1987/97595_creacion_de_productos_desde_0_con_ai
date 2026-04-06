# Clase del Roadmap II

## Introducción

En esta etapa del roadmap dejamos de pensar la aplicación solo como una interfaz visual y empezamos a entenderla como un **sistema completo**.
Un sistema digital real se construye a partir de tres pilares fundamentales:

* Frontend
* Backend
* Base de datos

Cada uno cumple un rol específico y tiene responsabilidades bien definidas. Separar correctamente estas responsabilidades es clave para que la aplicación sea segura, escalable y mantenible.

---

## Frontend

El **Frontend** es la capa de interacción entre el usuario y el sistema.

### Su rol principal

* Mostrar información al usuario
* Capturar acciones (clicks, formularios, navegación)
* Representar el estado del sistema de forma visual

### Qué hace

* Renderiza pantallas
* Envía solicitudes al backend
* Interpreta respuestas para mostrarlas correctamente

### Qué no debería hacer

* Definir reglas de negocio
* Validar decisiones críticas
* Guardar información sensible
* Decidir si una acción es válida o no

El frontend **propone acciones**, pero no tiene autoridad para decidir si esas acciones están permitidas.

---

## Backend

El **Backend** es el núcleo lógico del sistema.
Es donde viven las reglas, decisiones y comportamientos reales del producto.

### Responsabilidades principales

* Aplicar la lógica de negocio
* Validar datos recibidos desde el frontend
* Gestionar autenticación y autorización
* Coordinar flujos del sistema
* Integrarse con servicios externos
* Garantizar la consistencia de los datos

### Ejemplos de lógica en backend

* Validar credenciales de login
* Verificar si un usuario puede reservar un horario
* Evitar reservas duplicadas
* Enviar recordatorios o notificaciones
* Registrar eventos importantes del sistema

El backend **recibe pedidos**, decide si son válidos y ejecuta las acciones correspondientes.

---

## Bases de Datos

La **Base de Datos** es la memoria del sistema.

### Su función

* Almacenar información de forma persistente
* Ser la fuente de verdad del sistema
* Permitir consultas históricas y auditoría

### Qué se guarda

* Usuarios
* Reservas
* Estados (activo, cancelado, pendiente)
* Fechas y horarios
* Historial de acciones
* Información relevante para administradores

Sin base de datos:

* El sistema no recuerda nada
* No hay continuidad en el tiempo
* No existe coordinación real entre usuarios

---

## APIs: el puente entre Frontend y Backend

### ¿Qué es una API?

Una **API (Application Programming Interface)** es un conjunto de reglas que define cómo el frontend puede comunicarse con el backend.

Es el contrato que establece:

* Qué se puede pedir
* Cómo se pide
* Qué respuesta se recibe

### Por qué el backend debe exponer APIs

* Para centralizar la lógica
* Para aplicar reglas de seguridad
* Para controlar el acceso a los datos
* Para validar cada acción del usuario

### Seguridad en APIs

Las APIs deben ser seguras porque:

* El frontend puede ser manipulado
* Las solicitudes pueden ser falsificadas
* Los datos pueden ser sensibles

Por eso el backend:

* Valida autenticación
* Verifica permisos
* Controla qué datos devuelve
* Rechaza acciones inválidas

---

## Comunicación Frontend ↔ Backend

El flujo típico es:

1. El usuario interactúa con el frontend
2. El frontend envía una solicitud a una API
3. El backend valida la solicitud
4. El backend consulta o modifica la base de datos
5. El backend responde
6. El frontend muestra el resultado

Este flujo se repite para cada acción relevante del sistema.

---

## Integración con herramientas de “vibe coding”

Las herramientas de vibe coding (IA, asistentes de código, generación automática) pueden acelerar el desarrollo, pero **necesitan contexto y estructura**.

### Buenas prácticas al integrarlas

* Tener clara la arquitectura del sistema
* Definir bien qué hace cada capa
* Formular pedidos claros y específicos
* Explicar reglas de negocio y restricciones

### Ejemplo de pedido correcto

En lugar de:

> “Haceme una app de reservas”

Mejor:

> “Necesito un backend que valide reservas por horario, evite solapamientos, use autenticación y exponga APIs REST para un frontend web”

Cuanto mejor estructurado esté el sistema, mejor será el resultado que generen estas herramientas.

---

## Cierre conceptual

| Capa | Descripción |
|------|-------------|
| Frontend | Se enfoca en la experiencia del usuario |
| Backend | Toma decisiones y contiene la lógica de negocio |
| Base de datos | Guarda la historia y datos persistentes |
| APIs | Conectan frontend y backend |
| Seguridad | Reglas y protección viven en el backend |


Entender esta separación es el paso clave para dejar de construir demos y empezar a construir **productos reales**.
