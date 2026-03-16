# **Introducción al Vibe Coding**

[Material de clase en vivo](https://docs.google.com/presentation/d/1Cz7lsKyKDbExoKBWmULMlyvt_LKquKt-/edit?slide=id.g39f14169acf_0_91#slide=id.g39f14169acf_0_91)

## Repaso del material OnDemand



### **Puntos Principales**

1.  **¿Qué es Vibe Coding?**
    Una nueva forma de construir productos digitales donde la **IA es un colaborador permanente**. Permite describir lo que se quiere crear con un *prompt* (instrucción textual) y obtener interfaces, flujos y prototipos funcionales generados automáticamente.
    *   **Meta:** Reducir drásticamente la barrera técnica y el tiempo de desarrollo, permitiendo que personas no técnicas participen en la creación y facilitando la validación rápida de ideas.

2.  **Evolución de la Industria (Cascada → Agile → Vibe Coding)**
    *   **Cascada:** Modelo rígido, secuencial y lento. Los errores se detectan tarde.
    *   **Agile:** Introdujo iteraciones, feedback rápido y ciclos cortos, pero los roles seguían siendo especializados y la codificación era un cuello de botella.
    *   **Vibe Coding:** Con la IA, **construir ya no es el principal problema**. El desafío ahora es **definir qué construir** y **validar el valor real** del producto.

3.  **Cambio en los Roles**
    Los roles (PM, Diseñador, Desarrollador) no desaparecen, pero **se mezclan y su enfoque cambia**.
    *   Su valor ahora está en el **criterio**, la **validación de hipótesis** y el **pensamiento de producto**, más que en la ejecución técnica pura.
    *   Permite que equipos pequeños (1-2 personas) construyan un MVP funcional rápidamente.

4.  **El MVP (Producto Mínimo Viable) es la Estrella Norte**
    *   **No es un prototipo ni una demo.** Es la **versión mínima, pero funcional y usable**, cuyo único propósito es **validar una hipótesis central de valor** con usuarios reales.
    *   Se debe diferenciar claramente de:
        *   **POC (Proof of Concept):** Prueba técnica para ver si algo es posible.
        *   **Prototipo:** Simulación (generalmente sin código) para testear flujos y usabilidad.
        *   **MLP (Minimum Lovable Product):** La evolución del MVP, donde se añaden detalles que generan preferencia y retención.

5.  **Proceso para Definir un MVP**
    No se trata solo de "hacer menos". Es un proceso estratégico:
    1.  **Research:** Entender el problema y al usuario.
    2.  **Hipótesis:** Definir qué crees que soluciona el problema.
    3.  **Ideación / User Journey:** Mapear paso a paso cómo el usuario lograría su objetivo.
    4.  **Listado de Funcionalidades:** Derivarlas del journey, con precisión (no solo "login", sino "login con email y Google").
    5.  **Priorización:** Usar marcos como **MoSCoW** (Must, Should, Could, Won't) para elegir qué va al MVP.

6.  **El Desafío Real**
    Con Vibe Coding, **construir es fácil, decidir no**. El riesgo es crear sin dirección. El éxito está en **entender el problema del usuario** y **medir lo correcto**. El nuevo cuello de botella es la **distribución y la retención**.

---

### **Ejercicios para  Clase**

#### **Ejercicio 1: Clasificación - ¿Qué estoy viendo?** (5-10 min)
**Objetivo:** Afinar el criterio para diferenciar un POC, un Prototipo, un MVP y un MLP.

**Dinámica:** Mostrar o describir estos ejemplos y preguntar a la clase: "¿Qué es esto?"
1.  "Una pantalla de Figma con botones que no funcionan, pero permite visualizar el flujo de reserva del SUM." → **Prototipo**.
2.  "Un script que sube una foto del SUM a una API de IA para verificar si detecta objetos." → **POC**.
3.  "Una app web simple donde el usuario puede loguearse, ver un calendario, reservar un turno y recibir confirmación por mail." → **MVP**.
4.  "La misma app, pero ahora con un onboarding guiado, diseño pulido, notificaciones push y feedback animado al reservar." → **MLP**.

#### **Ejercicio 2: De la Idea al Prompt de Vibe Coding** (10-15 min)
**Objetivo:** Practicar el primer paso de materializar una idea usando IA.

**Dinámica:**
1.  **Paso 1 (Individual/Grupal):** Pedir a los estudiantes que piensen en un **"dolor real"** de su vida cotidiana o universitaria (ej: organizar compras grupales, recordatorios de préstamos de libros, turnos para usar la cocina).
2.  **Paso 2:** Que escriban en un papel una **frase simple** que defina el producto que lo solucionaría (ej: "Una app para registrar y dividir gastos entre roommates").
3.  **Paso 3 (Demostración en vivo):** Elegir una de esas frases. Abrir una herramienta de Vibe Coding (como **v0.dev** o **Lovable** en modo demo) y **escribir el prompt**.
    *   **Prompt de ejemplo:** "Crea la interfaz de una app móvil para dividir gastos entre compañeros de piso. Debe tener: 1) Una lista de gastos con nombre, monto y quién lo pagó. 2) Un botón para agregar un nuevo gasto. 3) Un resumen que muestre cuánto le debe cada uno al otro."
4.  **Paso 4:** Analizar en conjunto **qué generó la IA**: qué interpretó bien, qué decisiones de diseño tomó sola, qué falta o qué no funcionaría.

#### **Ejercicio 3: Priorización con MoSCoW** (10 min)
**Objetivo:** Aprender a recortar un producto a su esencia MVP.

**Dinámica:**
1.  Presentar un **caso común:** "Vamos a construir una app para vender productos artesanales online".
2.  Mostrar una **lista larga de funcionalidades** deseables:
    *   Catálogo de productos con fotos
    *   Carrito de compras
    *   Pasarela de pago (tarjeta, Mercado Pago)
    *   Sistema de reseñas y puntuaciones
    *   Perfil de usuario con historial
    *   Notificaciones por mail de estado del pedido
    *   Blog de consejos para artesanos
    *   Modo oscuro
    *   Búsqueda avanzada con filtros
    *   Login con redes sociales
3.  **Consigna para la clase (en grupos o votación rápida):** Usando **MoSCoW**, clasifiquen estas funcionalidades para el **MVP**.
    *   **Must (Debe tener):** Catálogo, Carrito, Pasarela de pago básica. *(Sin esto, el producto no cumple su función principal)*.
    *   **Should (Debería tener):** Perfil de usuario simple, Notificación de confirmación por email.
    *   **Could (Podría tener):** Login con redes sociales, Búsqueda simple.
    *   **Won't (No tendrá ahora):** Blog, Modo oscuro, Reseñas, Filtros avanzados.
4.  **Debate:** ¿Por qué ciertas funciones "queribles" (como las reseñas) quedan fuera del MVP? Conectar con el concepto: el MVP solo valida la hipótesis central ("¿La gente comprará artesanías por esta app?").

#### **Ejercicio 4: ¿Cuál es la Hipótesis Central?** (5 min)
**Objetivo:** Enfocarse en lo que realmente debe validar el MVP.

**Dinámica:** Para cada idea de producto, preguntar:
1.  **"App de Reservas de SUM":** Hipótesis: "Los vecinos de un edificio **evitarán conflictos y ahorrarán tiempo** reservando online en lugar de por un cuaderno físico."
2.  **"App de Gastos Compartidos":** Hipótesis: "Los roommates **dejarán de tener discusiones** y ahorrarán tiempo calculando manualmente, si tienen un registro claro y automático de deudas."
3.  **Punto clave:** El MVP no prueba si la app "funciona técnicamente", sino si **esa hipótesis de valor es cierta** para los usuarios.

---

### **Conclusión**

"Vibe Coding **nos da un superpoder: velocidad de construcción**. Pero ese superpoder es peligroso si no lo usamos con una **brújula clara**. La brújula es el **pensamiento de producto**: entender el problema, definir un MVP para validar valor, y tener el criterio para priorizar y medir lo importante. En este curso, no solo aprenderán a usar IA para construir, sino a pensar como dueños de producto."