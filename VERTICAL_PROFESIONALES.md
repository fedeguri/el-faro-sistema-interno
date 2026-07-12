# PLAYBOOK VERTICAL — PROFESIONALES
## El Faro · Especialización vertical · Julio 2026
### Psicólogos, nutricionistas, kinesiólogos, coaches, contadores, abogados, arquitectos, escribanos, consultores — Argentina y Chile

**Estado:** borrador para aprobación de Fede. No convertir en skill ni cargar a Notion hasta aprobación.
**Base:** research desde cero, verificado con búsqueda web. Un solo playbook: todas las profesiones comparten la misma estructura de conversión (confianza en la persona + turno); lo que varía es tono y paleta (matriz en sección 1).

---

## 0. RESEARCH

### 0.1 Referentes globales (verificados)

1. **Authentic Connections Therapy** (EE.UU.). "Book Free Consultation" dos veces en la home, directo a un Calendly de 15 minutos. **Lección central de la vertical:** la consulta inicial gratuita y corta es EL producto de entrada — baja la barrera, filtra curiosos y es exactamente el embudo de El Faro (producto de entrada → upsell). Calendly ya está en nuestro stack.
2. **My LA Therapy**. Botón "Book Session" sticky en mobile + artículos largos que posicionan como referente local. **Lección:** el botón de turno persistente (patrón compartido con Estética) + el blog como SEO por especialidad, no como diario.
3. **Robyn (Begin Counseling y similares del roundup de High Five Design)**. El hero habla del DOLOR del cliente ideal antes que del profesional ("¿te levantás con ansiedad?" > "soy licenciada en..."). **Lección de copy:** primera persona del visitante arriba; credenciales después. Perfectamente alineado con "vender transformación, no características".
4. **Dr. Bogan (vía Headway)**. Lista visible de los 39 estados donde está habilitada (PSYPACT). **Traducción local:** matrícula, jurisdicción y modalidad (presencial/online, provincias que atiende) visibles arriba — es el trust signal barato que casi nadie local muestra.
5. **Lydia Adams Coaching**. Escalera de servicios explícita (1-a-1 → grupo → talleres) + quiz como lead magnet en la home. **Lección:** la escalera de ticket del profesional se muestra, no se esconde; el lead magnet interactivo captura al que no está listo (encaja con la metodología Brevo+Netlify ya probada).
6. **Minaa B.** (trabajo social/educación). Marca personal = cara + libros + newsletter "80.000 lectores". **Lección:** para coaches/consultores, la audiencia acumulada ES el trust signal — el sitio debe capturarla (Brevo), no solo mostrarla.

**Patrones transversales:** foto real del profesional con contacto visual en el hero (nunca stock); una página por especialidad/servicio para SEO (Google rankea "psicólogo ansiedad San Luis" a la página dedicada, no a la lista de servicios); paletas calmas de neutros + un acento; consulta gratuita como CTA principal; formularios mínimos.

### 0.2 Benchmarking local AR/CL — dónde diferenciarse

- **El profesional argentino típico no tiene sitio:** vive en directorios (BuscoPsi, Doctoralia para salud) e Instagram, y coordina turnos a mano por WhatsApp. La guía de BuscoPsi lo confirma: agenda manual por WhatsApp "funciona con pocos pacientes pero escala mal"; cobro por transferencia/CBU o Mercado Pago.
- **Hallazgo técnico clave (verificado):** **Calendly NO cobra con medios de pago latinos** — sus pagos son solo Stripe/PayPal, inviables para cobrar en ARS. Existe todo un mercado de herramientas locales que nació de ese hueco.
- **Motores de turnos locales verificados:**

| Motor | Precio | Notas |
|---|---|---|
| **Turnito App** (AR) | Plan gratis real (3 agendas, 100 reservas/mes); premium ~$21.400 ARS/mes O 5% de comisión solo si cobrás por la app | **Recomendado por defecto.** MP nativo (seña o total), recordatorios automáticos por WhatsApp, genera el link de Google Meet solo tras cada reserva. Resuelve agenda + videollamada + pago anticipado + no-shows en una sola pieza. |
| **ReservaSimple** (AR/Latam) | Gratis 30 turnos/mes; premium $16.999 ARS/mes | MP integrado, y **botón/iFrame embebible en cualquier sitio HTML** — el puente más limpio con nuestros sitios estáticos. |
| **Calendly** (ya en stack) | Gratis básico | Solo para la consulta inicial GRATUITA (15 min, Meet automático). Para sesiones pagas en ARS, no sirve. |
| **Psicobit** (AR, solo psicólogos) | Pago | HC + facturación AFIP — se menciona si el cliente psicólogo pregunta por gestión clínica; no es parte del sitio (ver límite en playbook Salud). |

- **El gap = mismo patrón que Estética e Inmobiliarias:** el profesional tiene el motor (o le sobra con Turnito gratis) pero cero capa de marca. La página de Turnito/Calendly es genérica; el diferencial de El Faro es el sitio propio con la persona, el método y las especialidades, con el motor embebido debajo.

---

## 1. FIRMA VISUAL — "TRAZO"

Distinta de Áurea (espiral), Vivir Bonito (proporción), Horizonte y Destello (turismo) y Halo (estética). Coherente con faro/guía: acá la luz es **la firma de una persona que te acompaña**.

- **Elemento recurrente — el trazo:** un subrayado hecho a mano (path SVG con textura de lapicera, animable con `stroke-dashoffset` al entrar en viewport) que subraya UNA palabra clave del hero ("acompañarte", "ordenar", "resolver") y aparece bajo la firma/nombre del profesional. Remite a la firma profesional y la matrícula — lo humano detrás del título.
- **Regla de uso:** máximo 3 trazos por página (hero, sección método, CTA final). Color: siempre el acento del cliente.
- **Retrato con presencia:** la foto del profesional en el hero, grande, con contacto visual, fondo desaturado hacia la paleta del sitio. Sin foto real del profesional NO hay sitio de esta vertical (es el trust signal #1 verificado en todo el research).
- **Tipografía estándar:** serif humanista de lectura larga — **Lora** (distinta de Fraunces/turismo y Playfair/estética) + Work Sans + IBM Plex Mono para datos duros (matrícula, duración de sesión, honorarios).
- **Matriz de tono por profesión** (misma estructura, distinto clima):

| Profesión | Paleta base + acento | Clima |
|---|---|---|
| Psicólogos, coaches, nutrición | Neutros cálidos + verde salvia o terracota | Calma, cercanía |
| Kinesiología, fisioterapia | Neutros fríos + azul profundo o verde agua | Movimiento, recuperación |
| Contadores, abogados, escribanos | Grises piedra + azul tinta o borravino | Sobriedad, precisión — trazo más fino, menos curvo |
| Arquitectos, consultores | Blanco + negro + UN acento fuerte | Portfolio primero, texto mínimo |

- **Movimiento canónico:** scroll-reveal estándar + animación del trazo (una sola vez por elemento) + hover sutil en tarjetas de especialidad. Nada más — esta vertical pide quietud.

---

## 2. ESPECIFICACIÓN TÉCNICA — AGENDA + VIDEOLLAMADA + PAGO ANTICIPADO

**Arquitectura del embudo (decisión de la vertical):** dos motores para dos momentos, ambos envueltos por el sitio de marca:

**Momento 1 — Consulta inicial gratuita (15-20 min):** Calendly, ya en stack. Genera el Meet automático, cero cobro (no hace falta), plan gratis alcanza. Es el CTA principal del sitio ("Agendá una primera charla sin cargo"). Para el profesional que no quiere regalar tiempo, se reemplaza por el Momento 2 directo.

**Momento 2 — Sesiones pagas:** **Turnito** (recomendado) o ReservaSimple embebido/enlazado. El motor resuelve las cuatro necesidades de la base de Fede de una vez: agenda 24/7, link de videollamada (Meet) automático, **pago anticipado con Mercado Pago (seña o total)** y recordatorios por WhatsApp que matan el no-show. Costo mensual: lo paga el profesional; el plan gratis de Turnito o el modelo 5%-solo-si-cobrás hacen el cierre indoloro.

**Sobre el pago anticipado en sesiones profesionales (la duda de Fede):** no hace falta la Ruta A.5 de turismo acá — el motor ya concilia pago↔turno, que era justamente lo caro de construir. Lo que sí es regla de la vertical es la **política de reprogramación** (misma lógica que turismo/estética): reprogramar gratis con 24-48 hs de aviso; la seña se pierde solo por ausencia sin aviso. Reembolso solo si cancela el profesional. Visible junto a cada botón de agenda, en tono amable. La Ruta A pura (WhatsApp + link de MP manual) queda como fallback para el profesional que se niega a usar motor.

**Los demás pedidos de la base, con honestidad:**
- **Formularios:** formulario de pre-consulta con datos NO sensibles (nombre, contacto, motivo general en lista cerrada, cómo nos conociste) vía formulario de Brevo (alimenta la lista) o Google Form. **Límite duro que adelanta al playbook de Salud:** si el profesional es de salud (psicólogo, nutricionista, kinesiólogo), el sitio NO pide síntomas, diagnósticos ni medicación — eso es dato sensible (Ley 25.326) y va en la consulta, no en un form de marketing.
- **WhatsApp "con IA":** lo que el cliente de verdad necesita —recordatorios y confirmaciones automáticas— ya lo da el motor de turnos por WhatsApp. Un bot conversacional con IA real (WhatsApp Business API + backend) es **fuera de stack actual**: marcarlo como upsell futuro, no prometerlo en el paquete base.
- **Blog:** no es un diario — son **páginas por especialidad** (patrón SEO verificado: una página por "ansiedad", "honorarios de sucesiones", "nutrición deportiva") + 1-2 artículos por mes como add-on de mantenimiento. Estructura ya compatible con la metodología de contenido de El Faro.
- **Captación de leads:** lead magnet (guía/quiz en Netlify) + Brevo — metodología ya probada en Symbiosis, se aplica tal cual. El quiz tipo "¿qué tan ordenadas están tus finanzas?" es el formato estrella de la vertical (verificado en referentes).

**Costo de desarrollo:** sitio completo 8-12 hs (sin componentes nuevos: retrato+trazo, tarjetas de especialidad, embed del motor, formulario Brevo). Configurar el motor con servicios/precios del cliente: 1-2 hs facturables. **Vive en: Paquete Base.**

---

## 3. BANCO DE OBJECIONES + HOOKS

### Objeciones del cliente final (responder EN el sitio)

1. **"¿Esto es para alguien como yo?"** → hero que describe la situación del visitante, no el CV del profesional. Sección "trabajo con personas que..." con 3-4 casos típicos.
2. **"¿Cuánto sale?"** → honorarios visibles o "desde", en mono. El rubro local los esconde; mostrarlos filtra y genera confianza (misma regla que estética).
3. **"¿Online funciona igual?"** → sección corta: cómo es una sesión online, qué necesitás, testimonio de paciente/cliente online.
4. **"¿Quién me garantiza que sabe?"** → matrícula + formación + años, arriba y en mono. Casos/resultados donde la ética lo permita (contadores/arquitectos sí; psicólogos, testimonios anónimos).
5. **"¿Y si no puedo ir / me arrepiento?"** → política de reprogramación en 2 líneas junto al botón.
6. **"Me da pudor consultar"** → la consulta inicial gratuita y breve existe exactamente para esto; nombrarla como "primera charla" (no "evaluación").
7. **"¿Es confidencial?"** → línea explícita de confidencialidad/secreto profesional donde aplique.
8. **"¿Cuánto tarda en verse un resultado?"** → rango honesto por servicio ("proceso de X sesiones/meses"), nunca promesas.

### Hooks de primer mensaje (al profesional — compatibles con `el-faro-primer-mensaje`)

1. *"¿Cuántas horas por semana se te van coordinando turnos por WhatsApp? Eso se agenda solo — con recordatorio automático y seña cobrada antes de la sesión."*
2. *"Busqué '[profesión] en [ciudad]' y aparecen tres colegas tuyos antes que vos. No atienden mejor: tienen página y vos tenés Instagram."*
3. *"¿Cuántos turnos perdés por mes por gente que no aparece? Con seña por Mercado Pago y recordatorio por WhatsApp eso baja en serio — y queda armado con tu nombre y tu marca, no con una plantilla."*
4. *"Tu Linktree manda a la gente a cinco lados. Una página tuya la manda a un solo lugar: tu agenda."*
5. *"Te muestro cómo se ve la página de un [profesión] hecha por nosotros — 15 minutos de llamada y la ves funcionando."*

---

## 4. CHECKLIST DE CALIDAD — EXTENSIÓN PARA PROFESIONALES

Se suma al checklist de 25 puntos de `el-faro-perfiles-cliente`:

- [ ] Foto real del profesional en el hero (contacto visual, sin stock) — sin foto no se entrega
- [ ] Matrícula/registro + jurisdicción + modalidad (presencial/online, zonas que atiende) visibles arriba
- [ ] Hero en segunda persona (la situación del visitante), credenciales después
- [ ] Una página o sección propia por especialidad (SEO), no una lista única de servicios
- [ ] Honorarios visibles o "desde" — jamás "consultar precio" a secas
- [ ] Consulta inicial (gratuita o no) como CTA principal, agendable sin hablar con nadie
- [ ] Motor de turnos configurado con TODOS los servicios, duraciones y precios antes de entregar
- [ ] Política de reprogramación en tono amable junto a cada punto de agenda
- [ ] Formulario de contacto SIN datos sensibles de salud (si es profesión de salud)
- [ ] Línea de confidencialidad/secreto profesional donde aplique
- [ ] Lead magnet definido y conectado a Brevo (o marcado explícitamente como fase 2)
- [ ] Tono y paleta según la matriz de la sección 1 (un abogado no recibe el sitio de un coach)

---

## 5. PRICING ANCLA

| Entregable | Ticket | Justificación |
|---|---|---|
| **Base profesional individual** (sitio de marca + especialidades + motor embebido + formulario Brevo) | **USD 250-400** | Complejidad técnica baja (cero componentes nuevos), volumen de mercado enorme — es la vertical de mayor repetibilidad de El Faro. El profesional ya paga $17-21 mil ARS/mes por el motor: el sitio one-time se justifica solo. |
| **Centros / estudios multi-profesional** (equipo, varias agendas, más páginas) | **USD 400-700** | Más contenido, más fotos, decisión grupal. |
| **Mantenimiento** | Estándar El Faro con el piso nuevo | Add-on natural: 1-2 artículos de especialidad por mes (SEO) + newsletter Brevo — esta vertical es la mejor para vender contenido recurrente porque el profesional VIVE de la autoridad. |
| **Upsell futuro** | A cotizar | Bot de WhatsApp con IA real (WhatsApp Business API) — fuera de stack hoy, documentado como fase 2. |

---

## PRÓXIMOS PASOS (post-aprobación)

1. Buscar el primer caso real (¿hay algún profesional en el entorno de San Luis para caso de éxito, patrón Vivir Bonito/Web Luli?) y correrle `el-faro-ficha-nicho`.
2. Abrir cuenta de prueba en Turnito para conocer el flujo real de embed/seña antes de prometerlo.
3. Construir el componente "retrato + trazo" (SVG animado) como bloque reutilizable.
4. Cargar este playbook a la Biblioteca de Verticales.
