# 7.3 Validation Interviews

## 7.3.1. Diseño de entrevistas

Objetivo
- Validar las hipótesis de Lean UX relacionadas con la protección del activo (vino), la usabilidad del registro de inventario y la percepción de valor del reporte de rotación.

Alcance
- Sesiones dirigidas a los segmentos objetivo definidos en Capítulo I: (1) Dueños/administradores de restaurantes y cavas comerciales y (2) Coleccionistas / aficionados.
- Para cada segmento se planifican entre 3 y 5 entrevistas (rúbrica del curso).

Criterios de selección de entrevistados
- Representantes del segmento (propietario/administrador de cava, sommelier, coleccionista privado).
- Diversidad de tamaño de cava, nivel técnico y frecuencia de uso.


Instrumento: Guía de pruebas de prototipo (tareas y preguntas asociadas)

Instrucciones al moderador
- Indicar al participante que usará un prototipo interactivo (modo think-aloud: piense en voz alta).
- Registrar tiempos, errores, dudas y pedir que califique cada tarea al final (1–5).

Tareas (pedir al participante realizarlas en el prototipo)
1) Onboarding / primer acceso
	- Tarea: Abrir la app por primera vez e identificar cómo añadir una cava o perfil.
	- Métricas: tiempo hasta completar, pasos realizados, puntos de confusión.
	- Preguntas post-tarea: ¿Fue claro el primer paso? ¿Qué cambiaría?

2) Vincular sensor IoT (simular pairing)
	- Tarea: Vincular un sensor a la app y configurar umbrales básicos de temperatura.
	- Métricas: éxito/fracaso, tiempo, errores de mapeo de opciones.
	- Preguntas: ¿Qué tan confiable le parece la secuencia de vinculación? ¿Qué parte le resultó confusa?

3) Añadir botellas (foto/escaneo)
	- Tarea: Registrar 2 botellas nuevas usando foto o escaneo; completar datos mínimos (nombre, añada, ubicación).
	- Métricas: tiempo por botella, campos omitidos, tasa de éxito en escaneo automático.
	- Preguntas: ¿Fue rápido el proceso? ¿Qué campo fue innecesario o faltó?

4) Responder a una alerta (flujo de notificación)
	- Tarea: Recibir una notificación (simulada) de temperatura fuera de rango y ejecutar la acción recomendada (ej. silenciar, ver historial, llamar a soporte).
	- Métricas: tiempo hasta acción, acción elegida, dudas.
	- Preguntas: ¿Le parece útil la recomendación? ¿Qué otra acción esperaría ver?

5) Consultar historial térmico y reportes de rotación
	- Tarea: Abrir el panel de trazabilidad térmica y ubicar botellas con baja rotación o próximas a su ventana óptima.
	- Métricas: tiempo hasta identificar 3 botellas de interés, comprensión de gráficos.
	- Preguntas: ¿Los gráficos son entendibles? ¿Qué leyenda o ayuda le haría falta?

6) Registrar salida/venta (descorche)
	- Tarea: Registrar la salida de una botella y verificar que el stock se actualiza.
	- Métricas: éxito, pasos necesarios, errores de confirmación.
	- Preguntas: ¿El flujo es rápido y seguro? ¿Qué le haría confiar más en el registro?

Al ser un prototipo las Preguntas generales de validación del prototipo son para ambos segmentos (al final)


#### PREGUNTAS PARA EL SEGMENTO 1: Coleccionistas / aficionados.

- ¿Cuál consideras que es el objetivo principal de esta plataforma?
- ¿es fácil navegar por las pantallas?
- ¿Hubo alguna parte que te confundiera?
- ¿Las funciones presentadas cumplen con lo que esperabas?
- ¿Este sistema resolvería un problema real para ti?
- ¿Qué mejoras sugerirías antes del desarrollo final?
- ¿Qué característica le aportó mayor valor inmediato?
- ¿crees que sera optimo para personas de personas en la industria?


#### PREGUNTAS PARA EL SEGMENTO 2: Dueños/administradores de restaurantes y cavas comerciales

- ¿Cuál consideras que es el objetivo principal de esta plataforma?
- ¿es fácil navegar por las pantallas?
- ¿Hubo alguna parte que te confundiera?
- ¿Las funciones presentadas cumplen con lo que esperabas?
- ¿Este sistema resolvería un problema real para ti?
- ¿Qué mejoras sugerirías antes del desarrollo final?
- ¿Qué característica le aportó mayor valor inmediato?
- ¿crees que sera optimo para personas de personas en la industria?


## 7.3.2. Plantilla de resumen de entrevista (a incluir en el informe)

- Entrevista ID:
- Participante (Nombre / Edad / Distrito / Rol):
- Segmento objetivo:
- Fecha / Hora:
- Duración:
- Extracto de la transcripción (máx. 10 líneas con las respuestas más relevantes):
- Datos demográficos y tecnológicos (dispositivo, navegador, nivel técnico):
- Principales hallazgos (bullets):
	- Necesidades explícitas:
	- Frustraciones clave:
	- Comportamientos observados:
	- Citas relevantes (textuales):
- Implicaciones para el producto (qué asumir, qué priorizar):
- Evidencia (screenshot, enlace a video con timestamps):

## 7.3.3. Evaluaciones según heurísticas (plantilla)

Instrucciones breves
- Realizar la evaluación después de la sesión de validación o revisando la grabación de la interacción con el Landing Page / prototipo.
- Aplicar heurísticas de usabilidad (Nielsen), arquitectura de información y diseño inclusivo.
- Para cada hallazgo anotar severidad según la rúbrica (1–4) y recomendación.

Heurísticas mínimas a evaluar
- Visibilidad del estado del sistema
- Relación entre el sistema y el mundo real
- Libertad y control del usuario
- Consistencia y estándares
- Prevención de errores
- Reconocimiento antes que recuerdo
- Flexibilidad y eficiencia de uso
- Estética y diseño minimalista
- Ayuda y documentación
- Accesibilidad e inclusive design
- Arquitectura de información: encontrabilidad y etiquetas

Formato: Evaluación heurística (tabla)

| # | Problema detectado | Severidad (1-4) | Heurística violada | Evidencia (captura / timestamp) | Recomendación |
|---|---|---:|---|---|---|
| 1 | | | | | |
| 2 | | | | | |

Descripción detallada de un hallazgo (ejemplo)
- Problema: [resumen corto]
- Severidad: 3
- Heurística: Libertad y control del usuario
- Detalle: [descripción completa del problema observada en la sesión o video]
- Evidencia: [archivo imagen / enlace y timestamp]
- Recomendación: [acción propuesta priorizada]

Escala de severidad (según rúbrica)
- 1 Problema superficial
- 2 Problema menor
- 3 Problema mayor
- 4 Problema muy grave (impide la tarea)

Checklist rápida para la auditoría heurística
- [ ] Capturas con contexto y timestamps incluidos
- [ ] Severidad asignada y justificada
- [ ] Recomendación práctica y priorizada
- [ ] Relación con métricas/KPIs del experimento (si aplica)
- [ ] Inclusión de remediaciones rápidas (quick wins)

