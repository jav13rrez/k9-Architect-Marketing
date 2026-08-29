# 07 · Entregables y especificaciones

**Referencia para producción, posproducción y tráfico.**
Hermanos: [04 · Dirección de arte](04-direccion-de-arte.md) · [05 · Exterior](05-exterior-y-grafica-estatica.md) · [08 · Proceso](08-proceso-y-evaluacion.md)

> ⚠️ Las plataformas cambian especificaciones sin previo aviso. Aquí se fijan **ratios, duraciones y criterios duraderos**. Todo lo marcado `[VERIFICAR]` debe confirmarse en la interfaz del gestor de anuncios antes de exportar el lote final.

---

## 1. Principio de entrega

> **Se recompone, no se recorta.**

Un 9:16 no es un 16:9 con los lados cortados. Cada ratio se compone: el texto, el aire y el punto focal cambian. Se entrega un máster por ratio, no un máster con crops automáticos.

Corolario para rodaje: **encuadrar en open gate pensando en las tres reencuadres desde el storyboard**, no descubrirlo en montaje.

---

## 2. Audiovisual

### 2.1 Másteres

| Entregable | Especificación |
|---|---|
| Máster de conservación | 4K o superior, open gate, sin quemar textos, sin subtítulos, sin música |
| Máster de emisión | 2.39:1 o 16:9 según pieza, ProRes 422 HQ o superior |
| Máster limpio (*clean*) | Sin ningún texto en pantalla, para versiones de idioma |
| Máster con textos | Español |
| Máster con textos EN | Inglés, si el lote lo incluye |
| Archivos de subtítulos | `.srt` **y** `.vtt`, revisados a mano |
| Stems de audio | Diálogo / foley / ambiente / música, separados |
| Proyecto de montaje y grafismo | Entregable al cierre, con fuentes y assets |

### 2.2 Duraciones

Toda idea del Lote A debe existir en estas cinco:

```text
60 s   máster de marca
30 s   segunda emisión y digital premium
20 s   in-stream y social
15 s   social y pre-roll
 6 s   bumper — una idea, sin voz
```

**Regla de reducción:** el 6 s no es el 60 s acelerado. Es **un solo plano y una sola frase**. Si el concepto no sobrevive a 6 segundos, no es un concepto de campaña.

### 2.3 Ratios

| Ratio | Uso principal |
|---|---|
| **2.39:1** | Máster de cine y marca |
| **16:9** | YouTube, display de vídeo, pantallas |
| **9:16** | Reels, TikTok, Shorts, Stories |
| **4:5** | Feed de Meta |
| **1:1** | LinkedIn, X, feed cuadrado |

### 2.4 Texto y seguridad

- **Subtítulos quemados** en todas las versiones sociales. Corregidos manualmente, **dos líneas máximo**.
- **Texto crítico dentro del 80 % central** en 9:16 y 4:5: la interfaz de cada plataforma tapa bordes.
- **La pieza se entiende sin sonido.** Es criterio de aprobación, no una mejora.
- Ningún rótulo por debajo de **28 px en máster 4K**.

### 2.5 Audio

- Difusión europea: normalización a **EBU R128** `[VERIFICAR]` con el emisor.
- Plataformas digitales: normalizan por su cuenta. **No comprimir de más buscando volumen**: las piezas de esta marca son dinámicamente bajas por diseño y la compresión destruye el efecto.
- Entregar **estéreo y 5.1** cuando la pieza sea de emisión.
- **Música original o con licencia comercial verificada.** No se usa librería con parecido reconocible a un autor identificable.

---

## 3. Social de pago · por red

Un sistema por red, en su lenguaje nativo. **No la misma pieza recortada cinco veces.**

| Red | Formatos | Duraciones | Trabajo | Notas |
|---|---|---|---|---|
| **YouTube** | 16:9, 9:16 | 6 / 15 / 20 / 45 s | B2B principal | Idea completa antes del segundo 5. Ver nota §3.1 |
| **Meta** (IG/FB) | 9:16, 4:5, 1:1 | 15 / 25 / 40 s | B2C y B2B | Reels con subtítulos y versión promocionable |
| **TikTok** | 9:16 | 25 / 40 s | Descubrimiento por problema | Lenguaje nativo, no anuncio recortado. Música propia o librería comercial |
| **LinkedIn** | 1:1, 16:9, documento | 30 / 60 s + carrusel PDF | Autoridad B2B | Admite razonamiento largo. No usar como repositorio de anuncios |
| **X** | 16:9, 1:1 | 15 / 30 s | Conversación profesional | Tesis compacta |

### 3.1 Nota sobre YouTube en canales profesionales

Es el emplazamiento **más valioso y menos perdonavidas** del plan. En in-stream saltable el espectador se va en 5 segundos y ya existe una estrategia específica para ese canal en `docs/marketing/campaigns/youtube-eu/`. Consultarla antes de producir el lote.

Resumen: **pantalla primero, sin música en los 5 primeros segundos, y la idea completa antes del botón de saltar.**

---

## 4. Gráfica estática digital

| Uso | Formatos | Notas |
|---|---|---|
| Social estático | 1080×1080 · 1080×1350 · 1080×1920 | Sistema oscuro. Texto en el 80 % central |
| Carrusel | 1080×1350, hasta 10 láminas | Existen plantillas en `design-system/plantillas-carrusel/` |
| Cabecera de perfil | Según red `[VERIFICAR]` | Un solo logotipo para ambas audiencias |
| Display estándar | 300×250 · 728×90 · 160×600 · 320×50 · 970×250 | Sistema oscuro. **Una idea** |
| Display responsive | Set de imágenes + titulares + descripciones | Cada combinación debe cumplir el [06](06-claims-y-guardrails.md) |

**Toda pieza estática:** se entiende sin contexto, sin secuencia y sin sonido.

---

## 5. Exterior

Especificaciones de craft, iluminación, tipografía y producción de impresión en **[05 · Exterior y gráfica estática](05-exterior-y-grafica-estatica.md)**. No maquetar sin leerlo: el sistema oscuro **no se usa en soportes impresos**.

---

## 6. Nomenclatura de archivos

Obligatoria. Un lote mal nombrado es un lote que se pierde en tráfico.

```text
k9_<lote>_<concepto>_<audiencia>_<duracion>_<ratio>_<idioma>_<version>.<ext>

k9_A_dosPasos_master_60s_239_es_v03.mov
k9_B_veto_pro_20s_916_es_v01_sub.mp4
k9_D_veto_ooh_marquesina_120x175_es_v02.pdf
```

- `lote`: A · B · C · D · E
- `audiencia`: `pro` · `dueno` · `master`
- `sub` como sufijo si lleva subtítulos quemados
- Versionado `v01`, `v02`… **Nunca `final`, `final2`, `final_bueno`.**

---

## 7. Qué se entrega al cierre de cada lote

- [ ] Másteres de conservación, emisión y limpios
- [ ] Todas las duraciones y ratios del lote
- [ ] Subtítulos `.srt` y `.vtt` revisados
- [ ] Stems de audio separados
- [ ] Proyectos de montaje y grafismo, con fuentes y assets
- [ ] Artes finales abiertos y cerrados
- [ ] **Ficha de claims por pieza**: cada rótulo y cada línea de voz, con su estado según [06](06-claims-y-guardrails.md)
- [ ] Documentación de derechos: música, imagen de personas, localizaciones, animales
- [ ] Informe de bienestar animal del rodaje, si hubo animales
- [ ] Prueba de color contractual firmada, si hubo impresión
- [ ] Manual de adaptación: cómo se recompone el concepto a un formato nuevo sin romperlo
