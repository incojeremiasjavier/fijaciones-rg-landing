# Auditoría Forense — Landing Fijaciones RG
**Archivo:** `fijaciones-rg-landing.html` · **Fecha:** 2026-08-14 · **Auditor:** CPGO

---

## 0. Supuestos declarados
- **Cliente:** Fijaciones RG (Jeremías y Felipe Ramos). Confirmado por memoria de negocio.
- **Objetivo del sitio:** captar cotizaciones de **ferreterías pequeñas/medianas** de Santiago (Independencia y alrededores) → lead a WhatsApp/formulario. Confirmado.
- **Etapa:** Fase 1 (comisionistas del tata). El sitio proyecta capacidad de fabricación/despacho propios que hoy son infraestructura del tata → ver hallazgo #4.
- **Dominio:** no existe aún; asumí `fijacionesrg.cl` como placeholder en los meta. **Debe reemplazarse al publicar.**
- **Competencia de referencia:** Otero Industrial, Ferretería San Martín, Todo Ferretero (de la memoria de prospectos).

---

## 1. Veredicto global

**Score: 8.4 / 10** — Esto **no** es un sitio de $100 ni "vibe coding". Es un build de nivel real:
tipografía correcta (Archivo + IBM Plex Mono, **ninguna** fuente prohibida), paleta contenida
(grafito + oro zincado, ≤5 hex núcleo), copy sensorial ("que sujetan de verdad", "factura desde
el primer perno"), movimiento con gusto (shimmer, reveal, dock magnético, blueprint draw-in, visor
3D real en three.js), formulario funcional con fallback a WhatsApp, y responsive con
`prefers-reduced-motion` respetado.

Lo que lo separa de un **$10M impecable** no es diseño — es **confianza, SEO técnico y robustez de
producción**. Ahí están los 3 hallazgos críticos.

---

## 2. Los 3 hallazgos más críticos

### 🔴 #1 — Prueba social fabricada (riesgo legal + de credibilidad)
- **Reseñas inventadas** con nombres y ferreterías reales-verosímiles (Rodrigo Muñoz · El Maestro, etc.), todas 4–5★ (JS línea ~1439).
- **Muros de logos de clientes y proveedores inventados** ("Metalúrgica Prime", "Zinctek"…) (JS ~1421).
- **Por qué importa:** una ferretería que googlea esos nombres detecta el invento en 30 segundos → mata la confianza justo en el segmento que valora "trato directo y serio". En Chile además expone a reclamo por publicidad engañosa (SERNAC).
- **Fix:** hasta tener testimonios reales, reemplazar por **garantías verificables** ("Respuesta el mismo día hábil", "Factura desde el pedido 1", "Cambio sin costo si la medida no calza"). Los logos de proveedores → sustituir por **sellos de norma** (Grado 8.8/10.9, ISO métrica, A2/A4) que sí puedes respaldar.

### 🔴 #2 — SEO técnico incompleto para un negocio 100% local *(YA CORREGIDO EN PARTE)*
- **Faltaban** Open Graph/Twitter (sin preview al compartir en WhatsApp — tu canal #1), `canonical`, favicon, `theme-color` y **JSON-LD LocalBusiness**. Para un negocio de barrio, el schema local es lo que te mete en el paquete de mapas de Google.
- **Acción aplicada:** inyecté OG + Twitter Card + favicon inline (marca RG) + `theme-color` + **JSON-LD `HardwareStore`** con dirección, teléfono, horario y ofertas. **Debes** reemplazar el dominio placeholder y crear la imagen `og-fijaciones-rg.jpg` (1200×630).

### 🔴 #3 — Dependencia frágil de imágenes hotlinkeadas de Pexels
- **Todas** las fotos de productos y servicios se cargan desde `images.pexels.com` con `referrerpolicy="no-referrer"` (síntoma de esquivar hotlink-protection). Si Pexels bloquea el hotlink o cambia la URL, **la landing queda con huecos**. Además: no son *tus* productos → resta autenticidad, y no traen `width/height` → **CLS** (salto de layout, penaliza Core Web Vitals).
- **Fix:** descargar, optimizar (WebP ~150–250KB) y **servir local** desde `/img/`. Idealmente, fotos reales de tu stock. Añadir `width`/`height` a cada `<img>`.

---

## 3. Matriz de transformación ($100 → $10.000)

| Dimensión | Estado actual (evidencia) | Nivel $10M |
|---|---|---|
| **Confianza** | Reseñas y logos inventados; email `@gmail.com` | Testimonios reales o garantías verificables; correo con dominio propio |
| **SEO técnico** | Sin OG/JSON-LD/favicon (corregido) | Schema LocalBusiness + OG + sitemap + og-image real |
| **Robustez** | Imágenes hotlink Pexels, sin width/height (CLS) | Assets locales optimizados, dimensiones fijas, LCP <2.5s |
| **Coherencia negocio** | Copy dice "fabricación/camión propio" (es del tata en Fase 1) | Claims sostenibles: "despacho propio en 24–48h" sí; matizar "fabricación" |
| **Contacto** | Web3Forms key expuesta en JS, sin honeypot | Botcheck/honeypot activo; endpoint con anti-spam |

---

## 4. Hallazgo estratégico (coherencia con Fase 1)
La landing vende a RG como **fabricante con taller y camión propios** ("el taller mecaniza",
"fabricación propia y bodega surtida"). Según la memoria de negocio, en **Fase 1** esa
infraestructura es del **tata** y RG opera como comisionista. No es mentira (tienes acceso real a
esa capacidad), pero **cuida el overpromise**: si un cliente pide una fabricación especial urgente y
la respuesta depende de la agenda del taller del tata, el "lo fabricamos contra plano" puede
generar fricción. **Recomendación:** mantener el posicionamiento (es fuerte), pero tener claro
internamente el SLA real antes de prometer plazos de fabricación.

---

## 5. Hallazgos secundarios (rápidos)
- **Accesibilidad/contraste:** grises `#5f6672`, `#6b7078`, `#868c96` sobre fondo oscuro quedan bajo AA en texto pequeño. Subir a ≥ `#8a90-9a` en footer/notas.
- **Web3Forms:** la `access_key` va en el cliente (inevitable en su modelo), pero **activa el honeypot/botcheck** de Web3Forms para evitar spam a tu inbox.
- **`three.js r128`** desde cdnjs: versión antigua. Funciona y tiene fallback correcto, pero considera fijar una versión mantenida o self-host.
- **Fuentes:** cargas 6 pesos de Archivo; con 3–4 (400/600/800/900) bajas el peso del render inicial.
- **`<img>` sin `width/height`** en todas las tarjetas → CLS. Añadir dimensiones.
- **Footer dice "Sitio de demostración"** — recuerda quitarlo al publicar.

---

## 6. Lo que está muy bien (no tocar)
- Sistema de diseño coherente y con "firma" (blueprint técnico + cotas + shimmer oro).
- Copy directo y sensorial, alineado a la BRAND-VOICE del proyecto.
- Visor 3D real con selector de terminado (zincado/galv/inox/negro) y hotspots: diferenciador genuino, casi nadie en el rubro lo tiene.
- Formulario con degradación elegante a WhatsApp (canal correcto para el segmento).
- Dock magnético + chat con quick-replies útiles y accesibles.

---

## 7. Siguientes pasos (priorizados)
1. **Hoy:** reemplazar `fijacionesrg.cl` por tu dominio real en los meta y JSON-LD; crear `og-fijaciones-rg.jpg` (1200×630).
2. **Esta semana:** bajar las 12 imágenes Pexels, optimizar a WebP y servir desde `/img/` con `width/height`. O reemplazar por fotos reales de stock.
3. **Antes de publicar:** decidir sobre reseñas/logos — testimonios reales o cambiar a bloque de garantías. Quitar "Sitio de demostración".
4. **Configurar** correo con dominio (`contacto@tudominio.cl`) y activar botcheck de Web3Forms.
5. **Validar** contraste AA en footer/notas.
