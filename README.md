# GEO (Generative Engine Optimization) — Repositorio Central de Assets y Schemas

Repositorio centralizado con los activos técnicos, configuraciones y marcado semántico diseñados para la optimización en motores de búsqueda impulsados por Inteligencia Artificial (**GEO - Generative Engine Optimization** / LLM SEO).

Este proyecto contiene los artefactos necesarios para facilitar el rastreo, indexación, comprensión contextual y citación por parte de asistentes y motores de búsqueda generativa tales como **SearchGPT / OpenAI**, **Perplexity AI**, **Claude / Anthropic**, **Google Gemini / AI Overviews** y **Microsoft Copilot**.

---

## 📁 Clientes y Proyectos Actuales

El repositorio está organizado por directorios correspondientes a cada cliente/marca:

| Directorio | Cliente / Entidad | Sector | Tipo de Schema Principal |
| :--- | :--- | :--- | :--- |
| `centrogoianodavisao/` | **Centro Goiano da Visão** | Salud / Oftalmología | `MedicalClinic`, `Physician`, `MedicalProcedure` |
| `consciente/` | **Consciente Construtora** | Inmobiliario / Construcción | `RealEstateAgent`, `Organization` |
| `drricardobittar/` | **Dr. Ricardo Bittar** | Salud / Cirugía Plástica Facial | `Physician`, `MedicalBusiness` |
| `hospitaljacobfacuri/` | **Hospital Jacob Facuri** | Salud / Hospital General & Urgencias | `Hospital`, `EmergencyService`, `MedicalSpecialty` |
| `reserva35/` | **Reserva 35** | E-commerce / Vinos, Licores y Gourmet | `Winery`, `Store`, `Product` |

---

## 🧱 Anatomía de los Assets de GEO

Cada directorio de proyecto contiene una suite estandarizada de archivos optimizados para LLMs y motores de búsqueda tradicionales:

### 1. `llms.txt` (Estándar para LLMs)
- **Propósito:** Resumen conciso, estructurado en Markdown, diseñado para consumo directo y rápido por agentes de IA en búsquedas semánticas.
- **Contenido:** Propuesta de valor, información crítica de contacto, horarios, servicios clave y enlaces a la documentación detallada.
- **Ubicación en producción:** Debe servirse en la raíz del dominio: `https://dominio.com.br/llms.txt`.

### 2. `llms-full.txt` (Base de Conocimiento Profunda)
- **Propósito:** Documento canónico exhaustivo para ingesta profunda de contexto en ventanas grandes de contexto de LLMs.
- **Contenido:** Matriz completa de servicios, cuerpo médico con registros (CRM/RQE), catálogo de exámenes y cirugías, preguntas frecuentes (FAQ) y políticas.
- **Ubicación en producción:** Servir en: `https://dominio.com.br/llms-full.txt`.

### 3. Marcado Semántico JSON-LD (`*.json`)
- **Propósito:** Grafos de conocimiento estructurados bajo la especificación de **Schema.org** (`@graph`).
- **Archivos habituales:**
  - `home.json`: Identidad de la organización, datos de contacto, enlaces sociales, dirección física y servicios principales.
  - `corpo-clinico.json` / `especialidades.json` / `procedimentos.json`: Detalle semántico de médicos, credenciales y procedimientos.
  - `hospital.json` / `clinica.json`: Especificación técnica del centro médico y equipamiento.
- **Ubicación en producción:** Inyectar en el HTML (`<script type="application/ld+json">`) de las páginas correspondientes.

### 4. `robots.txt` (Directivas para Agentes de IA)
- **Propósito:** Configurar directivas específicas para rastreadores de IA modernos y señales de contenido (`Content-Signal`).
- **Bots contemplados:** `OAI-SearchBot`, `ChatGPT-User`, `Claude-SearchBot`, `Claude-User`, `PerplexityBot`, `GoogleOther`, `Google-Agent`, entre otros.
- **Header / Meta:** `Content-Signal: search=yes, ai-input=yes, ai-train=yes`.
- **Ubicación en producción:** `https://dominio.com.br/robots.txt`.

### 5. `sitemap.xml` & `site.webmanifest`
- **`sitemap.xml`:** Índice canónico de páginas públicas para garantizar un rastreo eficiente.
- **`site.webmanifest`:** Metadatos de Progressive Web App (PWA), colores institucionales e iconos.

---

## 🚀 Guía de Implementación en Producción

### Servir Archivos Estáticos (`llms.txt`, `llms-full.txt`, `robots.txt`)

En frameworks modernos como **Next.js**, **Astro** o **Nuxt**:
- Copiar los archivos a la carpeta `public/` del proyecto web:
  ```bash
  public/
  ├── llms.txt
  ├── llms-full.txt
  ├── robots.txt
  ├── sitemap.xml
  └── site.webmanifest
  ```

En servidores web convencionales (**Nginx** / **Apache**):
- Colocar los archivos directamente en el `document_root`. Asegurarse de que el tipo MIME para `.txt` sea `text/plain; charset=utf-8`.

### Inyección de JSON-LD en HTML

Para implementar los esquemas de Schema.org en las vistas de la aplicación:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    /* Contenido extraído del archivo .json correspondiente */
  ]
}
</script>
```

---

## 🛠️ Validación y Control de Calidad

Antes de desplegar cualquier cambio a producción, se recomienda verificar los assets con las siguientes herramientas:

1. **Validación de Schema.org:**
   - [Schema.org Validator](https://validator.schema.org/)
   - [Google Rich Results Test](https://search.google.com/test/rich-results)
2. **Validación de Robots.txt y Sitemaps:**
   - [Google Search Console — Herramienta de prueba de robots.txt](https://www.google.com/webmasters/tools/robots-testing-tool)
3. **Validación de `llms.txt`:**
   - [llmstxt.org Directory & Validator](https://llmstxt.org/)
4. **Validación de Sintaxis JSON:**
   ```bash
   # Validación rápida por terminal
   python3 -m json.tool <ruta-archivo.json> > /dev/null
   ```

---

## ➕ Procedimiento para Añadir un Nuevo Cliente

Para integrar un nuevo cliente al flujo de GEO:

1. **Crear el directorio:**
   ```bash
   mkdir nombrecliente
   ```
2. **Generar los assets base:**
   - `llms.txt`: Resumen ejecutivo y enlaces canónicos.
   - `llms-full.txt`: Documentación exhaustiva para contextualización.
   - `robots.txt`: Directivas amigables con bots de búsqueda generativa.
   - `home.json`: Schema.org de la organización principal.
   - `sitemap.xml`: Estructura canónica de URLs.
3. **Verificar sintaxis:** Validar los archivos JSON y URLs canónicas.
4. **Commit y Documentación:** Registrar la nueva entidad en este `README.md`.
