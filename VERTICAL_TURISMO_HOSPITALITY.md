# PLAYBOOK VERTICAL — TURISMO / HOSPITALITY
## El Faro · Especialización vertical · Julio 2026
### Alojamientos, cabañas, complejos recreativos, excursiones — Argentina y Chile

**Estado:** borrador para aprobación de Fede. No convertir en skill ni cargar a Notion hasta aprobación.
**Base:** auditoría del sitio real de Joe (Centro El Progreso, Casablanca) + research verificado con búsqueda web.

---

## 0. AUDITORÍA DEL COMPONENTE REAL (sitio de Joe) VS ESTÁNDAR GLOBAL

### 0.1 Qué está al nivel (se generaliza tal cual)

Contra los referentes globales analizados (sección 0.3), el sitio de Joe ya tiene resuelto lo que la competencia local ni siquiera intenta:

| Componente | Estado | Veredicto |
|---|---|---|
| Tokens CSS con paleta propia del lugar (verde parrón, vino, terracota, piscina) | Paleta derivada del Valle de Casablanca, no genérica | **Al nivel.** Es exactamente el enfoque de firma visual por lugar que usan los referentes de punta. Generalizar el *método*, no la paleta. |
| Tipografía Fraunces + Work Sans + IBM Plex Mono | Display expresiva + sans limpia + mono para datos | **Al nivel.** El uso de mono para fechas/precios/etiquetas es un detalle que la competencia local no tiene. Se adopta como estándar de la vertical. |
| Hero slideshow Ken Burns + dots + stats bajo el fold | 5 slides, transición 1.6s, stats con borde superior | **Al nivel.** Mismo patrón que los sitios cinemáticos de punta. Mejora menor: pausar autoplay en `prefers-reduced-motion` (el keyframe ya lo contempla, el `setInterval` no). |
| Selector de servicio → precio en vivo + resumen sticky | 6 servicios, `data-precio`/`data-nombre`, resumen se arma solo | **Al nivel y diferencial.** Ningún benchmark local chico tiene esto. Es el corazón del componente reutilizable. |
| Calendario JS puro (bloqueadas, pasado, hoy, seleccionado, `Intl` locale) | Sin librerías, lunes-primero, leyenda de estados | **Al nivel funcional.** Gaps de datos abajo (0.2). |
| Mensaje WhatsApp prellenado con toda la reserva | Servicio + fecha + personas + nombre + tel + comentario | **Al nivel.** Es la Ruta A funcionando. Se conserva como flujo por defecto. |
| Galería con filtros por categoría + lightbox + item destacado | 16 fotos, 5 categorías, grid con `g-big` | **Al nivel.** |
| Cinta de fechas turísticas con scroll-snap | Feriados CL 2026 + Vendimia de Casablanca destacada | **Al nivel y diferencial.** Nadie local hace esto. Se generaliza como componente "calendario comercial del destino" (feriados AR o CL + eventos del lugar). |
| `prefers-reduced-motion`, header con estado scrolled, menú mobile, WA flotante con pulso | — | **Al nivel.** |

**Conclusión de la auditoría:** el sitio de Joe no es un punto de partida a mejorar — es un 80% del componente final. El salto de calidad no está en el diseño (ya compite), está en **datos, pago y producción** (0.2).

### 0.2 Gaps a corregir antes de generalizar

**Los 3 conocidos:**

1. **Botón de pago = `alert()`.** Resuelto en sección 2 (Rutas A y B especificadas).
2. **WhatsApp hardcodeado (`56900000000` repetido 4 veces).** Corrección: un objeto `CONFIG` único al inicio del JS con `whatsapp`, `nombreNegocio`, `moneda`, `locale` (`es-AR`/`es-CL`), `servicios[]` (nombre, precio, tipo día/hora/noche) y `fechasBloqueadas[]`. Todo el sitio lee de ahí. En la skill: el CONFIG es el primer bloque que se completa con datos del cliente — un solo lugar, cero búsqueda-y-reemplazo.
3. **Imágenes base64.** Correcto para preview en artifact (regla El Faro vigente). Paso de migración a producción, a documentar en la skill: al subir a GitHub, extraer base64 → `/assets/img/` en WebP (hero ≤ 200KB, galería ≤ 120KB), reemplazar por rutas relativas, `loading="lazy"` bajo el fold, hero sin lazy. Con 32 imágenes embebidas el HTML pesa 10MB — eso en producción es un sitio que no carga en 4G rural, que es exactamente donde está el cliente de esta vertical.

**Gaps nuevos detectados en la auditoría:**

4. **Emojis como íconos** (🏊 🔥 🏕️ 🎱 🏓 🎾 💬 📲). Viola la regla ya escrita en `el-faro-perfiles-cliente` (SVG, nunca emojis). Reemplazar por set SVG de línea consistente. Es el detalle #1 que separa "hecho con IA" de producto profesional.
5. **Sin GA4 + Pixel Meta.** Regla El Faro del día 1. Agregar con placeholders al generalizar.
6. **Sin Open Graph.** El link se comparte por WhatsApp — la miniatura ES la primera impresión. Prioridad ya documentada en la skill; acá faltó.
7. **Validación con `alert('elige una fecha')`.** Reemplazar por mensaje inline en el resumen sticky (borde rojo + texto). Los `alert()` gritan prototipo.
8. **Disponibilidad sin fuente de verdad.** Las fechas bloqueadas están hardcodeadas en el JS. Pregunta que ningún prospecto va a perdonar: *¿quién actualiza el calendario cuando entra una reserva?* Respuesta por paquete:
   - **Base:** el calendario se presenta como "fechas de alta demanda / consultá disponibilidad" (bloquea feriados + lo que el dueño informe). Actualización = cambio chico cotizado o incluido en plan de mantenimiento. **Esto convierte el calendario en el mejor argumento de venta del plan mensual.**
   - **Crecimiento/Full:** el JS lee las bloqueadas por `fetch` de un JSON en el mismo repo o de una Google Sheet publicada como CSV (sin backend, dentro del stack). El dueño o El Faro edita la sheet; el sitio se actualiza solo.
9. **Disponibilidad no distingue servicio.** Una cabaña ocupada ≠ piscina llena. Los referentes globales muestran disponibilidad por unidad. Para el ticket que vendemos alcanza con: bloqueadas por servicio en el CONFIG (`fechasBloqueadas: { cabanas: [...], general: [...] }`) — el calendario se repinta al cambiar el selector. Costo: ~1h de refactor, salto de percepción enorme.
10. **Precio solo en 1 de 6 servicios** ("Consultar" en el resto). El research local muestra que el turista argentino/chileno decide por precio ancla. Regla de la vertical: **todo servicio con precio "desde"**, aunque sea rango. "Consultar" solo para eventos corporativos.
11. **Sin política de cancelación visible.** Ver checklist (sección 5) — es el punto de fricción #1 en reservas con seña.

### 0.3 Benchmarking — referentes globales (verificados por búsqueda)

Sin cadenas gigantes; todos aplicables a negocios chicos/medianos:

1. **Unyoked** (unyoked.co — AU/UK/NZ, cabañas off-grid). **Firma visual:** fotografía atmosférica de naturaleza + tipografía editorial; el producto casi no se ve, se ve la sensación. **Movimiento:** transiciones suaves al scroll, cero decoración. **Flujo:** buscador por "cerca de [ciudad]" → cabaña → fechas → pago; venden en 3 pasos. **Copy:** venden desconexión y cura del burnout, no metros cuadrados ("más árboles que gente"). **Lección:** el ángulo emocional es escape/reset; la cercanía a la ciudad ("a 1-2 horas de...") es el dato racional que cierra. El Progreso ya lo hace ("a una hora de Santiago y Valparaíso") — se vuelve regla de la vertical.
2. **Postcard Cabins** (postcardcabins.com, ex-Getaway — EE.UU.). **Firma:** "design-forward cabins" — fotos consistentes de un mismo objeto (la cabaña + fogón). **Flujo:** FAQ operativa brutalmente clara (mascotas $X, sin recepción, código por SMS, límite de agua caliente). **Lección:** la transparencia operativa ES contenido de conversión — reduce consultas de WhatsApp repetidas, argumento directo para el dueño.
3. **Eastwind Hotels** (Catskills, NY — boutique chico). **Firma:** full-width de bosques con niebla, layout abierto y aireado. **Estructura:** ubicación → amenities (sauna, fogones, trails) → reserva. **Lección:** las amenities se muestran como experiencias con foto, no como lista con tildes.
4. **Basecamp Hotel** (Lake Tahoe). **Firma:** tema camping llevado a todo (texturas de mapa de sendero, papel arrugado). **Lección:** un motivo visual del rubro aplicado con consistencia total hace memorable un negocio chico. Valida el enfoque de firma visual por cliente que El Faro ya usa.
5. **Lincolnville Motel** (Maine — motel de cabañas humilde). **Lección clave para nuestro ticket:** no pretende ser lo que no es; branding simple, fotos honestas, navegación directa. Un negocio familiar con sitio honesto y bien hecho le gana a uno pretencioso. Es el norte para Perfil A turismo.
6. **Varena Treehouse** (Lituania — negocio chico de cabañas). Minimalismo + fotos del entorno + reserva en pocos clics. Prueba de que el estándar global es alcanzable sin plataforma enterprise.

### 0.4 Benchmarking local AR/CL — dónde diferenciarse

- **Patrón dominante:** el complejo chico argentino/chileno NO tiene sitio propio con reserva — vive en Booking/Airbnb (15-18% de comisión por reserva) o en directorios regionales (interpatagonia, sierrasdelaventana.com.ar) que cobran por publicar y derivan a "contactar al dueño".
- **Sitios propios existentes** (ej. verificado: complejomardecobo.com): un párrafo, teléfono, mail. Sin calendario, sin precios, sin galería decente, sin mobile.
- **El argumento comercial de la vertical sale solo:** *"Cada reserva que entra por Booking te cuesta 15-18%. El sitio se paga con las primeras reservas directas del año."* Los propios directorios locales lo publicitan ("ahorrás hasta 20% de comisiones reservando directo") — el mercado ya está educado en el problema.
- **Dónde diferenciarse:** calendario visible + precio ancla + WhatsApp prellenado + fechas turísticas del destino. Ninguno local lo tiene junto. El componente de Joe ya lo tiene.

---

## 1. FIRMA VISUAL DE EL FARO PARA LA VERTICAL

**Nombre interno: "Horizonte y Destello".** Distinta de Áurea (espiral dorada) y Vivir Bonito (proporción áurea/naturales); coherente con faro = luz que orienta.

- **Elemento recurrente — la línea de horizonte:** una línea horizontal fina (1px, color acento) que cruza como divisor de secciones y subraya los eyebrows. En el sitio de Joe ya existe embrionariamente (el `::before` del eyebrow); se sistematiza.
- **El destello:** un punto de luz cálida (radial-gradient chico, siempre en el mismo tono ámbar de El Faro `#E8A33D` aprox.) que marca el CTA principal de cada pantalla y el día seleccionado del calendario. Es la firma trans-cliente: la paleta cambia por destino, el destello no.
- **Sello de coordenadas:** un sello circular en mono (`33°19'S 71°24'W · VALLE DE CASABLANCA`) en el hero o footer, opcionalmente rotando lento. Ancla el sitio a un lugar real — es LA firma de turismo (paralelo del sello de cosecha de Vivir Bonito, pero geográfico, no orgánico).
- **Paleta por clima del destino** (método, no paleta fija): agua/costa → azules profundos + arena; valle/viña → verdes + vino + terracota (Casablanca ya validada); sierra/monte → grises piedra + ocres + verde seco. Siempre: 1 oscuro dominante, 1 crema base, 1-2 acentos del lugar, + destello ámbar El Faro.
- **Tipografía estándar de la vertical:** Fraunces (display, ya validada por Joe — su carácter "viejo mundo" calza con hospitality) + Work Sans (cuerpo) + IBM Plex Mono (fechas, precios, coordenadas, etiquetas). No cambiar por cliente salvo pedido; la variación de marca la da la paleta y las fotos.
- **Movimiento canónico:** Ken Burns en hero (validado), scroll-reveal estándar de la skill, cinta de fechas con scroll-snap, y un solo efecto nuevo: el destello del CTA "respira" (opacity 0.85↔1, 3s) — sutil, apagado con reduced-motion.

---

## 2. ESPECIFICACIÓN TÉCNICA — SISTEMA DE RESERVA + PAGO

Punto de partida: selector + calendario + resumen + WhatsApp de Joe, con las correcciones de 0.2 (CONFIG parametrizado, disponibilidad por servicio, fuente de datos según paquete).

### Ruta A — WhatsApp + link de pago manual (RECOMENDADA PARA ARRANCAR)

**Flujo:** el visitante arma la reserva en el sitio → "Enviar solicitud" abre WhatsApp con el mensaje prellenado (ya funciona) → el dueño confirma disponibilidad → envía por WhatsApp el link de pago de la seña → pagada la seña, la fecha se bloquea (actualización de calendario según paquete, gap 8).

**Cómo se genera el link de pago (cero código):**
- **Argentina:** Link de pago de Mercado Pago, se crea desde el panel/app de MP en 1 minuto, monto libre o fijo. Ya es el estándar de cobro de El Faro.
- **Chile:** **Link de Pago Webpay.cl de Transbank** — producto oficial para vender sin sitio web: se contrata 100% online desde el Portal de Clientes, activación en ~24h, sin costo fijo mensual, comisión ~1,79% + IVA débito / ~2,79% + IVA crédito (referencia; varía por rubro). Requiere inicio de actividades en SII (o seleccionar categoría). El dueño crea el link desde el navegador y lo manda por WhatsApp. **Esto resuelve la adaptación Chile pendiente para la propuesta de Centro El Progreso.** Alternativa si el cliente no está formalizado: Flow.cl (cuenta con RUT personal, links de pago, acepta Webpay).

**Mejora incluida sin costo real ("Ruta A.5" — semiautomática, hallazgo del research):**
Tanto MP (links de pago fijos por servicio) como Transbank (Botones Webpay Plus de monto fijo, y URLs públicas por producto en Webpay.cl que incluyen botón HTML embebible) permiten **poner el botón "Pagar seña de $X" directo en el sitio estático, sin backend**. El botón del sitio deja de ser un alert() y pasa a abrir el checkout real con monto fijo por servicio. Limitación honesta: monto fijo (una seña estándar por tipo de servicio) y sin conciliación automática con el calendario — la confirmación sigue siendo manual por WhatsApp. Para el 90% de los clientes de esta vertical, alcanza y sobra.

**Costo de desarrollo:** Ruta A pura: 0-1h (texto del sitio + SOP de cobro para el dueño). Ruta A.5: 2-4h (alta de links por servicio + botones + textos de confirmación). **Vive en: Paquete Base (USD 350-600).**

**Pros:** cero riesgo técnico, coincide con el modelo de cobro ya documentado en el Archivo Maestro, el dueño mantiene control humano (clave en Perfil A), funciona igual en AR y CL. **Contras:** fricción de un paso extra; la seña puede demorarse y la fecha quedar en el limbo (mitigación: SOP de "la fecha se libera si la seña no entra en 24h", visible en el sitio).

### Ruta B — Integración automática (Checkout Pro / Webpay Plus)

**Realidad técnica:** ni Mercado Pago Checkout Pro ni Webpay Plus se pueden integrar 100% desde el front. Crear la preferencia de pago (MP) o la transacción (Transbank) requiere un **access token secreto que no puede vivir en el HTML** — necesita ejecutarse server-side.

**Solución DENTRO del stack actual (sin servidor propio):** **Vercel Serverless Functions.** El mismo repo GitHub que ya deploya el sitio suma una carpeta `/api` con dos funciones:
1. `/api/crear-pago` → recibe servicio+fecha, crea la preferencia en MP (o transacción Webpay Plus REST) con el token guardado como variable de entorno de Vercel, devuelve la URL de checkout → el botón del sitio redirige ahí.
2. `/api/webhook-pago` → recibe la notificación de pago aprobado (webhook/`notification_url`), y avisa al dueño (mail vía Brevo o registro en la Google Sheet de disponibilidad).

Esto está dentro del free tier de Vercel y del flujo GitHub→Vercel ya documentado. **No es "fuera de stack": es el mismo stack usando una capacidad que ya tenemos y no usábamos.**

**Lo que SÍ empuja el ticket:** el pago automático solo tiene sentido si el calendario refleja la reserva automáticamente — y eso exige una fuente de datos escribible (Google Sheet vía webhook, o KV de Vercel). Sumale cuentas de prueba, estados de pago (aprobado/pendiente/rechazado), reembolsos de seña, y pantallas de retorno (`back_urls`).

**Costo de desarrollo estimado:** primera implementación 12-20h (incluye sandbox, webhooks, estados, pruebas AR y CL por separado — Webpay Plus y MP son integraciones distintas). Replicada como componente de la skill: 4-6h por cliente. **Vive en: paquete de USD 1.000+ (o como upgrade del Crecimiento/Full).** A USD 200-600 la Ruta B destruye la rentabilidad; decirlo de frente en la propuesta: *"reserva con pago automático es el paquete grande"*.

**Decisión recomendada:** lanzar la vertical con **Ruta A.5 como estándar del Base** (checkout real, sin backend) y **Ruta B como upsell documentado** para cuando un cliente lo pida y lo pague. Primer candidato natural para Ruta B: Centro El Progreso a los 6 meses, si el volumen lo justifica — mismo patrón que Áurea con su e-commerce.

---

## 3. BANCO DE OBJECIONES + HOOKS

### Objeciones del comprador final (para responder EN el sitio, sin nombrarlas)

1. **"¿Y si llueve / hace frío?"** → sección "tu día, con cualquier clima": quinchos techados, salón, política de reprogramación por lluvia. (El Progreso tiene los quinchos; hoy no juega esa carta.)
2. **"¿Qué pasa con la seña si cancelo?"** → política de cancelación en 3 líneas, visible junto al botón de pago. Regla: reprogramación gratis con X días de aviso > devolución (protege al dueño, tranquiliza al cliente).
3. **"¿Es seguro para los chicos?"** → piscinas cercadas, profundidades, sector para los más pequeños — con foto. (Ya está en el copy de servicios de Joe; subirlo de jerarquía.)
4. **"¿Puedo llevar mi comida / mi mascota?"** → FAQ operativa estilo Postcard Cabins: qué incluye, qué se puede traer, mascotas sí/no y condiciones. Cada respuesta clara = 10 WhatsApp menos por semana (esto también se le vende al dueño).
5. **"¿Cómo llego?"** → mapa + minutos desde las 2 ciudades ancla + botón "Cómo llegar" a Google Maps.
6. **"¿Va a estar lleno?"** → capacidad máxima por día visible (El Progreso ya muestra 38-39) — la exclusividad tranquiliza y justifica la seña.
7. **"¿Las fotos son reales?"** → galería etiquetada "fotos reales de nuestras familias" (Joe ya lo escribió — se vuelve regla de la vertical) + reseñas de Google embebidas o citadas con nombre.
8. **"Está caro para un día"** → precio anclado a la experiencia completa ("todo incluido en tu pase") y comparado implícitamente: chips de qué incluye al lado del precio.

### Hooks de primer mensaje (prospección al dueño — compatibles con `el-faro-primer-mensaje`)

1. *"Vi que [complejo] labura con Booking/reserva por teléfono. ¿Sabés cuánto se te va por año en comisiones? Con reservas directas desde tu propia página, eso queda en tu bolsillo."*
2. *"Busqué '[rubro] en [zona]' en Google y tu competencia aparece antes que vos — y eso que tienen peor lugar. No es el predio, es la página."*
3. *"¿Cuántas veces por semana contestás por WhatsApp 'hola, ¿precio?', '¿está libre el finde largo?'? Una página con calendario y precios te saca el 80% de esos mensajes."*
4. *"Se viene [Semana Santa / Vendimia / feriado XX] y la gente ya está googleando dónde ir. Si no tenés página con reserva, esa demanda se la lleva el que sí tiene."*
5. *"Te muestro algo: [link preview de otro complejo hecho por El Faro]. Eso mismo, con tus fotos y tus precios, funcionando en 48hs. Primero coordinemos una llamada de 15 minutos."* (La preview propia solo post-llamada, regla vigente; acá se muestra el caso de éxito ajeno.)

---

## 4. CHECKLIST DE CALIDAD — EXTENSIÓN PARA TURISMO/HOSPITALITY

Se suma al checklist de 25 puntos de `el-faro-perfiles-cliente` (que aplica completo). Solo lo específico del rubro:

- [ ] Política de cancelación/reprogramación de seña visible junto al botón de reserva (máx. 3 líneas)
- [ ] Todo servicio con precio "desde" — "Consultar" solo para eventos corporativos
- [ ] Capacidad máxima y horarios visibles (día completo / por hora / por noche, bien diferenciados)
- [ ] Distancia en minutos desde 2 ciudades ancla + botón "Cómo llegar" (Google Maps)
- [ ] FAQ operativa: qué incluye, qué traer, mascotas, estacionamiento, clima/plan B
- [ ] Cinta de fechas turísticas del año en curso (feriados del país + eventos del destino) con CTA "reservá con anticipación"
- [ ] Calendario con fuente de actualización DEFINIDA y acordada con el cliente (¿quién bloquea fechas y cómo?) — nunca entregar disponibilidad que va a quedar vieja
- [ ] Disponibilidad diferenciada por servicio si hay alojamiento + pase de día
- [ ] Galería con etiqueta de autenticidad ("fotos reales de...") y al menos 30% de fotos CON personas
- [ ] Temporada alta/baja reflejada en precios si aplica
- [ ] `CONFIG` completo: WhatsApp real, moneda y locale correctos (ARS/es-AR vs CLP/es-CL), medios de pago del país (MP vs Webpay)
- [ ] Cero emojis como íconos; set SVG consistente
- [ ] Migración base64 → /assets WebP hecha antes del deploy a producción (nunca deployar el HTML de preview)

---

## 5. PRICING ANCLA DE LA VERTICAL

| Entregable | Ticket | Justificación de mercado |
|---|---|---|
| **Base turismo** (sitio completo + calendario informativo + Ruta A.5 con botones de seña) | **USD 400-600** | Por encima del Base genérico de El Faro: el calendario + selector + resumen no lo tiene nadie en el mercado local, y el ahorro de comisiones de Booking (15-18% por reserva) hace el ROI evidente — un complejo que factura modesto en temporada recupera el sitio en semanas. |
| **Con pago integrado (Ruta B)** | **USD 1.000-1.400** | 12-20h reales de integración + valor de negocio alto (reserva 24/7 sin humano). Se vende como "tu recepcionista que no duerme". |
| **Mantenimiento mensual** | **Piso más alto que el genérico** (arranque sugerido: $25-35.000 ARS/mes o equivalente CLP) | En esta vertical el mantenimiento tiene trabajo recurrente REAL y visible: actualizar disponibilidad, fechas turísticas del año, precios por temporada, fotos nuevas. Es la vertical ideal para ejecutar la suba de precios de mantenimiento ya decidida — acá el cliente VE el trabajo todos los meses. |
| Hosting anual | $20.000 ARS (regla vigente) / equivalente CLP para Chile — verificar costo real del dominio .cl en Hostinger antes de la propuesta de El Progreso | Costo de terceros, línea separada, como siempre. |

**Nota Chile:** cotizar en CLP con referencia fija (no atar a ARS). La comisión de Webpay la absorbe el cliente (es su pasarela) — dejarlo explícito en la propuesta.

---

## PRÓXIMOS PASOS (post-aprobación de Fede)

1. Convertir sección 0.2 + 2 en refactor del sitio de El Progreso (CONFIG, SVG, OG, GA4, Ruta A.5 con Webpay.cl) → es a la vez la entrega del cliente real y el template de la vertical.
2. Extender `el-faro-perfiles-cliente` con: firma "Horizonte y Destello", componente reserva (selector+calendario+resumen parametrizados), checklist de la sección 4. Alternativa: skill nueva `el-faro-vertical-turismo` que herede de perfiles-cliente — decidir según peso.
3. Cargar este playbook a la Biblioteca de Verticales de Notion.
4. Resolver con Laura de El Progreso los datos pendientes (precios por servicio, temporadas, mascotas) — el CONFIG los necesita todos.
