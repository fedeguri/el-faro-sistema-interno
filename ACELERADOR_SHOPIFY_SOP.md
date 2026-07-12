# ACELERADOR DE SHOPIFY — SOP AUTOMATIZADO POR CONECTOR
## El Faro · Diseño de arquitectura · Julio 2026

**Estado:** especificación para revisión de Fede. La prueba en vivo se hace en otra sesión, contra la tienda real de Shudita, con el conector conectado a esa tienda.
**Base:** Metodología de Proyectos del Archivo Maestro v3 (Semanas 1-4) mapeada contra las definiciones REALES de las herramientas del conector de Shopify (verificadas, no supuestas).
**Modelo operativo:** una tienda conectada por vez. Conectar → correr el procedimiento completo → verificar → recién ahí pasar a la siguiente. `get-shop-info` es siempre el paso 0 para confirmar contra qué tienda se está trabajando.

---

## HALLAZGOS CLAVE DEL CONECTOR (leídos de las herramientas reales)

Antes del mapeo, cinco capacidades que cambian el diseño del procedimiento:

1. **`create-product` crea en DRAFT por defecto.** El patrón de seguridad viene gratis: se carga todo el catálogo en borrador, se verifica, y recién al final `bulk-update-product-status` pasa todo a ACTIVE de una vez. Nada a medio armar queda visible al público.
2. **Las colecciones smart aceptan reglas por TAG.** La arquitectura de 3 niveles de ticket se implementa con tags (`nivel-1`, `nivel-2`, `nivel-3`) al crear cada producto → tres colecciones smart que se pueblan solas. Un producto cambia de nivel cambiándole el tag, sin tocar colecciones.
3. **Las imágenes exigen URL HTTPS pública** — rutas locales fallan, y **no hay herramienta de subida de imágenes en el conector** (corrección de Claude Sonnet, verificado contra las 25 herramientas reales — `upload-image` no existe, solo se la menciona en la descripción de `create-product` como referencia externa). El único flujo real: fotos del cliente → hostear antes en repo/Netlify → esa URL pública en `create-product`.
4. **`run-analytics-query` (ShopifyQL) consulta `conversion_rate`, sesiones y embudo directamente** — el corte de "conversión orgánica >2% antes de prender ads" de Semana 4 se verifica por conector, sin entrar al admin.
5. **`graphql_query`/`graphql_mutation` + `validate_graphql_codeblocks`** son la vía de escape para lo que las herramientas empaquetadas no cubren (políticas de la tienda, páginas, metafields). Regla: **siempre validar el GraphQL antes de ejecutar** — el validador existe exactamente para cazar campos inventados.

---

## 1. MAPEO SOP → ACCIONES DEL CONECTOR

Categorías: **[C]** conector Shopify directo · **[S]** automatizable fuera del conector (skill de El Faro u otra herramienta) · **[H]** humano, sin automatización honesta.

### Semana 1 — Fundaciones

| Paso del SOP | Cat. | Cómo se ejecuta |
|---|---|---|
| Diagnóstico completo: producto, mercado, validación | **[S]** | `el-faro-ficha-nicho` (research web real + Perfil A/B/C). Paso bloqueante: sin Ficha no se sigue. |
| Arquitectura de 3 niveles de producto | **[H]→[C]** | La **clasificación** de qué producto va en qué nivel es decisión humana (Fede + cliente, con la regla de ticket del Archivo). La **ejecución** es conector: tags `nivel-1/2/3` en `create-product` + 3 colecciones smart (`create-collection` con `ruleSet` TAG EQUALS). |
| Definir ticket protagonista y recorrido | **[H]** | Decisión estratégica. Sin automatización. |
| Elegir stack según proyecto | **[H]** | Decisión (Shopify vs sitio HTML — ya hay criterio en el Archivo). |
| Instalar GA4 y Pixel Meta desde el día 1 | **[H]** | **El conector NO lo cubre.** Se instala en el admin de Shopify vía canales Google & YouTube / Facebook & Instagram (o pegando el snippet en el tema). Es el olvido más probable del armado automatizado → va primero en el checklist de la sección 4. |

### Semana 2 — Tienda

| Paso del SOP | Cat. | Cómo se ejecuta |
|---|---|---|
| Carga de catálogo (productos con copy, fotos, precios, variantes) | **[C]** | `create-product` en batch: `title`, `descriptionHtml` (ya escrito, ver sección 3), `tags` de nivel, `productType`, `variants` con `price` + `sku` + `inventoryItem.tracked: true`, `images` (URLs públicas ya hosteadas en repo/Netlify — sin herramienta de subida en el conector). Queda en DRAFT. |
| Colecciones (protagonista visible, secundarias, rescate oculto) | **[C]** | `create-collection` smart por TAG. La descripción de la herramienta confirma que publica al canal Online Store — pero **qué colección entra al menú principal es edición de navegación, no del conector** (ver [H] abajo). |
| Stock inicial | **[C]** | `get-inventory-levels` → `set-inventory` (con `compareQuantity`, que falla seguro si el stock cambió entre lectura y escritura). |
| Home optimizada (trust bar → hero → combos → testimonios → CTA) | **[S]+[H]** | El orden de secciones se arma en el editor de tema de Dawn (humano). Los bloques custom (trust bar, banner envío gratis) los genera `el-faro-ajustes-tema` en Liquid y el humano los pega. El conector no edita temas. |
| Páginas de producto con tabs (Qué incluye / Cómo usar / Por qué / FAQ) | **[S]** | `el-faro-ajustes-tema` genera el Liquid; el contenido de los tabs puede viajar en el `descriptionHtml` con la estructura HTML que el Liquid espera (metodología ya probada en Symbiosis). Pegado: humano, una sola vez por tienda. |
| Reviews (Judge.me con bug en Dawn → hardcodeadas) | **[S]+[H]** | Instalar app: humano. Reviews hardcodeadas: `el-faro-ajustes-tema`. |
| Políticas de envíos y devoluciones | **[C con aprobación H]** | Claude redacta el borrador → **Fede/cliente aprueban el texto** (es contenido legal, nunca se publica sin ojo humano) → se cargan vía `graphql_mutation` (mutación de políticas de la tienda, validada antes con `validate_graphql_codeblocks`). Plan B si la mutación no está disponible en la versión de API: pegar a mano (2 min). |
| WhatsApp visible en todo el sitio | **[S]** | Botón flotante en Liquid → `el-faro-ajustes-tema`. |
| Footer completo (dirección, medios de pago, legales) | **[H]** | Editor de tema. Checklist manual. |
| Menú de navegación (solo Nivel 1 visible) | **[H]** | Admin → Navigation. Posible vía GraphQL en versiones recientes de la API, pero no está garantizado en las herramientas del conector → se trata como manual hasta probarlo en vivo contra Shudita. |
| Métodos de pago (Mercado Pago) y envíos (Andreani) | **[H]** | Credenciales y contratos del cliente. Nunca automatizable, y no debería serlo (regla de seguridad: credenciales las maneja el humano). |

### Semana 3 — Contenido y automatización

| Paso del SOP | Cat. | Cómo se ejecuta |
|---|---|---|
| Código de descuento | **[C]** | `create-discount` (código, %, alcance por colección, mínimo de compra, vigencia). Ojo: la herramienta **pide definir elegibilidad de clientes y fecha de inicio explícitamente** — dos decisiones que hay que traer resueltas de antemano (default El Faro: `all_customers`, inicio inmediato, sin fecha de fin salvo campaña puntual). |
| 30 posts Instagram en batch | **[S]** | Claude (copy) + DALL-E (generación) + Canva (edición — hay conector de Canva disponible para automatizar la composición). Fuera de Shopify. |
| Lead magnet en Netlify | **[S]** | Flujo ya documentado en el Archivo (Claude genera → GitHub → Netlify). |
| Sistema captación orgánica IG (palabra clave + DM automático) | **[H]** | Instagram Creator Tools, se configura desde el celular del cliente/Joe. Sin API accesible. |
| Secuencias Brevo (bienvenida, abandono) | **[S]+[H]** | Claude genera los HTML (`el-faro-newsletter` para el diseño de marca); armar la automatización en Brevo es clic humano (una vez). |
| Newsletter de lanzamiento | **[S]** | `el-faro-newsletter`. |

### Semana 4 — Lanzamiento

| Paso del SOP | Cat. | Cómo se ejecuta |
|---|---|---|
| Activar el catálogo completo | **[C]** | `bulk-update-product-status` → ACTIVE (por colección o lista de IDs; máx. 50 por llamada, puede haber fallas parciales → verificar después con `search_products status:draft`). |
| Revisión final como cliente (modo incógnito) | **[H]** | Insustituible. El conector ve datos, no ve la tienda como la ve un comprador. |
| Verificación de datos previa al lanzamiento | **[C]** | Batería de queries de la sección 4 (productos sin imagen, sin descripción, en draft, colecciones vacías). |
| Conversión orgánica >2% antes de ads | **[C]** | `run-analytics-query`: `FROM sessions SHOW sessions, conversion_rate TIMESERIES day SINCE -30d UNTIL today`. |
| Landing dedicada tráfico frío | **[S]+[H]** | Página en Shopify (posible vía `graphql_mutation` pageCreate, validar antes) o landing HTML del stack El Faro. Diseño: humano decide. |
| Primera campaña Meta Ads | **[H]** | Presupuesto real, cuenta del cliente. Nunca automatizado. |
| Rutina de métricas (15 min/día) | **[C]** | `run-analytics-query` + `list-orders`: el reporte diario se puede pedir en una conversación con la tienda conectada. Candidato natural a tarea programada más adelante. |

**Resumen honesto:** el conector automatiza el **corazón de la Semana 2** (catálogo + colecciones + stock + descuentos) y la **verificación de la Semana 4**. El tema (Liquid/diseño), los pagos, los envíos, GA4/Pixel y las redes siguen siendo mitad skill + mitad humano. La ganancia real: la carga de catálogo que hoy lleva horas de clics pasa a minutos, con menos errores de tipeo — y la verificación pre-lanzamiento deja de depender de la memoria.

---

## 2. SECUENCIA DE ARMADO — DE "TIENDA RECIÉN CREADA" A "LISTA PARA SEMANA 4"

Precondiciones: Ficha de Nicho hecha · Perfil asignado · lista de productos con fotos y precios · tienda Shopify creada y conectada al conector.

```
Paso 0 — Confirmar tienda conectada
  Ejecuta: conector (get-shop-info)
  Insumo: —
  Verificación: nombre y dominio coinciden con el cliente que se va a armar.
  REGLA DURA del modelo una-tienda-por-vez: si no coincide, switch-shop y
  re-verificar ANTES de crear nada. Ninguna escritura sin este paso.

Paso 1 — Clasificar el catálogo por nivel de ticket
  Ejecuta: humano (Fede/Joe) con Claude como apoyo, regla de Arquitectura de Ticket
  Insumo: lista de productos con precios
  Verificación: cada producto tiene nivel asignado; hay UN protagonista claro (combo
  o producto estrella); el rescate low-ticket no compite con el protagonista.

Paso 2 — Generar el copy completo en batch (ANTES de tocar la tienda)
  Ejecuta: skill el-faro-reescritor-descripciones
  Insumo: lista de productos + Ficha de Nicho (voz del rubro)
  Verificación: documento único de revisión con todas las descripciones;
  Fede/cliente aprueban ANTES de cargar. (Fundamento en sección 3.)

Paso 3 — Subir las fotos al CDN
  Ejecuta: hosteo previo en repo/Netlify (no existe herramienta de subida de imágenes en el conector) → URL pública HTTPS por producto
  Insumo: fotos del cliente, renombradas por producto
  Verificación: cada producto tiene al menos 1 URL HTTPS válida; sin URL no se
  crea el producto (regla: producto sin foto no entra ni en draft).

Paso 4 — Crear las 3 colecciones smart por nivel
  Ejecuta: conector (create-collection con ruleSet TAG EQUALS nivel-1/2/3)
  Insumo: nombres de colección con la voz del rubro (de la Ficha, no "Nivel 1")
  Verificación: get-collection muestra las reglas correctas; las colecciones
  existen ANTES que los productos para que se pueblen solas al cargar.

Paso 5 — Cargar el catálogo completo en DRAFT
  Ejecuta: conector (create-product por producto: title, descriptionHtml aprobado,
  tags de nivel, productType, vendor, variants con price+sku+inventoryItem.tracked,
  images con URLs del paso 3). NO pasar status: el default DRAFT es el seguro.
  Insumo: pasos 2 y 3 completos
  Verificación: search_products status:draft devuelve N = total del catálogo.

Paso 6 — Verificar que las colecciones se poblaron
  Ejecuta: conector (get-collection por colección)
  Verificación: la suma de productos de las 3 colecciones = N; ningún producto
  huérfano (search_products con tag_not:nivel-1 AND tag_not:nivel-2 AND tag_not:nivel-3 → 0).

Paso 7 — Setear stock inicial
  Ejecuta: conector (get-inventory-levels → set-inventory con compareQuantity)
  Insumo: stock real informado por el cliente
  Verificación: ningún variant trackeado en 0 salvo decisión explícita.

Paso 8 — Código de descuento de lanzamiento
  Ejecuta: conector (create-discount)
  Insumo: decisiones tomadas de antemano: %, código, all_customers, inicio, fin
  Verificación: el código aparece activo; probarlo en checkout es parte del Paso 13.

Paso 9 — Tema: home, tabs, trust bar, WhatsApp, footer
  Ejecuta: skill el-faro-ajustes-tema (genera Liquid) + humano (pega en Dawn y
  ordena secciones de la home)
  Insumo: Ficha de Nicho (paleta/voz), assets de marca
  Verificación: checklist de 25 puntos de el-faro-perfiles-cliente, mitad "tienda".

Paso 10 — Políticas de envío/devoluciones/privacidad
  Ejecuta: Claude redacta → humano APRUEBA texto → conector (graphql_mutation
  validada con validate_graphql_codeblocks) o pegado manual
  Verificación: las 3 políticas visibles en el footer del storefront.

Paso 11 — Menú de navegación
  Ejecuta: humano (Admin → Navigation)
  Verificación: SOLO la colección protagonista (Nivel 1) en el menú principal;
  Nivel 2 accesible pero no protagonista; Nivel 3 en NINGÚN menú.

Paso 12 — GA4 + Pixel Meta + Mercado Pago + Andreani
  Ejecuta: humano (canales/apps de Shopify + credenciales del cliente)
  Verificación: evento PageView visible en GA4 DebugView y en el Pixel Helper;
  compra de prueba llega hasta la pantalla de pago de MP.

Paso 13 — Barrido de calidad automatizado
  Ejecuta: conector (batería de queries de la sección 4)
  Verificación: cero hallazgos, o hallazgos resueltos.

Paso 14 — Activación
  Ejecuta: conector (bulk-update-product-status → ACTIVE) + humano (revisión
  final en incógnito, compra de prueba completa)
  Verificación: search_products status:draft → 0; la tienda queda en Semana 4
  (contenido, newsletter, ads) según SOP normal.
```

---

## 3. COPY DE PRODUCTO EN BATCH — DECISIÓN DE FLUJO

**Decisión: generar TODO el copy primero, cargar productos ya completos. Nunca cargar "en blanco" y actualizar después.**

| Criterio | Copy primero + `create-product` completo | Cargar en blanco + `update-product` después |
|---|---|---|
| Llamadas al conector | N (una por producto) | 2N (crear + actualizar) — doble superficie de error |
| Riesgo de publicar a medias | Nulo: nada existe sin copy | Real: un draft sin descripción puede activarse por error en el bulk final |
| Control de calidad humano | Un solo punto: Fede revisa TODAS las descripciones en un documento antes de que exista nada en la tienda | Fragmentado: revisar producto por producto ya cargado |
| Fallas parciales | Un producto que falla se recrea completo | Un update que falla deja un producto mudo y hay que detectarlo |
| Consistencia con la skill | `el-faro-reescritor-descripciones` YA trabaja en lote sobre una lista — es exactamente su formato de entrada/salida | Obligaría a la skill a trabajar contra GIDs de productos existentes |

**Flujo integrado:**
1. Lista de productos (nombre + descripción actual o solo nombre) → `el-faro-reescritor-descripciones` con la Ficha de Nicho → descripciones de 60-90 palabras con la voz del rubro.
2. Salida en un **documento de revisión único** (tabla: producto · nivel · precio · descripción · foto asignada). Fede/cliente aprueban ahí.
3. Aprobado → cada fila se convierte en una llamada `create-product` con el `descriptionHtml` final (si la tienda usa tabs de Dawn, el HTML ya viaja con la estructura que el Liquid de `el-faro-ajustes-tema` espera).
4. `update-product` queda reservado para **correcciones posteriores** (cambio de precio, foto nueva, ajuste de copy) — no es parte del armado inicial.

---

## 4. CHECKLIST DE CALIDAD DEL ARMADO AUTOMATIZADO

Extiende el checklist de 25 puntos de `el-faro-perfiles-cliente`. Enfocado en lo que falla específicamente cuando arma el conector. Cada punto trae su verificación ejecutable — la mayoría se corre con el propio conector en el Paso 13:

**Verificables por conector (barrido automatizado):**
- [ ] Ningún producto quedó en DRAFT tras la activación → `search_products` con `status:draft` = 0
- [ ] Ningún producto sin descripción → muestreo con `get-product` sobre el catálogo (o `graphql_query` filtrando `body_html` vacío)
- [ ] Ningún producto sin imagen → `get-product` por producto en el barrido; regla dura: sin foto no se crea (Paso 3)
- [ ] Ningún producto sin tag de nivel → `search_products` con `tag_not:nivel-1 AND tag_not:nivel-2 AND tag_not:nivel-3` = 0
- [ ] Las 3 colecciones tienen productos y la suma cierra → `get-collection` × 3
- [ ] Ningún variant con precio 0 o vacío → `search_products` con `price:0`
- [ ] Inventario: ningún trackeado en 0 sin decisión explícita → `get-inventory-levels` sobre protagonistas al menos
- [ ] Descuento activo, con la elegibilidad y vigencia decididas (no defaults accidentales) → revisar salida de `create-discount`
- [ ] `bulk-update-product-status` sin fallas parciales → re-consultar `status:draft` SIEMPRE después del bulk (la herramienta avisa que actualiza de a uno y puede fallar parcialmente; con más de 50 productos, correr en tandas)
- [ ] Conversión y sesiones reportando → `run-analytics-query` devuelve datos (si devuelve vacío a los días del lanzamiento, el tracking está roto)

**No verificables por conector (checklist manual obligatorio — acá vive el riesgo real del armado automatizado):**
- [ ] **GA4 + Pixel instalados** — el conector no los cubre y no los ve; es EL olvido típico. Verificar con DebugView/Pixel Helper, no de memoria.
- [ ] Colección Nivel 3 (rescate) fuera de todo menú y sin link en la home
- [ ] Menú principal: solo protagonista
- [ ] Políticas con texto aprobado (no borrador de Claude publicado sin leer)
- [ ] Mercado Pago activo con compra de prueba real hasta el final
- [ ] Andreani configurado con tarifas reales (no envío gratis accidental por zona sin tarifa)
- [ ] Tabs/trust bar/WhatsApp renderizando en mobile (el Liquid pegado a mano se prueba a mano)
- [ ] Open Graph de la tienda (título/descripción/imagen social en Preferencias) — mismo criterio que la vertical de sitios: el link se comparte por WhatsApp
- [ ] Revisión final en incógnito como comprador, siempre, sin excepción

---

## 5. CASO DE APLICACIÓN — SHUDITA (Paso 1: Fundaciones)

Lo que se sabe (Archivo Maestro): sahumerios, budas, artículos energéticos/bienestar · Perfil A (producto real, sin e-commerce) · cliente de confianza · modelo: armado de tienda + captación · **diagnóstico pendiente** — la Ficha de Nicho no se corrió.

**Cómo se ve el Paso 1 aplicando este procedimiento:**

1. **Correr `el-faro-ficha-nicho` primero.** Es paso bloqueante del SOP: referentes reales del nicho espiritual/bienestar en Argentina, vocabulario sí/no (el rubro tiene voz muy marcada: "energía", "armonía", "ritual" sí; tecnicismos no), motivación del visitante, objeción típica (calidad/origen de los productos). Sin esto no hay copy ni estructura.
2. **Hipótesis de arquitectura de niveles — A VALIDAR con el catálogo real, no es dato:**
   - Nivel 1 (protagonista): combos/kits rituales (ej. kit de armonización: sahumerios + porta + guía de uso) — máximo ticket, home + futura colección de ads.
   - Nivel 2: piezas individuales de ticket medio (budas, fuentes, decoración energética).
   - Nivel 3 (rescate, oculto): sahumerio/unidad suelta de bajo precio — solo mail de abandono/WhatsApp.
3. **Clasificación tag → colecciones smart** según sección 2, con nombres de colección en la voz del rubro que salga de la Ficha (no "Nivel 1").

**Qué falta pedirle a Fede/Joe antes de poder ejecutar (sin esto, nada de lo anterior arranca):**
- Catálogo real: lista de productos con **precios y stock** (no existe en el Archivo).
- **Fotos** por producto (calidad suficiente; definir si hace falta sesión o alcanza con las del cliente).
- Decisión de **ticket protagonista**: ¿existen combos hoy o hay que diseñarlos con el cliente? (En Perfil A casi siempre hay que diseñarlos — fue el aprendizaje de Symbiosis.)
- **Tienda Shopify creada y conectada** al conector (y confirmada con `get-shop-info` en el Paso 0).
- Datos para políticas: quién envía, desde dónde, plazos, cambios/devoluciones.
- WhatsApp del negocio y assets de marca (logo, paleta si existe).
- Credenciales que maneja el humano: Mercado Pago del cliente, alta en Andreani.

**Criterio de éxito de la prueba en vivo:** llegar del Paso 0 al Paso 8 (catálogo completo en draft + colecciones pobladas + descuento creado) en una sola sesión de conector, con el barrido del Paso 13 en cero hallazgos. Lo que se aprenda ahí (qué herramienta se comportó distinto a esta spec) actualiza este documento antes de convertirlo en skill.
