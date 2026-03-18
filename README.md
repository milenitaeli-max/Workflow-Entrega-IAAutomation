# Workflow-Entrega-IAAutomation
Workflow automatizado en N8N que obtiene ofertas laborales de una fuente externa + LLM 


# Descripción
Este proyecto implementa un workflow automatizado en n8n que:

Obtiene ofertas laborales desde una fuente externa
Analiza su relevancia utilizando modelos de lenguaje (LLM)
Genera resúmenes automáticos
Envía notificaciones por email

# Objetivo
Demostrar la capacidad de:
Orquestar múltiples nodos LLM
Aplicar lógica condicional basada en IA
Automatizar procesos con n8n

# Flujo del sistema
Trigger → Fetch → Transform → Split → Clean → Store → Loop → LLM Clasificador → IF → LLM Generador → Email

# Descripción del workflow
Trigger automático: Ejecuta el flujo cada X minutos.
Obtención de datos: Se consumen ofertas desde una API/RSS.
Transformación: Conversión de XML a JSON.
Procesamiento: Separación y limpieza de datos.
Primer LLM (Clasificación) Determina si la oferta es: RELEVANTE/NO_RELEVANTE
Condicional (IF):Solo procesa ofertas relevantes.
Segundo LLM (Generación) Genera: Resumen - Motivos
Notificación: Envía email con la información procesada.

# Modelos utilizados
Groq (llama-3.1-8b-instant) para clasificación
Groq (llama-3.1-8b-instant) para generación

# Lógica condicional
resultado.status == "RELEVANTE"

# La Notificación Incluye:
Título del puesto
Empresa
Resumen generado
Link de la oferta

# Manejo de errores
Control de rate limits mediante nodo Wait
Validación de formato JSON
Uso de nodos previos ($node) para preservar datos

# Cómo ejecutar
Importar workflow/workflow.json en n8n
Configurar credenciales:
API Key de Groq
Email (SMTP/Gmail)

Ejecutar workflow
