# Changelog

Todas las novedades notables de este proyecto se documentan en este fichero.

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

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