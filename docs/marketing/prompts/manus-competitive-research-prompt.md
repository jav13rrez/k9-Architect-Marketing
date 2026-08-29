# Prompt para Manus — Investigación de mercado y producción de los documentos de lanzamiento

> **Para qué sirve esto:** encargo completo, en dos fases, para el modelo que
> hace la investigación de mercado y después escribe los documentos de
> marketing del lanzamiento (landing page, anuncios de pago, secuencia de
> emails, estrategia de campaña y guion de pitch deck). Se pega tal cual en la
> app Manus. No es documentación técnica del producto — reutiliza la
> descripción de funcionalidades ya documentada en `CLAUDE.md`,
> `docs/tsd/TSD-18-dual-experience.md`, `docs/decisions/ADR-008-pro-plan-editing-scope.md`,
> `HANDOFF.md` y `PROGRESS.md` para que la investigación esté bien orientada y
> el copy posterior no prometa nada que la app no haga.

**Origen:** v1 generada 2026-08-07. **v2 (2026-08-16)** reescrita a partir de
`HANDOFF.md` (sesiones 2026-08-12, 2026-08-13 y 2026-08-14), `PROGRESS.md`,
`docs/tsd/TSD-18-dual-experience.md`, `docs/decisions/ADR-008-pro-plan-editing-scope.md`,
`docs/tsd/TSD-13-category-variables.md` y lectura directa del código de
producción (`reportHtml.ts`, `attentionRules.ts`, `consulta-ia.tsx`).
**v3 (2026-08-22)** actualizada con `ADR-015-consulta-ia-engine-scope.md`,
`CONTEXT.md`, `entitlements.ts`, las tres landings de producción y el estado
de lanzamiento recogido en `HANDOFF.md`.

### Qué cambió en la v2 y por qué

La v1 infravaloraba tres cosas que son, de hecho, el producto:

1. **El plan clínico completo y su edición human-in-the-loop.** La app no
   "sugiere ejercicios": construye el programa de moldeamiento entero, con
   criterios objetivos por paso, y después deja que el profesional lo ajuste
   dentro de un rango de seguridad y le añada notas dictadas por voz paso a
   paso. Un profesional con veinte años de oficio sabe estructurar un plan; uno
   que empieza, no. Y ninguno de los dos tiene tiempo de documentarlo.
2. **La sincronización, no solo la vinculación.** La v1 decía que el pro
   "invita al cliente". Lo que importa es lo que pasa después: las cuentas
   quedan sincronizadas en los dos sentidos y cada sesión que el dueño trabaja
   en casa aparece sola en la ficha del profesional.
3. **La gestión y el informe como producto.** Control de qué ocurrió en cada
   sesión, notas, historial, y un PDF con la marca del profesional generado a
   partir de todo eso.

Además, la v2 añade la producción de los seis documentos de lanzamiento (antes
el encargo terminaba en el informe de investigación), los precios reales de
TSD-09 v2 con la mecánica de la prueba de 7 días (que la v1 no recogía: tarifa
anual, caps del trial, modo lectura al expirar), y una tabla de estado de
funcionalidades para que el copy venda **el producto del lanzamiento**, no el
del día en que se escribió el prompt.

La v3 corrige un cuarto vacío importante: **Consulta IA ya no es un rótulo ni
solo una posibilidad para profesionales.** Está disponible para dueño y
profesional. Se puede abrir como consulta general o anclarla explícitamente a
un perro/caso; responde únicamente a partir del corpus especializado, permite
repreguntar en el mismo hilo, muestra las fuentes disponibles y deriva en vez
de responder cuando detecta una señal de riesgo. La v3 incorpora además sus
cupos reales y elimina de las promesas de lanzamiento aquello que todavía no
es una experiencia verificable (white-labeling, visión por computador, carga
de logotipo, asientos de equipo y soporte prioritario).

### Cómo mantener este documento (importante)

El copy se escribe ahora y el producto se lanza después, así que el prompt
distingue tres estados: lo que ya está en producción, lo que estará listo el
día del lanzamiento (se vende con normalidad, sin "próximamente"), y lo que
queda fuera y no se puede prometer. Esa tabla vive dentro del prompt, en la
sección "QUÉ SE PUEDE VENDER Y QUÉ NO".

**La única edición que este documento necesita antes de pegarlo:** repasar esa
tabla y mover a la columna del medio cualquier funcionalidad que también vaya a
estar lista para el lanzamiento. Son treinta segundos y es lo que impide que el
copy prometa de menos —o de más.

Antes de reutilizarlo, contrasta la tabla contra el producto desplegado del día
del lanzamiento. En especial, no vuelvas a activar white-labeling, visión por
computador, carga de logo, asientos de equipo o soporte prioritario hasta que
la experiencia correspondiente exista y se haya verificado.

### Cómo usarlo

1. Repasar la tabla de estado de funcionalidades del prompt (sección "QUÉ SE
   PUEDE VENDER Y QUÉ NO") y mover lo que haga falta. Después, copiar el bloque
   completo en el chat de Manus.
2. Manus entrega primero la **Fase 1** (investigación) y **se detiene**.
3. Leer el informe. En él viene una recomendación razonada de a qué audiencia
   lanzar primero — esa decisión sale de la evidencia, no se toma antes.
4. Contestar en el chat con la audiencia aprobada (y cualquier corrección) para
   que Manus arranque la **Fase 2** y escriba los seis documentos.

La compuerta entre fases es deliberada: los seis entregables se construyen
sobre los hallazgos reales, no sobre suposiciones. Si Manus intenta saltarla y
entregarlo todo de golpe, pedirle que rehaga la Fase 2 después de revisar el
informe.

---

## El prompt

```
Eres un analista de mercado y copywriter de respuesta directa especializado en
el sector de bienestar y comportamiento canino. Trabajas en dos fases: primero
investigas, te detienes y esperas mi aprobación; después escribes los
documentos de lanzamiento a partir de lo que hayas encontrado. No escribas
NADA de la Fase 2 hasta que yo apruebe la Fase 1.

═══════════════════════════════════════
CONTEXTO DEL PRODUCTO
(léelo entero; NO lo copies literal en ningún entregable — es para que enfoques
la investigación y para que el copy posterior sea verdad)
═══════════════════════════════════════

Mi producto se llama K9 Behavioral Architect. Es una app (iOS/Android/web) que
diseña y gestiona programas de modificación de conducta canina usando Applied
Behavior Analysis (ABA) real — la misma disciplina científica que se usa en
terapia conductual humana, aplicada a perros. NO es "contenido genérico de
adiestramiento con una IA encima": es un motor de condicionamiento operante,
con varios agentes de IA especializados que colaboran para generar y hacer
progresar cada plan.

Cómo funciona el motor (esto es común a las dos audiencias):

- Diagnóstico funcional: la IA identifica POR QUÉ el perro hace lo que hace
  (qué función tiene la conducta), no solo QUÉ hace. Es la diferencia entre
  tratar la causa y tapar el síntoma.
- Plan de moldeamiento por pasos sucesivos, del más fácil al más difícil, con
  criterios objetivos en cada paso: distancia, duración, nivel de distracción,
  nivel de ayuda que se le da al perro, umbral de éxito y repeticiones.
- Regla del 80%: después de cada sesión, el motor decide con una regla
  estadística — si el éxito supera el 80% se avanza de nivel; entre 50% y 80%
  se repite para consolidar; por debajo del 50% el paso se parte en sub-pasos
  más fáciles; y si detecta un estancamiento (tres sesiones seguidas con
  varianza mínima) cambia de estrategia. No decide la intuición de nadie.
- Principio de un solo grado de dificultad a la vez: la IA nunca sube distancia,
  duración y distracción a la vez. Es el error más común de quien no tiene
  formación, y el que provoca los retrocesos.
- Welfare Reviewer: un agente revisor de bienestar animal con poder de veto
  revisa CADA plan antes de que llegue a nadie. Si detecta riesgo (por ejemplo
  agresión con lesión) bloquea el plan automático y deriva a un profesional o a
  un veterinario en vez de dejar que la persona siga sola. Tiene además topes
  duros de seguridad por edad (un cachorro de menos de 12 meses nunca trabaja
  más de 5 minutos; un adulto, más de 15).
- Guardia de seguridad durante el seguimiento: si en el reporte de una sesión
  se marca un incidente real (agresión con daño, señales de posible dolor o
  problema médico, estrés incapacitante), el sistema pausa el plan en el acto y
  deriva, sin esperar a que baje el porcentaje de éxito.
- Corpus científico propio: el motor consulta una base documental de literatura
  y protocolos clínicos de comportamiento canino antes de diseñar los pasos.
- Dictado por voz en toda la app, con una capa de IA que limpia y ordena lo
  dictado sin añadir jerga que la persona no usó.

A) DUEÑOS DE PERRO (B2C, app móvil, 7,99 €/mes tras prueba de 7 días)

- Describe el problema de su perro por voz o por escrito: tirones de correa,
  reactividad con otros perros, ansiedad por separación, agresividad, recall,
  obediencia básica, cuidado cooperativo, y más.
- Recibe el plan completo, escrito sin jerga técnica, con una explicación de
  por qué existe cada paso.
- Pantalla "Hoy": abre la app y en menos de 2 segundos sabe exactamente qué
  tiene que hacer hoy con su perro.
- Reporta cada sesión (también por voz): si lo consiguió o no, cuántas veces,
  cuánto duró, dónde, qué señales de estrés vio, qué falló y por qué. El motor
  decide el siguiente paso y se lo explica en lenguaje llano.
- Pipeline de generación transparente: mientras la IA trabaja ve las etapas
  reales (entendiendo el caso, analizando la función de la conducta, consultando
  el corpus científico, diseñando los pasos, revisión pedagógica, revisión de
  bienestar). No es una caja negra ni un spinner genérico.
- Si trabaja con un profesional vinculado, ve dentro de su plan las notas que
  su profesional le ha dejado en cada paso, y un aviso discreto en los pasos que
  el profesional ha ajustado.
- Biblioteca pública de contenido educativo sobre comportamiento canino, en
  español e inglés.
- Consulta IA: puede abrir una consulta general o anclarla explícitamente a un
  perro. Si la ancla, la respuesta considera el plan activo y las sesiones
  recientes de ese perro además del corpus especializado. Puede repreguntar
  dentro del mismo hilo, ver las fuentes disponibles y recibir lecturas de la
  Biblioteca. Si no hay material recuperado suficiente, lo reconoce; si la
  pregunta describe dolor, lesión, agresión con daño o estrés incapacitante,
  no improvisa y deriva. La consulta informa, pero no modifica el plan.

B) PROFESIONALES DEL COMPORTAMIENTO CANINO (B2B, escritorio + modo campo en
móvil, 29 €/mes o 79 €/mes tras prueba de 7 días)

Punto de partida real de este perfil: gestiona entre 25 y 40 casos activos
viviendo en WhatsApp, Google Calendar y notas sueltas, y pierde entre 4 y 6
horas por semana escribiendo informes.

1. Le construye el programa clínico entero, no una plantilla. A partir del caso
   obtiene el diagnóstico funcional y el plan de moldeamiento completo con
   criterios objetivos por paso, revisado por el agente de bienestar y apoyado
   en el corpus científico. Antes de generar, el profesional puede editar el
   resumen del caso que se le envía al motor: es experto, no se le esconde qué
   entra.
   IMPORTANTE PARA EL ÁNGULO: esto vale para dos perfiles muy distintos. Para
   quien lleva años de oficio, es velocidad y documentación de algo que ya sabe
   hacer. Para quien empieza —recién certificado, o formándose— es el andamiaje
   clínico que todavía no tiene: estructurar un programa por pasos con criterios
   objetivos es exactamente lo que no se aprende en un curso de fin de semana.
   Investiga las dos caras.
2. Ajuste del profesional (human-in-the-loop de verdad). El plan generado no es
   intocable:
   - Puede corregir los metros y los minutos de los pasos que el perro aún no ha
     hecho, dentro de un rango de ajuste seguro: hasta un 20% arriba o abajo del
     valor que propuso la IA, y nunca por encima del tope absoluto de seguridad
     por edad del perro. El sistema le muestra el rango permitido.
   - Puede añadir notas propias en cada paso, dictándolas por voz, y esas notas
     las ve su cliente dentro de su app.
   - Los campos que alimentan el motor (umbral de éxito, repeticiones, nivel de
     ayuda, nivel de distracción) están bloqueados por diseño: el rigor
     científico no se puede romper por accidente.
   - Toda edición queda auditada (quién, cuándo, valor original de la IA frente
     al valor editado), y el dueño ve un aviso discreto de que su profesional
     ajustó ese paso.
   El mensaje de fondo: la IA hace el trabajo pesado, el criterio profesional
   manda, y el bienestar del animal está protegido por construcción, no por
   confianza.
3. Control de lo que ocurrió en cada sesión. Cada sesión, presencial o de
   deberes, queda registrada con su resultado, valoración, señales de estrés
   concretas, duración, lugar, causa del fallo y notas. El caso tiene historial
   completo, no una carpeta de audios de WhatsApp.
4. Panel que responde "¿qué necesita mi atención hoy?": casos activos, citas de
   hoy, deberes reportados esta semana, y una lista de casos que requieren
   atención calculada automáticamente por tres criterios — el perro mostró
   estrés en la última sesión, el caso lleva tres o más sesiones estancado sin
   avanzar, o una sesión de deberes bajó del 50% de éxito. No hay que entrar
   caso a caso para enterarse.
5. Agenda con citas tipadas (evaluación, entrenamiento, seguimiento,
   videoconsulta) vinculadas al caso. Al marcar una cita como completada se
   encadena directamente el reporte de esa sesión: la agenda alimenta el motor,
   no es un calendario decorativo.
6. Informes en PDF con su marca, generados a partir de todo lo anterior:
   estado del caso, categoría del problema, sesiones completadas, progreso
   (paso X de Y), resumen del plan y una ficha narrativa por sesión que cuenta
   qué se trabajó y qué pasó. Se dicta lo que haga falta y el informe sale
   escrito. Es exactamente el trabajo que hoy le come de 4 a 6 horas a la
   semana.
7. EL FOSO COMPETITIVO — vinculación Y SINCRONIZACIÓN entre las dos cuentas,
   en los dos sentidos:
   - El profesional invita a su cliente con un enlace, o el dueño se vincula él
     mismo introduciendo el código de conexión de su profesional (en ese caso el
     profesional tiene que aprobar la solicitud: nadie accede a datos ajenos por
     escribir un código).
   - Una vez vinculadas, las cuentas quedan sincronizadas. El profesional puede
     crear el perro y el caso a nombre de su cliente, y ese plan aparece en la
     app del dueño sin que este tenga que hacer nada.
   - Y al revés, que es lo que de verdad cambia el trabajo del profesional: cada
     sesión de "deberes" que el cliente trabaja en casa y documenta en su app
     aparece automáticamente en la ficha del caso, con su resultado y sus notas,
     y cuenta en el panel del profesional. Ya no hay que perseguir a nadie por
     WhatsApp para saber si hizo los ejercicios, ni fiarse de un "sí, bien" el
     día de la siguiente cita.
   - El consentimiento es explícito en los dos sentidos y los permisos son de
     solo lectura sobre los datos clínicos del dueño, salvo las ediciones
     autorizadas del punto 2.
8. Consulta IA: puede abrir una consulta general o anclarla explícitamente a
   un caso. La respuesta se redacta a partir del mismo corpus científico y,
   cuando existe desacuerdo relevante, lo atribuye en vez de ocultarlo. Puede
   continuar con repreguntas dentro del hilo, consultar las fuentes disponibles
   y recibir lecturas de la Biblioteca; si el corpus no basta, lo reconoce. Si
   el texto describe una bandera roja de seguridad, no responde y deriva. Es
   una segunda opinión permanente, pero informa: no genera ni modifica planes,
   no sustituye su juicio ni toma decisiones por él.

C) PRECIOS, PRUEBA Y FACTURACIÓN

Tres planes, con mes y año (el año sale a diez meses, y ese es un argumento en
sí mismo):

- Plus — dueños: 7,99 €/mes o 79 €/año. Hasta 3 perros, 20 generaciones de plan
  y 50 hilos de Consulta IA al mes, planes activos ilimitados.
- Pro — profesionales: 29 €/mes o 290 €/año. Perros ilimitados, hasta 30 casos
  activos, 60 generaciones de plan y 200 hilos de Consulta IA al mes, CRM de
  clientes, agenda, modo campo, vinculación con clientes, informes con el
  nombre de su negocio, 1 usuario.
- Estudio — profesionales: 79 €/mes o 790 €/año. Todo lo de Pro con casos
  ilimitados, 150 generaciones de plan y 500 hilos de Consulta IA al mes.

En los tres planes, sin límite nunca: las sesiones y los reportes. Un usuario
jamás deja de documentar el trabajo de su perro porque se le haya acabado una
cuota — es una decisión de producto deliberada y se puede decir en el copy.
También en los tres: dictado por voz, historial con gráficas y exportación a
PDF.

Prueba de 7 días para todos, sin tarjeta. El dueño prueba Plus y el profesional
prueba Estudio, con tres topes durante la prueba: 1 perro, 5 generaciones de
plan y 10 hilos de Consulta IA. Todo lo demás está abierto. Al terminar la prueba sin suscribirse, la
cuenta pasa a modo lectura: sigue viendo su plan, su historial y la biblioteca,
pero no genera planes nuevos ni reporta sesiones. Los datos nunca se secuestran
—y ese matiz, bien contado, vende.

═══════════════════════════════════════
QUÉ SE PUEDE VENDER Y QUÉ NO
═══════════════════════════════════════

El copy describe el producto TAL Y COMO SERÁ EL DÍA DEL LANZAMIENTO. Todo lo
listado en los apartados A, B y C de arriba estará disponible ese día: escríbelo
en presente y con normalidad. No uses "próximamente", "muy pronto", "en la hoja
de ruta" ni fechas de disponibilidad para nada de eso.

Fuera del lanzamiento — no lo prometas, no lo insinúes, no construyas un ángulo
sobre ello:

- Sincronización con Google Calendar o invitaciones de calendario al cliente:
  la agenda es interna.
- Análisis de vídeo o visión por computador.
- White-labeling, carga de un archivo de logo, asientos de equipo o soporte
  prioritario: el PDF sí puede llevar el nombre del negocio, pero esas
  experiencias no se deben vender hasta que estén operativas y verificadas.
- Comunidad, foro, marketplace de profesionales o directorio público donde un
  dueño busque adiestrador.
- Notificaciones push masivas y campañas transaccionales dentro del producto.

Un matiz de precisión, no una prohibición: los informes llevan la marca del
profesional. Puedes decir "informes con tu marca"; no describas el proceso de
subir un archivo de logo salvo que se confirme que esa parte entra.

Y lo que no se inventa bajo ningún concepto:

- Cifras de usuarios, testimonios, casos de éxito, valoraciones, premios,
  apariciones en prensa o estudios propios. Si una pieza necesita prueba social,
  deja el hueco marcado como [PENDIENTE DE APORTAR] con una nota de qué haría
  falta para rellenarlo. Ni una cita, ni un número, ni un logo de cliente.

Y dos límites de fondo, por responsabilidad y por normativa de publicidad:

- Nunca prometas curación, resultados garantizados ni plazos ("adiestra a tu
  perro en 7 días"). El producto trabaja con conducta animal, no con milagros.
- Nunca posiciones el producto como sustituto de un veterinario ni de un
  profesional presencial en casos de riesgo. El propio producto deriva esos
  casos: eso es un argumento de venta, no una limitación que esconder.

═══════════════════════════════════════
FASE 1 — INVESTIGACIÓN (entrégala y DETENTE)
═══════════════════════════════════════

Investiga las DOS audiencias, dueños y profesionales. No asumas todavía a cuál
vamos a lanzar la campaña: decidirlo es una de tus conclusiones.

### BLOQUE 1 — Análisis de competencia

Identifica y analiza:

1. Apps de adiestramiento y comportamiento canino con IA (competencia directa
   B2C): Dogo, GoodPup, Zigzag Puppy Training, Woofz, Pupford, Spot & Tango,
   CleverPet y cualquier otra que encuentres, priorizando las disponibles en
   España y el mercado hispanohablante, e incluyendo las líderes de EE.UU. y
   Reino Unido si son relevantes.
2. Software de gestión para adiestradores, educadores y centros caninos
   (competencia directa B2B): Gingr, Pawfinity, PetExec, Trainer's Pantry,
   Time To Pet y equivalentes en español si existen. Busca también software de
   gestión de práctica ABA humana (por ejemplo CentralReach o Rethink) como
   analogía de categoría: qué funcionalidades consideran imprescindibles, qué
   precios sostienen y cómo justifican el rigor clínico.
3. Herramientas de seguimiento cliente-profesional en sectores análogos
   (fisioterapia, entrenamiento personal, nutrición, logopedia): apps donde el
   profesional prescribe un programa y el cliente lo ejecuta y reporta en casa.
   Es el modelo exacto de nuestro foso — quiero saber qué funciona ahí, qué
   precios se pagan y qué falla en la adherencia del cliente.
4. Competencia indirecta: educadores y adiestradores individuales y sus webs
   (cómo se presentan, qué precios cobran, qué prometen), contenido gratuito
   masivo (canales de YouTube y cuentas de TikTok e Instagram de adiestramiento
   con audiencias grandes), grupos de Facebook de dueños con problemas de
   conducta, y la formación para nuevos educadores caninos (qué cursos y
   certificaciones existen en España, qué cuestan, y qué se les enseña —o no—
   sobre estructurar programas de intervención).

Para cada competidor relevante extrae:

- Propuesta de valor y mensaje principal en su web o ficha de app.
- Precio y modelo (suscripción, pago único, freemium).
- Funcionalidades clave.
- Valoración media y quejas textuales reales de usuarios (App Store, Google
  Play, Trustpilot, comentarios). Cita las frases originales, no las resumas.
- Qué NO ofrecen que mi producto sí ofrece. Busca especialmente: ausencia de
  base científica real, ausencia de diagnóstico funcional (tratan síntomas),
  ausencia de detección de riesgo y derivación, planes genéricos no adaptados
  al perro concreto, ausencia de progresión basada en datos de la sesión, y en
  B2B: ausencia de generación de informes, ausencia de seguimiento del cliente
  entre citas, y ausencia de cualquier contenido clínico (los CRM del sector
  gestionan reservas y pagos, no casos).

### BLOQUE 2 — Puntos de dolor del cliente ideal

Investiga en foros, grupos y reseñas (Reddit, especialmente r/reactivedogs,
r/DogTrainingTips, r/dogs y r/OpenDogTraining; grupos de Facebook de dueños con
perros reactivos, agresivos o con ansiedad; comentarios en vídeos de YouTube de
adiestramiento; reseñas de apps competidoras; reseñas de Google de adiestradores
locales; grupos y foros profesionales de educadores caninos en español).

Sobre dueños de perro con problemas de conducta:

- Qué frases usan literalmente para describir su frustración (cítalas textuales
  con su fuente).
- Qué han probado antes que no funcionó, y por qué según ellos.
- Qué miedos tienen: empeorar el problema, que su perro sea "un caso perdido",
  el coste de un adiestrador presencial, quedar en ridículo, la seguridad de
  otras personas y otros perros, que les juzguen como malos dueños.
- En qué momento del día y en qué situación sienten más el problema.
- Qué pasa entre sesión y sesión: ¿saben qué hacer cada día? ¿abandonan? ¿en
  qué momento exacto abandonan?
- Qué buscan literalmente en Google cuando tienen este problema (para orientar
  las keywords de Ads).

Sobre profesionales del comportamiento canino, SEGMENTANDO POR VETERANÍA
(esta segmentación es importante, no la mezcles):

- Profesionales consolidados (más de 5 años, cartera llena): qué dicen sobre la
  carga administrativa y los informes, sobre clientes que no cumplen las tareas
  entre sesiones, sobre las herramientas que usan hoy (WhatsApp, Excel,
  Calendar) y sus límites, y sobre cuánto tiempo real pierden documentando.
- Profesionales que empiezan (recién certificados, primeros clientes): qué
  dicen sobre la inseguridad al diseñar un programa de intervención, sobre
  qué hacer cuando un caso se complica, sobre cómo estructurar y presentar su
  trabajo para parecer profesional ante un cliente, y sobre el miedo a
  equivocarse con un perro reactivo o agresivo. Busca en foros de formación,
  comentarios de cursos y grupos de recién titulados.
- De ambos: su actitud hacia la IA aplicada a su profesión. ¿Escepticismo? ¿Por
  qué exactamente? ¿Miedo a ser sustituidos, a perder credibilidad ante el
  cliente, a que la IA dé un consejo peligroso? Cita las frases reales.
- Qué les hace confiar o desconfiar de una herramienta nueva, y qué les haría
  pagar 29 € o 79 € al mes por una.
- Cómo cobran hoy, cuánto cobran por sesión y por programa, y cómo justifican
  su precio ante el cliente.

### BLOQUE 3 — Síntesis y recomendación

1. Los 5 dolores más agudos por audiencia, ordenados por intensidad de la
   evidencia encontrada (no por tu intuición), cada uno con su cita y su fuente.
2. Ángulos de mensaje: 8-10 posibles ganchos basados en los dolores más fuertes.
   No los redactes todavía en modo publicitario — un insight por frase, con el
   dolor que ataca y la funcionalidad concreta que lo responde.
3. RECOMENDACIÓN DE AUDIENCIA PARA LA PRIMERA CAMPAÑA, razonada con la
   evidencia que has encontrado, no con opiniones generales. Compara las dos
   audiencias en: intensidad del dolor, disposición a pagar, coste estimado de
   adquisición y competencia por las keywords, debilidad de la competencia
   existente, y efecto de arrastre (una audiencia trae a la otra por la
   vinculación de cuentas). Da una recomendación clara, di qué te haría cambiar
   de opinión, y qué dato te falta para estar seguro.

DETENTE AQUÍ. Entrega la Fase 1 y espera mi aprobación explícita, incluida la
audiencia elegida, antes de escribir una sola línea de la Fase 2.

═══════════════════════════════════════
FASE 2 — LOS SEIS DOCUMENTOS DE LANZAMIENTO
(solo después de mi aprobación)
═══════════════════════════════════════

Reglas comunes a los seis:

- Todo lo que escribas tiene que apoyarse en un hallazgo real de la Fase 1.
  Cuando uses un dolor, indica entre corchetes de qué hallazgo sale. Si algo te
  lo estás inventando, no lo escribas.
- Respeta la sección "QUÉ SE PUEDE VENDER Y QUÉ NO" al pie de la letra.
- Español de España, natural y directo. Sin emojis. Sin superlativos vacíos
  ("revolucionario", "la mejor app del mundo"). Sin jerga ABA en el material
  dirigido a dueños; con vocabulario técnico correcto en el material dirigido a
  profesionales, que la detectan y la valoran.
- El tono con el profesional es de igual a igual: la herramienta es un copiloto
  que le devuelve horas y le da respaldo científico, nunca un sustituto de su
  criterio. Decirle lo contrario es la forma más rápida de perderlo.
- Entrega cada documento por separado, completo y autónomo, listo para usar sin
  reescritura. Nada de esquemas ni de "aquí iría un párrafo sobre X".

--- ENTREGABLE 1 — Análisis de Mercado, Competencia y Puntos de Dolor ---

Documento formal a partir de la Fase 1, ampliado con:
- Tamaño y estructura del mercado en España (perros censados, gasto medio por
  perro, número estimado de educadores y centros caninos en activo, tendencia
  de los últimos años). Cita fuentes; marca las estimaciones como estimaciones.
- Tabla comparativa de competidores: nombre, tipo, precio, propuesta de valor,
  debilidad principal, fuente.
- Los puntos de dolor, 10-15 por audiencia, cada uno con la cita textual real,
  su fuente y la funcionalidad concreta de K9 que lo responde.
- Mapa de posicionamiento: dónde queda K9 frente a las apps de contenido
  genérico, frente al CRM de gestión sin contenido clínico y frente al
  profesional presencial.
- Riesgos del mercado y objeciones estructurales previsibles.

--- ENTREGABLE 2 — Landing page: contenido detallado y copy completo ---

Para la audiencia aprobada. Entrega el copy final, sección a sección, listo
para maquetar:
- Estructura completa en orden, indicando en cada sección su objetivo y qué
  dolor ataca.
- Above the fold: titular, subtitular, CTA principal y prueba visual que
  debería acompañarlo (descríbela, no la generes).
- Sección de problema: el dolor, con el lenguaje literal encontrado en la
  investigación.
- Sección de mecanismo: cómo funciona, en tres pasos, sin jerga.
- Sección de diferenciadores, con el foso (sincronización de cuentas, control
  del caso, informes, plan editable con seguridad) explicado en beneficios, no
  en funcionalidades.
- Manejo explícito de las objeciones reales que hayas encontrado en la Fase 1
  (por ejemplo: escepticismo hacia la IA, "yo ya sé diseñar programas", "mis
  clientes no van a usar otra app", precio, seguridad del animal).
- Precios: tabla comparativa de los planes con su precio mensual y anual, qué
  incluye cada uno, y el copy que empuja al anual. La prueba de 7 días sin
  tarjeta es un argumento de peso — dale el sitio que merece, y explica qué
  pasa al terminarla (modo lectura, los datos se conservan) porque quita el
  miedo a empezar.
- FAQ de 8-10 preguntas basadas en dudas reales de la investigación.
- CTA final y microcopy de formulario (etiquetas, texto del botón, mensaje de
  confirmación, nota de privacidad).
- Meta título y meta descripción, y textos alternativos sugeridos para las
  imágenes.
- 3 variantes alternativas del titular principal para test A/B, cada una con
  el ángulo que explora.
- Al final, un bloque compacto de "adaptación a la otra audiencia": qué
  secciones cambian y con qué copy, por si lanzamos también a la segunda.

--- ENTREGABLE 3 — Seis anuncios de tráfico de pago ---

Seis anuncios, cada uno construido sobre un gancho DISTINTO de los de la
landing (no seis variantes del mismo). Reparto sugerido: cuatro para Meta
(Facebook e Instagram) y dos para Google Search; ajústalo si la investigación
dice otra cosa, y justifica el cambio.

Para cada anuncio:
- Gancho y dolor que ataca, con referencia al hallazgo de la Fase 1.
- Plataforma y formato.
- Copy completo: texto principal, titular, descripción y llamada a la acción.
  Para Google Search: 5 titulares y 3 descripciones respetando los límites de
  caracteres, más la lista de keywords y de negativas.
- Concepto creativo descrito (qué se ve, qué pasa, qué texto va en pantalla).
  No generes imágenes.
- Segmentación e intereses sugeridos.
- Qué métrica indica que ese ángulo funciona y cuándo matarlo.

--- ENTREGABLE 4 — Secuencia de emails de lanzamiento ---

Secuencia de 7 emails cuyo hilo conductor es la metodología ABA: cada email
enseña un principio real del método y, enseñándolo, vende. El lector tiene que
terminar la secuencia sabiendo algo que no sabía, aunque no compre.

Sugerencia de arco (ajústalo si la investigación lo desmiente, y justifícalo):
el problema no es el perro sino la falta de método; qué es el análisis funcional
y por qué "por qué lo hace" importa más que "qué hace"; la regla del 80% y por
qué la intuición falla; el error de subir tres dificultades a la vez; por qué el
bienestar del animal es un límite y no un extra; qué pasa entre sesión y sesión
(el argumento del seguimiento y la sincronización); y cierre con oferta.

La secuencia tiene que encajar con la mecánica real de la prueba: 7 días sin
tarjeta, con 1 perro y 5 generaciones de plan durante la prueba, y modo lectura
al terminar sin suscribirse. Mapea explícitamente cada email sobre ese arco —
el momento de activación de los primeros días (que genere su primer plan y
reporte su primera sesión es lo que decide la conversión), el aviso antes de que
expire, y el correo posterior a quien se quedó en modo lectura, que es el que
más dinero deja sobre la mesa si no existe.

Para cada email:
- Objetivo y momento de envío (día y disparador).
- Asunto principal más dos alternativas, y preheader.
- Cuerpo completo, listo para enviar.
- CTA única y clara.
- Criterio de segmentación o de salida de la secuencia (por ejemplo, quien ya
  se ha suscrito deja de recibir los correos de conversión).
Añade al final los criterios de éxito de la secuencia (aperturas, clics,
conversión de prueba a pago) y qué hacer con quien no abre.

--- ENTREGABLE 5 — Presentación de la estrategia de campaña de lanzamiento ---

Presentación en formato de diapositivas (título más contenido de cada una,
en texto; no generes el archivo de diseño):
- Objetivo del lanzamiento y KPIs, con cifras objetivo.
- Audiencia elegida y por qué, resumiendo la evidencia.
- Propuesta de valor y mensajes centrales.
- Fases: pre-lanzamiento, lanzamiento y post-lanzamiento, con duración y
  actividades de cada una.
- Canales y papel de cada uno, incluido el orgánico y la biblioteca de contenido
  educativo que ya existe.
- Embudo completo con las métricas objetivo en cada paso (impresiones, CTR,
  coste por lead, conversión a prueba, activación durante la prueba, conversión
  a pago) y el coste de adquisición máximo que aguanta cada plan, calculado
  sobre los precios reales (7,99 €/mes o 79 €/año; 29 €/mes o 290 €/año;
  79 €/mes o 790 €/año) y con supuestos de permanencia explícitos. Di qué pasa
  con esos números si la permanencia es la mitad de la que supones.
- Presupuesto y reparto por canal, con al menos dos escenarios de inversión.
- Calendario semana a semana.
- Plan de medición: qué se mide, con qué, y qué decisión se toma con cada dato.
- Riesgos y plan B.

--- ENTREGABLE 6 — Guion de presentación para inversores y socios ---

Guion hablado de pitch deck, 12-15 diapositivas. Para cada una: título,
contenido de la diapositiva y el guion de lo que se dice en voz alta (párrafos
reales, no bullets).

Arco: problema y su tamaño; por qué las soluciones actuales no funcionan; la
solución y su demostración; el mecanismo científico como barrera de entrada
(motor ABA, revisión de bienestar con veto, corpus propio); el modelo de dos
caras y por qué la sincronización de cuentas genera retención y adquisición
cruzada; mercado; modelo de negocio y unit economics; tracción y estado real
del producto; competencia y por qué no nos alcanzan; hoja de ruta; equipo;
la petición concreta y en qué se emplea.

Añade al final un anexo con las 10 preguntas más difíciles que hará un
inversor (incluidas: por qué no lo copia un competidor con más dinero, qué pasa
si la IA da un consejo que daña a un perro, y por qué un profesional pagaría
por esto en vez de seguir con WhatsApp) y una respuesta preparada para cada una.

TODA cifra de tracción, financiera o de mercado que no puedas sostener con una
fuente va marcada como [DATO PENDIENTE] y con una nota de qué haría falta para
rellenarla. Un pitch con un dato inventado es un pitch muerto.

═══════════════════════════════════════
FUENTES
═══════════════════════════════════════

Prioriza fuentes en español y del mercado español e hispanohablante, e incluye
hallazgos en inglés cuando aporten un dolor o un competidor importante que no
exista en español. Cita siempre la fuente con enlace o con el nombre del foro o
la red. Distingue siempre entre lo que has verificado y lo que estás estimando.
```

---

## Qué hacer con cada entregable, una vez lo tengas

| Entregable | Siguiente paso en este repo |
|---|---|
| 1. Análisis de mercado | Archivar en `docs/marketing/`. Es el insumo de todo lo demás y la base del pitch. |
| 2. Landing page | Pasarla por la skill `copywriting` para afinar el copy, y por `page-cro` antes de publicar. La maquetación debe seguir el design system (`.claude/rules/frontend.md`: sin emojis, iconos Lucide, tipografía y colores del proyecto). |
| 3. Seis anuncios | Revisar con la skill `paid-ads`. Verificar límites de caracteres reales de cada plataforma antes de subirlos. |
| 4. Secuencia de emails | Revisar con la skill `email-sequence` si está disponible; si no, con `copywriting`. |
| 5. Estrategia de campaña | Decisión del fundador: presupuesto y calendario son compuerta humana, no se ejecutan solos. |
| 6. Guion de pitch deck | Rellenar los `[DATO PENDIENTE]` con datos reales antes de enseñárselo a nadie. La skill `pptx` puede montar el archivo a partir del guion. |

**Antes de publicar cualquier pieza:** contrastar cada afirmación sobre el
producto contra `HANDOFF.md` y `PROGRESS.md`. El copy se escribe describiendo el
producto del día del lanzamiento, así que hay una ventana en la que la landing
promete cosas que la app todavía no hace — eso es normal y deliberado, pero la
pieza no se publica hasta que lo prometido está en producción y verificado con
el protocolo de despliegue de `CLAUDE.md`. La tabla de estado de funcionalidades
del prompt es correcta a fecha 2026-08-16: revisarla y actualizarla cada vez que
se vuelva a usar este documento.
