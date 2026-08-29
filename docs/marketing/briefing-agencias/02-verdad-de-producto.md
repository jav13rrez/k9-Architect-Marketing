# 02 · Verdad de producto

**Lectura obligatoria. Este es el documento anti-invención.**
Hermanos: [01 · Plataforma](01-plataforma-de-marca.md) · [06 · Claims](06-claims-y-guardrails.md)

> Si vas a escribir un guion, un titular o una pantalla de producto, **este documento manda sobre tu intuición.** Casi todo el trabajo publicitario rechazado en esta categoría se rechaza porque describe un producto que no existe.

---

## 1. El bucle central

Todo lo que hace K9 es esto, y nada de esto es opcional en la narrativa:

```text
describir el caso
   → formular una hipótesis funcional
      → construir un programa por pasos
         → ejecutar y reportar una sesión
            → decidir el siguiente ajuste
               → conservar el historial
```

En la experiencia profesional se amplía:

```text
caso → plan revisable → práctica reportada por el dueño
     → señal de atención → informe
```

**Si tu idea no toca este bucle, no está hablando de K9.**

## 2. Qué ocurre exactamente cuando se genera un plan

Una cadena de responsabilidades, no «una IA»:

| Paso | Qué hace |
|---|---|
| Interaction Agent | Convierte la descripción informal en observación estructurada y repregunta si falta información |
| Assessment Agent | Formula la hipótesis funcional y decide si el caso sigue, necesita observación o exige derivación |
| Shaping Planner + Step Builder | Diseñan la estructura y los pasos |
| Validación determinista | Comprueba reglas que no pueden depender de la variabilidad de un modelo |
| Juez pedagógico | Revisa reglas adicionales |
| **Welfare Reviewer** | Revisa el plan final **y puede vetarlo** |

Consulta además un corpus especializado. **Aviso importante:** la recuperación del corpus es *fail-soft* — puede fallar y dejar que el proceso continúe. **Está prohibido afirmar que todos los planes se apoyan siempre en fragmentos recuperados.**

## 3. La regla de progresión — el corazón del producto

Después de cada sesión reportada, el sistema decide. La regla está implementada y es determinista:

| Resultado registrado | Decisión |
|---|---|
| Éxito **por encima del 80 %**, sin estrés | Avanzar |
| Éxito entre 50 % y 80 % | Repetir para consolidar |
| Menos del 50 % **con** una dificultad excesiva identificable | **Reducir una dimensión** |
| Menos del 50 % sin esa señal | Dividir el paso |
| Tres sesiones con varianza mínima | Cambiar estrategia o escalar |
| Estrés con éxito alto | **No avanzar** |
| Agresión con daño, posible dolor médico o estrés incapacitante | **Pausar y derivar** |

**Para guionistas:** esta tabla es una mina. Es lo único que ningún competidor puede enseñar en pantalla, y contiene la idea más contraintuitiva del producto: **el sistema puede decidir retroceder, y eso es un acierto, no un fallo.**

**Precisión obligatoria:** el umbral técnico es `> 0.8`, estrictamente mayor. Se escribe **«por encima del 80 %»**. Nunca «80 % o más» ni «≥ 80 %».

## 4. Las tres D

Distancia, duración y distracción. **Solo una puede aumentar a la vez.** Es el principio «una dificultad cada vez». Es correcto y deseable usarlo en comunicación: es concreto, visual y verdadero.

## 5. Los tres mecanismos de seguridad

Son **tres cosas distintas** y no deben mezclarse en una pieza técnica. Operan en momentos y entradas diferentes:

| Mecanismo | Cuándo actúa | Qué hace |
|---|---|---|
| **Welfare Reviewer** | Sobre un plan ya generado | Puede **vetarlo** |
| **Guard de sesión** | Sobre un incidente reportado en una sesión | **Pausa** el plan (`SAFETY_HOLD`) |
| **Bandera roja de Consulta IA** | Sobre el texto de una consulta | **Detiene la respuesta y deriva** |

Los tres están verificados en código y pruebas. **Son el activo comunicativo más potente y menos explotado del producto.**

## 6. Qué ve el dueño

- **Hoy:** la siguiente práctica disponible y el estado reciente del perro.
- Crear un plan describiendo la conducta por escrito o, donde esté soportado, por voz.
- **Reportar una sesión:** resultado, intentos, duración, lugar, señales de estrés, causa de fallo y notas.
- Historial de planes y sesiones. Los ajustes del profesional aparecen diferenciados.
- Vincularse con un profesional aceptando invitación o introduciendo su código, **siempre con consentimiento**.

## 7. Qué ve el profesional

- **Panel** con casos activos, citas del día, prácticas reportadas y **señales de atención**: estrés reciente, estancamiento y resultados bajos.
- Clientes y casos: cliente, perro, plan, sesiones e citas conectados.
- **Agenda interna** semanal con citas tipadas. **No se sincroniza con Google, Apple ni Outlook.**
- **Ajuste del paso:** puede editar distancia, duración o distracción de pasos **todavía no ejecutados**, dentro de un rango seguro, con topes por edad. Añade notas por paso. Todo deja **auditoría**: valor original, valor editado, actor y fecha.
- **No puede** modificar libremente umbral de éxito, repeticiones ni nivel de ayuda si eso rompe las invariantes del motor.
- **Informe PDF** generado desde el historial, con el **nombre del negocio en texto**.

## 8. Consulta IA

Motor separado del generador de planes.

- Consulta general, o hilo anclado a un perro o caso concreto.
- Responde desde el corpus y **muestra fuentes disponibles**.
- Redacción distinta por perfil: una dirección clara para el dueño; respuesta atribuida con desacuerdos visibles para el profesional.
- Una bandera roja detiene la respuesta y deriva.
- **No modifica el expediente, ni el plan, ni la progresión.**

**Estado:** implementada en código para ambos roles, **pendiente de verificación en producción**. Y en la UE activa obligaciones de transparencia de IA. **No se puede convertir en el eje principal de una campaña hoy.** Ver [06 · §4](06-claims-y-guardrails.md).

## 9. Glosario para guion y copy

| Término | Qué significa |
|---|---|
| **Caso** | Unidad profesional que conecta cliente, perro, objetivo, plan y seguimiento |
| **Plan de moldeamiento** | Secuencia graduada de pasos con criterios observables |
| **Sesión** | Ejecución y registro de un paso |
| **Regla del 80 %** | La política determinista de la §3 |
| **Three Ds** | Distancia, duración, distracción |
| **Meseta** | Tres resultados recientes del mismo paso con varianza por debajo del umbral |
| **`SAFETY_HOLD`** | Pausa del plan por incidente de seguridad reportado |
| **Modo lectura** | Al terminar prueba o suscripción, los datos siguen visibles; no se generan cosas nuevas |
| **Anclaje** | Perro o caso elegido explícitamente para dar contexto a una consulta |

## 10. Planes y precios

| Plan | Para | Precio mostrado | Perros | Casos | Planes/mes | Hilos IA/mes |
|---|---|---:|---:|---:|---:|---:|
| Plus | Dueño | 7,99 €/mes · 79 €/año | 3 | — | 20 | 50 |
| Pro | Profesional | 29 €/mes · 290 €/año | ilimitados | 30 | 60 | 200 |
| Estudio | Profesional | 79 €/mes · 790 €/año | ilimitados | ilimitados | 150 | 500 |

Prueba de 7 días sin tarjeta: 1 perro, 5 generaciones y 10 hilos.

> ⚠️ **Estas cifras NO se publican todavía.** Solo hay evidencia de compra verificada para un flujo Pro. Ninguna pieza creativa puede mostrar precios ni condiciones de prueba sin autorización expresa. Ver [06 · §5](06-claims-y-guardrails.md).

---

# 11. Lo que K9 NO hace · leer dos veces

Esta lista existe porque cada punto ha aparecido en algún borrador creativo de esta categoría. **Ninguna de estas cosas puede aparecer, insinuarse ni sugerirse visualmente.**

### Plataforma

- ❌ **No hay app en App Store ni Google Play.** Es una **aplicación web**. Prohibidos los badges de tienda, las pantallas de descarga y los planos de alguien descargándola.
- ❌ No hay voz ni dictado nativo en iOS/Android. Solo web, en navegadores compatibles.
- ❌ No sincroniza con Google Calendar, Apple Calendar ni Outlook. No envía invitaciones de calendario.
- ❌ No hay procesamiento sin conexión.
- ❌ No hay inicio de sesión con Google ni con Apple.

### Producto

- ❌ **No analiza vídeo, cámara, postura ni visión por computador.** Nada de un móvil apuntando a un perro y una IA leyéndolo. Es el error creativo más frecuente de la categoría.
- ❌ No hay logotipo de imagen en los informes. Solo el **nombre del negocio en texto**. No hay white-label.
- ❌ No hay gestión de equipos, asientos ni usuarios adicionales.
- ❌ No hay comunidad, foro, marketplace ni directorio público de profesionales.
- ❌ No hay sistema de deberes con asignación, vencimiento y recordatorios.
- ❌ No hay historial navegable de conversaciones anteriores de Consulta IA.
- ❌ No hay correos transaccionales propios de invitación ni recordatorio.

### Resultados

- ❌ **No cura, no rehabilita, no elimina una conducta.**
- ❌ No promete resultados en un plazo. Ni «7 días», ni «un mes», ni «pronto».
- ❌ No tiene una tasa de éxito propia. No existe. No se puede inventar.
- ❌ No garantiza que la IA no se equivoque.
- ❌ **No sustituye al veterinario, al etólogo clínico ni al profesional presencial.**
- ❌ No diagnostica.

### Negocio

- ❌ No hay usuarios, clientes ni profesionales activos que se puedan citar.
- ❌ No hay testimonios, valoraciones, premios, prensa ni logos de clientes.
- ❌ No hay ahorro medio de horas, ni tiempo de generación de informe, ni número medio de casos.
- ❌ No hay tracción, retención ni efecto de red demostrados.

> **Regla final:** ante la duda sobre si algo existe, **asume que no** y pregunta. Es más barato que rehacer una producción.
