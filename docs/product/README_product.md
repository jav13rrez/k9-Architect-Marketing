# K9 Behavioral Architect — Documentación maestra de producto

**Corte de información:** 22 de agosto de 2026  
**Propietario del documento:** fundador / Product Owner  
**Regla de uso:** una especificación describe intención; el código demuestra implementación; una prueba en producción demuestra disponibilidad.

## Qué documento usar

| Documento | Audiencia principal | Responde a |
|---|---|---|
| [Product Reference](./PRODUCT-REFERENCE.md) | Producto, marketing, ventas, soporte, inversores y futuros agentes | Qué es K9, para quién existe, qué hace, cómo se relacionan sus módulos y cuáles son sus reglas. |
| [Manual de Producto](./PRODUCT-MANUAL.md) | Usuarios, soporte, onboarding, demos y equipo comercial | Cómo se utiliza el producto de extremo a extremo y qué puede esperar cada perfil. |
| [Tech Stack y Arquitectura](./TECH-STACK.md) | Ingeniería, due diligence técnica e inversores técnicos | Cómo está construido, dónde viven los datos, cómo fluye la IA y cómo se despliega y verifica. |
| [Readiness y Registro de Promesas](./RELEASE-READINESS-AND-CLAIMS.md) | Fundador, marketing, legal, ventas e inversores | Qué puede afirmarse, qué necesita una salvedad y qué no puede prometerse todavía. |
| [Hoja de ruta documental](./DOCUMENTATION-ROADMAP.md) | Fundador, lanzamiento y fundraising | Qué crear después: messaging, legal, métricas, pitch deck y data room, y qué evidencia exige cada pieza. |
| [Auditoría de fuentes](./product-source-audit.md) | Mantenimiento interno | Evidencia primaria del repositorio que respalda esta documentación. |

## Jerarquía de fuentes

Cuando dos documentos discrepen, usar este orden:

1. Evidencia reciente de producción registrada en `HANDOFF.md` o una verificación equivalente reproducible.
2. Código y migraciones actuales.
3. ADR vigente.
4. TSD vigente.
5. `PROGRESS.md` y documentación de marketing.
6. TSD o planes históricos sustituidos.

`TSD-00` conserva planes históricos de febrero de 2026 que ya no representan necesariamente el sistema construido. No debe utilizarse como prueba de disponibilidad.

## Estados documentales

- **VERIFICADO:** existe evidencia de comportamiento real o verificación explícita.
- **IMPLEMENTADO:** existe en el código actual, pero falta evidencia de producción suficiente.
- **PARCIAL:** solo una plataforma, rol o tramo del flujo está operativo o verificado.
- **PLANIFICADO:** existe diseño, TSD, ADR, flag o texto, pero no una experiencia completa utilizable.
- **NO PROMETER:** no debe aparecer como capacidad disponible hasta superar su condición de salida.

## Mantenimiento

Actualizar primero `RELEASE-READINESS-AND-CLAIMS.md` cuando cambie una capacidad. Después propagar el cambio a los otros documentos y a las landings. Nunca mover una capacidad a **VERIFICADO** únicamente porque exista una rama, un TSD, una migración o un flag de entitlement.
