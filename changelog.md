# Changelog

Todas las novedades notables de este proyecto se documentan en este fichero.

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

---

## [1.2.1] — 2026-07-12

Versión de correcciones y ampliaciones sobre los informes y exportaciones del Paso 2 y el
Paso 3, sin cambios en la lógica de validación ni en el motor de sorteo.

### Fixed

- `extraerCodigoDeTitulo()` no reconocía títulos de Excel con espacios alrededor de los
  guiones del código de plaza (p. ej. "PLAZA PADCL2 - D00337 - 19"), dejando el campo
  Código de la plaza vacío pese a haberse cargado la propuesta correctamente, y con ello
  el botón "Validar propuesta" deshabilitado sin ningún aviso claro del motivo. Corregido
  ampliando la expresión regular para admitir espacios y normalizando el resultado
  eliminándolos (`PADCL2-D00337-19`).

### Added

- Informe de validación descargable en PDF (Paso 2): añadido un enlace a la normativa
  oficial aplicable justo debajo del reglamento (`2402876a` para Ayudante Doctor,
  `reglamento-pdf` para el Acuerdo 26/09/2024), y una tabla con los datos completos de la
  propuesta (en su numeración original), con las filas resaltadas — rojo para anomalía sin
  resolver, morado para excepción CPU ya aceptada, ámbar para aviso (p. ej. equivalencia de
  categoría). Ambos elementos aparecen únicamente en el PDF descargable, no en la vista en
  pantalla del Paso 2.
- Acta de composición en Excel (Paso 3, `exportarActaExcel()`): dos pestañas nuevas junto a
  "Composición" —
  - **"Introducción de datos"**: la propuesta tal como la mandó el Departamento, en su
    numeración original (antes del sorteo), con título fusionado A1:G1 ("PROPUESTA
    COMISION [código]") y el mismo estilo de cabecera que "Composición". Columna B
    intencionadamente en blanco (sin DNI), ocupando la posición de esa columna en la
    plantilla original.
  - **"Sorteo"**: la propuesta reordenada tras el sorteo, agrupada por bloque (Bloque A
    primero, Bloque B después, igual que en el PDF), con las columnas "Sorteo" (valor de
    la secuencia de bolas en la posición que le corresponde dentro de esta tabla agrupada)
    y "Ordenación bloques" (número de orden original de la persona en la propuesta, art.
    12.1). Fila 10 (primera del Bloque B) con borde superior más grueso para diferenciar
    visualmente los bloques. DNI mostrado enmascarado, igual que en el resto de la app.
  - Orden final de las pestañas del libro: Introducción de datos → Composición → Sorteo.
  - `calcularComposicion()` expone ahora también `ordenBolas` en su resultado, para poder
    construir la columna "Sorteo" de la nueva pestaña.
  - Estilos de celda (relleno de cabecera, bordes, fuente) y el cálculo de ancho automático
    de columna, antes definidos dentro de `exportarActaExcel()`, extraídos a constantes de
    módulo (`EXCEL_ESTILO_*`) y a la función `excelAnchoAuto()`, reutilizadas por las tres
    pestañas en vez de duplicar el código.
- Acta de composición en PDF (Paso 3, `exportarActaPDF()`): añadida al final, después de la
  tabla de la propuesta reordenada del Bloque B, la sección "Anomalías y avisos" (excepciones
  CPU aceptadas, avisos y sus referencias), idéntica a la ya mostrada en el informe del Paso
  2. Extraída a la función compartida `renderBloqueAnomaliasPDF()`, usada por ambos informes
  para que no puedan divergir entre sí.

### Verified

- Columna "Sorteo" de la pestaña homónima contrastada fila a fila contra un caso real
  (`PADCL2-D00040-4`, propuesta y "algoritmo definitivo" aportados por Fernando):
  coincidencia exacta en orden de filas, columna Sorteo, columna Ordenación bloques y resto
  de campos.
- Sección "Anomalías y avisos" del acta PDF contrastada contra el texto exacto de ese mismo
  caso real (4 excepciones CPU de categoría no válida en Bloque B): coincidencia exacta.

---

## [1.2.0] — 2026-07-10

Incorpora la subcategoría **Agregado** (Acuerdo 26/09/2024, BOPV 10/10/2024), reutilizando
gran parte del motor ya construido para Titular en la v1.1.0. Verificada por ahora solo en
perfil bilingüe (CASO-006); el perfil no bilingüe queda pendiente de un caso real para
contrastarlo — ver "Known issues".

### Added

- Subcategoría `agregado` habilitada en `REGLAMENTOS.acuerdo2024.subcategorias` (art.
  12.4.d): categorías permitidas Catedrático/a, Profesor/a Pleno, Titular de Universidad
  o Agregado/a. Bloque A reutiliza el mismo enrutado 13.2.1/13.2.2 que Pleno; Bloque B
  reutiliza `bloqueB_titular()` (art. 13.3.b), ya generalizado para Titular y Agregado.
- Equivalencia de categoría: "Profesor/a Contratado/a Doctor/a" (PDC) y "Profesor/a
  Permanente Laboral" / "Laboral Permanente" (nueva denominación LOSU) se admiten como
  categoría equiparada a Agregado/a (art. 12.4.d) y, específicamente en Ayudante Doctor,
  como equiparada a Titular de Universidad (art. 3.1.b). En la UPV/EHU ambas
  denominaciones designan la misma figura laboral que "Agregado/a" (Ley del Sistema
  Universitario Vasco / certificación Unibasq); no consta expresamente citada en ninguno
  de los dos reglamentos. Centralizada en la constante `STEMS_EQUIVALENTES_AGREGADO`
  para no duplicar la lista entre `REGLAMENTOS` y `validarPropuesta()`.
- Cuadro informativo nuevo en el Paso 2 (`renderAvisoEquivalenciasCategoria()`): se
  muestra automáticamente cuando el contexto admite esta equivalencia (Ayudante Doctor o
  Agregado), explica el criterio aplicado y su justificación, y lista las filas concretas
  de la propuesta actual afectadas, si las hay.
- CASO-006 (Agregado bilingüe, AGC8L1-D00331-20) documentado como caso de referencia,
  marcado "analizado, no decisivo": la composición coincide con la de la plantilla
  oficial, pero la distribución de categorías del Bloque B (8 Catedráticos de 9) hace que
  el algoritmo simple (art. 13.3.a) y el de Titular/Agregado (art. 13.3.b) den el mismo
  resultado en este caso concreto, por lo que no sirve para contrastar de forma decisiva
  la implementación del art. 13.3.b en Agregado.
- Acta en PDF (`exportarActaPDF()`): añadidas, después de la traza del procedimiento, dos
  secciones nuevas — "Orden del sorteo" (secuencia completa de extracción) y "Propuesta
  reordenada por bloques" (listas de Bloque A y Bloque B ya en el orden usado por el
  algoritmo, con número, nombre, universidad, categoría, perfil lingüístico y sexo), para
  poder reproducir manualmente cada paso de la traza. `calcularComposicion()` expone ahora
  `listaReordenadaA`/`listaReordenadaB` en su resultado para alimentar estas tablas.
- Maquetación del acta en Excel (`exportarActaExcel()`), copiada de una plantilla de
  referencia (`muestra_comision.xlsx`) usando `xlsx-js-style` en vez de `xlsx.full.min.js`
  (la edición community de SheetJS no admite escribir estilos, solo leerlos): cabecera con
  relleno dorado claro (`#FFF2CC`), negrita, centrada y con ajuste de texto; bordes finos
  en cabecera y datos; anchos de columna calibrados; fila separadora entre titulares y
  suplentes con relleno amarillo; título fusionado A1:G1 en negrita; mayúsculas forzadas
  en Nombre y Apellidos y Universidad; auto-ajuste de ancho en Cuerpo-Categoría y en ambas
  columnas de Área de Conocimiento según el contenido más largo de cada propuesta.

### Fixed

- `bloqueB_titular()` (art. 13.3.b) producía solo 5 personas en vez de 6 cuando las dos
  primeras elegidas ya eran ambas Catedrático/Pleno (`cpEnTitular > 1`): la rama
  correspondiente solo añadía una persona más antes de saltar a los controles de mínimos
  de la 5ª/6ª posición, cuando en ese punto la lista solo tenía 3 elementos — en realidad
  rellenaba las posiciones 4 y 5, dejando la 6 sin cubrir. Corregido añadiendo la llamada
  que faltaba para alcanzar la posición 4 antes de aplicar dichos controles. Afecta por
  igual a Titular y Agregado; **pendiente de re-verificar CASO-005 con este fix
  aplicado**, ya que no consta si el caso original disparaba esa rama del código.
- Validación de categorías del Bloque B en Ayudante Doctor (`CATEGORIAS_BLOQUE_B_AYUDANTE_DOCTOR`)
  comparaba con igualdad de cadena exacta contra un array corto (`'CATEDRÁTICO'`,
  `'CATEDRATICO'`, `'TITULAR'`), con lo que formas tan habituales como "CATEDRÁTICA" o
  "PROFESORA TITULAR" se habrían marcado como anomalía. Corregido usando `esCategoria()`
  por raíz léxica, igual que el resto del validador.
- DNI eliminado de ambas exportaciones del acta (Excel y PDF): al ser un dato personal, no
  debe figurar en documentos que se incorporan al expediente. Sigue mostrándose
  enmascarado en la vista en pantalla del Paso 3 (no es una exportación).

### Known issues

- Agregado solo se ha verificado en perfil **bilingüe** (CASO-006). El perfil no
  bilingüe (art. 13.2.2 en Bloque A) comparte código con Pleno no bilingüe, pero no se ha
  contrastado con ningún caso real de Agregado no bilingüe — pendiente de un caso para
  congelarlo.
- CASO-006 no permite confirmar ni descartar la necesidad del algoritmo del art. 13.3.b
  en Agregado (ver "Added"); sigue pendiente un caso con más Titulares/Agregados en el
  Bloque B que fuerce la divergencia entre art. 13.3.a y art. 13.3.b, como ya se buscó sin
  éxito para Titular en la v1.1.0.
- La equivalencia PDC / Permanente Laboral = Agregado/Titular no consta expresamente en
  el texto de ninguno de los dos reglamentos aplicados; se basa en que ambas
  denominaciones corresponden a la misma figura laboral en la UPV/EHU (LSUV/Unibasq vs.
  término estatal), confirmado por Fernando (Vicerrectorado de PDI). No se ha extendido
  esta equivalencia a la subcategoría Titular del Acuerdo 2024 (decisión explícita: PDC
  cuenta como Agregado, no como Titular, dentro del Acuerdo 2024).
- Persisten sin corregir, heredados de la v1.1.0: el uso de `isUPV()` en vez de posición
  en funciones de render puramente informativas, y la cita del art. 11.9 para situación
  administrativa en Ayudante Doctor.

### Not included in this version

- Profesorado Personal Investigador Permanente (dos versiones normativas identificadas,
  Resolución 20/10/2008 y su regulación asociada) — no implementado.

---

## [1.1.0] — 2026-07-08

Incorpora la subcategoría **Titular** (Acuerdo 26/09/2024, BOPV 10/10/2024), en perfil
bilingüe y no bilingüe. Agregado sigue fuera de esta versión (deshabilitado en la
interfaz, previsto para v1.2).

### Added

- Subcategoría `titular` habilitada en `REGLAMENTOS.acuerdo2024.subcategorias`, con
  categorías permitidas Catedrático/a o Titular de Universidad.
- `esTitular()` y `esCatedraticoOPleno()` como nuevos helpers de categoría.
- `bloqueB_titular()`: nuevo algoritmo de sorteo para Bloque B específico de Titular y
  Agregado (art. 13.3.b), distinto del algoritmo simple de Catedrático/Pleno (art.
  13.3.a). Aplica de forma estricta la prioridad de categoría sobre la alternancia de
  género: obliga a que haya al menos tres personas Catedrático/Pleno en el conjunto de
  seis (titulares + suplentes) tras la 5ª elección, y al menos cuatro tras la 6ª,
  forzando la selección de una persona de esa categoría cuando la alternancia de género
  por sí sola no lo garantizaría.
- Nueva regla de validación del mínimo del 40% de Catedrático/Pleno en cada bloque de la
  propuesta (art. 12.4.c para Titular, art. 12.4.d para Agregado), con selector en el
  Paso 2: por defecto se aplica el criterio habitual de redondeo a la baja (mínimo 3 de 8
  ó 9), con opción de activar el criterio estricto de redondeo al alza (mínimo 4).
  Este selector solo afecta a la validación de la propuesta original; el forzado de 3/4
  del art. 13.3.b dentro del propio sorteo son cifras fijas del artículo y no dependen de
  él. Se añadió un aviso explícito en la traza del Paso 3 aclarando esta distinción.
- Referencia normativa añadida a todos los mensajes de conformidad (✓) del Paso 2, no
  solo a las anomalías: numeración, tamaño de bloques, UPV/EHU en Bloque A, situación
  administrativa, equilibrio de género, capacidad bilingüe/trilingüe, categorías y el
  nuevo 40%.
- CASO-005 (Titular bilingüe, TUC8/1-D00144-9) documentado como caso de referencia,
  verificado por análisis normativo artículo por artículo. No se marca como "Validado"
  en el sentido de coincidir con la plantilla oficial de esa plaza, porque dicha
  plantilla aplica el algoritmo incorrecto (13.3.a en vez de 13.3.b) en Bloque B — ver
  "Known issues".

### Fixed

Bugs detectados y corregidos durante el desarrollo de esta versión:

- `esCatedratico()` comparaba con la cadena literal `'CATEDRATICO'` y no reconocía la
  forma femenina `'CATEDRÁTICA'` — corregido usando la raíz léxica `CATEDRATIC`.
- La comprobación de categorías permitidas por subcategoría (`categoriasPermitidas`)
  usaba igualdad de cadena exacta contra la categoría completa, incompatible con
  categorías expresadas como raíz léxica — corregido usando `esCategoria()` (coincidencia
  por subcadena normalizada) en vez de `Array.includes()`, con `categoriasLabel` como
  etiqueta legible independiente para los mensajes.
- El enrutado de Bloque A entre el régimen general (art. 13.2.1) y el específico de
  Pleno/Agregado no bilingüe (art. 13.2.2) se decidía solo por el perfil lingüístico,
  ignorando la subcategoría: Catedrático no bilingüe aplicaba por error el régimen de
  13.2.2. Corregido enrutando también por subcategoría (Catedrático y Titular usan
  siempre 13.2.1; Pleno/Agregado usan 13.2.2 solo si no son bilingües). No afectaba a
  ningún caso congelado (ninguno cubría Catedrático no bilingüe), pero sí a Titular.
- `validarPropuesta()` calculaba Bloque A/B por afiliación institucional (`isUPV()`) en
  vez de por posición para Acuerdo 2024, dando por ejemplo 0 mujeres en Bloque A cuando
  en realidad las había, en propuestas donde el Bloque A incluye personal externo por la
  excepción del art. 12.1.A — corregido reutilizando `getBloquesPropuesta()` de forma
  consistente en todos los checks del Paso 2 (tamaño, género, bilingüismo, categorías,
  40%).
- El propio motor de sorteo tenía el mismo problema de raíz: `calcularComposicion()`
  pasaba la lista reordenada completa (17 personas) a las funciones de Bloque A y B, que
  filtraban internamente por afiliación en vez de por posición. En una propuesta con
  Bloque A parcialmente externo (excepción art. 12.1.A), el "pool" de Bloque A quedaba
  reducido a las pocas personas realmente UPV/EHU, agotándose antes de completar los tres
  pares exigidos (titular + 2 parejas de suplentes) — corregido separando la lista
  reordenada en `listaReordenadaA`/`listaReordenadaB` por posición (nº 1–8 / nº 9–17)
  antes de invocar cada algoritmo, y ajustando `elegePareja()` para que, en el régimen
  general, la primera persona de la pareja se busque explícitamente por afiliación
  UPV/EHU dentro del pool (antes se asumía que el pool ya venía pre-filtrado).
- El requisito de bilingüismo del 100% en Bloque A (art. 12.2) se exigía para cualquier
  subcategoría en plaza bilingüe; en realidad es específico de Pleno y Agregado. Para
  Catedrático y Titular rige el régimen general del art. 12.1.A (mínimo 5 de 8) —
  corregido enrutando también por subcategoría.
- El rango 2–4 de personas UPV/EHU en Bloque A (art. 12.3) se exigía para cualquier
  subcategoría no bilingüe; en realidad es específico de Pleno y Agregado. Para
  Catedrático y Titular rige el mínimo general de 2 (con la expectativa habitual de que
  las 8 sean UPV/EHU, salvo excepción justificada) — corregido del mismo modo.
- Las citas de artículo de la traza del sorteo de Bloque A en Acuerdo 2024 mostraban
  "art. 4.2.a/b" (los de Ayudante Doctor) por reutilizar literalmente esa misma función
  — corregido parametrizando la referencia normativa (`refA`/`refB`) según el reglamento
  que invoca el algoritmo, sin alterar la lógica de selección.
- Variable muerta (`bloqueA` sin uso) eliminada de `renderResultadoSorteo()`.

### Known issues

- Seis casos reales de Titular contrastados hasta la fecha muestran de forma consistente
  que la plantilla Excel oficial aplica el algoritmo simple de Catedrático/Pleno (art.
  13.3.a, solo alternancia de género) en el Bloque B de las plazas de Titular, en vez del
  específico que exige el art. 13.3.b (prioridad de categoría Catedrático/Pleno sobre la
  alternancia de género). El resultado de la plantilla incumple sistemáticamente el
  mínimo de personas Catedrático/Pleno exigido en el conjunto final de Bloque B. El
  validador aplica el art. 13.3.b correctamente; Bloque A ha coincidido siempre entre
  plantilla y validador en los seis casos.
- Ningún caso de Titular está congelado en el sentido de "coincide con un resultado
  oficial correcto", por el motivo anterior. CASO-005 documenta un resultado verificado
  por análisis normativo propio, no por la plantilla oficial de esa plaza.
- La interpretación de "forzar Catedrático/Pleno" en la 5ª y 6ª elección del art. 13.3.b
  prioriza siempre la categoría sobre la alternancia de género cuando ambas entran en
  conflicto (interpretación estricta, sin caso oficial correcto disponible para
  contrastarla).
- Persisten sin corregir, por quedar fuera del alcance de esta versión: el uso de
  `isUPV()` en vez de posición en algunas funciones de render fuera de
  `validarPropuesta()` (contadores puramente informativos, sin efecto en la validación
  ni en el sorteo), y la cita del art. 11.9 para situación administrativa en Ayudante
  Doctor (heredada de la v1.0.0, pendiente de revisión con el texto completo de ese
  reglamento).

### Not included in this version

- Profesorado Agregado (art. 12.4.d y art. 13.3.b) — deshabilitado en la interfaz,
  previsto para v1.2. Comparte gran parte de la lógica ya construida para Titular
  (mismo `bloqueB_titular()`, mismo check del 40%), pero difiere en la regla de
  categorías permitidas y en el enrutado de Bloque A (usa art. 13.2.2 cuando no es
  bilingüe, como Pleno, no siempre 13.2.1 como Titular).

---

## [1.0.0] — 2026-07-07

Primera versión estable del validador. Cubre la validación de propuestas y el cálculo de
composición de Comisión de Selección para:

- **Profesorado Ayudante Doctor** (Acuerdo Consejo de Gobierno, 11 junio 2024).
- **Catedrático** y **Pleno** (Acuerdo 26/09/2024, BOPV 10/10/2024), en perfil bilingüe y
  no bilingüe.

Titular y Agregado quedan fuera de esta versión (deshabilitados en la interfaz, previstos
para v1.1).

### Added

- Parseo de la propuesta desde Excel (`.xlsx`), con detección de cabeceras por nombre y
  posición de respaldo (`crearIndiceColumnas`), y detección automática del código de plaza
  desde el título del fichero.
- Motor de validación (`validarPropuesta()`) que comprueba, según el reglamento aplicable:
  numeración 1–17 sin huecos ni duplicados, tamaño y proporción de bloques, situación
  administrativa, área de conocimiento, equilibrio de género, capacidad bilingüe/trilingüe
  y categoría académica — con mensajes de anomalía referenciados al artículo aplicable y
  sugerencia de corrección.
- Mecanismo de excepción CPU: cualquier anomalía puede marcarse como validada por la
  Comisión de Planificación Universitaria, con referencia de acta, sin bloquear el sorteo.
- Motor de sorteo (`calcularComposicion()`) que reordena la propuesta según el resultado
  del sorteo público y aplica el algoritmo de formación de pareja/alternancia de género
  correspondiente a cada bloque y cada régimen normativo, con traza paso a paso de cada
  decisión y su artículo de referencia.
- Entrada del sorteo por bolas individuales o como secuencia de texto.
- Exportación a Excel y PDF (vía impresión del navegador) tanto del informe de validación
  como del acta de composición final, con DNI enmascarado en pantalla.
- Cuatro casos de referencia congelados como regresión: CASO-001 (Ayudante Doctor),
  CASO-002 (Catedrático bilingüe), CASO-003 (Pleno bilingüe), CASO-004 (Pleno no
  bilingüe).

### Fixed

Bugs detectados y corregidos durante el desarrollo, acumulados hasta esta versión:

- Comparación de categoría por igualdad de cadena exacta, que bloqueaba todas las
  propuestas de Acuerdo 2024; sustituida por comparación de subcadena normalizada.
- Regla de emparejamiento del Bloque A (art. 13.2.1 vs. 13.2.2) aplicada según el perfil
  bilingüe en vez de según la subcategoría: Catedrático usa siempre 13.2.1; Pleno/Agregado
  usa 13.2.2 solo cuando la plaza no es bilingüe.
- Duplicación silenciosa de personas entre Bloque A y Bloque B cuando el art. 13.2.2
  incorporaba candidatos externos al Bloque A, que el Bloque B volvía a seleccionar por su
  cuenta al no excluir a quienes ya se habían usado — corregido separando la lista
  reordenada en dos sublistas por posición (nº 1–8 / nº 9–17) antes de aplicar el
  algoritmo de cada bloque.
- Reconocimiento de variantes de categoría (femeninas, abreviaturas, euskera) que fallaba
  con formas como "Catedrática", "CU", "TU" o "Katedraduna" — corregido con
  `normalizarCategoria()` y comparación por raíz léxica (`CATEDRATIC`, `PLEN`, etc.) en vez
  de por palabra completa.
- `validarPropuesta()` calculaba el Bloque A/B por afiliación institucional (`isUPV()`) en
  vez de por posición para Acuerdo 2024, dando conteos incorrectos de UPV/EHU en Bloque A
  y de paridad de género — corregido usando `getBloquesPropuesta()` de forma consistente
  en toda la aplicación; se añadió además una comprobación explícita de personas UPV/EHU
  coladas en el Bloque B (no permitido por art. 12.1.B).
- Categoría llegando como cadena compuesta con género flexionado (p. ej. "PROFESORA
  CATEDRATICA") en vez de la palabra clave aislada — resuelto con `esCategoria()` sobre
  raíces léxicas, y una etiqueta separada (`categoriasLabel`) para que los mensajes de
  error sigan siendo legibles.
- Etiquetado del código de fila ("UPV/EHU" vs. "EXT") calculado por afiliación individual
  en vez de por bloque de origen: las personas externas que completan el Bloque A (art.
  12.3) se mostraban como "EXT" en vez de "UPV/EHU" — corregido con el helper
  `codigoBloque()`, que distingue por posición en Acuerdo 2024 y por afiliación en
  Ayudante Doctor.

### Known issues

- La cita del artículo para la situación administrativa en plazas de Ayudante Doctor
  referencia por ahora el art. 11.9 del reglamento de Acuerdo 2024 (incorrecto para ese
  caso); pendiente de corregir con el texto completo del reglamento de Ayudante Doctor.
- No se ha podido contrastar este validador contra la plantilla Excel oficial como fuente
  fiable: se ha detectado que dicha plantilla desalinea las columnas de nombre y
  universidad en las filas de suplentes (ver CASO-004). El validador se apoya en la
  verificación manual del articulado y en los casos de referencia congelados, no en la
  plantilla.

### Not included in this version

- Profesorado Titular y Agregado (art. 12.4.c/d y art. 13.3.b, con los umbrales del 40%
  de Catedrático/Pleno) — deshabilitados en la interfaz, previstos para v1.1.