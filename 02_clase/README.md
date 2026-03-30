# De la Idea al MVP con IA

_Resumen del material on demand (contenido de la plataforma)_

## **Idea Central**
No empieces con la solución, empieza con el problema. La meta no es "tener un SaaS", sino validar que estás resolviendo un **dolor real** para **personas reales**. La IA puede acelerar todo este proceso, pero nunca reemplazar la validación con usuarios.

---

### 1. **Descubre el Problema Real** (No tu idea)

Olvídate de las pantallas por un momento. Pregúntate:

- **¿Qué problema resuelvo?** No "un SaaS de reservas", sino "administradores de coworking que pierden ingresos porque gestionan reservas con Excel y WhatsApp, generando dobles reservas y facturación caótica".

- **¿Para quién?** No "los coworkings", sino "Laura, la administradora de un espacio con 35 miembros, que cada fin de semana cruza mensajes de WhatsApp para saber quién pagó su membresía y quién no".

- **¿Cómo lo resuelven hoy?** Usualmente con Excel para membresías, WhatsApp para reservas, Google Calendar para salas, y hojas de cálculo para facturación (esto genera errores, conflictos y horas no facturables).

**Herramienta IA útil:**
> *Prompt:* "Genera una lista de dolores (operativos, financieros y emocionales) que enfrentan los administradores de espacios de coworking al gestionar reservas, membresías y facturación con herramientas manuales."

---

### 2. **Organiza la Información y Genera Ideas Claras**

No es "hacer un calendario". Es definir oportunidades concretas basadas en lo que descubriste.

1. **Extrae patrones:** ¿Qué se repite en las entrevistas?
   - "Cada fin de mes pierdo 2 días enteros facturando"
   - "Los miembros se quejan porque no saben si la sala está libre"
   - "A veces dos personas reservan el mismo espacio y tengo que mediar"

2. **Dibuja el camino del usuario (User Journey):** Sigue los pasos de "Laura" para gestionar una reserva hoy. Identifica en qué paso sufre más.
   - Miembro envía WhatsApp → Laura revisa Excel → Laura confirma disponibilidad → Laura anota en hoja → Laura cobra manualmente → ERROR: doble reserva

3. **Formula oportunidades:** En formato "¿Cómo podríamos...?"
   - ¿Cómo podríamos centralizar la disponibilidad de todos los espacios en un solo lugar visible para todos?
   - ¿Cómo podríamos automatizar la facturación recurrente para que Laura no pierda 2 días al mes?
   - ¿Cómo podríamos dar autonomía al miembro para que reserve sin depender de Laura?

**Herramienta IA útil:**
> *Prompt:* "Dado el siguiente patrón '[Los administradores de coworking pierden 10-15 horas semanales gestionando reservas y facturación manualmente, generando dobles reservas y retrasos en cobros]', genera 3 oportunidades de solución en formato '¿Cómo podríamos...?' para un SaaS multitenant."

---

### 3. **Define tu MVP: El Mínimo para Aprender**

El MVP no es la versión más barata de tu producto soñado. Es el **experimento más pequeño** para probar tu hipótesis principal.

**Hipótesis:**
> "Si los miembros de un coworking pueden ver la disponibilidad en tiempo real y reservar espacios por sí mismos a través de un portal web, y el sistema genera automáticamente las facturas de membresías, los administradores reducirán su carga administrativa en un 70% y eliminarán las dobles reservas."

**MVP (Mínimo):** Un portal web con dos vistas:

| Vista | Funcionalidades mínimas |
|-------|------------------------|
| **Vista Miembro** | Ver calendario con espacios disponibles, reservar un espacio en 2 clics, ver mis reservas activas |
| **Vista Admin** | Ver todas las reservas del día, gestionar espacios (agregar/editar), ver quién debe pagar |

**NO necesita en MVP:**
- App móvil nativa (funciona con web responsive)
- Integración con cerraduras inteligentes
- Múltiples sedes para un mismo coworking
- Reportes avanzados y analytics complejos
- Marketplace de eventos o servicios extra
- Chat interno entre miembros

**Herramienta IA útil:**
> *Prompt:* "Prioriza estas funcionalidades para un MVP de SaaS de administración de coworking, usando el método MoSCoW (Must, Should, Could, Won't): Gestión de espacios, Calendario de reservas, Portal de miembros, Facturación automática, Login de admin, Reportes básicos, Pasarela de pagos, App móvil, Múltiples sedes."

---

### 4. **Construye en Etapas (con Vibe Coding)**

No intentes hacer todo al mismo tiempo. Avanza por capas, validando en cada una antes de continuar:

| Etapa | Objetivo | Qué construyes | Cómo validas |
|-------|----------|----------------|--------------|
| **Etapa 1 - Esqueleto** | Validar que el flujo se entiende | Pantallas con datos falsos (mock). Admin ve calendario, miembro puede hacer clic en "reservar". | Mostrar a 3 administradores. ¿Entienden cómo se usa? ¿El flujo tiene sentido? |
| **Etapa 2 - Datos Reales** | Validar que el producto funciona | Conectar a base de datos (Supabase). Las reservas persisten. Los espacios se guardan. | Probar con 1 coworking real. Que suban sus espacios y hagan 5 reservas de prueba. |
| **Etapa 3 - Usuarios Reales** | Validar que el producto es usado | Agregar autenticación (login). Cada coworking tiene su URL única (multitenant). | Que 5 miembros del coworking reserven sin ayuda del admin. Medir % de reservas exitosas. |
| **Etapa 4 - Facturación** | Validar el modelo de negocio | Integrar pasarela de pagos (Stripe/MercadoPago). Facturación automática de membresías. | Que el primer ciclo de cobros se complete. Medir % de pagos automatizados. |

**Herramienta IA útil:**
> *Prompt:* "Soy un creador construyendo un SaaS de coworking. Dame un plan paso a paso para implementar autenticación multitenant con Supabase, donde cada coworking tenga su propia URL y sus usuarios no puedan ver datos de otros coworkings."

---

## **Conclusión: Puntos Clave para el Creador**

1. **Ámate del problema, no de tu idea.** Tu primera idea probablemente esté equivocada. La investigación te acerca a la versión correcta. En este caso, el problema no es "falta de app", es "Laura pierde 2 días facturando".

2. **La IA es tu asistente de investigación e ideación,** no tu fuente de verdad. Úsala para ampliar perspectivas, generar preguntas y organizar información. La validación final es con personas reales: administradores y miembros de coworkings.

3. **Un MVP es un experimento, no un producto completo.** Su éxito se mide por el **aprendizaje validado**, no por la cantidad de features. Define 1 o 2 hipótesis clave y construye sólo lo necesario para probarlas.
   - Hipótesis 1: ¿Los miembros reservan sin ayuda si tienen visibilidad?
   - Hipótesis 2: ¿Los administradores pagan por automatizar facturación?

4. **Construye en capas.** 
   - Capa 1: Haz que *se vea* y *se entienda* (flujo con datos mock)
   - Capa 2: Haz que *funcione de verdad* (datos persistentes)
   - Capa 3: Hazlo *personal y escalable* (login + multitenant)
   - Capa 4: Hazlo *rentable* (facturación automática)

5. **El momento de la verdad es la URL pública.** Cuando tu MVP esté en línea y un coworking real (aunque sea uno solo) lo use para gestionar sus reservas diarias, habrás pasado de la teoría a la creación de un producto real. Allí comienza el aprendizaje verdadero.

---

## *Challenge recomendado*

**Tu meta al final de esta unidad:**

Poder mostrar un link (URL pública) donde:
- Un administrador de coworking pueda entrar, ver un calendario y gestionar sus espacios
- Un miembro pueda reservar un espacio sin ayuda
- Los datos persistan (si reservas hoy, mañana sigue ahí)

Ese es el primer y más importante paso en el camino de cualquier producto digital. No necesitas facturación automática en la primera entrega. Necesitas **un fragmento verificable del problema resuelto**.

---

## *Bonus: Preguntas para Reflexionar con los Alumnos*

| Pregunta | Propósito |
|----------|-----------|
| ¿Qué pasaría si en lugar de construir un SaaS, primero ayudas a Laura a facturar en 1 hora con una planilla mejorada? | Cuestionar si el producto es la solución o hay un camino más simple |
| ¿Cuál es la hipótesis más riesgosa de tu proyecto? ¿La técnica o la de adopción? | Identificar qué validar primero |
| Si solo pudieras mostrar UNA pantalla funcional en tu MVP, ¿cuál sería y por qué? | Forzar priorización extrema |
