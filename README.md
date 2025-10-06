# Instrucción turning / Templates
Usar plantillas fijas de [instrucciones optimizadas](https://www.ibm.com/es-es/think/topics/instruction-tuning). Algunas fuentes para consular:

---
**1. IBM – Instruction Tuning**
- **Enlace:** [IBM – Instruction Tuning](https://www.ibm.com/es-es/think/topics/instruction-tuning)
- **Descripción:** Explica el concepto de instruction tuning, cómo estructurar prompts y ejemplos para datasets de entrenamiento, incluyendo clasificación, extracción y generación de texto.

---
**2. Hugging Face – Datasets y Prompt Engineering**
- **Enlace:** [Hugging Face Datasets](https://huggingface.co/docs/datasets/)
- **Descripción:** La documentación de Hugging Face incluye ejemplos de cómo estructurar datasets para fine-tuning, con plantillas para tareas como clasificación, QA, y generación de texto.

---
**3. Google – Prompt Engineering Guide**
- **Enlace:** [Google – Prompt Engineering Guide](https://ai.google.dev/docs/prompt_guide)
- **Descripción:** Guía práctica sobre cómo diseñar prompts efectivos, con ejemplos de instrucciones claras y respuestas esperadas, aplicables a múltiples idiomas.

---
**4. Papers With Code – Instruction Tuning**
- **Enlace:** [Papers With Code – Instruction Tuning](https://paperswithcode.com/method/instruction-tuning)
- **Descripción:** Recopila papers y ejemplos de instruction tuning, incluyendo datasets públicos y estructuras de prompts para diferentes tareas de NLP.

---
**5. Stanford NLP – Datasets y Ejemplos**
- **Enlace:** [Stanford NLP](https://nlp.stanford.edu/)
- **Descripción:** Ofrece recursos y ejemplos de cómo estructurar datos para entrenamiento supervisado, con énfasis en consistencia y evaluación automática.

---
**6. GitHub – Datasets para Fine-Tuning**
- **Ejemplo:** [Datasets de Hugging Face en GitHub](https://github.com/huggingface/datasets)
- **Descripción:** Repositorios con datasets estructurados para fine-tuning, incluyendo ejemplos en español y otros idiomas.

---
**7. ArXiv – Papers sobre Instruction Tuning**
- **Ejemplo:** [FLAN: Scaling Instruction-Finetuned Language Models](https://arxiv.org/abs/2109.01652)
- **Descripción:** Paper que detalla cómo estructurar instrucciones y ejemplos para mejorar el rendimiento de modelos de lenguaje.

---

### Plantilla general
Esquema para construir ejemplos consistentes en el dataset:

- Tarea: Describe de forma breve y accionable lo que debe hacer el modelo.  
- Datos: Proporciona el contenido de entrada necesario para cumplir la tarea.  
- Respuesta esperada: Muestra exactamente el formato y el contenido objetivo que el modelo debería producir.

### Ejemplo 1 (clasificación)
- Tarea: Clasifica el sentimiento del texto como “positivo”, “negativo” o “neutro”.  
- Datos: “El producto llegó antes de lo previsto y funciona perfectamente.”  
- Respuesta esperada: positivo

### Ejemplo 2 (extracción estructurada)
- Tarea: Extrae entidades de tipo persona, organización y fecha en formato JSON con claves “personas”, “organizaciones”, “fechas”.  
- Datos: “María Gómez firmó un acuerdo con TechNova el 12 de septiembre de 2024.”  
- Respuesta esperada: {"personas":["María Gómez"],"organizaciones":["TechNova"],"fechas":["2024-09-12"]}

### Ejemplo 3 (transformación de texto)
- Tarea: Reescribe el texto en voz activa, manteniendo el significado y el idioma.  
- Datos: “El informe fue revisado por el equipo de calidad antes de su publicación.”  
- Respuesta esperada: “El equipo de calidad revisó el informe antes de su publicación.”

### Ejemplo 4 (QA con formato fijo)
- Tarea: Responde a la pregunta usando solo la evidencia, en máximo dos frases, y devuelve también una puntuación de confianza entre 0 y 1.  
- Datos: “Evidencia: La capital de Chile es Santiago. Pregunta: ¿Cuál es la capital de Chile?”  
- Respuesta esperada: “La capital de Chile es Santiago. Confianza: 0.98”

### Ejemplo 5 (instrucción + validación)
- Tarea: Resume el texto en ≤30 palabras y termina con una etiqueta [OK] si el resumen está dentro del límite; de lo contrario, usa [EXCESO].  
- Datos: “El comité anunció nuevas directrices para la presentación de proyectos de investigación, con énfasis en transparencia de datos y reproducibilidad.”  
- Respuesta esperada: “El comité publicó directrices para propuestas de investigación, priorizando transparencia de datos y reproducibilidad. [OK]”

### Nota de uso
- Mantener campos estables (“Tarea”, “Datos”, “Respuesta esperada”) facilita el entrenamiento supervisado y las evaluaciones automáticas.  
- Para datasets conversacionales, se puede mapear “Tarea” a rol sistema/usuario, “Datos” a contenido del usuario y “Respuesta esperada” al contenido del asistente, preservando el formato requerido por el modelo.

## Ejemplos extras

¡Excelente! Aquí tienes más ejemplos de **prompts de instrucción tuning** y **plantillas** en español, organizados por tipo de tarea y con variaciones útiles para datasets de entrenamiento. Incluyo también ejemplos para contextos conversacionales y tareas más complejas.

---

## **1. Plantillas para Tareas Específicas**

### **Clasificación Avanzada**
- **Tarea:** Clasifica el texto según la intención del usuario: “consulta”, “queja”, “solicitud de información”, “elogio”.
- **Datos:** “No entiendo por qué mi pedido aún no ha llegado. Llevan dos semanas de retraso.”
- **Respuesta esperada:** queja

### **Extracción con Relaciones**
- **Tarea:** Extrae las relaciones entre personas y organizaciones en formato JSON, usando las claves “persona”, “rol”, “organización”.
- **Datos:** “Ana López fue nombrada directora de Innovación en GreenTech el mes pasado.”
- **Respuesta esperada:**
  ```json
  {"relaciones": [{"persona": "Ana López", "rol": "directora de Innovación", "organización": "GreenTech"}]}
  ```

### **Generación Condicional**
- **Tarea:** Genera una respuesta de correo electrónico formal si el tono del mensaje original es “urgente”; de lo contrario, usa un tono neutral.
- **Datos:** “Necesito que me envíes el informe antes de las 3 pm hoy, es crítico para la reunión.”
- **Respuesta esperada:**
  ```
  Estimado/a [Nombre],
  He recibido su solicitud y le confirmo que el informe estará en su bandeja antes de las 3 pm.
  Quedo atento/a a cualquier otra necesidad urgente.
  Saludos cordiales,
  [Firma]
  ```

---

## **2. Plantillas para Datasets Conversacionales**

### **Diálogo con Roles**
- **Tarea:** Simula una conversación entre un usuario y un asistente virtual. El asistente debe responder con empatía y ofrecer soluciones prácticas.
- **Datos:**
  - **Usuario:** “Mi tarjeta de crédito no funciona en el extranjero, ¿qué hago?”
  - **Asistente:** “Lamento escuchar eso. ¿Podría confirmarme si activó la opción de uso internacional en su cuenta? Si no, puedo guiarle para hacerlo ahora mismo.”

### **Respuesta con Validación**
- **Tarea:** Responde a la pregunta del usuario y valida si la respuesta cumple con las políticas de la empresa (ejemplo: no prometer plazos no confirmados).
- **Datos:** “¿Cuándo llegará mi paquete?”
- **Respuesta esperada:** “Según el seguimiento, su paquete está en tránsito y la fecha estimada de entrega es el 10 de octubre. [Cumple políticas]”

---

## **3. Plantillas para Tareas Creativas**

### **Generación de Contenido con Restricciones**
- **Tarea:** Escribe un post para redes sociales promocionando un producto, usando ≤140 caracteres y incluyendo un emoji.
- **Datos:** “Nuevo lanzamiento: auriculares inalámbricos con cancelación de ruido.”
- **Respuesta esperada:** “🎧 ¡Escucha solo lo que quieres! Nuevos auriculares inalámbricos con cancelación de ruido. ¡Disponibles ya! #SonidoPerfecto”

### **Transformación de Estilo**
- **Tarea:** Convierte el texto formal a un estilo coloquial, manteniendo la información clave.
- **Datos:** “Se les informa que la reunión programada para el día de mañana ha sido pospuesta hasta nuevo aviso.”
- **Respuesta esperada:** “Oye, la reunión de mañana se movió, te aviso cuando sepamos la nueva fecha.”

---

## **4. Plantillas para Evaluación Automática**

### **Respuesta con Métricas**
- **Tarea:** Responde la pregunta y asigna una puntuación de claridad (1-5) y relevancia (1-5) a tu respuesta.
- **Datos:** “¿Cómo puedo resetear la contraseña de mi cuenta?”
- **Respuesta esperada:**
  ```
  Para resetear su contraseña, vaya a 'Iniciar sesión', haga clic en '¿Olvidó su contraseña?' e ingrese su correo electrónico. Recibirá un enlace para crear una nueva.
  Claridad: 5
  Relevancia: 5
  ```

### **Comparación de Respuestas**
- **Tarea:** Genera dos respuestas posibles a la misma pregunta y selecciona la mejor según los criterios: claridad, empatía y precisión.
- **Datos:** “Mi vuelo fue cancelado, ¿qué opciones tengo?”
- **Respuesta esperada:**
  - **Opción A:** “Lamentamos la cancelación. Puede solicitar un reembolso o reprogramar su vuelo sin costo.”
  - **Opción B:** “Entendemos su frustración. Le ofrecemos reembolso total o reprogramación prioritaria. ¿Prefiere que le ayudemos con alguna de estas opciones?”
  - **Selección:** Opción B (mejor empatía y claridad)

---

## **5. Plantillas para Tareas Multilingües**

### **Traducción con Adaptación Cultural**
- **Tarea:** Traduce el texto al español (España) y adapta las referencias culturales si es necesario.
- **Datos:** “Please bring a dish to pass for the potluck at the office.”
- **Respuesta esperada:** “Por favor, trae un plato para compartir en la comida colectiva de la oficina.”

---

## **Notas Clave**
- **Consistencia:** Usar siempre los mismos campos (“Tarea”, “Datos”, “Respuesta esperada”) facilita el entrenamiento y la evaluación.
- **Variedad:** Incluir ejemplos con errores comunes (ej: respuestas fuera de formato) ayuda a robustecer el modelo.
- **Contexto:** Para tareas conversacionales, añadir el historial de la conversación como parte de “Datos” mejora la coherencia.



