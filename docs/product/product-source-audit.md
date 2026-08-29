# Auditoría de fuentes del producto — K9 Behavioral Architect

**Fecha de corte:** 2026-08-22  
**Propósito:** fuente factual para redactar la documentación de producto, el manual, el dossier para inversores y el documento de stack tecnológico.  
**Alcance:** únicamente fuentes primarias del repositorio: código ejecutable, migraciones, pruebas, ADR/TSD y registros de entrega cuando distinguen expresamente lo verificado de lo no verificado.

> Este documento no es copy comercial. Es una auditoría de lo que se puede afirmar con respaldo. Una capacidad presente en código se marca como **implementada en el repositorio**; eso no equivale por sí solo a que su despliegue actual, configuración externa o experiencia visual se hayan vuelto a comprobar en producción durante esta auditoría.

## 1. Criterio de evidencia

| Estado | Significado |
|---|---|
| **Implementado** | Existe un flujo ejecutable completo o una operación real en código y base de datos. |
| **Implementado con dependencia externa** | El código existe, pero el resultado requiere configuración ajena al repositorio, como Stripe, Supabase o compatibilidad del navegador. |
| **Verificado en producción** | HANDOFF/PROGRESS aporta una prueba explícita y concreta, no solo una afirmación de “hecho”. |
| **Parcial o aproximado** | El producto entrega valor, pero el dato o flujo se obtiene mediante un modelo provisional que no debe describirse con más precisión de la real. |
| **No prometible** | Solo existe como spec, flag de entitlement, placeholder, configuración pendiente o afirmación sin verificación suficiente. |

Las referencias se expresan como `ruta:línea`. Cuando un documento histórico contradice al código actual, prevalece el código; cuando se habla de producción, prevalece la evidencia operativa más reciente y explícita.

## 2. Definición verificable del producto

K9 Behavioral Architect es una aplicación web/multiplataforma de educación y seguimiento del comportamiento canino que estructura el trabajo alrededor de:

1. un perfil del perro;
2. un caso o problema observable;
3. un plan progresivo generado con IA y sometido a controles pedagógicos y de bienestar;
4. sesiones reportadas con datos de éxito, contexto y señales de estrés;
5. un motor de progresión basado en criterios;
6. una Biblioteca bilingüe;
7. una Consulta IA basada en el corpus del producto;
8. y, para profesionales, CRM ligero, vinculación con dueños, agenda, señales de atención, ajuste acotado del plan e informes.

La aplicación reconoce dos roles de cuenta: `owner` y `professional` (`app/src/hooks/useAuth.tsx:22-24`). El shell profesional está protegido frente a cuentas Owner y los usuarios Professional son enviados a su panel (`app/src/app/_layout.tsx:85-98`).

## 3. Capacidades actuales para dueños (B2C)

### 3.1 Cuenta, acceso y onboarding

- Alta e inicio de sesión por correo y contraseña mediante Supabase Auth (`app/src/hooks/useAuth.tsx:103-138`).
- Elección de tipo de cuenta durante el alta; el perfil persiste `account_type` y, para profesionales, `business_name` (`app/src/hooks/useAuth.tsx:103-121`).
- Onboarding con creación del perfil del perro y datos como raza, edad, peso, sexo, condiciones médicas y alergias (`app/src/app/(auth)/onboarding.tsx:109-128`; esquema en `supabase/migrations/202604111200_create_dogs.sql:9-23`).
- Gestión de varios perros según el plan contratado; desde Inicio se puede seleccionar perro, añadir otro, limpiar su historial de entrenamiento o aplicar borrado lógico del perro, sus planes y sus sesiones (`app/src/app/(auth)/(tabs)/hoy.tsx:388-420,623-647`; operaciones en `app/src/app/(auth)/(tabs)/hoy.tsx:272-300`).
- Los inicios de sesión con Google y Apple **no están implementados**: los métodos existen pero están vacíos (`app/src/hooks/useAuth.tsx:169-170`).

### 3.2 Creación de planes

- El usuario elige entre siete categorías actuales: obediencia básica, educación cívica, modificación de conducta, cuidado cooperativo, deporte canino, trabajo operacional y perro de asistencia (`app/src/constants/categories.ts:38-89`).
- Cada categoría solicita datos específicos y observables. Por ejemplo, modificación de conducta pide conducta, antecedente, consecuencia, contextos de éxito, intervenciones previas y riesgo; cuidado cooperativo pregunta procedimiento, reacción, urgencia y reforzadores (`app/src/app/(auth)/new-plan.tsx:52-93`).
- Los formularios aceptan texto y dictado cuando el navegador soporta Web Speech (`app/src/app/(auth)/new-plan.tsx:590-634`; `app/src/hooks/voice/useVoiceInput.ts:28-40`).
- La petición de generación llega a la Edge Function `generate-plan` desde el hook del cliente (`app/src/hooks/usePlan.ts:251-253`).
- Antes de gastar llamadas a IA, el backend valida autenticación, estado de suscripción y cupo (`supabase/functions/generate-plan/index.ts:1010-1103`). El consumo de generación se hace en servidor y mediante una operación atómica (`supabase/functions/generate-plan/index.ts:1198-1213`; `supabase/migrations/20260819170000_consume_plan_generation.sql:23-80`).

### 3.3 Motor de planificación conductual

El pipeline actual contiene, en términos funcionales:

- interpretación del relato y limpieza de la conducta observable;
- evaluación funcional mediante el marco ABC;
- decisión `proceed`, `probe` o `block` según calidad de la información y riesgos;
- diseño macro del plan;
- construcción de pasos e instrucciones para el dueño;
- consulta del corpus RAG cuando procede;
- validación pedagógica determinista y mediante juez;
- revisión de bienestar con capacidad de veto;
- persistencia del plan aprobado y creación de su primera sesión.

Las piezas principales están en `supabase/functions/generate-plan/index.ts:126-316,320-438,524-594,602-887,1347-1489,1500-1655` y el revisor de bienestar en `supabase/functions/generate-plan/welfare.ts`.

Reglas que sí están respaldadas por el código:

- se priorizan métodos sin aversivos y seguros para el bienestar (`supabase/functions/generate-plan/index.ts:664-671`);
- el diseño mueve una sola D —distancia, duración o distracción— por paso y busca aproximadamente un 80 % de éxito antes de avanzar (`supabase/functions/generate-plan/index.ts:552-556`);
- en desensibilización/contracondicionamiento se exige una progresión gradual y se prohíbe flooding (`supabase/functions/generate-plan/index.ts:545-556`);
- un caso con información insuficiente puede generar un único paso provisional de observación, no un falso plan completo (`supabase/functions/generate-plan/index.ts:632-644,1270-1279`);
- un caso con banderas de seguridad reales se bloquea y deriva (`supabase/functions/generate-plan/index.ts:1230-1247`);
- un plan rechazado por bienestar no se persiste como plan aprobado (`supabase/functions/generate-plan/index.ts:1433-1473`).

### 3.4 Sesiones, seguimiento y progresión

- La pantalla Inicio presenta el perro seleccionado, el plan activo, progreso, actividad semanal y la próxima sesión pendiente (`app/src/app/(auth)/(tabs)/hoy.tsx:318-324,424-620`).
- Una sesión permite iniciar el trabajo, seguir las instrucciones del paso y registrar resultados (`app/src/app/(auth)/session/[id].tsx:63-217`).
- El reporte recoge repeticiones correctas/totales, valoración, señales de estrés, duración, entorno, notas, causas de dificultad y tres tipos de incidente grave (`app/src/app/(auth)/session/report.tsx:156-229,460-591`).
- La progresión es determinista en su regla base:
  - más del 80 %: `ADVANCE`;
  - 50–80 %: `REPEAT` o `CHANGE` si hay meseta;
  - menos del 50 %: `SPLIT` o escalado según historial;
  - señales de estrés impiden avanzar aunque se supere el umbral;
  - un incidente grave genera `SAFETY_HOLD`.
  Fuentes: `supabase/functions/process-session-report/rules.ts:90-143` y `supabase/functions/process-session-report/index.ts:4-15,405-552`.
- `SPLIT` y `CHANGE` pueden recurrir a Gemini para dividir un paso o modificar el enfoque; la regla de decisión y los controles principales permanecen en código determinista (`supabase/functions/process-session-report/index.ts:15-28,56-78,432-538`).
- Un `SAFETY_HOLD` pausa el plan, solicita revisión humana y no crea una siguiente sesión normal (`supabase/functions/process-session-report/index.ts:548-564,641-673`).
- Se mantiene historial por plan y sesiones completadas (`app/src/app/(auth)/plan-history/[id].tsx:58-101`).

### 3.5 Consulta IA para dueños

Consulta IA está implementada para los dos perfiles, no es ya un placeholder (`app/src/components/ConsultaIaScreen.tsx:1-20`). Para el dueño ofrece:

- pregunta escrita o dictada;
- consulta general sin datos clínicos o anclaje explícito a uno de sus perros;
- respuestas basadas en recuperación del corpus;
- fuentes al pie;
- aviso de corpus insuficiente en lugar de inventar;
- lecturas recomendadas de la Biblioteca;
- repreguntas dentro del mismo hilo;
- seis turnos de usuario por hilo y memoria corta de cuatro intercambios;
- cupo mensual propio, independiente del cupo de planes.

Evidencia de pantalla y llamada: `app/src/components/ConsultaIaScreen.tsx:202-280,294-425`. Límites de hilo: `supabase/functions/_shared/consultaMemory.ts:23-31`. Persistencia, seguridad, recuperación y respuesta: `supabase/functions/consulta-ia/index.ts:192-224,259-294,331-463`.

La consulta sin anclaje no incorpora datos clínicos. Cuando hay anclaje, el servidor carga un contexto acotado del perro, su plan más reciente y sesiones relevantes, siempre sujeto a RLS (`supabase/functions/consulta-ia/loadCase.ts:46-106`). El anclaje no se deduce del texto y no cambia a mitad del hilo (`supabase/functions/consulta-ia/index.ts:17-22,192-209`).

La redacción para Owner usa una postura única de K9 y mantiene las fuentes al pie; la redacción profesional puede atribuir autores y mostrar discrepancias reales (`docs/decisions/ADR-015-consulta-ia-engine-scope.md:80-90`).

Limitación actual: los hilos se persisten, pero la UI no permite volver a abrir y releer el listado histórico de hilos (`app/src/components/ConsultaIaScreen.tsx:19-21`).

### 3.6 Biblioteca

- La Biblioteca tiene superficie pública indexable y es accesible desde la app autenticada en la misma URL (`app/src/app/_layout.tsx:64-68`).
- Ofrece navegación por categorías, etiquetas y niveles, con contenidos bilingües español/inglés (`app/src/app/(public)/library/index.tsx:80-148`; `app/src/constants/libraryTaxonomy.ts`).
- Los posts son HTML estáticos alojados bajo `app/public/library/`; el repositorio contiene decenas de directorios de contenido y una tabla `library_docs` que actúa como índice (`supabase/migrations/20260608134300_create_library_docs.sql`).
- La Biblioteca es también el destino de las lecturas recomendadas de Consulta IA (`app/src/components/ConsultaIaScreen.tsx:384-399`).

## 4. Capacidades actuales para profesionales (B2B)

### 4.1 Shell y navegación

El profesional dispone de Panel, Agenda, Clientes, Casos, Consulta IA, Biblioteca, Informes y Ajustes (`app/src/constants/proNav.ts:29-55`). Puede entrar también en las pantallas compartidas de plan y sesión para ver y operar el mismo flujo que ve el cliente (`app/src/app/_layout.tsx:103-105`).

### 4.2 Panel operativo

El Panel obtiene datos reales de planes, citas, perros y sesiones; no es una maqueta (`app/src/components/pro/panel/usePanelData.ts:102-155`). Muestra:

- casos activos;
- citas del día;
- sesiones de entrenamiento completadas durante la semana;
- casos que requieren atención;
- agenda del día.

Fuentes: `app/src/components/pro/panel/usePanelData.ts:91-95,193-224` y `app/src/app/(pro)/panel.tsx`.

“Requiere atención” se calcula si la última actividad refleja alguna de estas señales:

- éxito superior al 80 % con señales de estrés;
- meseta de tres sesiones del mismo paso con varianza inferior a 0,01;
- última sesión por debajo del 50 %.

Fuente: `app/src/components/pro/panel/attentionRules.ts:25-28,42-84`.

Matiz importante: el indicador llamado “deberes esta semana” cuenta sesiones `training` completadas. No existe un tipo de sesión específico “deberes en casa” distinto de la sesión normal; el código lo documenta como aproximación (`app/src/components/pro/panel/usePanelData.ts:16-21,124-130`). La landing puede hablar de sesiones reportadas o práctica reportada, pero no debe sugerir un subsistema independiente de asignación de deberes si no se explica esta equivalencia.

### 4.3 CRM de clientes y casos

- Alta de clientes con nombre, email, teléfono, origen y notas (`app/src/app/(pro)/clientes/nuevo.tsx:21-58`).
- Listado, búsqueda, recuento de perros, casos activos, estado de vinculación y última actividad (`app/src/app/(pro)/clientes/index.tsx:53-70,213-260`).
- Ficha editable con datos de contacto, perros/casos, alta de caso, cita, invitación e informe (`app/src/app/(pro)/clientes/[id].tsx:1-34,65-115`).
- Vista de Casos construida con perros, planes, sesiones, citas y clientes (`app/src/components/pro/clientCaseData.ts:105-172`; `app/src/app/(pro)/casos/index.tsx`).
- Creación de un perro/caso bajo la cuenta del dueño cuando existe vinculación, protegida por RLS (`app/src/components/pro/clientCaseData.ts:179-199`; `supabase/migrations/20260813140000_pro_creates_dogs_for_linked_clients.sql:13-32`).
- Asociación inicial cliente–caso mediante una cita de apertura (`app/src/components/pro/clientCaseData.ts:207-232`).

Limitación de modelo: `dogs` todavía no contiene `client_id`; la relación caso–cliente se deriva de `appointments` (`app/src/components/pro/clientCaseData.ts:3-21`; `app/src/app/(pro)/clientes/[id].tsx:3-6`). Funciona para el flujo actual, pero no se debe presentar como un CRM relacional maduro o como una arquitectura multi-organización.

### 4.4 Vinculación profesional–dueño

Existen dos caminos:

- el profesional invita a un cliente mediante un enlace con token;
- el dueño introduce el código de conexión del profesional y este aprueba o rechaza la solicitud.

La invitación se crea en `app/src/services/invitations.ts:25-43` y se acepta en la ruta pública `app/src/app/(public)/invitacion/[token].tsx`. Las solicitudes Owner→Pro se gestionan en `app/src/services/connections.ts:62-81` y se muestran con acciones aprobar/rechazar en `app/src/app/(pro)/clientes/index.tsx:175-209`.

Las migraciones protegen la operación: el dueño solo puede apuntar a un perfil profesional y la aprobación queda acotada al profesional autenticado (`supabase/migrations/20260805130100_create_connection_requests.sql:109-164,198-236`). Las políticas cross-tenant permiten al profesional leer y escribir solo los perros, planes y sesiones de clientes vinculados (`supabase/migrations/20260805120100_pro_reads_linked_client_data.sql:33-65`; `supabase/migrations/20260813120000_pro_writes_linked_client_plans_sessions.sql:48-64`).

No existe envío transaccional propio: la aplicación prepara un enlace para compartir por las opciones del dispositivo; el profesional elige email, WhatsApp, SMS u otro canal (`app/src/components/pro/InviteClientModal.tsx:1-5`).

### 4.5 Agenda y modo de campo

- Agenda semanal de lunes a domingo en escritorio y vista de día en móvil (`app/src/app/(pro)/agenda/index.tsx:1-7,23-47,82-135`).
- Alta de citas vinculables a cliente, perro y plan (`app/src/components/pro/agenda/NewAppointmentModal.tsx:82-150`).
- Estados programada, completada, cancelada y no presentado (`app/src/components/pro/agenda/AppointmentDetailModal.tsx:34-36,118-149`).
- Al completar una cita vinculada a un plan, la aplicación busca la sesión pendiente y abre directamente el flujo de sesión (`app/src/components/pro/agenda/AppointmentDetailModal.tsx:45-70`).
- El mismo detalle de cita puede abrirse desde el Panel, permitiendo el flujo operativo de campo (`app/src/components/pro/panel/usePanelData.ts:66-80`).

No hay recordatorios push; `expo-notifications` no está instalado y el contador de citas solo sirve para la interfaz (`app/src/components/pro/agenda/useTodayAppointmentCount.ts:3-4`).

### 4.6 Ajuste profesional del plan

El profesional puede ajustar una variable concreta del paso dentro de un rango seguro y añadir una nota. La escritura se hace a través de `edit-plan-step`, no mediante una actualización directa desde el cliente (`app/src/components/pro/plan/ProStepAdjust.tsx:281,391,510`).

El alcance está deliberadamente acotado:

- modifica una sola variable elegible del paso;
- respeta límites seguros y topes de edad;
- no regenera el plan completo;
- mantiene auditoría append-only en `plan_step_edits` y el Owner puede leer los ajustes (`supabase/migrations/20260813150000_create_plan_step_edits.sql:50-98`).

No se puede prometer edición libre de cualquier campo ni un editor visual completo del protocolo. Esa alternativa fue descartada o diferida (`docs/decisions/ADR-008-pro-plan-editing-scope.md`; `docs/decisions/ADR-013-pro-step-variable-editing.md:220`).

### 4.7 Informes profesionales

- Selector de caso y carga de datos reales de cliente, perro, plan, progreso y sesiones (`app/src/app/(pro)/informes.tsx:4-7,116-161`; `app/src/components/pro/informes/reportData.ts:66-108,292-358`).
- Desglose por sesión: éxito, señales de estrés, duración, entorno, notas, causa de dificultad, incidentes, indicación del paso y consejo correctivo (`app/src/components/pro/informes/reportData.ts:112-159`).
- En web se abre un documento imprimible; en móvil se genera un PDF y se ofrece compartirlo (`app/src/components/pro/informes/useReportGenerator.ts:24-60`).
- La marca del informe es el nombre del negocio en texto. No existe logo de imagen (`app/src/app/(pro)/informes.tsx:1-10`).

### 4.8 Consulta IA profesional

Usa la misma recuperación que Owner, pero el servidor decide el registro según `profiles.account_type`; la UI no puede hacerse pasar por otro perfil (`app/src/components/ConsultaIaScreen.tsx:12-19,148-153`; `supabase/functions/consulta-ia/index.ts:157-175`).

La respuesta profesional puede nombrar autores y mostrar discrepancias entre escuelas. El selector de anclaje lista perros propios y de clientes vinculados de acuerdo con RLS (`app/src/components/ConsultaIaScreen.tsx:28-35,202-215`).

## 5. Roles, permisos y autoridad de seguridad

### 5.1 Roles del producto

| Rol | Ámbito funcional |
|---|---|
| Owner | Sus perros, planes, sesiones, historial, Biblioteca, Consulta IA, perfil, conexión con profesional. |
| Professional | Suite profesional; sus clientes/citas/casos y datos de dueños vinculados; también las superficies compartidas de plan/sesión. |

No existe un tercer rol real de miembro, administrador de organización o supervisor. “Studio” es un tier comercial, no un rol de cuenta: la restricción de `account_type` solo admite `owner` y `professional` (`supabase/migrations/20260803140000_add_account_type_to_profiles.sql:1-5`).

### 5.2 Controles efectivos

- El guard de rutas impide que un Owner entre en el shell Pro (`app/src/app/_layout.tsx:85-98`).
- Los perfiles, perros, planes y sesiones del Owner están protegidos por Row Level Security y `auth.uid()` (`supabase/migrations/202604111204_create_profiles.sql:97-106`; `supabase/migrations/202604111200_create_dogs.sql:45-50`; `supabase/migrations/202604111201_create_shaping_plans.sql:103-116`; `supabase/migrations/202604111202_create_sessions.sql:54-65`).
- Clientes y citas se limitan a `professional_id = auth.uid()` (`supabase/migrations/20260803140100_create_clients_table.sql:19-25`; `supabase/migrations/20260803140200_create_appointments_table.sql:29-35`).
- El acceso de un Pro a los datos de un Owner requiere vinculación y está acotado mediante funciones/policies específicas (`supabase/migrations/20260805120100_pro_reads_linked_client_data.sql`; `supabase/migrations/20260813120000_pro_writes_linked_client_plans_sessions.sql`).
- Los hilos y turnos de Consulta IA son privados por usuario mediante RLS (`supabase/migrations/20260820213000_create_consulta_ia_threads.sql:55-82`).
- `rag-query` valida JWT o service key y `match_documents` solo concede ejecución a `service_role`, reduciendo el riesgo de exfiltración del corpus (`supabase/functions/rag-query/index.ts:194-234`; `supabase/migrations/20260703160000_lock_down_match_documents.sql:9-19`).

Limitación importante: el acceso al shell profesional se decide por `account_type`, no por `entitlements.hasProSuite`. El root guard no consulta el plan de pago (`app/src/app/_layout.tsx:85-96`). Por tanto, hoy no debe afirmarse que la Suite Pro queda técnicamente inaccesible solo por no pagar un tier Pro; el bloqueo de generación y los límites sí se resuelven aparte en entitlements.

## 6. Planes, cupos y facturación

### 6.1 Contrato de entitlements implementado

| Plan | Perros | Planes activos | Casos activos | Generaciones de plan/mes | Hilos de Consulta IA/mes | Suite Pro | Informe con marca de texto | Asientos declarados |
|---|---:|---:|---:|---:|---:|---|---|---:|
| Plus | 3 | ilimitados | 0 | 20 | 50 | No | No | 1 |
| Pro | ilimitados | ilimitados | 30 | 60 | 200 | Sí | Sí | 1 |
| Studio | ilimitados | ilimitados | ilimitados | 150 | 500 | Sí | Sí | 3 |

Fuente de verdad de los límites: `app/src/services/entitlements.ts:22-77`, espejada y comprobada contra el servidor. No existe tier gratuito perpetuo (`app/src/services/entitlements.ts:85-90`).

Prueba de siete días:

- máximo 1 perro;
- máximo 5 generaciones de plan;
- máximo 10 hilos de Consulta IA.

Fuente: `app/src/services/entitlements.ts:79-83`.

Los contadores de generación de plan y Consulta IA son independientes (`app/src/services/entitlements.ts:27-29,147-156`). Reportar sesiones no consume generaciones; el modo lectura sí impide reportar sesiones nuevas (`app/src/services/entitlements.ts:383-398`).

Los estados cancelado, incompleto, prueba vencida o periodo largamente vencido pasan a modo lectura; `past_due` tiene periodo de gracia mientras Stripe reintenta (`app/src/services/entitlements.ts:360-389`). Los datos existentes siguen consultables según el copy del módulo (`app/src/services/entitlements.ts:464-485`).

### 6.2 Precios: no tratarlos como definitivos

La interfaz contiene cifras orientativas —Plus 7,99/79; Pro 29/290; Studio 79/790—, pero el propio archivo dice que son precios **de demostración**. El precio real lo determina el `price_id` configurado en Stripe/Supabase (`app/src/constants/tiers.ts:1-6,20-67`). Tampoco debe inferirse moneda real de mercado: la UI presenta `$` (`app/src/components/billing/PricingCard.tsx:31-35`).

Conclusión: hasta que el fundador confirme catálogo, moneda, impuestos y entorno live, no se deben publicar esas cantidades como precio contractual.

### 6.3 Stripe

- Checkout web implementado, alojado por Stripe; en apps nativas el pago está explícitamente deshabilitado (`app/src/services/billing.ts:29-42`; `app/src/app/(auth)/pricing.tsx:43-49`).
- El cliente envía tier e intervalo, no identificadores de precio; el servidor resuelve el catálogo (`app/src/app/(auth)/pricing.tsx:54-69`; `app/src/services/billing.ts:14-18`).
- Webhook con verificación de firma e idempotencia implementada (`supabase/functions/stripe-webhook/index.ts:1-8`; `supabase/migrations/20260819190000_stripe_webhook_events.sql:1-38`).
- HANDOFF registra una compra de prueba Pro con `checkout.session.completed` recibido y procesado, por lo que el recorrido Checkout → webhook → `subscriptions` sí fue verificado al menos una vez (`HANDOFF.md:382-420`).
- No están verificados en el dashboard los otros tres eventos manejados por el código: actualización, eliminación y fallo de factura (`HANDOFF.md:50-57`).
- El Billing Portal tiene código, pero su propia cabecera registra que la cuenta de prueba tenía cero configuraciones y que fallaría hasta configurarlo externamente (`supabase/functions/create-portal-session/index.ts:9-19`). No se puede prometer todavía gestión autoservicio de cambio de plan, tarjeta, facturas o baja como flujo operativo confirmado.

## 7. Arquitectura y stack tecnológico

### 7.1 Cliente

| Capa | Tecnología | Evidencia |
|---|---|---|
| Framework | Expo 55 + React Native 0.83 + React 19 | `app/package.json:16-29` |
| Navegación | Expo Router 55, rutas tipadas | `app/package.json:22`; `app/app.json:33-42` |
| Web | React Native Web + Metro; export estático desplegable | `app/package.json:28`; `app/app.json:29-31`; `app/vercel.json:1-4` |
| Tipado/validación | TypeScript 5.9 + Zod | `app/package.json:29,37-39` |
| UI | Componentes React Native, Lucide, Space Grotesk y JetBrains Mono | `app/package.json:16-17,24`; `app/src/app/_layout.tsx:21-31` |
| Estado local | Context/hook propios; AsyncStorage para preferencias | `app/src/providers`; `app/src/i18n/LocaleProvider.tsx` |
| Sesión móvil | Expo SecureStore | `app/src/services/supabase.ts:1-23` |
| Impresión/archivos | expo-print + expo-sharing | `app/package.json:23,26`; `app/src/components/pro/informes/useReportGenerator.ts` |

El mismo código apunta a web, iOS y Android (`app/app.json:15-31`), pero “multiplataforma” no significa paridad completa: pago y dictado tienen límites por plataforma documentados en este informe.

### 7.2 Backend y datos

| Capa | Tecnología/uso |
|---|---|
| Backend gestionado | Supabase: Auth, Postgres, RLS y Edge Functions Deno. |
| Cliente de datos | `@supabase/supabase-js`. |
| Modelo | tablas de perfiles, perros, planes, sesiones, registros ABC, objetivos, clientes, citas, suscripciones, corpus, biblioteca, hilos/turnos de Consulta y auditorías. |
| Seguridad de datos | RLS por propietario/profesional y funciones acotadas para vinculación cross-tenant. |
| Despliegue web | Vercel mediante `expo export --platform web`. |
| Builds nativos | EAS configurado al menos para APK preview. |

Fuentes: `app/src/services/supabase.ts:6-53`, `supabase/migrations/`, `app/vercel.json:1-4`, `app/eas.json:1-11`.

Edge Functions presentes en el repositorio:

- `generate-plan`
- `process-session-report`
- `rag-query`
- `consulta-ia`
- `edit-plan-step`
- `tidy-dictation`
- `create-checkout`
- `create-portal-session`
- `stripe-webhook`

### 7.3 IA y RAG

- Proveedor único de razonamiento: Gemini, familia Flash Lite (`docs/decisions/ADR-001-claude-sonnet-only.md:1-6,50-52`).
- Modelo por defecto actual: `gemini-3.1-flash-lite`, configurable por `GEMINI_MODEL` (`supabase/functions/_shared/gemini.ts:18-20`).
- Helper común con JSON mode, validación estructural, reintentos por errores transitorios y un reintento de formato (`supabase/functions/_shared/gemini.ts:1-14,27-43,65-133`).
- Embeddings: `gemini-embedding-001`, salida de 768 dimensiones (`supabase/functions/rag-query/index.ts:7-12,31-36,82-103`).
- Vector store: PostgreSQL con pgvector y búsqueda por similitud coseno; el índice vigente está definido como HNSW (`supabase/migrations/20260511100000_enable_vector_extension.sql`; `supabase/migrations/20260701_swap_ivfflat_to_hnsw.sql:19-23`).
- RAG filtra Tier 1, aplica ponderación por tipo de fragmento, diversifica fuentes y registra consultas (`supabase/functions/rag-query/index.ts:62-73,283-349`).
- El plan usa umbral 0,55 y tolera fallo del RAG continuando sin corpus, dejando auditoría `fail_soft` (`supabase/functions/generate-plan/index.ts:469-502,1291-1324`).
- Consulta IA exige corpus para redactar; si es insuficiente lo declara (`app/src/components/ConsultaIaScreen.tsx:360-380`; `supabase/functions/consulta-ia/draft.ts`).

No describir el sistema como LangGraph en producción: el código actual orquesta el pipeline dentro de Edge Functions; las menciones a LangGraph en TSD son arquitectura futura o histórica.

### 7.4 Voz

- Dictado web con `SpeechRecognition`/`webkitSpeechRecognition`; si el navegador no lo soporta, el botón no aparece y el teclado sigue disponible (`app/src/hooks/voice/useVoiceInput.ts:1-6,28-40`).
- El audio no se sube a Supabase ni se guarda por K9; llega texto transcrito al flujo (`docs/decisions/ADR-003-voice-on-device.md:90-101`).
- En Chrome, el propio navegador puede enviar audio a Google; por ello no debe afirmarse “todo el audio se procesa localmente” en web (`docs/decisions/ADR-003-voice-on-device.md:78-80`).
- La implementación nativa STT/TTS descrita en el ADR es una decisión, pero el hook actual declara Fase A solo web y `isSupported=false` en nativo (`app/src/hooks/voice/useVoiceInput.ts:1-6`). Prometer voz nativa hoy sería incorrecto.

### 7.5 Integraciones externas reales

- Supabase Auth/Postgres/Edge Functions.
- Google Gemini API para generación y embeddings.
- Stripe para Checkout, webhooks y potencial Billing Portal.
- Vercel para web.
- Expo/EAS para builds.
- APIs de voz del navegador.

No hay integraciones operativas verificadas con calendarios externos, CRM externos, WhatsApp API, email transaccional, videollamadas, veterinarias, wearables o sistemas de gestión de clínicas.

## 8. Bienestar, seguridad y privacidad

### 8.1 Guardrails implementados

- Evaluación de banderas de riesgo al crear un plan y derivación si hay agresión, dolor, lesión, autolesión, cambio súbito o riesgo a terceros (`supabase/functions/generate-plan/index.ts:1230-1247`).
- Welfare Reviewer que inspecciona el plan y las condiciones médicas del perro antes de aprobarlo (`supabase/functions/generate-plan/welfare.ts:24-49`; persistencia en `supabase/functions/generate-plan/index.ts:1433-1512`).
- Reglas de pedagogía y bienestar: un D por vez, 80 %, recuperación hacia menor dificultad, límites de duración y evitación de flooding (`supabase/functions/generate-plan/index.ts:538-556,664-715,900-988`).
- Reporte de incidentes determinista con `SAFETY_HOLD` (`supabase/functions/process-session-report/rules.ts:71-107`).
- Consulta IA clasifica cada pregunta antes de recuperar/redactar. Si el clasificador falla, el diseño falla cerrado y deriva en vez de responder (`supabase/functions/_shared/consultaSafetyClassifier.ts:18-26,183-231,252-259`).

Lenguaje permitido: “controles de bienestar”, “detección de señales de riesgo”, “pausa y derivación”, “criterios conservadores”.  
Lenguaje no respaldado: “diagnóstico clínico”, “garantía de seguridad”, “tratamiento veterinario”, “sustituye al veterinario/etólogo/educador”, “previene todos los incidentes”.

### 8.2 Privacidad y protección técnica

- Tokens móviles en Keychain/Keystore mediante SecureStore; en web, sesión persistida en `localStorage` (`app/src/services/supabase.ts:1-23,43-52`).
- RLS para datos propios y vinculados, según §5.2.
- Consulta general sin acceso a datos del perro y anclaje explícito; no se infiere un caso desde el texto (`supabase/functions/consulta-ia/index.ts:17-22,259-281`).
- Hilos de Consulta privados por usuario mediante RLS (`supabase/migrations/20260820213000_create_consulta_ia_threads.sql:55-82`).
- RAG protegido por autenticación y RPC restringida a service role (`supabase/functions/rag-query/index.ts:194-234`; `supabase/migrations/20260703160000_lock_down_match_documents.sql:9-19`).
- No se almacena audio desde la funcionalidad de voz (`docs/decisions/ADR-003-voice-on-device.md:90-101`).

No se encontró en el repositorio un paquete legal completo de privacidad, términos, cookies, DPA/RGPD, política de retención, exportación de datos o borrado integral de cuenta. Existe borrado lógico de entidades, pero no debe confundirse con cumplimiento legal de derecho de supresión. No se puede prometer “cumplimiento RGPD completo”, “certificación”, “cifrado end-to-end” o “datos clínicos anonimizados” basándose solo en este código.

## 9. Lista precisa de funcionalidades no operativas, no verificadas o no prometibles

### 9.1 No operativas en el producto actual

1. **White-label completo.** Solo existen flags de entitlement y una TSD. No hay tabla/runtime de branding operativo, carga de logo, paleta por tenant ni sustitución integral de marca. Los informes solo usan `business_name` en texto (`app/src/app/(pro)/informes.tsx:1-10`; `docs/tsd/TSD-10-white-labeling.md:20-37`).
2. **Logo de imagen en informes.** No existen `logo_url` ni bucket de Storage para esa función (`app/src/app/(pro)/informes.tsx:7-10`).
3. **Computer Vision.** Existe la TSD-11 y el flag `hasComputerVision`, pero no una cámara, subida de vídeo, inferencia o corrección visual operativa (`app/src/services/entitlements.ts:33-35,74-75`; `docs/tsd/TSD-11-computer-vision.md`).
4. **Equipos de tres profesionales / organizaciones multiusuario.** `seats: 3` es solo un número en entitlements. No hay modelo de organización, invitación de miembros, roles internos ni administración de asientos (`app/src/services/entitlements.ts:22-35,65-75`).
5. **Dominios personalizados, plantillas de email y organización multiusuario.** La propia TSD los marca como futuros (`docs/tsd/TSD-10-white-labeling.md:34-37`).
6. **Inicio de sesión Google/Apple.** Métodos vacíos (`app/src/hooks/useAuth.tsx:169-170`).
7. **Voz nativa iOS/Android.** El hook actual es web-only (`app/src/hooks/voice/useVoiceInput.ts:1-6`).
8. **Pagos in-app nativos.** Checkout solo web (`app/src/services/billing.ts:34-42`).
9. **Historial reabrible de Consulta IA.** Los hilos se guardan, pero la pantalla no lista ni reabre hilos anteriores (`app/src/components/ConsultaIaScreen.tsx:19-21`).
10. **Notificaciones push/recordatorios.** No está instalado `expo-notifications` (`app/src/components/pro/agenda/useTodayAppointmentCount.ts:3-4`).
11. **Email transaccional de invitaciones.** Se comparte enlace mediante el dispositivo; no existe proveedor de envío propio (`app/src/components/pro/InviteClientModal.tsx:1-5`).
12. **Relación canónica `dogs.client_id`.** El CRM deriva cliente–perro de citas; es un hueco de esquema conocido (`app/src/components/pro/clientCaseData.ts:3-21`).
13. **Tipo de entidad “deberes” independiente.** Se usan sesiones `training` completadas como señal de práctica/deberes (`app/src/components/pro/panel/usePanelData.ts:16-21`).

### 9.2 Implementadas pero dependientes de configuración o verificación externa

1. **Billing Portal de Stripe.** Código listo, configuración externa ausente según la verificación registrada; no prometer autoservicio de bajas/cambios hasta probarlo (`supabase/functions/create-portal-session/index.ts:9-19`).
2. **Webhooks de renovación, cancelación e impago.** El código los maneja, pero solo `checkout.session.completed` tiene una prueba documentada contra Stripe (`HANDOFF.md:50-57,382-420`).
3. **Precios definitivos y moneda.** Los valores del frontend son de demostración (`app/src/constants/tiers.ts:1-6`).
4. **Entrega fiable de emails de confirmación.** Supabase intentó un correo a dominio corporativo, pero no llegó; falta SMTP propio (`HANDOFF.md:42-47`).
5. **Avisos visuales de impago, expiración y límite de prueba.** Están en código, pero HANDOFF los marca sin verificación visual (`HANDOFF.md:37-41,60-61`).
6. **Paridad móvil completa.** Hay configuración Expo/EAS, pero voz y compra no tienen paridad; no afirmar disponibilidad App Store/Google Play sin evidencia de publicación.

### 9.3 Afirmaciones científicas o de IA que requieren matiz

1. **“Respuestas exclusivamente científicas”** debe traducirse a “respuestas construidas a partir del corpus curado de K9”. No equivale a revisión clínica individual, consenso científico universal ni ausencia de error.
2. **Consulta IA no tiene todavía un eval set propio equivalente al de `generate-plan`.** ADR-015 declara esa deuda (`docs/decisions/ADR-015-consulta-ia-engine-scope.md:151-153`).
3. **Los cupos de Consulta son una hipótesis de producto confirmada como punto de partida, no una cifra optimizada por uso real** (`docs/decisions/ADR-015-consulta-ia-engine-scope.md:162-166`).
4. **El aumento a cuatro fragmentos por fuente no está medido con RAGAS** (`docs/decisions/ADR-015-consulta-ia-engine-scope.md:167-168`).
5. **Atribución del corpus profesional.** HANDOFF documenta metadatos de autor/título no presentables en una parte del corpus y un issue de saneamiento: no prometer atribución bibliográfica impecable hasta completar la limpieza (`HANDOFF.md:161-166,225-309`).
6. **RAG fail-soft en generación de plan.** Si el retrieval falla, el plan puede continuar sin corpus y queda auditado como tal (`supabase/functions/generate-plan/index.ts:459-502,1306-1324`). Por ello no se puede afirmar que absolutamente todos los planes están siempre “generados desde el corpus”.
7. **Resultados garantizados.** La progresión adapta criterios según reportes, pero no garantiza cambio conductual, plazo ni porcentaje de éxito individual.

### 9.4 Afirmaciones comerciales que no deben hacerse todavía

- “White-label disponible”.
- “Sube tu logo y personaliza toda la app”.
- “Hasta tres profesionales trabajando en la misma organización”.
- “Análisis automático de vídeo / visión por computador”.
- “La IA observa al perro”.
- “Diagnostica la causa del comportamiento”.
- “Sustituye al educador, etólogo o veterinario”.
- “Cumplimiento RGPD certificado/completo”.
- “Cifrado end-to-end”.
- “Disponible con compra integrada en iOS y Android”.
- “Recordatorios automáticos por push, email o WhatsApp”.
- “Integración con Google Calendar/Outlook”.
- “Precio definitivo de 7,99/29/79” sin validar catálogo live y moneda.
- “Todas las respuestas/planes usan siempre el corpus”.
- “Fuentes bibliográficas siempre limpias y completas”.
- “Billing Portal operativo” hasta configurarlo y verificarlo.

## 10. Qué sí puede prometerse con formulación prudente

| Capacidad | Formulación defendible |
|---|---|
| Planes | “Convierte un objetivo o problema observable en un plan progresivo con criterios y controles de bienestar.” |
| Adaptación | “La siguiente sesión se decide a partir de los resultados reportados, aplicando reglas de progreso, repetición o simplificación.” |
| Owner–Pro | “Dueño y profesional pueden trabajar sobre el mismo perro, plan y sesiones después de vincular sus cuentas.” |
| Señales | “El Panel destaca casos con estrés reportado, bajo éxito o posible meseta.” |
| Consulta IA | “Permite preguntar sobre el corpus de K9, de forma general o anclada a un perro/caso autorizado, con fuentes y derivación ante señales de riesgo.” |
| Informes | “Genera un informe imprimible/PDF con plan, progreso y sesiones; puede incluir el nombre del negocio como marca de texto.” |
| Biblioteca | “Biblioteca pública bilingüe de fundamentos, técnicas y protocolos.” |
| Privacidad técnica | “Los datos se aíslan mediante autenticación y políticas de acceso por usuario/vinculación.” |
| Voz | “Dictado disponible en navegadores compatibles.” |
| Seguridad | “Los casos de riesgo pueden bloquearse o pausarse y recomendar evaluación humana.” |

## 11. Riesgos y trabajos previos a una presentación formal a inversores

Estos no impiden enseñar el producto, pero deben separarse claramente entre “producto actual” y “roadmap”:

1. Confirmar catálogo live, moneda, impuestos y condiciones reales de prueba.
2. Configurar y probar Billing Portal y los tres eventos Stripe aún no verificados.
3. Decidir si Studio se ofrece ya. Hoy su promesa comercial incluye capacidades —asientos, white-label, Computer Vision— que no existen como producto.
4. Crear paquete legal mínimo: privacidad, términos, cookies, proveedores/subprocesadores, retención, exportación y borrado de cuenta.
5. Completar saneamiento de atribuciones del corpus antes de vender “fuentes impecables” al profesional.
6. Crear eval set específico de Consulta IA y registrar métricas por perfil, anclaje, seguridad, atribución e insuficiencia de corpus.
7. Resolver `dogs.client_id` o documentar formalmente la relación actual derivada de citas.
8. Decidir si “deberes” será una entidad propia o si el lenguaje de producto seguirá describiendo sesiones de práctica reportadas.
9. Validar publicación móvil y paridad deseada; hoy web es la superficie más completa.
10. Separar la oferta presente de la hoja de ruta: white-label, equipos, Computer Vision, notificaciones e integraciones externas.

## 12. Resumen ejecutivo de auditoría

El producto supera con claridad un prototipo simple: el repositorio contiene un loop Owner completo, un motor adaptativo con controles de seguridad, una suite profesional operativa, vinculación de cuentas, agenda, informes, facturación web y Consulta IA para ambos perfiles.

La diferenciación más defendible no es “una IA que da consejos”, sino la cadena integrada:

**caso → plan con criterios → práctica reportada → señales de atención/adaptación → informe**, con el profesional y el dueño trabajando sobre datos compartidos y autorizados.

Las principales zonas que no deben contaminar el discurso actual son Studio/white-label/equipos/Computer Vision, precios no confirmados, Billing Portal no configurado, voz/pagos nativos, garantías clínicas y afirmaciones absolutas de privacidad o rigor científico. Esas capacidades deben figurar como roadmap, hipótesis o dependencia pendiente, nunca como producto disponible.
