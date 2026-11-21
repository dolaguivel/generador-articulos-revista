# Generador de Artículos por Revista — guía rápida

Sistema web para preparar artículos científicos breves (4–8 páginas publicadas) adaptados a 36 revistas de Perú y Latinoamérica: las 6 que indicaste y 30 más. Cada artículo se orienta al **tipo de revista** (educación, gestión, computación, bibliotecología, administración pública, salud, etc.), aunque el tema sea tecnológico.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `generador-articulos-por-revista.html` | El sistema completo en un solo archivo. Ábrelo en Chrome, Edge o Firefox con internet: búsqueda en OpenAlex y verificación de DOI con Crossref/DataCite en vivo. |
| Enlace del artefacto en Claude | El mismo sistema dentro de Claude, con redacción asistida por Claude. Ahí el navegador bloquea OpenAlex y Crossref: importa las fuentes con el Módulo 2. |
| `catalogo-revistas.csv` | Las 36 revistas con lo verificado (y lo que falta verificar), con sus fuentes. Se abre en Excel. |
| `informe-arbitro.md` | Resumen de las rondas de auditoría adversarial y de lo que se corrigió. |

## Flujo en 6 pasos

1. **Revista.** Filtra por tipo, país, Scopus verificado o «Aceptan 4–8 págs.» y abre la ficha: requisitos oficiales marcados como *verificado*, *verificar* o *estimado*.
2. **Proyecto.** Escribe tu tema tecnológico, elige el tipo de artículo (original cuantitativo, cualitativo, mixto, revisión, bibliométrico, diseño/DSR, caso o ensayo) y un enfoque para ese tipo de revista. Marca la casilla de datos solo si los tienes: «Ya tengo datos reales recogidos» en estudios empíricos o «Ya ejecuté la búsqueda y tengo el registro de cribado» en revisiones. Sin esa casilla, el sistema no permite resultados numéricos ni conteos PRISMA.
3. **Fuentes.** Busca (versión descargable) o importa el JSON del Módulo 2, RIS, BibTeX o una lista de DOI. Cada referencia queda *sin verificar* hasta comprobarla.
4. **Prompts.** El prompt maestro Q1 y 8 módulos por fase, personalizados para la revista. Pégalos en un modelo con búsqueda web.
5. **Borrador.** Editor con la estructura de la revista y presupuesto de palabras por sección. Dentro de Claude puedes redactar con IA (solo cita fuentes verificadas y se puede deshacer). Exporta a Word con el formato de la revista.
6. **Auditoría.** Revisa extensión, estructura, citas contra la lista, idioma y antigüedad de fuentes, marcadores pendientes, declaraciones e integridad de datos.

## Reglas que el sistema hace cumplir

- No hay referencias «verificadas» sin comprobación (Crossref, DataCite, OpenAlex o confirmación manual explícita).
- Sin datos reales declarados (o sin registro de búsqueda en revisiones), el artículo empírico **nunca** queda «listo para enviar»: la auditoría lo bloquea siempre y, además, señala como bloqueantes los estadísticos, conteos PRISMA, tablas con cifras y citas textuales de participantes que encuentre, aunque la oración lleve una cita. Las demás cifras (normas, versiones, cifras de la literatura) quedan como «Revisar».
- La metodología se adapta al tipo de artículo: un ensayo no pide muestra ni instrumentos; una revisión o bibliometría pide protocolo de búsqueda, no encuestas.
- La IA no es autora, no redacta agradecimientos ni biografías y su uso se declara.
- La revisión por pares es una simulación de apoyo; nada garantiza la aceptación.

## Decisiones tomadas por el sistema (ambigüedades resueltas)

- **«4–8 páginas»** se interpreta como páginas *publicadas* (≈650 palabras cada una). El plan muestra también las páginas de manuscrito en el formato de cada revista y avisa cuando la revista exige más. En artículos de investigación exigen más de 8 páginas: Propósitos y Representaciones, Psicología PUCP, Apuntes, Reforma y Democracia, Información Tecnológica, Formación Universitaria e Innovar; en revisiones, Reforma y Democracia, Ingenius e Innovar. El filtro «Aceptan 4–8 págs.» se calcula para el tipo de artículo que elegiste.
- **Límites por tipo de artículo:** cuando la revista fija límites distintos para revisiones o ensayos (PJM, UNSCH, Cuadernos ORT, Propósitos, RCS-LUZ, Ingenius, Liberabit, RCSI), el plan, el prompt y la auditoría usan el del tipo elegido. Los límites en páginas se convierten a palabras con la fuente y el interlineado oficiales de cada revista.
- **Las 30 revistas agregadas** se eligieron por uso entre investigadores peruanos y latinoamericanos, indexación (Scopus/SciELO/Latindex) y afinidad con temas tecnológicos aplicados a otras disciplinas. Se excluyeron revistas que no reciben envíos, salvo RCSI-UNSM, que se mantiene marcada como «no está recibiendo manuscritos».
- **Revistas sin norma de extensión publicada:** se usa tu meta de páginas y la ficha lo marca como *verificar*.
- **Límites en páginas** (UNSCH, Fénix, Apertura, RIB, etc.): se convierten a palabras con la fuente e interlineado de la revista y se ajusta la meta para no superar el máximo.
- **Proporción de fuentes en español:** 60 % por defecto (ajustable de 50 a 90 %), salvo revistas que exigen más fuentes en inglés (Información Tecnológica pide ≥50 % en inglés).
- **Cuartiles:** se muestran los del ranking por país de SCImago consultado el 17-11-2026; pueden variar por categoría y año.
- **Redacción con IA** solo dentro de Claude; en la versión descargable se usan los prompts en tu modelo.

## Antes de enviar

Abre las directrices oficiales de la revista y confirma los campos marcados *verificar*: indexación y cuartiles cambian, y varias revistas bloquearon la consulta automática de sus normas.
