| Modelo                                                         | Tipo de Prompt  | Precisión de la información | Tono de respuesta                  | Manejo de preguntas fuera del contexto | Presencia de alucinaciones | Observaciones                                                                                                                                                                                                    |
| -------------------------------------------------------------- | --------------- | --------------------------- | ---------------------------------- | -------------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Gemini Pro](https://gemini.google.com?utm_source=chatgpt.com) | Base            | Media                       | Informativo y explicativo          | Regular                                | Media                      | Respondió con buena cobertura general de carreras y modalidades, pero confundió conceptos como modalidades y tecnologías. Incorporó información posiblemente desactualizada y omitió algunas carreras oficiales. |
| [Claude Sonnet 4.6](https://claude.ai?utm_source=chatgpt.com)  | Base            | Alta                        | Formal y estructurado              | Bueno                                  | Baja                       | Presentó respuestas organizadas y coherentes con la estructura institucional de la UTPL. Agregó algunos datos temporales y cuantitativos que podrían variar según el periodo académico.                          |
| [Grok Fast](https://grok.com?utm_source=chatgpt.com)           | Base            | Media-Alta                  | Conversacional y descriptivo       | Regular                                | Media                      | Mostró buena cobertura general, pero utilizó cifras aproximadas e incorporó información adicional no verificada dentro del alcance del proyecto.                                                                 |
| [Gemini Pro](https://gemini.google.com?utm_source=chatgpt.com) | Contextualizado | Alta                        | Claro y académico                  | Bueno                                  | Baja                       | Utilizó correctamente la información proporcionada en la base de conocimiento. Presentó pequeños problemas de interpretación del contexto y respuestas algo resumidas.                                           |
| [Claude Sonnet 4.6](https://claude.ai?utm_source=chatgpt.com)  | Contextualizado | Muy alta                    | Profesional y preciso              | Muy bueno                              | Muy baja                   | Fue el modelo más alineado al contexto proporcionado. Usó únicamente la información entregada y mantuvo coherencia en toda la respuesta.                                                                         |
| [Grok Fast](https://grok.com?utm_source=chatgpt.com)           | Contextualizado | Media-Alta                  | Técnico y detallado                | Medio                                  | Media                      | Aunque aprovechó la base de conocimiento, continuó agregando datos externos como costos, enlaces y detalles no presentes en el contexto.                                                                         |
| [Gemini Pro](https://gemini.google.com?utm_source=chatgpt.com) | Con rol         | Alta                        | Institucional y formal             | Bueno                                  | Muy baja                   | Mostró mayor control y precisión. Sin embargo, sus respuestas tendieron a ser breves y poco detalladas en comparación con otros modelos.                                                                         |
| [Claude Sonnet 4.6](https://claude.ai?utm_source=chatgpt.com)  | Con rol         | Muy alta                    | Profesional, natural y orientativo | Excelente                              | Muy baja                   | Presentó el mejor desempeño general. Mantuvo el rol asignado, manejó correctamente límites del contexto y redujo significativamente las alucinaciones.                                                           |
| [Grok Fast](https://grok.com?utm_source=chatgpt.com)           | Con rol         | Alta                        | Técnico e institucional            | Bueno                                  | Baja                       | Mejoró considerablemente respecto a pruebas anteriores. Disminuyó el uso de información externa y respondió de forma más controlada.                                                                             |

## Modelos Evaluados

Se realizaron pruebas de rendimiento y precisión utilizando los siguientes modelos:

* **Gemini Pro**
* **Claude Sonnet 4.6**
* **Grok Fast**

---

## Estructura del Proyecto

El proyecto se dividió en cuatro fases principales para evaluar sistemáticamente el comportamiento de las respuestas generadas por los modelos.

### 1. Base de Conocimiento
Se creó un archivo fuente estructurado (CSV/XLSX) con información validada y curada de los programas académicos de la UTPL, abarcando:
* Carreras de grado
* Posgrados
* Educación continua

**Estructura de los datos:** Cada registro de la base contiene los siguientes campos obligatorios:
* Nombre oficial
* Tipo de programa
* Área de conocimiento
* Modalidad
* Duración
* Sedes activas
* Perfil de egreso

### 2. Fase Exploratoria
Se realizaron preguntas a los modelos **sin proporcionar contexto adicional** (Zero-shot sin RAG) con el objetivo de establecer una línea base e identificar:
* El nivel de conocimiento previo del modelo sobre la institución.
* Errores factuales.
* Información desactualizada.
* Alucinaciones en las respuestas.

### 3. Evaluación de Prompts
Para medir cómo el contexto y las instrucciones afectan la calidad de la respuesta, se probaron tres arquitecturas de prompts diferentes:

* **Prompt base:** Contiene únicamente la pregunta directa del usuario.
* **Prompt contextualizado:** Incluye fragmentos relevantes extraídos de la base de conocimiento inyectados justo antes de la pregunta.
* **Prompt con rol:** Asigna al modelo una personalidad específica (orientador académico oficial de la UTPL) y establece restricciones estrictas para que las respuestas se limiten única y exclusivamente al contexto proporcionado.

### 4. Refinamiento de Prompts
Con base en los resultados de la evaluación, se realizaron iteraciones adicionales en el diseño de los prompts para:
* Reducir la tasa de alucinaciones.
* Mejorar la precisión y fidelidad de los datos.
* Controlar el tono (hacerlo más profesional, claro y empático).
* Limitar estrictamente la inclusión de información externa no validada.

---

## Hallazgos Principales

Tras la ejecución de las pruebas y el refinamiento de los modelos, se obtuvieron las siguientes conclusiones:

1. **El contexto es clave:** La inyección de contexto (estrategia RAG) mejoró de forma drástica y significativa la precisión de todas las respuestas frente a la fase exploratoria.
2. **Efectividad del Rol:** Los "prompts con rol" que incluían restricciones explícitas demostraron ser la técnica más efectiva para mitigar y reducir las alucinaciones.
3. **Consistencia:** **Claude Sonnet 4.6** presentó el desempeño general más sólido y consistente al seguir instrucciones complejas y mantener las restricciones.
4. **Fugas de contexto:** **Grok Fast** mostró una tendencia recurrente a incorporar información externa a la base de datos (conocimiento paramétrico), incluso cuando se le proporcionaba contexto estricto.
5. **Concisión:** **Gemini Pro** generó respuestas altamente precisas, pero con una tendencia a ser más breves y directas en comparación con los otros modelos.
