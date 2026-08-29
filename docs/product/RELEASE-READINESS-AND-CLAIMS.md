# K9 Behavioral Architect — Readiness y Registro de Promesas

**Versión:** 1.0  
**Corte de información:** 22 de agosto de 2026  
**Propósito:** impedir que intención, código o copy se conviertan en una afirmación comercial no demostrada.

## 1. Regla de decisión

Una capacidad solo puede presentarse como disponible sin salvedades cuando cumple:

```text
implementada + desplegada + verificada en su plataforma/rol + respaldada por copy exacto
```

Si falta un tramo, debe describirse como implementada pendiente de verificación, beta limitada o planificada, según corresponda.

## 2. Leyenda

| Estado | Uso permitido |
|---|---|
| **VERIFICADO** | Puede demostrarse dentro del alcance exacto comprobado. |
| **IMPLEMENTADO / VERIFICAR** | Puede enseñarse en entorno controlado; no lanzar campaña hasta prueba de producción. |
| **PARCIAL** | Comunicar únicamente la parte operativa y la plataforma verificada. |
| **PLANIFICADO** | Roadmap, nunca presente comercial. |
| **PROHIBIDO** | Afirmación falsa, no sustentada o legalmente peligrosa. |

## 3. Capacidades del producto

| Capacidad | Estado | Qué sí puede decirse | Condición pendiente / evidencia |
|---|---|---|---|
| Generación de planes por pipeline | **VERIFICADO** | Crea programas por pasos con revisión pedagógica y de bienestar. | Evitar decir que el resultado es infalible o clínicamente validado. Código y pruebas en `generate-plan`; historial de producción en `HANDOFF.md`. |
| Regla de progresión por sesiones | **VERIFICADO** | El resultado registrado puede avanzar, repetir, reducir dificultad, dividir, cambiar o pausar. | Decir “por encima del 80 %”, no “80 % o más”. |
| Guard de seguridad en sesión | **VERIFICADO en código/pruebas** | Incidentes explícitos pueden pausar el plan y derivar. | Mantener pruebas y verificar UX de cada categoría en producción antes de una demostración pública crítica. |
| Welfare Reviewer con veto | **VERIFICADO con gate condicionado** | Cada plan final pasa por revisión de bienestar y puede ser rechazado. | Los golden masters se omiten si CI no dispone de `GEMINI_API_KEY`; monitorizar que el secret siga activo. |
| Experiencia del dueño web | **VERIFICADO/PARCIAL** | Hoy, planes, sesiones, historial, Biblioteca y perfil existen en la aplicación web. | Repetir smoke test del flujo completo tras cambios de lanzamiento. |
| Panel, clientes, casos y agenda Pro | **VERIFICADO** | Gestión de casos, agenda interna y panel de atención. | No afirmar sincronización con calendarios externos. |
| Vinculación dueño–profesional | **VERIFICADO** | Invitación y solicitud por código con consentimiento; seguimiento conectado. | No prometer adopción o cumplimiento del cliente. |
| Creación de perro/plan por Pro para dueño vinculado | **VERIFICADO** | El profesional puede iniciar el caso dentro de la relación autorizada. | Mantener revisión RLS al cambiar schema. |
| Ajuste profesional del paso | **VERIFICADO** | Ajustes permitidos dentro de rangos seguros, notas y auditoría. | Evitar “edita cualquier parte del plan”. |
| Informes PDF | **VERIFICADO** | Informe con marca textual del negocio y desglose de sesiones. | No decir “con tu logo” si se entiende imagen; no white-label. |
| Stripe Checkout | **VERIFICADO solo para un flujo Pro** | Existe compra, reconciliación y acceso posterior en la prueba realizada. | Probar los otros cinco precios y mensual/anual por rol. |
| Portal de facturación | **IMPLEMENTADO / BLOQUEADO POR CONFIGURACIÓN** | Existe integración técnica para abrir Stripe Billing Portal. | Crear/configurar el portal en Stripe y completar una sesión real; la configuración externa no está demostrada. |
| Estados trial/activa/exenta/lectura | **IMPLEMENTADO; parte verificada** | Prueba, suscripción, exención y modo lectura tienen reglas de servidor. | Verificar visualmente banners de checkout, impago, vencimiento y límite de prueba. |
| Eventos Stripe posteriores | **IMPLEMENTADO / VERIFICAR** | El webhook maneja actualización, cancelación e impago. | Confirmar en dashboard que los tres están suscritos y probarlos; solo `checkout.session.completed` tiene evidencia real. |
| Consulta IA Pro | **IMPLEMENTADO / VERIFICAR PRODUCCIÓN** | Código, persistencia, anclaje, seguridad, fuentes y redacción profesional existen. | Confirmar migraciones y función desplegadas; ejecutar smoke test con caso real. |
| Consulta IA Dueño | **IMPLEMENTADO / VERIFICAR PRODUCCIÓN** | Mismo motor con voz de K9 y anclaje a perro. | Confirmar ruta, permisos, cupo y derivación en producción. |
| Historial navegable de Consulta IA | **NO IMPLEMENTADO EN UI** | Los hilos y turnos se persisten en base de datos. | Crear listado, reapertura y estados de carga/error antes de prometer un archivo de consultas. |
| Biblioteca pública bilingüe | **VERIFICADO/PARCIAL** | Catálogo público con taxonomía y contenidos ES/EN disponibles. | No todos los documentos tienen necesariamente ambas traducciones; mantener fallback visible. |
| Dictado y lectura web | **PARCIAL** | Voz disponible en navegadores compatibles y limpieza del dictado. | Compatibilidad desigual; siempre ofrecer texto. |
| Voz nativa iOS/Android | **PLANIFICADO** | Arquitectura definida. | Añadir dependencias nativas, permisos, builds y pruebas en dispositivos. |
| Aplicación iOS/Android pública | **NO DEMOSTRADO** | El código usa Expo y tiene identificadores nativos. | Compilar, firmar, publicar y verificar fichas de tienda antes de decir “disponible”. |

## 4. Planes y facturación: qué anunciar

### Catálogo comunicable tras verificación final

- Plus: 7,99 €/mes o 79 €/año; 3 perros; 20 generaciones; 50 hilos de Consulta IA.
- Pro: 29 €/mes o 290 €/año; 30 casos; 60 generaciones; 200 hilos.
- Estudio: 79 €/mes o 790 €/año; casos ilimitados; 150 generaciones; 500 hilos.
- Prueba: 7 días sin tarjeta; 1 perro, 5 generaciones y 10 hilos.
- Reportes sin límite mientras la cuenta permita reportar.
- Modo lectura al terminar.

### Desalineación interna que debe corregirse

`app/src/constants/tiers.ts` presenta en Estudio “hasta 3 asientos”, “White-label” y “Computación avanzada”. Los entitlements también contienen flags/asientos. Sin embargo, no existe una experiencia real de equipo, personalización white-label ni visión por computador. Esos textos/flags son planificación o configuración futura, no producto entregado.

Antes del lanzamiento debe elegirse una de dos opciones:

1. ocultar esas características en toda UI comercial; o
2. construirlas y verificarlas.

No basta con que el entitlement sea `true`.

## 5. Funcionalidades que no se pueden prometer todavía

### Producto y plataforma

- Aplicación descargable y operativa en App Store o Google Play.
- Dictado/lectura por voz nativos en iOS y Android.
- Sincronización con Google Calendar, Apple Calendar u Outlook.
- Invitaciones de calendario al cliente.
- Análisis de vídeo, cámara, postura o visión por computador.
- White-labeling completo.
- Carga de logotipo de imagen; hoy solo existe nombre del negocio en texto.
- Gestión real de equipos, tres asientos o usuarios adicionales.
- Soporte prioritario como servicio operacional definido.
- Notificaciones push masivas o automatizaciones transaccionales de marketing.
- Comunidad, foro, marketplace o directorio público de profesionales.
- Procesamiento sin conexión/offline completo.
- Correos transaccionales propios para invitaciones, recordatorios o seguimiento; la invitación actual se comparte por el canal que elige el profesional.
- Inicio de sesión con Google o Apple; los manejadores actuales no tienen implementación.
- Compra o gestión completa de la suscripción dentro del cliente iOS/Android; Checkout funciona en web y el portal depende de configuración externa.
- Historial explorable y reapertura de conversaciones anteriores de Consulta IA.
- Un subsistema independiente de deberes con asignaciones, plazos y recordatorios; hoy el seguimiento se basa en sesiones de práctica reportadas.

### Resultados y seguridad

- Curación, rehabilitación garantizada o eliminación de una conducta.
- Resultados en un plazo concreto.
- Tasa de éxito propia de K9.
- Que la IA nunca se equivoca o que hace imposible un consejo dañino.
- Sustitución de veterinario, etólogo clínico o profesional presencial.
- Diagnóstico médico, veterinario o psicológico.
- Que “cumple RGPD” como conclusión legal cerrada.
- Que “los datos clínicos están cifrados” sin precisar proveedor, tránsito/reposo y revisión técnica/legal.
- Que todo el audio se procesa exclusivamente en el dispositivo; la Web Speech API puede depender del navegador o de su proveedor.
- Que todos los planes usan siempre corpus recuperado: el RAG del generador es fail-soft.
- Que todas las citas de Consulta IA son completas o correctas hasta terminar saneo y verificación.

### Negocio y prueba social

- Número de usuarios, clientes o profesionales activos.
- Testimonios, valoraciones, premios, prensa o logos de clientes no aportados.
- Ahorro promedio de 4–6 horas semanales.
- Que un informe tarda 45 segundos.
- Que el profesional medio gestiona 25–40 casos.
- Mejora de adherencia, retención o resultados atribuible a K9.
- CAC, LTV, churn, conversión o ingresos sin datos reales.
- Efecto de red probado por la vinculación.
- Tamaño de mercado propietario no respaldado por metodología y fuente.

Esas cifras pueden emplearse como hipótesis de investigación o ejemplos claramente marcados, nunca como resultados de K9.

## 6. Claims seguros y redacción recomendada

| Tema | Seguro | Evitar |
|---|---|---|
| Motor | “Convierte el caso en un programa por pasos con criterios observables.” | “Diagnostica y cura el problema.” |
| Adaptación | “Usa los reportes para decidir el siguiente ajuste.” | “Se adapta perfectamente a cada perro.” |
| Bienestar | “Puede pausar o derivar cuando detecta señales definidas de riesgo.” | “Garantiza que nunca ocurrirá daño.” |
| Profesional | “El profesional revisa y conserva el criterio.” | “La IA sustituye al adiestrador.” |
| Corpus | “Consulta un corpus especializado y muestra fuentes disponibles.” | “Todas las respuestas están científicamente demostradas.” |
| Informes | “PDF con el nombre de tu negocio.” | “Informe completamente personalizado con tu logo.” |
| Colaboración | “El reporte del dueño aparece en el caso vinculado.” | “Tus clientes harán los deberes.” |
| Suscripción | “Prueba de 7 días sin tarjeta y modo lectura al terminar.” | “Gratis” sin explicar duración y límites. |
| Plataforma | “Aplicación web construida con arquitectura Expo multiplataforma.” | “Disponible en iOS y Android” antes de tienda/build verificado. |

## 7. Pendientes de lanzamiento no funcionales

1. Políticas reales de privacidad y términos enlazados.
2. Revisión jurídica de tratamiento de datos, consentimiento y claims.
3. Banner/gestión de cookies si se instalan píxeles.
4. Analítica de producto y conversiones; Meta Pixel/Google Ads solo con consentimiento adecuado.
5. SMTP propio para mejorar entrega de correos de confirmación en dominios corporativos.
6. Prueba social real.
7. Canal y procedimiento de soporte/incidentes.
8. Política de respuesta ante incidentes de IA o acceso a datos.
9. Flujo visible de eliminación de cuenta y ejercicio de derechos; no se ha encontrado una experiencia completa en la interfaz actual.

## 8. Checklist para aprobar una afirmación

Antes de publicar cualquier página, anuncio, dossier o pitch:

- [ ] La afirmación corresponde al rol y plataforma correctos.
- [ ] Existe en código actual.
- [ ] Está desplegada.
- [ ] Se ha probado el flujo completo, no solo una pantalla.
- [ ] No depende de un flag sin experiencia asociada.
- [ ] La cifra tiene fuente, fecha y metodología.
- [ ] La redacción no convierte una salvaguarda en garantía absoluta.
- [ ] La afirmación sanitaria/legal ha sido revisada cuando corresponde.
- [ ] La landing, pricing interno y documentación dicen lo mismo.
- [ ] Se ha registrado la evidencia que permite cambiar su estado.

## 9. Condiciones de salida de los principales pendientes

| Pendiente | Se considera cerrado cuando… |
|---|---|
| Consulta IA | Dueño y Pro completan en producción: hilo general, anclado, repregunta, fuentes, insuficiencia, bandera roja y cupo. |
| Stripe completo | Los seis precios compran el tier/intervalo correcto y se prueban actualización, cancelación e impago. |
| Portal de Stripe | Existe una configuración activa de Billing Portal y una cuenta con customer real abre y vuelve correctamente. |
| Voz nativa | STT/TTS funcionan en builds firmados de iOS y Android con permisos, fallback y pruebas en dispositivo. |
| Apps nativas | Builds de producción aprobados y fichas públicas accesibles. |
| White-label | Configuración real cambia marca en superficies definidas y existe aislamiento por organización. |
| Equipos | Invitación, roles, baja, permisos y facturación de asientos funcionan de punta a punta. |
| Visión | Modelo, consentimiento, precisión, límites y experiencia están implementados y validados. |
| RGPD/legal | Políticas, contratos/proveedores, base jurídica, derechos y cookies revisados por profesional competente. |
| Claims de resultados | Estudio o datos de producto con metodología válida respaldan exactamente el claim. |

## 10. Evidencia primaria

- Estado reciente: [`HANDOFF.md`](../../HANDOFF.md), [`PROGRESS.md`](../../PROGRESS.md).
- Promesas actuales de landing: [`app/public/landing`](../../app/public/landing/).
- Planes y flags: [`tiers.ts`](../../app/src/constants/tiers.ts), [`entitlements.ts`](../../app/src/services/entitlements.ts).
- Voz: [`useVoiceInput.ts`](../../app/src/hooks/voice/useVoiceInput.ts), [`useVoiceOutput.ts`](../../app/src/hooks/voice/useVoiceOutput.ts), [`app/package.json`](../../app/package.json).
- Consulta IA: [`ADR-015`](../decisions/ADR-015-consulta-ia-engine-scope.md), [`consulta-ia/index.ts`](../../supabase/functions/consulta-ia/index.ts).
- Informes: [`reportHtml.ts`](../../app/src/components/pro/informes/reportHtml.ts).
- Checklist de tráfico: [`landing/README.md`](../../app/public/landing/README.md).
