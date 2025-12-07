# 🐍 LangChain: Modelos, Prompts y Parsers de Salida

Este proyecto es un cuaderno interactivo de Jupyter (`L1-Model_prompt_parser.ipynb`) que explora los componentes fundamentales para construir aplicaciones con Large Language Models (LLMs) utilizando la librería **LangChain** y la API de **OpenAI**.

## 🎯 Objetivos del Proyecto

El objetivo principal es demostrar cómo gestionar y estructurar las interacciones con un LLM.

1.  **Llamadas a API:** Mostrar las llamadas directas a la API de OpenAI.
2.  **Modularidad con LangChain:** Introducir las clases de LangChain para la gestión de:
    * **Modelos:** Configuración del LLM (`ChatOpenAI`).
    * **Prompts:** Uso de plantillas (`ChatPromptTemplate`) para crear instrucciones reutilizables.
    * **Output Parsers:** Extracción de datos estructurados (JSON) desde la salida de texto del LLM, convirtiéndolos en diccionarios de Python (`StructuredOutputParser`).

## ⚙️ Estructura y Componentes Clave

| Componente | Descripción |
| :--- | :--- |
| **`L1-Model_prompt_parser.ipynb`** | El cuaderno principal que contiene todo el código y las explicaciones. |
| **`dotenv`** | Utilizado para cargar la clave de la API de OpenAI de forma segura desde un archivo `.env`. |
| **`get_completion()`** | Una función simple para realizar llamadas directas a la API de OpenAI (sin LangChain). |
| **`ChatPromptTemplate`** | Clase clave de LangChain para definir mensajes y variables en el prompt. |
| **`StructuredOutputParser`** | Clase esencial para definir un esquema de salida (JSON) y convertir la respuesta de texto del LLM en un objeto de Python usable (`dict`). |
# 🐍 LangChain: Fundamentos para la Construcción de Aplicaciones con LLM

Este repositorio contiene una serie de cuadernos Jupyter que exploran los componentes fundamentales para construir aplicaciones robustas con Large Language Models (**LLMs**) utilizando la librería **LangChain** y la API de **OpenAI**.

## 🎯 Objetivos del Proyecto

El objetivo principal es pasar de las llamadas directas a la API de OpenAI a un enfoque estructurado y modular ofrecido por LangChain.

## ⚙️ Estructura del Repositorio

| Cuaderno | Conceptos Cubiertos | Enfoque Principal |
| :--- | :--- | :--- |
| `L1-Model_prompt_parser.ipynb` | Modelos, Prompts y Parsers de Salida | **Estructuración de la Entrada y Salida.** |
| `L2-Memory.ipynb` | Tipos de Memoria | **Persistencia del Contexto Conversacional.** |

---

## 1. 📝 Módulo de Modelos, Prompts y Parsers (L1)

Este módulo cubre la preparación de la entrada para el LLM y la interpretación de su salida.

| Componente | Función Técnica | Propósito Sencillo |
| :--- | :--- | :--- |
| **Modelos (LLMs)** | Clase `ChatOpenAI`. Es la interfaz estándar de LangChain para interactuar con los modelos de chat (ej., gpt-3.5). | El "control remoto" para enviar y recibir datos del robot inteligente. |
| **Prompts** | Clase `ChatPromptTemplate`. Define plantillas con *placeholders* (`{variable}`) para crear instrucciones reutilizables. | Separar la **instrucción fija** (la tarea) de las **entradas variables** (el texto del usuario, el estilo). |
| **Output Parsers** | Clases `ResponseSchema` y `StructuredOutputParser`. Fuerza al LLM a generar una salida en un formato específico (típicamente JSON) y la convierte en un objeto usable de Python (`dict`). | Tomar la respuesta del robot (que siempre es texto) y convertirla en una **estructura de datos** fácil de manipular. |

---

## 2. 🧠 Módulo de Memoria (L2)

Este módulo se enfoca en dotar a los *chatbots* de **contexto** para conversaciones coherentes, resolviendo el problema de que los LLMs son inherentemente "sin estado" (*stateless*).

| Tipo de Memoria | Función Principal | Control de Longitud |
| :--- | :--- | :--- |
| **`ConversationBufferMemory`** | Almacena el **historial completo** de la conversación. | **Ninguno.** El historial crece indefinidamente, afectando costo y velocidad. |
| **`ConversationBufferWindowMemory`** | Limita el historial, reteniendo solo los **últimos *k*** intercambios conversacionales (la "ventana"). | **Estricto por Intercambio (k).** Garantiza que solo el contexto más reciente se envíe al modelo. |
| **`ConversationTokenBufferMemory`** | Limita el historial según el **número total de *tokens*** consumidos. | **Estricto por Costo/Tamaño.** Ideal para controlar directamente el presupuesto de la API. |
| **`ConversationSummaryBufferMemory`** | **Resume** las partes más antiguas de la conversación (usando el LLM) y mantiene explícitas las interacciones recientes. | **Inteligente.** Mantiene el contexto relevante y el resumen informativo, evitando límites de *tokens*. |

---

## 🚀 Cómo Empezar

1.  **Clonar el repositorio.**
2.  **Configurar el Entorno:** Instala las librerías necesarias (mencionar `langchain`, `openai`, `python-dotenv`).
3.  **Configurar la Clave de API:** Crea un archivo `.env` en la raíz del proyecto para almacenar tu clave de OpenAI (`OPENAI_API_KEY="sk-xxxxxxxx"`).
4.  **Ejecutar los Cuadernos:** Abre los archivos `.ipynb` con Jupyter y ejecuta las celdas secuencialmente.
