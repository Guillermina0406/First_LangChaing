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
