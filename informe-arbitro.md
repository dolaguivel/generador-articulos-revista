# Informe del arbitraje adversarial

**Sistema:** Generador de Artículos por Revista (36 revistas de Perú y Latinoamérica).
**Método:** en cada ronda, un árbitro nuevo e independiente, que no participó en la construcción ni en rondas anteriores, auditó el sistema completo con el objetivo explícito de tumbarlo. Ejecutó las pruebas del equipo, escribió las suyas (motor en Node y navegador real con Playwright, en los modos descargable y artefacto, en escritorio y en móvil), recorrió el flujo de punta a punta y contrastó datos de las revistas en sus sitios oficiales. Después de cada rechazo se corrigió todo lo comprobado, se añadieron pruebas que reproducen cada caso y se lanzó una ronda nueva.

Desde la ronda 13, el árbitro aplica una escala de severidad explícita:
- **Crítico:** rompe el flujo, pierde datos o presenta como verificado algo falso.
- **Mayor:** un usuario de buena fe recibiría un resultado incorrecto sin poder notarlo.
- **Menor:** fallos de detectores heurísticos ante redacciones rebuscadas, avisos de más en la dirección segura o detalles de texto.

Solo se aprueba sin críticos ni mayores.

## Resumen por ronda

| Ronda | Veredicto | Críticos | Mayores | Menores | Qué se rechazó (lo principal) |
|---:|---|---:|---:|---:|---|
| 1 | Rechazado | 1 | 13 | 10 | Cualquier texto en «Datos» desactivaba las salvaguardas contra resultados inventados. Auditoría de citas con falsos positivos y negativos. La IA recibía referencias sin verificar. Crossref sin control de autores. Acciones destructivas sin confirmar. Autores institucionales, BibTeX con LaTeX y XSS. |
| 2 | Rechazado | 0 | 8 | 9 | Falsos críticos en citas («MINEDU (2023)», «de la Cruz»). Detector de cifras que bloqueaba revisiones y ensayos. Deshacer perdido mientras escribe la IA. Renumeración que corrompía enumeraciones. JSON del Módulo 2 con ```json. UNSCH superaba las 20 páginas. Informes y normas mal formateados. |
| 3 | Rechazado | 2 | 6 | 10 | Resultados inventados en notación APA (t, F, χ²) o con cita pasaban la auditoría. «Deshacer» de la IA borraba referencias importadas después. Etiqueta sin cerrar en el paso 2. Fase C pedía muestra para ensayos. |
| 4 | Rechazado | 1 | 2 | 12 | Resultados inventados en secciones combinadas, métricas en prosa y resultados cualitativos. Partículas en el segundo autor. Vancouver alteraba estadísticos con coma decimal. |
| 5 | Rechazado | 1 | 3 | 6 | Tablas markdown rellenas sin datos. Falsos críticos con «GPT-4», «ISO 25010» o leyes. Citas tras una cifra en Vancouver. Intervalos «[0,1]» tomados por citas en IEEE. |
| 6 | Rechazado | 0 | 4 | 4 | Ensayos con testimonios o pilotos propios sin aviso. Cifras citadas de la literatura marcadas como inventadas. «3,6 (1,8)» tomado por cita. «Rango de [1, 10]». |
| 7 | Rechazado | 1 | 3 | 7 | «Crossref ✓» para una referencia con coautor, revista y páginas inventados. Ensayos con pretest/postest sin aviso. |
| 8 | Rechazado | 1 | 4 | 7 | DOI de DataCite, libros y capítulos con metadatos inventados daban «verificado». Editar una referencia conservaba el sello. Falsos críticos y faltas de detección en ensayos. |
| 9 | Rechazado | 1 | 3 | 8 | En preprints, libros, informes y normas, la editorial se imprimía sin compararla. Años y leyes contados como «N personas». |
| 10 | Rechazado | 1 | 2 | 5 | «Artículo» sin revista imprimía una editorial sin comparar. Experiencia propia en ensayos sin aviso. Títulos con palabras sustituidas daban «coinciden». |
| 11 | Rechazado | 0 | 3 | 6 | Editoriales distintas aceptadas («Universidad de Chile» frente a «PUC de Chile»). Sustituciones con siglas, años y «con/sin» en títulos. La cita blanqueaba la experiencia propia. |
| 12 | Rechazado | 0 | 2 | 7 | Palabras añadidas al título daban «coinciden». Experiencia institucional («nuestra facultad», «donde enseño») sin aviso. |
| 13 | Rechazado | 0 | 2 | 8 | Primera persona con mayúscula inicial («Mis estudiantes…») no reconocida (regresión). Revistas alternativas de la Fase H que no aceptan el tipo de artículo. |
| 14 | Rechazado | 0 | 1 | 6 | Plural de modestia con verbos cortos («usamos», «vemos») e indicadores no educativos (consultas, residuos, ventas) sin aviso en ensayos. |
| 15 | Rechazado | 0 | 2 | 6 | Primera persona del singular en presente en ensayos («Veo que…», «Llevo dos años usando…») sin aviso. Límites de extensión por tipo de artículo de la ficha (PJM-revisión, UNSCH, Ingenius, RCS, RCSI) no aplicados. |
| 16 | Rechazado | 0 | 2 | 11 | El detector de experiencia propia dependía de una lista cerrada de verbos («He podido comprobar…», «Puedo ver que…»). RCS-LUZ y Propósitos convertían páginas a palabras con un formato por defecto en lugar del oficial. |
| 17 | **Aprobado** | 0 | 0 | 9 | Solo menores: matices heurísticos (tercera persona autorreferencial, imperfecto de experiencia, algunos «Revisar» de más) y detalles de formato y documentación. |

**Total: 17 rondas.** 16 rechazos y una aprobación final, sin críticos ni mayores pendientes.

## Qué se corrigió, por áreas

- **Integridad de los resultados.** Sin la casilla de datos reales (o de registro de búsqueda en las revisiones), el artículo nunca queda «listo». La auditoría bloquea los estadísticos en notación APA, las tablas con cifras, los conteos PRISMA, las citas textuales de participantes y los resultados cualitativos, aunque lleven una cita. Las cifras de la literatura citadas, las normas y las versiones quedan como «Revisar». En los ensayos se avisa de la experiencia propia, los pilotos y los testimonios, en primera persona, en el plural de modestia o en forma institucional.
- **Verificación de referencias.** Crossref y DataCite se comparan con los autores (con partículas y apellidos compuestos), el año (±2), la revista, las páginas, la editorial y el título (subtítulos, variantes y palabras sustituidas o añadidas). Se detectan las retractaciones. Editar una referencia le quita el sello de verificada. Solo las referencias verificadas se pueden citar y llegan a la IA.
- **Auditoría de citas.** Autor-año: autores institucionales y siglas, partículas, varios años por cita y segundo autor. Numéricas: IEEE y Vancouver sin confundir ecuaciones, tablas, enumeraciones, intervalos ni estadísticos con coma decimal. La renumeración se puede deshacer.
- **Adaptación a cada revista.** Las páginas se convierten a palabras con la fuente y el interlineado oficiales. Se aplican los límites por tipo de artículo. Se avisa cuando la revista exige más de 8 páginas. La estructura, las palabras clave y el resumen siguen las normas oficiales o se marcan como *verificar*. La Fase H solo propone revistas alternativas que aceptan el tipo de artículo.
- **Prompts por tipo de artículo.** La Fase D cambia según el tipo: resultados con datos reales, protocolo y plantillas PRISMA en las revisiones, o desarrollo argumentativo en los ensayos. Los ejemplos de cita están en el idioma del manuscrito. Cada perfil disciplinar tiene sus marcos, diseños, guías de reporte y revisores.
- **Robustez de la interfaz.** Hay confirmaciones con foco seguro y trampa de foco. Los campos quedan en solo lectura mientras escribe la IA. «Deshacer» incluye las referencias. La importación de proyectos se sanea, con XSS neutralizado. Hay aviso cuando el navegador no permite guardar. Se probó en móvil (390 px) sin desbordes, con accesibilidad verificada y sin dependencias externas de fuentes.

## Menores que quedan (no bloquean; el árbitro los dejó como recomendaciones)

- Algunas formas rebuscadas de experiencia propia en ensayos no generan aviso: la tercera persona autorreferencial («La autora ha constatado…») y el imperfecto o pluscuamperfecto de experiencia.
- Hay algunos avisos «Revisar» de más por homógrafos: van en la dirección segura y no bloquean.
- Hay detalles de formato por confirmar en las directrices de dos revistas (papel de Apertura y márgenes de Propósitos). Ya están marcados como *verificar* en la ficha.

## Verificación final

- Pruebas del motor (Node): **16 225 OK, 0 fallas.**
- Pruebas de extremo a extremo (Playwright, en los modos descargable y artefacto y con almacenamiento bloqueado): **0 fallas.**
- El archivo entregado es idéntico, byte a byte, a la versión que aprobó el árbitro en la ronda 17.
