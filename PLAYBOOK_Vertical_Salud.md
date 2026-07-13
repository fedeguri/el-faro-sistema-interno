# PLAYBOOK VERTICAL — SALUD
## El Faro · Especialización vertical · Julio 2026
### Odontólogos, dermatólogos, oftalmólogos, clínicas, veterinarias — Argentina y Chile

**Estado:** borrador para aprobación de Fede. No convertir en skill ni cargar a Notion hasta aprobación.
**Base:** research desde cero, verificado con búsqueda web (incluye marco legal argentino verificado en fuentes oficiales).

---

## 0. RESEARCH

### 0.1 Referentes globales (verificados)

1. **Tend** (NYC, cadena boutique dental). Reinventa la experiencia del paciente desde el sitio: video de marca, copy sin jerga, reserva arriba del fold. **Lección:** en salud el sitio no vende un servicio — desactiva un miedo. Todo lo demás es secundario.
2. **Prism Oral Surgery & Implants**. Hero para el paciente asustado: "Precision. Comfort. Compassion." — responde ansiedad (dolor, sedación, recuperación, costo) antes de mostrar procedimientos. **Lección de copy central de la vertical:** el ángulo emocional es alivio y seguridad, nunca tecnología.
3. **Vivid Specialized Dentistry** (Edmonton). Antes/después contados como **historias de pacientes** (no galería muda), contador de estadísticas animado, 200+ reseñas, "Book a Consult" en cada pantalla. **Lección:** el caso clínico narrado convierte más que la foto sola; el volumen de reseñas es el trust signal dominante.
4. **Pediatric (roundup Orbix)**. Urgencias visibles y claras ("emergencia dental: llamá ya al X"), obras sociales/financiación/formularios ANTES de la primera visita. **Lección:** la transparencia administrativa (qué cubre, cuánto sale, qué llevar) reduce fricción de mostrador — y es contenido que ningún competidor local publica.
5. **Jackson Family Dental**. Estética spa que baja la ansiedad; la fuente reporta +34% de conversión tras el rediseño. **Lección:** el diseño calmo es medible en turnos, no es decoración.
6. **Dentologie / Dntl Bar** (Chicago/NYC). Marca pop que desdramatiza el rubro. **Lección:** para clínicas jóvenes urbanas, romper el "celeste hospital" es en sí el posicionamiento.

**Patrones transversales:** reducir ansiedad por diseño; navegación por tratamiento + educación del paciente; equipo real con nombre y matrícula (nunca stock); obras sociales/medios de pago/financiación visibles; CTA de turno persistente; urgencias claras.

### 0.2 Benchmarking local AR/CL — dónde diferenciarse

- **El turno médico local vive en Doctoralia (DocPlanner)**: perfil + reputación + agenda. Para el paciente es cómodo; para la clínica es el mismo problema de siempre — la marca es de Doctoralia, la clínica es un renglón entre competidores, y paga por estar.
- **El sitio propio de la clínica chica argentina** es inexistente o una plantilla vieja sin turnos, sin precios, sin obras sociales listadas. Nadie publica la información administrativa que el paciente necesita (¿atendés mi obra social? ¿cuánto sale la consulta particular? ¿qué llevo?).
- **El gap de El Faro:** sitio propio con marca + contenido educativo + info administrativa completa, con el motor de turnos que la clínica YA usa embebido debajo (Doctoralia tiene widget de reservas para sitios propios; consultorios chicos pueden usar Turnito/ReservaSimple — ver playbook Profesionales). No competimos con Doctoralia: la envolvemos, igual que Gendu en Estética.

### 0.3 Marco legal — el límite duro de "historia clínica básica" (verificado en fuentes oficiales)

Esto responde la pregunta de Fede sin ambigüedad. Tres normas argentinas aplican:

- **Ley 26.529 (Derechos del Paciente):** la historia clínica es documento obligatorio, cronológico, foliado y completo; el paciente es su titular (copia en 48 hs si la pide); se conserva 10 años; y su versión informatizada (art. 13) exige integridad, autenticidad, inalterabilidad, perdurabilidad, accesos restringidos y trazabilidad.
- **Ley 25.326 (Protección de Datos Personales):** los datos de salud son **datos sensibles** — el nivel más alto de protección. Incumplir habilita habeas data ante la AAIP, acción civil por daños y denuncia ante el colegio profesional.
- **Ley 27.706:** programa federal de digitalización de historias clínicas (con su reglamentación) — el Estado ya define estándares para HCE.

**Conclusión operativa — regla innegociable de la vertical:**

> **El sitio que construye El Faro NUNCA almacena, transmite ni pide datos clínicos.** Nada de síntomas, diagnósticos, medicación, estudios ni "fichas de paciente" en formularios de Brevo, Google Forms o el hosting del sitio. Un formulario de marketing no cumple ni puede cumplir los requisitos del art. 13 (integridad, trazabilidad, inalterabilidad) — y el responsable legal ante una filtración es el profesional, nuestro cliente. "Historia clínica básica" NO es un feature del sitio: es el software médico especializado del cliente (el que ya usa su clínica, o soluciones tipo Psik para salud mental, HSI pública, etc.). El Faro puede recomendar categorías de software, jamás operar la HC ni improvisarla.

**Lo que el sitio SÍ hace (y es todo lo que el paciente necesita del sitio):** formulario de solicitud de turno con nombre, contacto, especialidad y motivo GENERAL en lista cerrada ("consulta", "control", "urgencia"), obra social. Los recordatorios "con IA" los da el motor de turnos (WhatsApp automático — ver Profesionales); no se construyen custom.

---

## 1. FIRMA VISUAL — "PULSO"

Distinta de todas las anteriores. Coherente con faro/luz: acá la luz es **señal de vida estable**.

- **Elemento recurrente — la línea de pulso:** una línea horizontal fina que recorre los dividers de sección, con UN latido sutil (pico de electrocardiograma minimalista, redondeado, nada dramático) en el punto donde está el CTA o el dato clave. Animable con `stroke-dashoffset` al entrar en viewport; estática con reduced-motion. Es la hermana clínica de la línea de horizonte de turismo — misma familia El Faro, señal distinta.
- **Regla:** el latido aparece solo en momentos de acción (turno, urgencias, teléfono). El resto de la línea es plana = calma.
- **Paleta base de la vertical:** blanco hueso + verde salvia o azul petróleo profundo + UN acento cálido (coral suave o ámbar) para CTAs. **Prohibido:** el celeste-hospital + blanco frío del rubro, y el rojo salvo en el bloque de urgencias (donde es funcional).
- **Tipografía estándar:** sans humanista muy legible como protagonista — **Source Sans 3 o Inter** para todo el cuerpo (en salud la legibilidad ES la marca) + una serif solo en titulares de historias de pacientes (Lora) + IBM Plex Mono para datos administrativos (horarios, obras sociales, matrículas).
- **Fotografía:** equipo e instalaciones reales, luz natural. Cero stock de médicos con brazos cruzados — el research global es unánime: el stock destruye la confianza en este rubro más que en ningún otro.
- **Movimiento canónico:** mínimo absoluto. Scroll-reveal suave + el pulso + contador de números (años, pacientes, reseñas — patrón Vivid). Nada más.

---## 2. ESPECIFICACIÓN TÉCNICA — TURNOS + LO QUE NO SE CONSTRUYE

**Decisión estructural (idéntica lógica a Estética):** no construir motor de turnos ni nada que toque datos clínicos. El sitio es la capa de marca, educación y administración; el motor y la HC son del ecosistema del cliente.

**Turnos, según el cliente:**
- **Clínica que ya usa Doctoralia** → embeber el widget de reservas de Doctoralia en el sitio propio (existe para este fin) o enlazar al perfil con el botón persistente. La reputación acumulada ahí se capitaliza, no se abandona.
- **Consultorio chico sin sistema** → Turnito/ReservaSimple (ver playbook Profesionales): MP para seña de particular, recordatorios WhatsApp, gratis para arrancar.
- **Clínica con software médico propio con turnos online** → enlazar a su portal de pacientes. El Faro no duplica.

**Bloque de urgencias (el "protocolo de emergencias" de la base de Fede):** es CONTENIDO, no software — una sección fija, visible desde el header, con: síntomas/situaciones que son urgencia en esa especialidad, qué hacer ahora, teléfono de guardia propio o del sistema de emergencias, horarios reales de atención de urgencias. En veterinarias, este bloque es lo más buscado del sitio (verificado en el patrón pediátrico: la búsqueda de emergencia es bajo estrés — claridad total, cero scrolls).

**Contenido educativo (el diferencial rentable):** páginas por tratamiento con la estructura verificada: qué es (1 línea) → qué se siente / cómo es la visita → duración y sesiones → cuidados previos/posteriores → precios particulares "desde" u obras sociales que lo cubren → FAQ. Más 2-3 historias de pacientes narradas (con consentimiento escrito). Este contenido es lo que Google rankea y lo que ninguna clínica local publica.

**Info administrativa completa:** obras sociales y prepagas atendidas (lista explícita, actualizable — es EL motivo de llamada #1), medios de pago y financiación, qué llevar a la primera consulta, cómo llegar/estacionamiento.

**SEO local:** Google Business Profile optimizado (categorías, fotos reales, horarios, preguntas respondidas) como parte del paquete — en salud, el mapa de Google ES la primera página del sitio.

**Costo de desarrollo:** 14-20 hs (más páginas y más rigor de contenido que Profesionales; el contenido educativo requiere validación del profesional — ciclo de revisión incluido en el plazo). **Vive en: paquete propio de la vertical (ver pricing).**

---

## 3. BANCO DE OBJECIONES + HOOKS

### Objeciones del paciente (responder EN el sitio)

1. **"¿Me va a doler?"** → línea "cómo es la visita / qué se siente" en cada ficha de tratamiento, honesta.
2. **"¿Atienden mi obra social?"** → lista completa y visible; si no atiende ninguna, precios particulares claros y financiación.
3. **"¿Cuánto me va a salir?"** → "desde" en tratamientos particulares + política de presupuesto sin cargo donde aplique.
4. **"¿Es de confianza este lugar?"** → equipo con nombre, foto y matrícula; reseñas de Google embebidas o citadas; años e historia del lugar.
5. **"¿Y si es una urgencia?"** → bloque de urgencias visible desde cualquier página.
6. **"¿Van a quererme vender tratamientos de más?"** → consulta diagnóstica como producto de entrada + copy de plan de tratamiento explicado por escrito.
7. **"¿Las fotos de resultados son reales?"** → historias de pacientes con consentimiento explícito y condiciones comparables (misma regla que Estética).
8. **"Hace años que no voy, me da vergüenza"** → (oro en odontología) sección "si hace mucho que no venís" sin juicio — los referentes globales que la tienen la explotan porque nadie más le habla a ese paciente.

### Hooks de primer mensaje (al profesional/clínica — compatibles con `el-faro-primer-mensaje`)

1. *"¿Cuántas llamadas por día atiende tu secretaria solo para responder '¿atienden [obra social]?'? Eso lo responde tu página — y la secretaria vuelve a atender pacientes."*
2. *"Tu clínica vive en el perfil de Doctoralia: entre dos competidores y con la marca de ellos. Tu propia página arriba de esa agenda te devuelve la marca sin perder los turnos."*
3. *"Busqué '[especialidad] en [ciudad]': aparece Doctoralia, aparece un colega, no aparecés vos. El paciente nuevo elige al que encuentra."*
4. *"¿Cuántos turnos se pierden por mes por ausencias? Recordatorio automático por WhatsApp + seña para particulares: eso se configura una vez y trabaja solo."*
5. *"Las urgencias te llegan por teléfono a cualquier hora preguntando lo mismo. Una página con 'qué hacer si...' y el teléfono de guardia filtra y ordena — y a la vez es lo que más confianza le da a un paciente nuevo."*

---

## 4. CHECKLIST DE CALIDAD — EXTENSIÓN PARA SALUD

Se suma al checklist de 25 puntos de `el-faro-perfiles-cliente`:

- [ ] **CERO datos clínicos en formularios del sitio** (regla legal de la sección 0.3) — motivo de consulta solo en lista cerrada general
- [ ] Matrículas del equipo visibles; director médico identificado si es clínica
- [ ] Obras sociales/prepagas listadas explícitamente y con fecha de última actualización acordada con el cliente
- [ ] Bloque de urgencias accesible desde el header, con teléfono clickeable
- [ ] Copy sin promesas de resultado ni superlativos médicos ("el mejor", "indoloro", "100% efectivo") — usar rangos y condiciones
- [ ] Historias/fotos de pacientes SOLO con consentimiento escrito confirmado en onboarding
- [ ] Disclaimer en contenido educativo: informativo, no reemplaza la consulta profesional
- [ ] Ficha por tratamiento completa (qué es, qué se siente, duración, cuidados, precio "desde" u OS que cubren)
- [ ] Sección "primera visita": qué llevar, cuánto dura, cómo llegar
- [ ] Motor de turnos del cliente embebido/enlazado y probado con un turno real de prueba
- [ ] Google Business Profile revisado y alineado con el sitio (horarios, teléfono, categorías)
- [ ] Fotos reales de equipo e instalaciones — el stock médico descalifica la entrega
- [ ] Veterinarias: urgencias 24 hs (propias o derivación) resueltas en el bloque de urgencias

---

## 5. PRICING ANCLA

Fede lo anticipó bien: esta vertical NO se ancla al genérico de USD 200-600.

| Entregable | Ticket | Justificación |
|---|---|---|
| **Consultorio individual** (1-2 profesionales) | **USD 400-600** | Estructura de Profesionales + rigor de contenido y marco legal de Salud. |
| **Clínica / centro multi-especialidad / veterinaria con urgencias** | **USD 600-900** | Más especialidades = más páginas educativas, más equipo, ciclo de validación médica del contenido, GBP incluido. La clínica factura alto y decide institucionalmente: el precio bajo acá genera desconfianza, no ventas. |
| **Mantenimiento** | **Piso alto** ($30.000+ ARS/mes o equivalente) | Trabajo recurrente real y visible: obras sociales que entran y salen (pasa todo el tiempo), precios particulares con inflación, historias de pacientes nuevas, artículos SEO. Junto con Inmobiliarias, la mejor vertical de recurrencia. |
| Fuera de alcance estándar | A derivar/cotizar aparte | Cualquier cosa que toque HC, portal de pacientes o telemedicina — se recomienda software especializado, El Faro no lo construye. |

---

## PRÓXIMOS PASOS (post-aprobación)

1. Validar la regla legal de la sección 0.3 con un profesional de confianza del rubro (5 minutos de charla — es la sección que más protege a El Faro).
2. Buscar primer caso: ¿odontólogo o veterinaria en el entorno? (Veterinaria es la puerta más fácil: menos sensibilidad regulatoria, urgencias como gancho.)
3. Construir el componente "línea de pulso" como bloque reutilizable.
4. Cargar este playbook a la Biblioteca de Verticales.
