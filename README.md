# 🐍 LangChain: Fundamentos para la Construcción de Aplicaciones con LLM

Este repositorio contiene una serie de cuadernos Jupyter que exploran los **bloques de construcción fundamentales** para crear aplicaciones robustas y modulares con Large Language Models (**LLMs**) utilizando la librería **LangChain** y la API de **OpenAI**.

## 🎯 Objetivos del Proyecto

El objetivo principal es pasar de las llamadas directas a la API de OpenAI a un enfoque estructurado y modular, aprendiendo a gestionar el **contexto** (Memoria), el **flujo** (Cadenas) y la **estructura de datos** (Parsers).

---

## ⚙️ Estructura del Repositorio y Conceptos Clave

| Cuaderno | Conceptos Cubiertos | Enfoque Principal |
| :--- | :--- | :--- |
| `L1-Model_prompt_parser.ipynb` | Modelos, Prompts y Parsers de Salida | **Estructuración de la Entrada y Salida (I/O).** |
| `L2-Memory.ipynb` | Tipos de Memoria | **Persistencia del Contexto Conversacional.** |
| `L3-Chains.ipynb` | Tipos de Cadenas (*Chains*) | **Automatización de Flujos de Trabajo Inteligentes.** |

---

## 1. 📝 Módulo de I/O: Modelos, Prompts y Parsers (L1)

Este módulo cubre la preparación de la entrada para el LLM y la interpretación de su salida.

| Componente | Función Técnica | Propósito Sencillo |
| :--- | :--- | :--- |
| **Prompts** | Clase `ChatPromptTemplate`. Define plantillas con *placeholders* (`{variable}`) para crear instrucciones reutilizables. | Separar la **instrucción fija** (la tarea) de las **entradas variables** (el texto del usuario, el estilo). |
| **Output Parsers** | Clases `ResponseSchema` y `StructuredOutputParser`. Fuerza al LLM a generar una salida en formato **JSON** y la convierte en un objeto usable de Python (`dict`). | Tomar la respuesta del robot (que es texto) y convertirla en una **estructura de datos** fácil de manipular. |
| **Modelos (LLMs)** | Clase `ChatOpenAI`. Es la interfaz estándar de LangChain para interactuar con los modelos de chat. | El "control remoto" para enviar y recibir datos del robot inteligente. |

---

## 2. 🧠 Módulo de Memoria (L2)

Este módulo se enfoca en dotar a los *chatbots* de **contexto**, resolviendo el problema de que los LLMs son inherentemente "sin estado" (*stateless*).

| Tipo de Memoria | Función Principal | Control de Longitud |
| :--- | :--- | :--- |
| **`ConversationBufferMemory`** | Almacena el **historial completo**. | **Ninguno.** El historial crece indefinidamente. |
| **`ConversationTokenBufferMemory`** | Limita el historial según el **número total de *tokens*** consumidos. | **Estricto por Costo/Tamaño.** Recorta mensajes antiguos para ajustarse al límite. |
| **`ConversationSummaryBufferMemory`** | **Resume** las partes más antiguas de la conversación (usando el LLM) y mantiene explícitas las interacciones recientes. | **Inteligente.** Mantiene el contexto relevante y el resumen informativo. |

---

## 3. ⛓️ Módulo de Cadenas (*Chains*) (L3)

El módulo de Cadenas cubre la automatización de flujos de trabajo al permitir enlazar múltiples operaciones con LLMs. 

| Tipo de Cadena | Función Principal | Control de Flujo |
| :--- | :--- | :--- |
| **`LLMChain`** | La cadena más básica. Combina un LLM con una plantilla de prompt para una **tarea única**. | Directo. |
| **`SequentialChain`** | Permite **flujos de trabajo complejos** donde se combinan subcadenas con múltiples entradas y salidas. | Secuencial (Múltiples entradas/salidas). |
| **`RouterChain`** | Utiliza un **Agente LLM** para analizar la entrada y **decidir a qué subcadena especializada** debe enrutar la petición. | **Decisión Inteligente.** (Ej., enrutar preguntas de Física a la cadena de Física). |

## 4. 📚 Módulo de QA sobre Documentos (RAG) (L4)

Este módulo es fundamental para construir sistemas de **Preguntas y Respuestas sobre datos propios** (RAG: *Retrieval-Augmented Generation*), superando el límite de contexto de los LLMs.

* **Embeddings:** Se introducen las **representaciones numéricas** (vectores) de texto que capturan el significado semántico.
* **Vector Stores:** Se utiliza la base de datos vectorial (`DocArrayInMemorySearch`) para **indexar** y **almacenar** los *embeddings* de los documentos.
* **Recuperación:** La cadena **`RetrievalQA`** combina el LLM con el **Recuperador** (`Retriever`) para buscar los fragmentos de documentos más relevantes a la consulta y solo pasar ese contexto al modelo.
* **Tipos de Cadena QA:** Se exploran estrategias para manejar grandes volúmenes de documentos, como **`stuff`**, **`map_reduce`**, y **`refine`**.

---

## 5. 🔬 Módulo de Evaluación (L5)

Este módulo se enfoca en la calidad y el mantenimiento de las aplicaciones de LLM.

* **Debugging (Depuración):** Se utiliza la opción **`verbose=True`** en las cadenas para inspeccionar el flujo de ejecución (el *prompt* enviado y los documentos recuperados) y diagnosticar problemas (ej. la recuperación falló o la generación fue incorrecta).
* **Generación de Ejemplos:** Se muestra cómo utilizar un LLM para crear automáticamente conjuntos de datos de evaluación (pares de **pregunta**, **respuesta ideal** y **contexto**).
* **Evaluación Asistida por LLM:** Se usa un **segundo LLM como juez** para calificar automáticamente la respuesta generada por la cadena de prueba contra la respuesta ideal, midiendo la **Corrección** y la **Fidelidad**.

---
## 6. 🤖 Módulo de Agentes (*Agents*) (L6)

Este módulo es la cúspide de la construcción con LangChain, presentando el LLM no como una herramienta de respuesta, sino como un **Motor de Razonamiento** capaz de decidir qué acciones tomar y qué herramientas utilizar para resolver tareas complejas de forma dinámica.

| Componente | Función Principal | Rol en el Flujo de Trabajo |
| :--- | :--- | :--- |
| **Agente (LLM)** | Actúa como el controlador principal y el motor de toma de decisiones. | **Piensa** (*Thought*), **actúa** (*Action*), y **observa** (*Observation*). |
| **Herramientas (*Tools*)** | Interfaces específicas para interactuar con datos externos (Web, bases de datos, código). | Proporcionan información fuera del conocimiento interno del LLM. |
| **Tipo ReAct** | **`CHAT_ZERO_SHOT_REACT_DESCRIPTION`** | Es la estrategia de *prompting* que obliga al Agente a razonar antes de actuar. |
| **Herramientas Personalizadas** | Funciones de Python decoradas con `@tool`. | Permite conectar el Agente a API, bases de datos o código local. |

### Flujo de Razonamiento (Ciclo ReAct)

El Agente resuelve las consultas iterativamente a través de un ciclo de tres pasos:

1.  **Pensamiento (`Thought`):** El Agente determina la mejor estrategia o la información que necesita.
2.  **Acción (`Action`):** El Agente selecciona la herramienta más adecuada (ej. DuckDuckGo, Wikipedia o una función personalizada).
3.  **Observación (`Observation`):** El resultado de la herramienta se devuelve al Agente, que lo utiliza como nuevo contexto para su siguiente pensamiento.
