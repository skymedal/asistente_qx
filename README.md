# Asistente de Quirófano

Prueba de concepto de un chatbot RAG que responde preguntas sobre técnicas quirúrgicas de prótesis de rodilla usando solo los manuales cargados, cita la sección de origen y rechaza todo lo que no está en ellos.

Trabajo de Fin de Máster en Inteligencia Artificial (IAcademia).

## Arquitectura

1. **Pregunta** del usuario en el chat (Dify).
2. **Recuperación**: embeddings `gemini-embedding-001`, búsqueda vectorial, Top K 4.
3. **Control de relevancia**: nodo SI/SINO; si ningún fragmento supera el umbral de 0,70, devuelve el mensaje de rechazo sin llamar al modelo.
4. **Generación**: `gpt-oss-120b` (Groq) con un prompt restrictivo que obliga a usar solo el contexto, no mezclar sistemas y citar documento y sección.

Mensaje de rechazo, idéntico en ambas barreras: *Esta consulta no está cubierta por los protocolos disponibles.*

## Calibración del umbral

| Pregunta | Tipo | Puntuación |
|---|---|---|
| Corte distal en la rodilla ACS | Cubierta | 0,83 |
| Dosis de cefazolina en profilaxis | Mismo ámbito, sin cobertura | 0,65 |
| ¿Quién ganó la Liga? | Ajena | 0,55 |

## Herramientas (coste cero)

Dify Cloud (Sandbox) · Google Gemini (embeddings) · Groq (LLM) · GitHub Pages.

## Aviso

Prueba de concepto académica. No es un producto sanitario ni sustituye al manual del fabricante, a los protocolos del centro ni al criterio del equipo quirúrgico. Los manuales usados son material técnico de los fabricantes, empleado con fines exclusivamente académicos y no incluido en este repositorio.
