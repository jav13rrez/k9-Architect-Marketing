# K9 Behavioral Architect — Hoja de ruta documental

**Propósito:** indicar qué documentos conviene crear después de la referencia maestra, qué decisión soporta cada uno y qué evidencia debe existir antes de redactarlo como material definitivo.

## 1. Paquete disponible desde ahora

| Documento | Uso |
|---|---|
| Product Reference | Fuente común para producto, marketing, ventas, soporte e inversores. |
| Manual de Producto | Onboarding, demostraciones, formación y soporte. |
| Tech Stack y Arquitectura | Continuidad técnica y due diligence. |
| Readiness y Registro de Promesas | Control de claims, pendientes y condiciones de lanzamiento. |
| Auditoría de fuentes | Trazabilidad interna entre afirmación y evidencia del repositorio. |

Este paquete explica con rigor **qué existe**. No sustituye los documentos que demuestran demanda, tracción, economía o cumplimiento.

## 2. Documentos para lanzamiento

| Prioridad | Documento | Contenido mínimo | Insumo que falta o debe confirmarse |
|---|---|---|---|
| P0 | Messaging House | Categoría, posicionamiento, propuesta por audiencia, tres pilares de valor, pruebas y vocabulario prohibido. | Decisión final sobre catálogo y capacidad Studio. |
| P0 | Kit de lanzamiento | Copy de landings, email, notas de prensa, publicaciones, guiones de demo, capturas y ficha de producto. | URLs productivas, CTA final, consentimiento analítico y disponibilidad por plataforma. |
| P0 | FAQ pública y política de soporte | Facturación, seguridad, limitaciones, cancelación, incidencias y escalado humano. | Canal, horario y compromiso de respuesta reales. |
| P0 | Paquete legal y privacidad | Privacidad, términos, cookies, encargados, retención, derechos y descargo conductual. | Revisión jurídica competente; inventario final de tratamientos y proveedores. |
| P1 | Guías de onboarding por rol | Primer valor del dueño y del profesional, checklist y recuperación ante bloqueo. | Pruebas de usabilidad y analítica de activación. |
| P1 | Battlecards comerciales | Alternativas por segmento, objeciones, diferencias demostrables y cuándo K9 no encaja. | Investigación competitiva actualizada y entrevistas. |

## 3. Paquete para inversores

### 3.1 One-pager ejecutivo

Una página con problema, solución, público, diferenciación, estado, modelo de ingresos, hitos y petición. Puede construirse ya, pero cualquier cifra de mercado o tracción debe estar respaldada.

### 3.2 Pitch deck

Estructura recomendada:

1. Problema y cambio de mercado.
2. Producto y recorrido conectado `caso → plan → práctica reportada → atención → informe`.
3. Demostración del momento de valor.
4. Segmentos y beachhead.
5. Mercado con metodología TAM/SAM/SOM explícita.
6. Competencia y alternativa actual del usuario.
7. Modelo de negocio y precios confirmados.
8. Go-to-market.
9. Tracción y cohortes.
10. Tecnología, datos, seguridad y defensibilidad.
11. Equipo.
12. Hitos, uso de fondos y ronda.

No presentar como “moat” aquello que solo sea una lista de funciones. La defensa potencial de K9 debe argumentarse con evidencia: integración del flujo B2C–B2B, datos longitudinales consentidos, doctrina de seguridad, calidad evaluada y costes de cambio; no con el uso genérico de IA.

### 3.3 Data room de due diligence

| Carpeta | Contenido esperado |
|---|---|
| Corporate | Sociedad, cap table, pactos, propiedad intelectual y contratos clave. |
| Product | Esta documentación, roadmap priorizado, demos y registro de versiones. |
| Technology | Arquitectura, seguridad, dependencias, continuidad, pruebas y riesgos conocidos. |
| Market | Investigación, entrevistas, segmentación y modelo TAM/SAM/SOM con fuentes. |
| Traction | Usuarios, activación, retención, uso por cohorte, conversión y cancelación. |
| Finance | Histórico, presupuesto, runway, escenarios, unit economics y supuestos. |
| Legal & privacy | Términos, privacidad, encargados, DPIA si aplica y gestión de derechos. |
| Commercial | Pipeline, pilotos, contratos, LOI y evidencia de willingness to pay. |

El data room no debe contener claves, secretos, datos personales crudos ni historias clínicas/conductuales identificables innecesarias.

### 3.4 Memo de inversión

Documento narrativo más profundo que el deck: tesis, por qué ahora, aprendizaje del mercado, estrategia, riesgos, escenarios y uso de capital. Es especialmente útil cuando la ronda depende más de comprensión del producto que de una presentación breve.

## 4. Sistema de métricas que debe preceder a los claims de tracción

Definir evento, ventana y denominador antes de publicar una cifra.

| Área | Métricas iniciales |
|---|---|
| Adquisición | Visita→registro, coste por registro, fuente y segmento. |
| Activación dueño | Perro creado, plan apto generado, primera sesión y primer reporte. |
| Activación profesional | Primer cliente/caso, plan revisado, práctica recibida e informe generado. |
| Valor recurrente | Sesiones reportadas por perro activo, profesionales con casos activos, consultas útiles. |
| Retención | D7/D30, cohortes mensuales, continuidad de planes y retorno del profesional. |
| Ingresos | Trial→pago, MRR/ARR, ARPA, cancelación, expansión y recuperación de impago. |
| Calidad y seguridad | Derivaciones, `SAFETY_HOLD`, errores de citas, incidentes y tiempo de resolución. |

Hasta disponer de datos limpios no deben inventarse tasas de éxito, ahorro temporal, NPS, retención ni número de usuarios.

## 5. Cadencia de mantenimiento

- En cada release: actualizar Product Reference, Manual y Registro de Promesas.
- Mensualmente: revisar catálogo, límites, proveedores, riesgos y métricas.
- Antes de campaña: congelar una versión aprobada del Messaging House y verificar cada claim.
- Antes de hablar con inversores: fechar deck y data room; adjuntar definición y fuente a toda métrica.
- Tras un cambio material de IA, datos o seguridad: actualizar Tech Stack, ADR correspondiente y documentación legal afectada.

## 6. Orden recomendado

1. Cerrar los pendientes P0 del Registro de Promesas.
2. Confirmar planes, moneda, impuestos, Stripe live y alcance real de Studio.
3. Completar paquete legal/privacidad.
4. Implantar analítica con diccionario de eventos y consentimiento.
5. Crear Messaging House y kit de lanzamiento.
6. Recoger entrevistas, pilotos y métricas de cohortes.
7. Construir one-pager, pitch deck y data room únicamente con evidencia fechada.

