# PLAYBOOK VERTICAL — ESTÉTICA
## El Faro · Especialización vertical · Julio 2026
### Centros de estética, spas, clínicas de belleza — Argentina y Chile

**Estado:** borrador para aprobación de Fede. No convertir en skill ni cargar a Notion hasta aprobación.
**Base:** research desde cero (no hay implementación previa de El Faro en esta vertical), verificado con búsqueda web.

---

## 0. RESEARCH

### 0.1 Referentes globales (verificados por búsqueda)

Todos aplicables a negocios chicos/medianos, sin franquicias internacionales:

1. **Tribeca MedSpa** (NYC). **Firma:** editorial sobrio, sliders simples, cero animación gratuita — diseño que envejece bien. **Estructura:** barra fija con teléfono + "Book Now" en TODAS las páginas; cajas de servicio interactivas en el home; tienda de productos como segundo ingreso. **Copy:** autoridad institucional. **Lección:** el botón de turno persistente es EL patrón de la vertical — el visitante decide en cualquier punto del scroll.
2. **Upkeep Med Spa** (NYC/Dallas). **Firma:** branding joven, tagline de posicionamiento ("Not Your Mother's Med Spa"). **Lección:** definir a QUIÉN le habla el centro (edad, primera vez vs. recurrente) cambia toda la paleta y el copy. Trasladable: el centro de barrio argentino que atiende "a la mujer real, no a la modelo" tiene ahí su ángulo.
3. **BeautyFix MedSpa** (NYC/Miami, Shopify). **Firma:** catálogo e-commerce de tratamientos, navegables como productos. **Lección clave:** tratar los tratamientos como fichas de producto (foto, qué es, duración, precio, botón) **quita la intimidación** del rubro — el visitante primerizo no quiere "pedir una consulta", quiere mirar el menú sin hablar con nadie.
4. **Skinney MedSpa** (NYC/Miami). **Firma:** dark luxury, flip-cards que revelan el detalle del tratamiento. **Movimiento:** microinteracción con propósito (revelar info), no decoración. **Lección:** el "lujo oscuro" funciona para clínicas de alto ticket; para el centro de barrio es contraproducente (intimida).
5. **Qazi Cosmetic Center** (California). **Firma:** hero oscuro + dorado que lidera con RESULTADO: "eliminá las cicatrices de acné — para siempre". **Lección:** mientras casi todos venden ambiente, los que convierten venden el resultado específico en el hero. El ángulo emocional del rubro no es "belleza": es **alivio de algo que incomoda hace años**.
6. **Milk + Honey** (Texas). **Firma:** serif + teal/dorado que tiende puente entre spa de relajación y clínica. **Lección:** si el centro hace ambas cosas (relax + aparatología), la marca tiene que abrazar las dos sin parecer dos negocios.
7. **Central Park Beauty** (NYC). **Estructura:** navegación doble — por tratamiento O por preocupación ("manchas", "flacidez", "vello"). **Lección:** la clienta no busca "radiofrecuencia", busca "papada". Navegar por preocupación es el patrón de conversión más robable de todo el research.

**Patrones transversales de los de punta:** (a) botón de turno fijo y persistente; (b) fichas por tratamiento con duración/sesiones/precio; (c) antes/después con marco cuidado (no collage de WhatsApp); (d) cara y credenciales del equipo bien arriba (confianza = personas, no aparatos); (e) copy de resultado y alivio, no de tecnología ("piel pareja en 4 sesiones", no "IPL de última generación").

### 0.2 Benchmarking local AR/CL — dónde diferenciarse

- **El patrón dominante local:** el centro de estética argentino/chileno NO tiene sitio propio. Su "web" es Instagram + un link de agenda genérica. Verificado en páginas reales de AgendaPro de centros argentinos (En Plenitud, Estética Agustina, Daniela Martínez): plantilla idéntica para todos, cero marca, políticas de cancelación pegadas EN MAYÚSCULAS en el campo de descripción, y avisos tipo "tocar timbre en puerta negra" mezclados con la lista de servicios. Funciona como agenda; como carta de presentación es un desastre.
- **Práctica local ya instalada (buena noticia):** la **seña previa para reservar turno** es estándar del rubro en Argentina — los centros ya la piden y las clientas ya la aceptan. No hay que evangelizar el pago anticipado; hay que hacerlo prolijo.
- **El gap = exactamente el producto de El Faro:** un sitio propio con marca real (la capa que Tribeca/BeautyFix tienen) MONTADO SOBRE el motor de turnos que ya usan o pueden usar. No competimos con AgendaPro — lo envolvemos.
- **Mapa de motores de turnos del mercado** (research verificado, para recomendar según cliente):

| Motor | Precio | Notas para El Faro |
|---|---|---|
| **Gendu** (AR) | Plan gratis sin límite de turnos; pagos desde ~$6.900 ARS/mes; 0% comisión; integra Mercado Pago | **Recomendado por defecto en Argentina** — precio en pesos, MP nativo para señas, plan gratis para arrancar. |
| **AgendaPro** (Latam) | Desde ~USD 40/mes, sin plan gratis | Para centros grandes/multi-sucursal, y **opción fuerte en Chile** (origen chileno, dominante allá). Sitio de reservas personalizable con logo y colores. |
| **Fresha** | Base gratis | Alternativa gratis internacional; menos arraigo local. |
| **Booksy** | USD/mes, sin Mercado Pago | Descartar para AR (costo en dólares + sin MP). |
| **Calendly** (ya en stack El Faro) | Gratis básico | Solo para centros de UNA profesional con pocos servicios; sin seña integrada (se resuelve con link de MP manual). |

### 0.3 Decisión de sistema de turnos: NO construir el calendario propio

El componente de calendario de Joe (turismo) resuelve **disponibilidad por día**. Estética necesita **turnos por hora × profesional × duración de tratamiento × sesiones múltiples**, con recordatorios anti-ausentismo y cobro de seña conciliado. Eso es un producto de software entero (es literalmente lo que venden Gendu/AgendaPro) y construirlo a USD 200-600 de ticket es un suicidio de rentabilidad, más el mantenimiento eterno.

**Reutilización honesta del componente de Joe:** sí sirve, adaptado, para UNA cosa — un "selector de tratamiento → resumen → WhatsApp prellenado" SIN calendario horario (el horario se coordina por WhatsApp o en el motor de turnos). Es la Ruta A de estética. El calendario por día de Joe queda para turismo.

---

## 1. FIRMA VISUAL DE EL FARO PARA LA VERTICAL

**Nombre interno: "Halo".** Distinta de Áurea (espiral), Vivir Bonito (áurea/naturales) y Turismo (horizonte/destello); coherente con faro = luz — acá la luz **envuelve** en vez de orientar.

- **Elemento recurrente — el halo:** un anillo fino de luz (border circular con gradiente sutil, o radial-gradient de fondo) que enmarca los tres momentos de conversión: la foto de la profesional, el antes/después, y el precio del tratamiento estrella. Regla: el halo aparece máximo 3-4 veces por página — es un subrayado, no un empapelado.
- **Luz de fondo:** radial-gradients muy suaves (5-8% de opacidad) detrás de secciones claves, que dan la sensación de piel iluminada sin usar ni una foto de stock de mujer con toalla.
- **Paleta base de la vertical:** neutros piel (crema, arena, piedra rosada) + UN acento profundo por cliente (vino, salvia, petróleo, cacao). Prohibido: el rosa chicle + dorado brillante del template de estética genérico, y el negro total (intimida al perfil de barrio; reservar dark solo para clínicas de ticket alto estilo Skinney).
- **Tipografía estándar de la vertical:** serif de alto contraste en display — **Libre Caslon Text o Playfair Display** (NO Cormorant Garamond: es la firma de Áurea) + sans geométrica humanista (Work Sans o Jost) + IBM Plex Mono solo para precios y duraciones ("45 MIN · 6 SESIONES").
- **Componente firma — antes/después con slider CSS puro:** `input range` + `clip-path`, sin librerías, con el halo como marco y etiqueta de consentimiento ("resultados reales, compartidos con autorización"). Ningún centro local tiene esto; es el equivalente al calendario de turismo: el componente que hace decir "quiero eso".
- **Movimiento canónico:** scroll-reveal estándar + hover de fichas de tratamiento que revela duración/sesiones/precio (versión liviana de las flip-cards de Skinney, sin 3D) + el halo con pulso lentísimo (4s) en el CTA principal. Todo apagado con reduced-motion.

---

## 2. ESPECIFICACIÓN TÉCNICA — SISTEMA DE TURNOS + SEÑA

### Ruta A — Selector + WhatsApp + seña por link manual

**Flujo:** ficha de tratamiento → "Reservar" abre el selector (tratamiento preseleccionado, zona/observaciones, nombre, teléfono, preferencia horaria en texto libre: "martes a la tarde") → resumen → WhatsApp prellenado → el centro propone horario → envía link de seña (Mercado Pago AR / Webpay.cl o Flow CL) → turno confirmado.

**Componente:** adaptación directa del selector+resumen de Joe, sin calendario. **Costo: 2-3h** (ya existe el 80%). **Vive en: Paquete Base.**

**Pros:** cero dependencia de terceros, el centro chico sigue su flujo actual (WhatsApp) pero ordenado, la seña ya es cultura del rubro. **Contras:** ida y vuelta para coordinar horario; sin recordatorios automáticos (el no-show es EL dolor del rubro y esta ruta no lo resuelve).

### Ruta B — Sitio de marca + motor de turnos embebido (RECOMENDADA COMO ESTÁNDAR)

**Flujo:** el sitio de El Faro es la cara (marca, fichas, antes/después, SEO local, OG para WhatsApp) y cada botón "Reservar" abre el motor de turnos del cliente — **Gendu en AR, AgendaPro en CL** — como embed o pestaña, con el servicio preseleccionado cuando la plataforma lo permita por URL. La seña se cobra dentro del motor (Gendu integra MP; AgendaPro tiene pagos online). Los recordatorios anti-ausentismo los pone el motor.

**Trabajo de El Faro:** configurar la cuenta del motor con los servicios/precios/duraciones del cliente (esto es servicio facturable, no favor), estilizar lo estilizable (AgendaPro permite logo y colores), y diseñar el puente visual sitio→agenda para que el salto no se sienta. **Costo: 4-8h** (sitio aparte). **Vive en: Base o Crecimiento.** Costo mensual del motor: lo paga el cliente (Gendu tiene plan gratis para arrancar — argumento de cierre perfecto).

**Nota de integración automática de pagos:** acá NO aplica la discusión serverless de turismo — el motor de turnos ya resuelve pago+conciliación+recordatorios. Construir eso a medida (functions de Vercel + MP) solo se justificaría para una clínica grande que quiera checkout propio, ticket USD 1.000+ — marcarlo como fuera de alcance estándar de la vertical y cotizar aparte si aparece.

**Decisión recomendada:** vender siempre Ruta B como estándar ("tu página + tu agenda que trabaja sola") y usar Ruta A solo cuando el cliente se niega a adoptar un motor de turnos o es una profesional sola con 10 turnos por semana.

---

## 3. BANCO DE OBJECIONES + HOOKS

### Objeciones de la clienta final (para responder EN el sitio, sin nombrarlas)

1. **"¿Duele?"** → en cada ficha de tratamiento, línea fija "qué se siente" con lenguaje honesto ("molestia leve, tolerable" > "indoloro" — la sobrepromesa mata la confianza).
2. **"¿Cuántas sesiones necesito de verdad?"** → duración + rango de sesiones en la ficha, en mono, sin letra chica. La transparencia acá es EL diferencial contra el rubro que esconde el número.
3. **"¿Es seguro? ¿Quién me atiende?"** → sección equipo con foto, nombre, matrícula/certificaciones. En estética la confianza es una persona con nombre, no un aparato.
4. **"¿Las fotos de resultados son truchas?"** → antes/después propios con etiqueta de consentimiento y condiciones reales ("misma luz, sin filtro, sesión 4 de 6").
5. **"¿Y si pago la seña y no puedo ir?"** → política de reprogramación en 2 líneas junto al botón: reprogramar gratis con 24-48h de aviso; la seña se pierde solo con ausencia sin aviso. (Es la política real que el rubro local ya usa — el diferencial es decirla ANTES y en tono amable, no en mayúsculas dentro del campo de descripción.)
6. **"Me da vergüenza consultar"** → navegación por preocupación (patrón Central Park Beauty): "manchas", "vello", "flacidez", "acné" — la clienta llega a la solución sin tener que escribirle a nadie.
7. **"Está caro"** → precio anclado por sesión Y por plan ("$X la sesión · plan 6 sesiones $Y") + cuotas de MP visibles. El rubro local esconde precios; mostrarlos filtra curiosas y atrae decididas.
8. **"¿Me van a querer vender de más?"** → CTA de entrada de bajo compromiso: "diagnóstico de piel sin cargo" o "primera consulta" como producto de entrada (embudo: consulta → tratamiento → plan).

### Hooks de primer mensaje (prospección al dueño/a — compatibles con `el-faro-primer-mensaje`)

1. *"Vi que manejás los turnos por Instagram y WhatsApp. ¿Cuántas horas por semana se te van en coordinar horarios y perseguir señas? Eso se automatiza — y tu página lo hace mientras atendés."*
2. *"Tu trabajo se ve increíble en las historias… que desaparecen a las 24 horas. Una página con tus resultados (antes/después con marca propia) trabaja para vos todos los días, no un día."*
3. *"¿Cuántos turnos perdés por mes por ausencias? Un sistema con seña online y recordatorio automático baja eso en serio — y lo dejamos armado con tu marca, no con la plantilla que usan todas."*
4. *"Busqué 'depilación definitiva en [ciudad]' — aparecen tres competidoras tuyas y vos no. No es que trabajen mejor: tienen página y vos tenés solo Instagram."*
5. *"Tu link de reservas es la misma plantilla gris que usan otros veinte centros. La clienta nueva no ve TU marca ni tus resultados antes de decidir. Te muestro cómo se ve un centro con página propia — llamada de 15 minutos y te lo enseño."*

---

## 4. CHECKLIST DE CALIDAD — EXTENSIÓN PARA ESTÉTICA

Se suma al checklist de 25 puntos de `el-faro-perfiles-cliente` (que aplica completo). Solo lo específico del rubro:

- [ ] Galería de resultados SOLO con consentimiento de imagen confirmado por el cliente — pedirlo explícitamente en el onboarding; sin consentimiento, no se publica (riesgo legal y de confianza)
- [ ] Antes/después en condiciones comparables y con etiqueta de autenticidad; nunca fotos de stock presentadas como resultados
- [ ] Ficha por tratamiento con: qué es (1 línea), qué se siente, duración, rango de sesiones, precio (por sesión y plan), cuidados pre/post
- [ ] Copy sin promesas médicas absolutas ("definitiva", "elimina para siempre", "sin ningún riesgo") — usar "progresiva", "reducción", "resultados visibles desde…"; contraindicaciones mencionadas donde aplique
- [ ] Nombre, foto y credenciales/matrícula del equipo visibles arriba del fold o en sección propia
- [ ] Navegación doble: por tratamiento Y por preocupación
- [ ] Botón "Reservar" persistente (header fijo) + en cada ficha de tratamiento
- [ ] Política de seña y reprogramación en tono amable, junto a cada punto de reserva (no en mayúsculas, no escondida)
- [ ] Producto de entrada definido (consulta/diagnóstico) como CTA de bajo compromiso
- [ ] Motor de turnos configurado con TODOS los servicios, duraciones y precios reales antes de la entrega (la agenda vacía o desactualizada mata la conversión el día 1)
- [ ] Horarios de atención + ubicación + cómo llegar (el negocio es 100% local: SEO local y Google Maps pesan más que en cualquier otra vertical)
- [ ] Instagram enlazado como prueba social viva (el rubro vive ahí; el sitio no lo reemplaza, lo capitaliza)

---

## 5. PRICING ANCLA DE LA VERTICAL

| Entregable | Ticket | Justificación de mercado |
|---|---|---|
| **Base estética** (sitio de marca + fichas + antes/después + Ruta A o puente a motor de turnos) | **USD 250-450** | Menor complejidad técnica que turismo (sin calendario propio, sin pago custom). El mercado local paga USD 40/mes solo por AgendaPro — un sitio propio one-time a este ticket es fácil de justificar. Piso USD 250: nunca competir con "la página de Wix del sobrino". |
| **Con motor de turnos configurado (Ruta B completa)** | **USD 400-600** | Suma la configuración completa de Gendu/AgendaPro (servicios, precios, señas, recordatorios) + puente visual. Se vende como "tu recepcionista digital". |
| **Mantenimiento mensual** | Estándar El Faro (con la suba de piso ya decidida) | Trabajo recurrente natural del rubro: promos del mes, precios (inflación AR obliga a actualizar seguido — argumento real), resultados nuevos a la galería. |
| **Add-on natural: newsletter mensual Brevo** | Según catálogo de add-ons | El rubro vive de la recompra (sesiones, mantenimiento, promos) — es LA vertical para vender la reactivación de base y el newsletter con diseño de marca ya probados en Symbiosis. |

**Nota Chile:** misma lógica, precios en CLP; motor recomendado AgendaPro (dominante allá); seña por Webpay.cl/Flow según formalización del cliente (detalle completo en el playbook de Turismo, sección 2 — aplica igual).

---

## PRÓXIMOS PASOS (post-aprobación de Fede)

1. Validar la firma "Halo" con un caso real — buscar 1 centro de estética conocido para caso de éxito (mismo patrón de arranque que Vivir Bonito/Web Luli), idealmente en San Luis.
2. Correr `el-faro-ficha-nicho` completa sobre ese primer caso (este playbook es de vertical, no reemplaza la Ficha por cliente).
3. Construir el componente antes/después (slider CSS) y las fichas de tratamiento como bloques reutilizables de `el-faro-perfiles-cliente`.
4. Abrir cuenta de prueba en Gendu para conocer el flujo real de embed/seña antes de prometerlo en una propuesta.
5. Cargar este playbook a la Biblioteca de Verticales de Notion.
