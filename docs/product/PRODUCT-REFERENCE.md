# K9 Behavioral Architect — Product Reference Documentation

**Versión:** 1.0  
**Corte de información:** 22 de agosto de 2026  
**Ámbito:** producto construido y estado de lanzamiento; no sustituye asesoramiento jurídico, veterinario ni clínico.

## 1. Resumen ejecutivo

K9 Behavioral Architect es una plataforma web y de arquitectura móvil para diseñar, ejecutar, seguir y documentar programas individualizados de modificación de conducta canina. Combina un motor de planificación basado en principios de análisis aplicado de conducta, seguimiento estructurado de sesiones, recuperación sobre un corpus especializado y una experiencia conectada para dueños y profesionales.

El producto no se limita a recomendar contenido. Su bucle central es:

```text
describir el caso → formular una hipótesis funcional → construir un plan por pasos
→ ejecutar y reportar una sesión → decidir el siguiente ajuste → conservar el historial
```

En la experiencia profesional, ese bucle se amplía:

```text
caso → plan revisable → práctica reportada por el dueño → señal de atención → informe
```

La propuesta de valor es distinta para cada audiencia:

- **Dueño:** claridad diaria, progresión adaptativa y límites de seguridad sin tener que interpretar teoría conductual.
- **Profesional:** estructura, seguimiento entre citas, trazabilidad e informes sin ceder su criterio a la IA.

## 2. Problema que resuelve

### Para dueños

Los recursos convencionales suelen entregar vídeos, artículos o consejos aislados. El dueño todavía tiene que decidir qué aplica a su perro, cuánto exigir, cuándo avanzar y qué hacer cuando hay un retroceso. K9 convierte esa incertidumbre en un programa secuencial y un siguiente paso visible.

### Para profesionales

La información de un caso suele fragmentarse entre agenda, mensajes, notas, audios y memoria. Además, el trabajo que realiza el dueño entre citas es difícil de observar. K9 conecta el expediente, el plan, los reportes en casa, las señales de atención y el informe final.

## 3. Principios de producto

1. **Bienestar por encima de métricas.** Un porcentaje alto de éxito no permite avanzar si hay señales de estrés relevantes.
2. **Una dificultad cada vez.** Distancia, duración y distracción no aumentan simultáneamente.
3. **Decisiones observables.** El avance se basa en resultados registrados, no solo en impresión subjetiva.
4. **El profesional conserva el criterio.** La IA estructura y documenta; el profesional revisa, ajusta dentro de límites y decide cómo usar la información.
5. **Consentimiento explícito.** La vinculación entre dueño y profesional requiere invitación aceptada o solicitud mediante código aprobada.
6. **Los datos no se convierten en rehén.** Una cuenta sin suscripción activa entra en modo lectura en vez de perder el historial.
7. **La documentación alimenta el producto.** Reportar una sesión no es una tarea administrativa periférica: es el dato que hace progresar el plan.

## 4. Audiencias y roles

| Rol | Objetivo | Superficie principal | Autoridad |
|---|---|---|---|
| Dueño | Trabajar con su perro y entender qué hacer hoy | Hoy, Planes, nuevo plan, sesión, Consulta IA, Biblioteca, Perfil | Propietario de sus perros, planes y sesiones. |
| Profesional | Gestionar clientes y casos, supervisar trabajo y documentarlo | Panel, Agenda, Clientes, Casos, Consulta IA, Biblioteca, Informes, Ajustes | Acceso a datos de clientes vinculados y escrituras expresamente autorizadas. |
| Servicios backend | Ejecutar reglas, IA, facturación y persistencia | Supabase Edge Functions y funciones SQL | Autoridad técnica bajo autenticación, RLS y validaciones del servidor. |

No existe en la interfaz actual un rol operativo completo de administrador de estudio con gestión real de varios asientos. Que el plan Estudio tenga un número configurado de asientos no equivale a disponer de esa experiencia.

## 5. Capacidades comunes

### 5.1 Cuenta y acceso

- Registro con elección explícita de cuenta de dueño o profesional.
- Autenticación y sesión mediante Supabase Auth.
- Separación de shells y navegación por rol.
- Suscripción, prueba, modo lectura y cuenta exenta gestionados por entitlements del servidor.
- Acceso a checkout y portal de facturación de Stripe.

El checkout tiene evidencia real para una compra Pro. El portal de facturación dispone de integración en código, pero necesita configuración activa en Stripe antes de considerarse operativo.

El acceso implementado es mediante correo electrónico y contraseña. Los métodos de Google y Apple todavía no tienen implementación funcional. Además, la apertura de Stripe Checkout está habilitada en web y desactivada deliberadamente en el cliente nativo actual.

### 5.2 Motor de planes

El motor ejecuta una cadena de responsabilidades diferenciadas:

1. **Interaction Agent:** convierte la descripción informal en una observación conductual estructurada y solicita información adicional cuando falta.
2. **Assessment Agent:** formula la hipótesis funcional y decide si el caso puede continuar, necesita observación o exige derivación.
3. **Shaping Planner y Step Builder:** diseñan la estructura y los pasos del programa.
4. **Validación pedagógica determinista:** comprueba reglas que no deben depender de la variabilidad de un modelo.
5. **Juez pedagógico:** revisa reglas clínicas adicionales.
6. **Welfare Reviewer:** revisa el plan final y puede vetarlo.

El sistema consulta el corpus especializado mediante RAG. El fallo de recuperación está diseñado como *fail-soft*: puede quedar registrado y permitir que el pipeline continúe. Por ello no debe afirmarse que todos los planes están necesariamente sustentados por fragmentos recuperados en cada ejecución sin consultar la telemetría del plan concreto.

### 5.3 Progresión tras cada sesión

La regla implementada aplica estas decisiones:

| Condición | Decisión habitual |
|---|---|
| Éxito superior al 80 %, sin estrés | Avanzar. |
| Éxito entre 50 % y 80 % | Repetir para consolidar. |
| Menos del 50 % con una dificultad excesiva identificable | Reducir una dimensión. |
| Menos del 50 % sin esa señal | Dividir el paso. |
| Tres sesiones con varianza mínima | Cambiar estrategia o escalar según el resultado. |
| Estrés con éxito alto | No avanzar. |
| Agresión con daño, posible dolor/problema médico o estrés incapacitante | Pausar y derivar. |

El umbral técnico de avance es `successRate > 0.8`, no `>= 0.8`. En copy público conviene decir “por encima del 80 %” o “regla del 80 %”, evitando una precisión matemática incorrecta.

### 5.4 Consulta IA

Consulta IA es un motor separado de la generación de planes:

- Permite una consulta general o un hilo anclado explícitamente a un perro/caso.
- Un anclaje puede incorporar plan activo y sesiones recientes.
- Responde a partir del corpus especializado, no debería completar con conocimiento general cuando la recuperación no basta.
- Admite repreguntas con memoria corta y un límite de turnos.
- Muestra fuentes disponibles y puede recomendar lecturas de la Biblioteca.
- La redacción cambia por perfil: una dirección clara para el dueño; respuesta atribuida y desacuerdos visibles para el profesional.
- Una bandera roja en el texto detiene la respuesta y deriva.
- No modifica el expediente, el plan ni la progresión.
- Su cupo se cuenta por hilo y es independiente del cupo de generaciones de plan.

Consulta IA está implementada en el repositorio para ambos roles. Su disponibilidad en producción debe verificarse antes de presentarla como funcionalidad ya desplegada.

### 5.5 Voz

- La aplicación web implementa entrada y salida mediante Web Speech API en navegadores compatibles.
- El dictado puede limpiarse y ordenarse mediante una Edge Function con Gemini.
- El audio no se guarda como archivo en el esquema descrito.
- La implementación nativa prevista con APIs de iOS/Android no está presente en las dependencias actuales. Por tanto, “dictado en toda la app móvil” no debe prometerse hasta construirlo y verificarlo en dispositivo.

### 5.6 Biblioteca

- Biblioteca educativa pública con taxonomía, categorías, etiquetas y niveles.
- Contenido en español e inglés cuando existe versión traducida.
- Parte del catálogo se publica como HTML estático y la aplicación consulta `library_docs`.
- Consulta IA puede recomendar lecturas por categoría y etiquetas.

## 6. Experiencia del dueño

### 6.1 Inicio y alta del perro

El dueño crea su cuenta, registra datos básicos del perro y accede al área autenticada. La pantalla Hoy concentra el siguiente trabajo disponible y el estado reciente.

### 6.2 Creación de un plan

1. Selecciona o crea el perro.
2. Describe el comportamiento por escrito o, donde la plataforma lo soporte, por voz.
3. Completa preguntas de observación y posibles repreguntas del motor.
4. Ve el progreso del pipeline.
5. Recibe el plan o una indicación de observación/derivación.

### 6.3 Sesión y reporte

El dueño inicia el paso pendiente, realiza la práctica y registra resultado, intentos, duración, lugar, señales de estrés, causa de fallo y notas. El motor calcula la decisión y actualiza el plan/historial.

### 6.4 Historial

Puede consultar planes y sesiones anteriores. Los ajustes hechos por un profesional vinculado quedan diferenciados y sus notas pueden aparecer en el paso.

### 6.5 Vinculación con profesional

El dueño puede:

- aceptar una invitación enviada por el profesional; o
- introducir el código de conexión del profesional y esperar su aprobación.

La vinculación permite al profesional consultar el caso y, dentro de los permisos implementados, crear planes/sesiones y ajustar pasos autorizados. El consentimiento no se deduce ni se concede solo por conocer un código.

## 7. Experiencia profesional

### 7.1 Panel

Resume casos activos, citas del día, prácticas reportadas y casos que requieren atención. Las señales de atención incluyen estrés reciente, estancamiento y reportes con éxito bajo.

### 7.2 Clientes y casos

- Alta y edición de clientes.
- Relación entre cliente, perro, plan, sesiones y citas.
- Creación de perro/caso para un cliente vinculado.
- Revisión del resumen enviado al motor antes de generar.

### 7.3 Agenda y modo campo

- Vista semanal y citas tipadas: evaluación, entrenamiento, seguimiento y videoconsulta.
- Las citas pueden vincularse a cliente/caso.
- Completar una cita puede encadenar el reporte de sesión.
- La agenda es interna: no está sincronizada con Google Calendar y no envía invitaciones externas.

### 7.4 Ajuste profesional del plan

El profesional puede intervenir sin convertir el plan en una hoja libre:

- Ajustar variables permitidas de pasos todavía no ejecutados dentro de un rango seguro.
- Editar distancia, duración o nivel de distracción cuando esa sea la variable que trabaja el paso.
- Mantener topes por edad y reglas direccionales de seguridad en exposición.
- Añadir notas por paso, incluidas notas dictadas donde la voz esté soportada.
- Dejar auditoría de valor original, valor editado, actor y fecha.

No puede modificar libremente umbral de éxito, repeticiones ni nivel de ayuda si hacerlo rompe las invariantes del motor.

### 7.5 Seguimiento conectado

Los deberes que el cliente registra desde su cuenta aparecen en la ficha del caso profesional. El valor comercial es la trazabilidad del trabajo entre citas; no debe prometerse que la aplicación obligará al cliente a cumplir.

En el modelo actual, “deberes” no es una entidad independiente con asignación, vencimiento y recordatorios. El panel aproxima ese concepto mediante sesiones de práctica (`training`) completadas y reportadas por el dueño. En comunicación precisa conviene hablar de **prácticas o sesiones reportadas**.

### 7.6 Informes

El profesional puede generar un informe PDF a partir de los datos del caso y sus sesiones. Incluye estado, categoría, progreso, resumen del plan y narrativa por sesión. La marca actual es el **nombre del negocio en texto**. No existe carga de logotipo ni white-labeling completo.

## 8. Planes, precios y límites

| Plan | Audiencia | Precio mostrado | Perros | Casos activos | Planes/mes | Hilos de Consulta IA/mes |
|---|---|---:|---:|---:|---:|---:|
| Plus | Dueño | 7,99 €/mes o 79 €/año | 3 | No aplica | 20 | 50 |
| Pro | Profesional | 29 €/mes o 290 €/año | Ilimitados | 30 | 60 | 200 |
| Estudio | Profesional | 79 €/mes o 790 €/año | Ilimitados | Ilimitados | 150 | 500 |

Estos importes proceden de constantes de interfaz marcadas como demostración y no deben tratarse como oferta contractual por sí solos. La autoridad de cobro son los Price IDs configurados en Stripe desde el servidor; antes de publicar precios hay que confirmar catálogo, moneda, impuestos e intervalos en producción.

Reglas comunes:

- Prueba de 7 días sin tarjeta.
- Durante la prueba: 1 perro, 5 generaciones de plan y 10 hilos de Consulta IA.
- Los reportes de sesión no consumen cupo; solo se bloquean en modo lectura.
- Generaciones de plan y Consulta IA tienen contadores separados.
- Al expirar prueba/suscripción, los datos siguen visibles en modo lectura.
- `past_due` mantiene temporalmente acceso mientras Stripe reintenta y debe mostrar aviso.
- Las cuentas exentas conservan las capacidades de su perfil sin cupos.

Los hilos de Consulta IA se persisten técnicamente, pero la interfaz actual no ofrece un listado para navegar y reabrir conversaciones anteriores. Puede prometerse continuidad dentro del hilo activo, no un archivo de consultas explorable.

Los seis precios de Stripe son configuración del servidor. Se verificó un checkout Pro completo, pero no todos los planes e intervalos con compras reales. Presentar la tabla como catálogo previsto/actual requiere confirmar la configuración completa antes del lanzamiento.

## 9. Seguridad, bienestar y privacidad

### 9.1 Cortafuegos conductuales

K9 utiliza tres mecanismos distintos:

1. **Welfare Reviewer:** veta un plan generado.
2. **Guard de sesión:** pausa por incidentes explícitamente reportados.
3. **Bandera roja de Consulta IA:** clasifica el texto y deriva antes de responder.

No deben mezclarse en comunicación técnica: operan en entradas y momentos diferentes.

### 9.2 Seguridad de datos

- PostgreSQL/Supabase con Row Level Security en las tablas sensibles.
- Acceso cruzado dueño–profesional mediante políticas y funciones específicas.
- Token de sesión en SecureStore nativo o almacenamiento adaptado en web.
- Stripe firma sus webhooks; el endpoint no depende de JWT de usuario.
- Las Edge Functions desplegadas con `--no-verify-jwt` verifican identidad dentro del código cuando corresponde. Ese detalle exige mantener pruebas y revisión: el gateway no constituye por sí solo la barrera.

### 9.3 Límites de afirmación

No hay políticas legales completas enlazadas ni banner de cookies operativo en las landings. Tampoco se ha localizado una experiencia completa de eliminación de cuenta o gestión de derechos. “Cumple RGPD” no debe afirmarse como conclusión jurídica. Puede describirse la arquitectura de control de acceso y cifrado del proveedor solo con documentación técnica y revisión legal apropiada.

## 10. Diferenciación

La diferenciación defendible hoy no es una función aislada de IA. Es la unión de:

```text
plan estructurado + progresión por datos + bienestar + colaboración dueño/profesional
+ seguimiento entre citas + Consulta IA acotada + informe trazable
```

Cada pieza puede ser copiada. La profundidad está en las reglas compartidas, la trazabilidad, el corpus, el modelo de datos y la experiencia dual funcionando como un único sistema.

## 11. Modelo de negocio y efectos de red operativos

- B2C por suscripción Plus.
- B2B por suscripción Pro o Estudio.
- El profesional puede introducir al dueño mediante invitación.
- Un dueño existente puede solicitar vincularse con un profesional.
- La sincronización puede generar adquisición cruzada y aumentar coste de cambio por historial compartido.

Esto es un **bucle de distribución potencial**, no una tracción demostrada ni un efecto de red probado. No existen todavía cifras de cohortes que demuestren adquisición cruzada o retención diferencial.

## 12. Métricas que deberían gobernar el producto

- Activación del dueño: primer plan generado y primera sesión reportada.
- Activación profesional: primer cliente/caso y primer informe o reporte sincronizado.
- Retención: usuarios que continúan reportando sesiones después de la primera semana.
- Adherencia: proporción de casos vinculados con actividad en casa.
- Seguridad: derivaciones, vetos, `SAFETY_HOLD` y falsos negativos detectados.
- Calidad IA: validez estructural, calidad RAG, correcciones pedagógicas y tasa de fail-soft.
- Negocio: conversión prueba→pago, churn, ARPU, CAC y recuperación de CAC por plan.

El repositorio contiene medición de retención y evaluación RAG, pero no hay datos comerciales suficientes para presentar tracción, mejora conductual, ahorro medio o retención como resultados probados.

## 13. Glosario esencial

| Término | Definición |
|---|---|
| Caso | Unidad profesional que conecta cliente, perro, objetivo, plan y seguimiento. |
| Plan de moldeamiento | Secuencia graduada de pasos con criterios observables. |
| Sesión | Ejecución y registro de un paso del plan. |
| Regla del 80 % | Política determinista de avance, repetición, reducción, división o cambio. |
| Three Ds | Distancia, duración y distracción; solo una debe aumentar a la vez. |
| Meseta | Tres resultados recientes del mismo paso con varianza inferior al umbral configurado. |
| Consulta IA | Hilo informativo sobre el corpus; no es chat general ni cambia el plan. |
| Anclaje | Perro/caso elegido explícitamente para aportar datos al hilo. |
| Welfare Reviewer | Revisor del plan con poder de veto. |
| `SAFETY_HOLD` | Pausa del plan por incidente de seguridad reportado. |
| Respuesta atribuida | Respuesta profesional que identifica autores y desacuerdos. |
| Voz de K9 | Respuesta simplificada al dueño coherente con la doctrina del producto. |
| Modo lectura | Conservación del acceso a datos sin nuevas generaciones, consultas o reportes. |

## 14. Fuentes primarias

- Estado y evidencia: [`HANDOFF.md`](../../HANDOFF.md), [`PROGRESS.md`](../../PROGRESS.md).
- Vocabulario: [`CONTEXT.md`](../../CONTEXT.md).
- Experiencia dual: [`TSD-18`](../tsd/TSD-18-dual-experience.md).
- Motor: [`generate-plan`](../../supabase/functions/generate-plan/index.ts), [`process-session-report/rules.ts`](../../supabase/functions/process-session-report/rules.ts).
- Consulta IA: [`ADR-015`](../decisions/ADR-015-consulta-ia-engine-scope.md), [`consulta-ia`](../../supabase/functions/consulta-ia/index.ts).
- Planes y estados: [`entitlements.ts`](../../app/src/services/entitlements.ts), [`tiers.ts`](../../app/src/constants/tiers.ts).
- Referencia de promesas: [`RELEASE-READINESS-AND-CLAIMS.md`](./RELEASE-READINESS-AND-CLAIMS.md).
