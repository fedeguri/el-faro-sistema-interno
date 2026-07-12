# ANÁLISIS — PATRONES QUE HACEN QUE UNA PÁGINA SE VEA "TOP"
## El Faro · Julio 2026 · Insumo para prompt de Fable

Investigado contra research real de tendencias 2026 (Awwwards, agencias especializadas, UX Collective).
Objetivo: que ninguna de las 5 verticales de El Faro se vea "como un blog" — plantilla genérica,
columna única, cards uniformes sin jerarquía, cero firma visual.

**Advertencia de calibración (de la skill de diseño de El Faro):** hay 3 looks que el diseño con IA
repite sin pensar: fondo crema + serif alto contraste + acento terracota; fondo casi negro + un
acento verde ácido o vermellón; layout tipo diario con hairlines y cero border-radius. Los tres son
válidos si el brief los pide — pero por defecto son la salida genérica de cualquier IA, no una
decisión. El Faro ya evita esto con la firma por vertical (Horizonte y Destello, Halo, Trazo, Pulso,
Plano) — hay que sostenerlo también en los patrones de interacción, no solo en la paleta.

---

## A. MOVIMIENTO DE SCROLL / STORYTELLING

| Patrón | Qué es | Fit por vertical |
|---|---|---|
| **Scroll-triggered reveal con propósito narrativo** | No fade-in genérico — cada sección revela algo que construye sobre la anterior (no decorativo, informativo) | Todas, ya lo usamos |
| **Scroll-as-navigation (wayfinding)** | Indicador de progreso o marcador visual de "dónde estoy" en una página larga | Salud (protocolo de emergencias como recorrido), Inmobiliarias (ficha larga de propiedad) |
| **Parallax de profundidad por capas** | Fondo, capa media y primer plano se mueven a velocidades distintas al scrollear | Turismo (hero de destino), Inmobiliarias (retícula de plano de fondo) |
| **Scroll narrativo de producto/escena** | El scroll "avanza" una escena (ej: un mapa que se despliega, una cabaña que se arma) | Turismo (alto impacto, alto costo — reservar para el paquete Full) |
| **Sticky reveal (elemento fijo mientras el contenido pasa al lado)** | La imagen o dato clave queda fija mientras el texto scrollea a su lado | Salud (ficha de tratamiento), Profesionales (proceso de trabajo) |

## B. CURSOR E INTERACCIÓN CON EL PUNTERO

| Patrón | Qué es | Fit por vertical |
|---|---|---|
| **Botón magnético** (ya en la demo) | El botón se acerca sutilmente al cursor cuando pasa cerca | Turismo, Estética, Inmobiliarias |
| **Cursor-glow ambiental** (ya en la demo) | Halo de luz que sigue al cursor dentro de una sección | Turismo, Estética |
| **Cursor custom contextual** | El cursor cambia de forma/texto según sobre qué elemento pasa ("Ver", "Reservar", "→") | Inmobiliarias (sobre el mapa), Turismo (sobre la galería) — cuidado: en mobile no existe cursor, siempre necesita fallback |
| **Tilt 3D en tarjetas** (ya en la demo) | La tarjeta se inclina según la posición del mouse, con reflejo que sigue el cursor | Inmobiliarias (fichas de propiedad), Turismo (tarjetas de servicio) |
| **Hover con "peek" de contenido oculto** | Al pasar el mouse, se asoma un dato extra sin hacer clic (precio, disponibilidad) | Estética (ya lo tenemos en las fichas Halo) |
| **Cursor como pincel/máscara** | El cursor "revela" una segunda imagen o texto oculto al pasar por encima (efecto linterna) | Estética (antes/después con linterna en vez de slider — variante más premium del componente que ya existe) |
| **Magnetic snap de galería** | Las imágenes de una galería se alinean/snapean al cursor al pasar cerca, dando sensación táctil | Turismo, Inmobiliarias |

**Nota importante de accesibilidad:** ningún patrón de cursor puede ser la ÚNICA forma de acceder a
información — mobile/touch no tiene cursor. Todo patrón de esta categoría necesita su versión táctil
(tap en vez de hover) ya resuelta, como ya hicimos en el componente Halo.

## C. TIPOGRAFÍA CINÉTICA

| Patrón | Qué es | Fit por vertical |
|---|---|---|
| **Texto con revelado escalonado** (ya en la demo) | Palabras o letras que suben/aparecen una por una al cargar | Todas, con moderación |
| **Kinetic headline en hero** | El titular principal se arma con una animación de peso variable (font-weight que cambia) o de trazo | Profesionales ("Trazo" es la vertical con más margen para esto — literal en la firma) |
| **Texto que "se estira" al hacer scroll** | Letras que cambian de tracking/ancho según posición de scroll | Solo para un hero puntual, alto riesgo de verse gimmick si se abusa |
| **Subrayado/marcador animado en palabra clave** | Ya lo construimos en Trazo — aplica el mismo principio a otras verticales con su propio motivo (línea de pulso bajo palabra clave en Salud, por ejemplo) | Ya implementado en Trazo |

## D. PROFUNDIDAD Y 3D

| Patrón | Qué es | Fit por vertical |
|---|---|---|
| **Objetos 3D que reaccionan al cursor/scroll** | Un elemento 3D simple (no un modelo complejo) que gira o se inclina | Turismo (alto impacto en hero), Inmobiliarias (maqueta simplificada de planta) — requiere Three.js, evaluar costo/beneficio por cliente |
| **Capas apiladas con sombra progresiva** | Tarjetas que se "levantan" del fondo con sombra que crece al hover, sensación de objetos reales | Estética (fichas de tratamiento), Inmobiliarias (fichas de propiedad) |
| **Glassmorphism con criterio** | Paneles semitransparentes con blur — "está de vuelta" según el research 2026, pero hay que usarlo con más madurez que en 2021: solo en overlays/modales, nunca en toda la página | Estética, Turismo — con moderación, es fácil que se vea dated si se abusa |
| **Bento grid** | Layout tipo colcha de retazos con bloques de distinto tamaño, cada uno con su propia jerarquía | Inmobiliarias (dashboard de zona/mercado), Profesionales (escalera de servicios) |

## E. MICRO-INTERACCIONES DE FEEDBACK (la categoría más importante según el research 2026)

El hallazgo más consistente de la investigación: las micro-interacciones en 2026 **enseñan**, no
decoran. No es "que se mueva algo", es que el movimiento le diga algo al usuario. Ejemplos aplicables:

| Patrón | Qué es | Fit por vertical |
|---|---|---|
| **Validación de formulario que enseña, no que regaña** | En vez de "campo inválido" en rojo, una animación breve que muestra qué está bien ahora (ej: el candado que se abre) | Todas — el formulario de reserva/turno de cada vertical |
| **Confirmación con peso** | Al completar una acción (reservar, enviar), una animación breve y contenida confirma — no un alert genérico | Todas — coherente con haber sacado los `alert()` de los componentes ya construidos |
| **Estado de carga con personalidad** | Mientras algo procesa (el filtro del buscador de Inmobiliarias, por ejemplo), un indicador que es parte de la marca, no un spinner genérico | Inmobiliarias, Turismo |
| **Progreso visible en formularios largos** | Si el formulario de pre-tasación (Inmobiliarias) o el de turno tiene varios pasos, mostrar en qué paso está | Inmobiliarias, Salud |

**Regla de oro del research:** animaciones de menos de 300ms para feedback de acción — más que eso
se siente lento, no premium.

## F. TRANSICIONES Y CARGA

| Patrón | Qué es | Fit por vertical |
|---|---|---|
| **Transición de página sin corte** | Al navegar entre secciones/páginas del sitio, un cruce suave en vez de blanco-carga-blanco | Todas, alto impacto percibido, complejidad media |
| **Loader de marca (si hace falta esperar)** | Si el sitio tiene alguna carga real (mapa, imágenes pesadas), un loader que usa el motivo visual de la vertical (ej: el pulso cargando en Salud, la rosa de los vientos girando en Inmobiliarias) en vez de un spinner genérico | Salud, Inmobiliarias |

## G. LO QUE ROMPE EL "LOOK DE BLOG" — checklist anti-genérico

Esto es tan importante como los patrones de arriba. Un sitio se ve "como blog" cuando tiene:

- Una sola columna centrada de texto sin variación de ancho o ritmo
- Cards idénticas en grid uniforme, sin ninguna destacada ni jerarquía visual
- Espaciado por defecto de framework (Bootstrap/WordPress) sin ritmo propio
- Cero elemento de firma — nada que sea reconociblemente de esa marca si le sacás el logo
- Fotos de stock genéricas en vez de reales
- Botones default del navegador o sin tratamiento
- Ningún momento "hero" — el título de arriba es igual de peso que el resto

**La firma visual de cada vertical de El Faro ya ataca esto de raíz** (el destello, el halo, el
trazo, el pulso, la retícula) — el trabajo de esta ronda es sumarle interacción a esas firmas, no
reemplazarlas.

## H. SONIDO (mencionar, no priorizar)

El research 2026 marca sonido sutil como tendencia emergente (confirmaciones, transiciones) — pero
siempre opcional, silenciable, y ligado a accesibilidad. Para El Faro: **descartar por ahora**. Es
la categoría con menos retorno para el ticket que manejamos y el mayor riesgo de sentirse invasivo
si se hace mal. Revisar en un año si sigue siendo tendencia real y no una moda de paso.

## I. PERSONALIZACIÓN ADAPTATIVA (mencionar como horizonte, no para esta ronda)

El research menciona sitios que cambian contenido según el visitante (nuevo vs. recurrente, hora del
día). Interesante para el futuro (ej: Inmobiliarias mostrando "propiedades nuevas desde tu última
visita"), pero requiere estado/backend — fuera del stack estático actual. Anotar como línea de
Ruta B/upsell futuro, mismo criterio que ya usamos con IA real en WhatsApp o búsqueda en Inmobiliarias.

---

## PRIORIZACIÓN SUGERIDA PARA EL PRÓXIMO PROMPT A FABLE

No pedir las 9 categorías completas — es demasiado para una tanda. Priorizar:

1. **Categoría E (micro-interacciones que enseñan)** — el hallazgo más respaldado por el research,
   aplica a las 5 verticales, y ya tenemos la base (sacamos los `alert()` en todos los componentes).
2. **Categoría B (cursor)** — ya validamos el concepto con la demo, ampliar el repertorio con
   variantes por vertical (cursor de linterna en Estética, tilt en Inmobiliarias).
3. **Categoría A (scroll con propósito)** — el sticky reveal es directamente aplicable a fichas
   largas (Salud, Inmobiliarias) sin mucho costo de desarrollo.
4. Dejar 3D real (D) y transiciones de página completas (F) para una ronda posterior — son las de
   mayor costo de desarrollo relativo al beneficio en el ticket actual.
