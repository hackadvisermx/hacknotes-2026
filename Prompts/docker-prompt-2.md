Quiero que generes un plan de aprendizaje de {{topic}} desde cero hasta experto, orientado a {{audience}}. 
Entrega TODO en {{language}} con estilo ultra detallado y paso a paso.

OBJETIVO GENERAL
- Programa intensivo de {{weeks}} semanas (de fundamentos a proyecto final).
- Cada semana incluye: 
  1) Sección teórica clara y profunda 
  2) 10 retos prácticos extensos.
- Enfoque/énfasis: {{focus}}.

CONTENIDO Y ALCANCE
1) Estructura por semana ({{weeks}} semanas):
   - Sección teórica: conceptos clave, buenas prácticas, riesgos, seguridad/hardening (si aplica).
   - 10 retos prácticos. Para cada reto:
     - Comando(s) exactos a ejecutar (copiables).
     - Explicación detallada de cada comando y su objetivo.
     - Criterios de éxito / verificación.
     - Notas de seguridad (si aplica): {{security_topics}}.
     - Diagrama ASCII (si aporta): redes/volúmenes/orquestación/flujo.

2) Tablas iniciales y generales:
   - Requisitos técnicos (SO, herramientas, RAM/CPU/Disco, CLI, diferencias Linux/macOS/WSL).
   - Tabla de comandos más usados (según {{topic}}).
   - Flujos de trabajo recomendados (dev→build→test→scan→push→deploy, multi-stage, caching, tagging).
   - Recursos y documentación oficial (docs, referencias, guías).

3) Diagramas ASCII (compatibles con cualquier fuente monoespaciada):
   - NO uses box-drawing Unicode. Usa solo: + - | = < > ^ v * #.
   - Incluye diagramas clave (redes, volúmenes/binds, orquestación) adaptados a {{topic}}.

4) Sección extra final:
   - {{advanced_challenges_count}} retos avanzados (temas avanzados relevantes para {{topic}} y {{focus}}).

FORMATO DE ENTREGA (MARKDOWN DIVIDIDO)
- SOLO Markdown (sin HTML para anclas).
- Entrega una estructura navegable con enlaces relativos:

  /
  ├─ README.md
  ├─ intro/
  │  ├─ requisitos.md
  │  ├─ comandos.md
  │  ├─ flujos.md
  │  └─ recursos.md
  ├─ semanas/
  │  ├─ semana-01/
  │  │  ├─ index.md
  │  │  ├─ teoria.md
  │  │  ├─ retos.md            # índice a archivos (no anclas)
  │  │  └─ retos/
  │  │     ├─ reto-01-01-<slug>.md
  │  │     ├─ reto-01-02-<slug>.md
  │  │     └─ … reto-01-10-<slug>.md
  │  ├─ …
  │  └─ semana-{{weeks}}/
  └─ extra/
     └─ retos-avanzados.md     # lista de {{advanced_challenges_count}} retos

- Reglas de navegación en Markdown:
  - En cada `retos.md`, el **Índice de Retos** enlaza a archivos: `./retos/reto-XX-YY-<slug>.md` (no usar `#anclas`).
  - En cada `index.md`, incluir enlaces a `./teoria.md` y `./retos.md`, más un índice rápido a cada archivo de reto.
  - En cada archivo de reto:
    - `# Reto W.R — Título`
    - Barra superior e inferior con: 
      `⟵ Reto anterior · Índice de retos (semana WW) · Reto siguiente ⟶`
      usando rutas relativas a archivos.
  - En `README.md`, índice maestro a semanas, teoría, retos y cada archivo de reto.
  - Nombres de archivo coherentes: `reto-XX-YY-<slug>.md` (minúsculas, sin acentos, con guiones).

ESTILO Y CALIDAD
- Lenguaje: {{language}} (variante: {{locale}}).
- Explicaciones rigurosas y docentes. Para cada comando: flags, efectos, salida esperada y errores comunes.
- Contexto de seguridad cuando aplique: amenazas, controles, trade-offs (usar {{security_topics}}).
- Pasos de verificación (logs, ps, curl, pruebas funcionales).
- Diferencias por plataforma cuando impacten (Linux/macOS/WSL).

ENTREGABLES ADICIONALES
- **ZIP Markdown navegable** con toda la estructura.
- **PDF** con:
  - Portada.
  - Página de Navegación rápida (enlaces a semanas e intro/extra).
  - TOC clicable y marcadores laterales (Semana → Teoría/Retos → Retos).
  - Bloques de código resaltados (fondo, borde, padding).
  - **Word-wrap por ancho sin caracteres invisibles**:
    - Cortar por espacios, `&&`, `||`, `/ : . - _ = ? ! & # % + @ > < | ; ,`.
    - Forzar salto por ancho si un token sigue largo.
  - Diagramas ASCII solo con + - | = < > ^ v * #.

VALIDACIONES (OBLIGATORIAS)
- Enlaces relativos verificados (README → semanas → retos → archivos).
- `retos.md` enlaza **solo a archivos** de reto.
- Diagramas ASCII alineados.
- Bloques de código no se salen del margen en PDF (sin ZWSP).
- Ortografía técnica coherente.

CRITERIOS DE ACEPTACIÓN
- {{weeks}} semanas completas, 10 retos/semana (= {{weeks}}0 retos), + {{advanced_challenges_count}} avanzados.
- Estructura de carpetas EXACTA y navegación funcional en Markdown puro.
- PDF con navegación rápida, TOC, marcadores, wrap correcto y diagramas limpios.
- ZIP(s) generados.

EXTRAS (opcionales, si lo pido)
- `SUMMARY.md` (GitBook) o `mkdocs.yml` (MkDocs).
- Versión print-friendly (B/N).
- Cheat sheet 1–2 páginas.
- Repo listo para Git (README, LICENSE, .gitignore).

PARÁMETROS
- {{topic}} = "Competencia técnica fundamental en los dominios de ciberseguridad tanto ofensivos como defensivos"
- {{audience}} = "estudiantes universitarios de ciberseguridad" | "equipo blue o read " | 
- {{language}} = "español"
- {{locale}} = "es-MX"
- {{weeks}} = 16
- {{focus}} = "ejercicios prácticos de ciberseguridad"
- {{security_topics}} = " 
  Penetration testing processes and methodologies, Information gathering & reconnaissance techniques, Attacking Windows & Linux targets, Web application penetration testing, Manual & automated exploitation, Vulnerability scanning, Lateral Movement, Post-exploitation enumeration, Windows & Linux Privilege escalation, Vulnerability/Risk communication and reporting, Network Traffic Analysis, SOC Processes & Methodologies, Security Monitoring, Log Analysis, Intrusion Detection, SIEM-assisted Log Analysis (Elastic)
  "
- {{advanced_challenges_count}} = 30
