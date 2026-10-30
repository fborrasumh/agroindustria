# AgroindustrIA

Práctica adaptativa, simulacro, problemas de proyecto y laboratorio APPCC de Proyectos de Industrias Agroalimentarias (UMH 2778). Aplicación web de un solo fichero.

**Usar la app:** https://fborrasumh.github.io/agroindustria/

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23823263.svg)](https://doi.org/10.5281/zenodo.23823263)

**Idiomas:** español (por defecto), inglés, portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

Sistema de aprendizaje de la asignatura **2778 Proyectos de Industrias Agroalimentarias** (optativa, 1.er curso, 2.º semestre, 4,5 ECTS) del Máster Universitario en Gestión y Diseño de Proyectos e Instalaciones (Escuela Politécnica Superior de Orihuela, Universidad Miguel Hernández de Elche), construido a partir de su Guía Docente 2026-2027 (validada el 02/07/2026).

## Qué hace

- **Práctica adaptativa por unidad (sin clave, sin conexión).** 44 preguntas propias, 4 por cada una de las 11 unidades de la guía, en tres idiomas y etiquetadas por nivel de Bloom. Cada respuesta va con la seguridad declarada (seguro / dudo / lo adivino) y una explicación inmediata. Una prueba automática comprueba que la opción correcta no está siempre en la misma posición ni es claramente la más larga.
- **Ruta explicable.** Un modelo Elo simplificado por unidad (Pelánek, 2016) con olvido exponencial (21 días) estima el dominio. La siguiente pregunta se elige con reglas deterministas: primero vuelve lo fallado (tras otras tres), luego los repasos espaciados vencidos (1, 3, 7, 16 y 35 días) y después preguntas nuevas de la unidad menos dominada, con dificultad ajustada a un 70 % de acierto esperado; nunca dos seguidas de la misma unidad si hay otras. El estudiante ve **por qué le toca** cada pregunta.
- **Simulacro con la corrección literal de la guía:** cuatro opciones, «tres preguntas mal contestadas anularán una pregunta correcta y las no contestadas no puntuarán», es decir `Nota = ((correctas − incorrectas / 3) / nº de preguntas) · 10`. Enseña el cálculo con los números y, con los datos de la propia práctica, si al estudiante le conviene contestar cuando duda (umbral del 25 %).
- **Calculadora de la evaluación continua** (40 % test + 60 % tareas, con un mínimo de 4 en cada parte).
- **Problemas de proyecto con solución calculada (sin IA).** Siete tipos de dimensionado: volumen de una cámara frigorífica, potencia frigorífica para enfriar producto, tiempo de esterilización (D, z, F0), número de máquinas de una línea, depósitos de recepción de leche, depósitos de fermentación de una bodega y carga orgánica (DBO5) del agua residual. Los datos salen de un **código de serie** (mismo código → mismos datos), la solución la calcula el código y se contrasta con un segundo método (informe de calidad con 200 variantes por tipo), se admite un 2 % por redondeo y se **diagnostican los errores típicos** (factor de llenado al revés, kJ/h en vez de kW, exponente de la tasa letal invertido, redondeo de máquinas hacia abajo, conversiones de unidades…). Solución paso a paso tras acertar o tras dos intentos. Hoja de problemas en Word.
- **Laboratorio APPCC.** Árbol de decisiones clásico del Codex (P1-P4) aplicado por el código a las etapas de tres procesos de ejemplo (conserva de judías verdes, leche pasteurizada, jamón cocido) o a etapas propias, con comparación frente a una propuesta de referencia y exportación del cuadro a CSV y Word.
- **Comentarios de la IA a tu plan APPCC o a tu proyecto**, con dos listas de comprobación: los 7 principios del APPCC (Codex, CXC 1-1969, rev. 2020) y los documentos de un proyecto según la UNE 157001:2014. El código hace un recuento orientativo por palabras clave; cada comentario de la IA debe apoyarse en una frase literal del texto, que el código verifica; las cifras de la IA que no están en el texto se señalan; **no pone notas** (si la IA escribe una se le pide repetir y, si persiste, el código quita la frase y lo avisa).
- **Preguntas desde los apuntes:** la IA propone preguntas a partir de un fragmento de apuntes; el código descarta las que no traen una cita literal, las que tienen opciones repetidas o la respuesta mal indicada, y avisa si la correcta es la más larga o hay cifras ajenas.
- **Progreso:** dominio por unidad, repasos pendientes, problemas resueltos y calibración de la seguridad.
- **Panel del profesorado:** analítica de ítems (dificultad, discriminación ítem-resto, uso de distractores) a partir de ficheros anónimos del alumnado; exportación del banco a **Moodle XML** (una categoría por unidad, −33,33333 % por error, como la guía), **GIFT** y CSV; hoja de soluciones de problemas para un grupo (un código por estudiante).
- **Ejemplos sin clave:** un plan APPCC ficticio con comentarios precalculados (en los tres idiomas) y datos simulados para el panel, declarados como tales.

## Cómo se usa la IA

Solo para los comentarios al plan o al proyecto y para crear preguntas desde los apuntes, con la propia clave de OpenAI, Google Gemini o Anthropic Claude. La clave se guarda solo en el navegador. No hace falta servidor. **La IA propone; el código comprueba.**

## Privacidad

Todo se guarda en el navegador (IndexedDB). La práctica, el simulacro, los problemas, el árbol, el progreso y el panel del profesorado no envían nada. Al proveedor de IA solo sale el texto que la persona decide enviar, con correos, teléfonos y DNI/NIE enmascarados, y antes del primer envío de la sesión se muestra la muestra exacta. La política de seguridad del contenido (CSP) impide conexiones a cualquier otro origen.

**Fichero anónimo de respuestas** (`agroindustria/eventos/1`), descarga voluntaria con casilla de conformidad:

| Campo | Contenido |
|---|---|
| `seud` | Seudónimo aleatorio generado en el navegador (`E-XXXXXX`) |
| `ev[].i` | Identificador de la pregunta del banco (`u4-2`…); las creadas con IA no se exportan |
| `ev[].u` | Unidad (1-11) |
| `ev[].o` | Opción elegida en el orden original (0-3) o `null` si se dejó en blanco |
| `ev[].c` | 1 si es correcta, 0 si no |
| `ev[].cf` | Seguridad declarada: `seguro`, `dudo`, `azar` o `blanco` |
| `ev[].d` | Día relativo desde la primera respuesta (sin fechas ni horas) |

## Límites

- **Las 44 preguntas, las respuestas de referencia del árbol y los datos de los problemas son una primera propuesta pendiente de revisión por el profesorado de la asignatura.** Se redactaron a partir de la guía y de conocimiento general de la materia, no de los materiales de clase. Las referencias a normas (Reglamentos (CE) 852/2004 y 853/2004, RSCIEI, Directiva de aguas minerales…) deben comprobarse con la versión vigente.
- Los datos de los problemas son didácticos y verosímiles, no de proyectos reales; los modelos son los de manual (sin pérdidas, calentamiento instantáneo…).
- La clasificación de una etapa como PCC depende del análisis de peligros y de los prerrequisitos de cada industria: la referencia es una propuesta, no una verdad única. Se usa el árbol clásico (2003); la revisión de 2020 del Codex incluye otro ejemplo de árbol.
- Las listas de comprobación de los comentarios son una propuesta: la guía no publica los criterios de las tareas. El recuento por palabras clave es orientativo.
- Los resultados de aprendizaje por unidad son una **propuesta** de reescritura medible; los oficiales son los diez objetivos de la guía.
- El dominio estimado es una señal para orientar el repaso, no una predicción de la nota. **No se ha medido** que la app mejore el rendimiento.
- Probado con IA simulada (incluidas respuestas que inventan citas, cifras y notas) en Chromium, con axe-core (WCAG 2.2 AA, cero infracciones en las pantallas probadas), sin conexión, con CPU ralentizada ×4 y en móvil en los tres idiomas; no se ha probado con claves reales de los tres proveedores ni con lectores de pantalla reales.
- Investigar con los datos (publicar resultados) exige aprobación previa del comité de ética de investigación (OEP en la UMH), consentimiento informado y RGPD; la app produce el dataset, no la evidencia.

## Análisis de la guía docente (resumen)

1. **Descripción frente a contenidos:** la descripción incluye «Industrias pesqueras» y «Almazaras», que ninguna unidad trata; bebidas, diseño higiénico y APPCC no aparecen en la descripción.
2. **Objetivos:** varios con verbos no observables («Estudiar», «Conocer», «Mejorar en los conocimientos»…); se alinean uno a uno con las unidades, pero ninguno con un instrumento de evaluación.
3. **Tareas (60 %):** sin enumeración, pesos ni criterios en la guía («según se especifica en la plataforma virtual»).
4. **Prueba única:** 90 minutos en «Características de la prueba» y 180 minutos en «Criterios de corrección».
5. **Evaluación continua:** no consta qué pasa con menos de un 4 en una parte ni la recuperación. La corrección del test es coherente (con cuatro opciones, el azar vale 0 de media).
6. **Bibliografía:** básica de 1994 a 2006 y complementaria hasta 2013; faltan los Reglamentos (CE) 852/2004 y 853/2004, los Principios generales de higiene del Codex (rev. 2020) y el Reglamento (UE) 2021/382.
7. **Carga:** 4,5 ECTS sin reparto de horas ni práctica evaluable del test antes del examen.
8. **Erratas:** «https.//aulavirtualepso.umh.es» y «a cerca de».

## Adoptar la app en otra asignatura o universidad

El contenido de la asignatura está en bloques de datos al principio del script (`CURSO`, `EVAL`, `UNIDADES`, `ITEMS`, `PROCESOS`, `LISTAS`; en el proyecto fuente, `src/curriculum.js`) y las plantillas de problemas en `src/calculo.js`. La lógica (modelo de dominio, ruta, simulacro, árbol, analítica, exportaciones) no depende de la asignatura.

## Fundamentos

- Roediger, H. L. y Karpicke, J. D. (2006). Test-enhanced learning. *Psychological Science*, 17(3), 249-255. https://doi.org/10.1111/j.1467-9280.2006.01693.x
- Cepeda, N. J. et al. (2006). Distributed practice in verbal recall tasks. *Psychological Bulletin*, 132(3), 354-380. https://doi.org/10.1037/0033-2909.132.3.354
- Dunlosky, J. et al. (2013). Improving students' learning with effective learning techniques. *Psychological Science in the Public Interest*, 14(1), 4-58. https://doi.org/10.1177/1529100612453266
- Pelánek, R. (2016). Applications of the Elo rating system in adaptive educational systems. *Computers & Education*. https://doi.org/10.1016/j.compedu.2016.03.017

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche), Joaquín Julián Pastor Pérez (Universidad Miguel Hernández de Elche) y María José Frutos Fernández (Universidad Miguel Hernández de Elche).

A partir de la Guía Docente 2026-2027 de la asignatura 2778 Proyectos de Industrias Agroalimentarias (Máster Universitario en Gestión y Diseño de Proyectos e Instalaciones, Escuela Politécnica Superior de Orihuela, UMH), que imparten los profesores Joaquín Julián Pastor Pérez y María José Frutos Fernández.

Roles (CRediT): Fernando Borrás Rocher — conceptualización, software, metodología, validación (pruebas), redacción. Joaquín Julián Pastor Pérez y María José Frutos Fernández — recursos (asignatura y Guía Docente en la que se basa la app). Los roles pueden ajustarse en una versión posterior.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · Joaquín Julián Pastor Pérez [0000-0002-3065-2494](https://orcid.org/0000-0002-3065-2494) · María José Frutos Fernández [0000-0003-0620-5050](https://orcid.org/0000-0003-0620-5050)

## Cómo citar

Borrás Rocher, F., Pastor Pérez, J. J. y Frutos Fernández, M. J. (2026). *AgroindustrIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23823263](https://doi.org/10.5281/zenodo.23823263)

## Licencia

MIT. Véase [LICENSE](LICENSE).
