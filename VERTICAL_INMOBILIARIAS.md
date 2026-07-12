# PLAYBOOK VERTICAL — INMOBILIARIAS
## El Faro · Especialización vertical · Julio 2026
### Inmobiliarias y corredores — Argentina y Chile

**Estado:** borrador para aprobación de Fede. No convertir en skill ni cargar a Notion hasta aprobación.
**Base:** research desde cero, verificado con búsqueda web.

---

## 0. RESEARCH

### 0.1 Referentes globales (verificados)

1. **Village Properties** (Santa Bárbara). Paleta y motivos tomados de la arquitectura local (revival español). **Lección:** la inmobiliaria vende un LUGAR — el sitio debe verse como el lugar, no como un software. Valida el método de firma-por-destino que El Faro ya usa en turismo.
2. **Home In Amelia Island** (Florida). La agente como persona (about, fotos con su familia) + referencias hiperlocalizadas para SEO. **Lección:** en mercados chicos, el corredor con cara conocida le gana a la marca corporativa — y las páginas por barrio/zona son el SEO de la vertical.
3. **NextDoor Property**. Sitio entero dedicado a UNA cosa: "queremos comprar tu casa". **Lección estratégica central:** los sitios que captan PROPIETARIOS con un mensaje brutalmente claro son una categoría propia — y en el mercado local casi nadie lo hace (ver 0.2). La captación de dueños que pidió Fede no es una sección: es una landing dedicada.
4. **Forty Ninth Living** (Canadá). Buscador "Find Your Unit" con filtros simples + menú sticky + CTAs sembrados. **Lección:** para carteras chicas/medianas, filtros simples y honestos convierten más que el buscador gigante de portal.
5. **Compass** (EE.UU.). Insights de mercado (precio medio, días en mercado) como contenido de autoridad. **Lección adaptable:** un bloque trimestral de "cómo está el mercado en [ciudad]" (hecho con datos públicos + criterio del corredor) posiciona como experto — contenido de mantenimiento perfecto.
6. **Janet McAfee / Avantgarde** (lujo). Grid blanco y negro, tipografía elegante, fotos enormes. **Lección:** en la ficha de propiedad, la foto manda y el texto acompaña en columnas cortas; specs en tabla limpia.

**Patrones transversales:** buscador con filtros arriba del fold; mapa interactivo; fichas con fotos grandes y specs escaneables; hiperlocalidad (barrios con nombre); el agente como persona; y la captación de vendedores como línea de negocio separada.

### 0.2 Benchmarking local AR/CL — dónde diferenciarse

- **El ecosistema local verificado:** la inmobiliaria argentina vive de **Zonaprop/Argenprop/MercadoLibre** (paga por publicar, la marca y el lead son del portal) y gestiona con **Tokko Broker** (CRM #1 de Latam, planes por cantidad de propiedades desde 15, difusión a portales, red entre inmobiliarias, API disponible). Competidores modernos como KiteProp (desde USD 10/mes) suman tasador con comparables y 30+ portales — el mercado del CRM está resuelto y peleado: **El Faro no compite ahí.**
- **La "web propia" típica es la plantilla gratuita de Tokko** (verificado en sitios demo tipo tuinmobiliaria.com.ar): idéntica entre inmobiliarias, cero marca, cero barrio, cero persona. El mismo patrón exacto que AgendaPro en Estética y Turnito en Profesionales: motor resuelto, marca inexistente.
- **El gap doble de El Faro:** (1) la capa de marca —el sitio que se ve como el lugar y como el corredor, no como el CRM—; (2) la landing de captación de propietarios, que casi ninguna inmobiliaria chica local tiene y es donde está la plata real (la exclusiva de venta).
- **Argumento comercial:** cada lead de portal es compartido y pago; el lead del sitio propio es exclusivo y gratis. Y la inmobiliaria que capta al propietario capta la comisión entera.

---

## 1. FIRMA VISUAL — "PLANO"

Distinta de todas las anteriores. Coherente con faro/guía: acá la luz es **ubicación exacta — saber dónde estás parado**.

- **Elemento recurrente — la retícula de plano:** un grid arquitectónico finísimo (líneas 1px al 4-6% de opacidad) como fondo de secciones clave, sobre el que las fotos de propiedades "flotan" como láminas. Remite al plano de obra y da orden sin decorar.
- **Cotas y datos en mono:** superficies, ambientes, coordenadas y precios SIEMPRE en IBM Plex Mono con estilo de cota de plano (`120 M² · 3 AMB · GARAGE`). Es la firma tipográfica de la vertical.
- **La rosa de los vientos / norte:** un pequeño indicador de norte (SVG) como sello en el mapa y el footer — el guiño geográfico de la familia El Faro (paralelo del sello de coordenadas de turismo, pero técnico en vez de romántico).
- **Paleta base:** blanco arquitectura + grafito + UN acento por cliente (ladrillo, verde bosque, azul cianotipo — el cianotipo/blueprint es la opción más "plano" de todas). Fotos grandes con tratamiento consistente.
- **Tipografía estándar:** sans geométrica de carácter — **Archivo o Space Grotesk** (ninguna usada en otra vertical) + IBM Plex Mono para cotas. Sin serif: esta vertical es técnica y contemporánea.
- **Movimiento canónico:** scroll-reveal + hover de ficha que eleva la lámina sobre la retícula + transición suave de filtros (fade del grid de resultados). El mapa no se anima solo.

---

## 2. ESPECIFICACIÓN TÉCNICA — CATÁLOGO + BUSCADOR + MAPA + CAPTACIÓN

### La pieza compleja: buscador + mapa SIN backend (viable, y es pariente del patrón de turismo)

**Arquitectura (Ruta A — estándar del paquete base):**
- **Fuente de verdad:** `propiedades.json` en el repo — o Google Sheet publicada como CSV, exactamente el patrón de disponibilidad ya especificado en Turismo (gap 8). Cada propiedad: id, operación (venta/alquiler), tipo, zona/barrio, precio+moneda, m², ambientes, amenities, lat/lng, fotos (rutas), estado (disponible/reservada/vendida), destacada.
- **Buscador:** filtros en JS puro sobre ese JSON (operación, tipo, zona, rango de precio, ambientes) — mismo patrón del filtro de galería del sitio de Joe, con más campos. Para carteras de hasta ~100-150 propiedades, el filtrado client-side es instantáneo; más que eso, la inmobiliaria ya es grande para este paquete.
- **Mapa:** **Leaflet + OpenStreetMap** (librería open source, sin API key, sin costo, sin backend) con markers generados del MISMO JSON; click en marker → ficha. Google Maps embed queda como alternativa si el cliente lo exige, pero Leaflet evita el tema de claves y facturación de Google. **Sobre el "mapa con IA" de la base:** en un sitio estático no hay IA — lo honesto es "mapa interactivo con filtros cruzados" (filtrás y el mapa se actualiza), que es lo que el visitante realmente quiere. Búsqueda en lenguaje natural con IA real = upsell futuro, fuera de stack, marcado como tal.
- **Ficha de propiedad:** galería con lightbox (componente de Joe, reutilizado tal cual) + cotas en mono + mapa individual + **botón "Agendar visita"** = resumen→WhatsApp prellenado con la propiedad, fecha tentativa y datos del interesado (adaptación directa del componente de reservas de turismo, sin calendario — la visita se coordina por WhatsApp o con Calendly del agente).
- **Actualización de cartera:** con Google Sheet como fuente, la inmobiliaria carga/da de baja propiedades sola (plan de mantenimiento menor) o lo hace El Faro (plan mayor). **Regla dura: propiedad vendida = fuera del sitio o marcada VENDIDA en 48 hs** — la publicación vencida es el asesino #1 de confianza del rubro (ver objeciones).

**Ruta B — sincronización con Tokko (upsell, fuera del ticket base):** Tokko expone API para unificar el sitio propio con el CRM. Sincronizar cartera automáticamente requiere un paso de build o función serverless (mismo patrón Vercel Functions ya especificado en la Ruta B de Turismo) + mapeo de datos + manejo de fotos. Estimación: 15-25 hs primera vez. Solo se vende si la inmobiliaria tiene volumen real (50+ propiedades rotando) y paga el ticket correspondiente. Hasta entonces, la Sheet manda.

### CRM: no construir, integrar livianito

El CRM ya existe y el cliente probablemente ya lo paga (Tokko o similar). El "CRM básico" del paquete de El Faro es: cada formulario del sitio (consulta por propiedad, visita, tasación) llega por mail Y queda en una Google Sheet de leads con fecha, origen y propiedad — suficiente para la inmobiliaria chica sin CRM, y compatible con importar al CRM si lo tiene. Nada más.

### Captación de propietarios (el diferencial de la vertical)

**Landing dedicada** `/vende-tu-propiedad` con mensaje único estilo NextDoor: qué gana el dueño (tasación fundamentada sin cargo, plan de difusión concreto, actualización semanal), formulario de pre-tasación (dirección/zona, tipo, m² aproximados, estado, expectativa — datos del inmueble, nada sensible) → WhatsApp/mail al corredor. El entregable de la inmobiliaria hacia el dueño (informe de tasación) es de ellos; el sitio genera el lead. Esta landing se promociona con la metodología de captación orgánica IG ya probada (carrusel "¿cuánto vale tu casa en [ciudad] hoy?" + palabra clave + DM automático).

**Costo de desarrollo total (Ruta A completa):** 20-30 hs — buscador+mapa+fichas+landing propietarios son componentes nuevos reales (los primeros se amortizan en el segundo cliente). **Vive en: paquete propio de la vertical.**

---

## 3. BANCO DE OBJECIONES + HOOKS

### Objeciones del cliente final (comprador/inquilino Y propietario — responder EN el sitio)

1. **"¿Sigue disponible?"** (la pregunta #1 del rubro) → estado visible en cada ficha + regla de 48 hs + fecha de última actualización de la cartera en el buscador.
2. **"Las fotos no van a ser como la realidad"** → fotos reales, muchas, con luz honesta; specs exactas en cotas; mapa con ubicación real (no "zona aproximada" salvo pedido del dueño).
3. **"¿Cuánto hay de gastos además del precio?"** → sección transparente: honorarios, sellados, expensas — el que lo publica primero se queda con la confianza.
4. **"¿Esta inmobiliaria es seria?"** → matrícula del corredor visible (obligatoria en el rubro), años, el equipo con cara, reseñas de Google.
5. **(Propietario) "Me van a tasar alto para captarme y después me piden bajar"** → copy de la landing: "tasación fundamentada con comparables, no un número para conquistarte" — atacar la práctica de frente es el diferencial.
6. **(Propietario) "La van a publicar y olvidarse"** → plan de difusión concreto en la landing (portales + sitio + redes) y compromiso de reporte periódico.
7. **"No quiero dejar mis datos para que me llamen veinte veces"** → formularios mínimos + "te contactamos una vez por WhatsApp".
8. **"¿Puedo ir a verla ya?"** → botón de visita con WhatsApp prellenado en cada ficha — cero fricción entre interés y visita.

### Hooks de primer mensaje (al dueño de la inmobiliaria — compatibles con `el-faro-primer-mensaje`)

1. *"Cada lead que te manda Zonaprop lo pagás y lo comparte tu competencia. Los que entran por tu propia página son gratis y exclusivos — y hoy tu página es la misma plantilla de Tokko que usan todos."*
2. *"Busqué 'inmobiliaria en [ciudad]': aparece Zonaprop, aparece un colega, vos no. El dueño que quiere vender googlea eso antes de decidir a quién llamarte."*
3. *"Tu web tiene propiedades vendidas hace meses todavía publicadas. El que entra y ve eso no te consulta por las que sí tenés."*
4. *"Todos captan compradores; casi nadie capta dueños. Una página de 'vendé tu propiedad' con tasación sin cargo te trae exclusivas — te muestro cómo se ve."*
5. *"¿Cuántas veces por día contestás '¿sigue disponible?' y '¿cuánto son las expensas?'? Una página con la cartera al día y los gastos claros te ahorra el 80% de esos mensajes."*

---

## 4. CHECKLIST DE CALIDAD — EXTENSIÓN PARA INMOBILIARIAS

Se suma al checklist de 25 puntos de `el-faro-perfiles-cliente`:

- [ ] Matrícula del corredor visible (footer + about) — obligación del rubro
- [ ] Fuente de verdad de la cartera DEFINIDA y acordada (¿quién actualiza, Sheet o El Faro?) — regla de 48 hs para vendidas/alquiladas por escrito con el cliente
- [ ] Buscador con filtros funcionando sobre el 100% de la cartera cargada; cero propiedades "de relleno"
- [ ] Mapa con TODAS las propiedades geolocalizadas correctamente (verificar lat/lng una por una — un pin errado en otra ciudad destruye la confianza)
- [ ] Ficha completa: fotos suficientes (mínimo 5), cotas en mono, gastos/expensas, estado, botón de visita
- [ ] Landing de captación de propietarios publicada y enlazada desde el header (no escondida)
- [ ] Leads llegando a mail + Sheet, probado con un envío real de cada formulario
- [ ] Disclaimer estándar del rubro (medidas y precios orientativos, sujetos a título)
- [ ] Fotos: sin marcas de agua de portales ajenos, sin capturas de Zonaprop
- [ ] Zonas/barrios con nombre real local (SEO hiperlocal) — página o sección por zona si la cartera lo justifica
- [ ] Precios con moneda explícita (USD/ARS/UF) y coherente en toda la cartera
- [ ] Open Graph por defecto del sitio + verificación de que las fichas comparten bien por WhatsApp (es cómo circulan las propiedades acá)

---

## 5. PRICING ANCLA

Fede lo anticipó: ticket alto. El research lo confirma — hay componentes nuevos reales, la inmobiliaria factura comisiones grandes y ya paga CRM + portales todos los meses.

| Entregable | Ticket | Justificación |
|---|---|---|
| **Base inmobiliaria** (sitio de marca + catálogo con buscador y mapa Leaflet + fichas + landing de propietarios + leads a Sheet) | **USD 600-1.200** | 20-30 hs reales de componentes nuevos; el ROI es tangible: una sola exclusiva captada por la landing paga el sitio varias veces. Contra lo que ya gastan por mes en portales, el one-time es fácil de anclar. |
| **Ruta B: sync automático con Tokko (API)** | **+USD 400-800** | 15-25 hs de integración; solo para carteras de 50+ propiedades con rotación real. |
| **Mantenimiento** | **$30.000-50.000 ARS/mes** (o equivalente) según quién carga la cartera | **La mejor vertical de recurrencia de El Faro:** altas/bajas de propiedades son trabajo semanal visible. Plan menor: la inmobiliaria carga en la Sheet, El Faro supervisa + contenido. Plan mayor: El Faro carga todo + bloque trimestral de mercado + redes. |
| Add-on natural | Según catálogo | Campaña de captación orgánica IG apuntada a la landing de propietarios — metodología ya probada, aplicada al mensaje "¿cuánto vale tu casa hoy?". |

---

## PRÓXIMOS PASOS (post-aprobación)

1. Construir los dos componentes nuevos como bloques reutilizables: (a) buscador+grid de fichas sobre JSON, (b) mapa Leaflet con markers desde el mismo JSON. Son la inversión de la vertical — se amortizan desde el segundo cliente.
2. Adaptar el componente resumen→WhatsApp de turismo como "Agendar visita".
3. Buscar el primer caso (¿hay inmobiliaria o corredor conocido en San Luis/Merlo? El corredor individual de pueblo turístico une esta vertical con la de Turismo — cabañas en venta).
4. Cargar este playbook a la Biblioteca de Verticales.
