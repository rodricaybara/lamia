## [1.2.8] - 2026-10-20

### Added
- **Interruptor del art. 13.3.b en el Bloque B de Agregado (Paso 3, encima de "Calcular composición")**: el art. 13.3 no regula expresamente el Bloque B de las plazas de Agregado, por lo que el criterio se deja a elección del usuario. Solo aparece en Acuerdo 26/09/2024 con subcategoría Agregado.
  - **OFF (por defecto, criterio actual)**: alternancia de sexos, art. 13.3.a (`bloqueB_alternando`).
  - **ON**: se interpreta que Agregado se asimila a Titular y se aplica el art. 13.3.b (`bloqueB_titular`).
  - Nuevo campo `STATE.aplicar133bAgregado` y manejador `toggleCriterio133b()`. Se reinicia a OFF al cambiar de tipo de plaza o de subcategoría. Al cambiarlo se descarta el resultado ya calculado (`STATE.resultado = null`), para que ni la pantalla ni las exportaciones muestren una composición obtenida con el criterio anterior.
  - No se ofrece en Pleno porque no tendría efecto: sus categorías permitidas son solo Catedrático/a y Profesor/a Pleno, por lo que todo su Bloque B cumple ya la exigencia de categoría del art. 13.3.b y el resultado es idéntico al del art. 13.3.a (comprobado con 20.000 listas aleatorias, 0 diferencias).
- **Nota aclaratoria del criterio aplicado en el Bloque B** (Pleno y Agregado), visible en pantalla y en las dos actas. Texto único generado por la nueva función `notaCriterioBloqueB(subcategoria, usa133b)`:
  - **Pleno**: no está regulada expresamente la composición del Bloque B; se aplica el art. 13.3.a, bien por aplicarse directamente la alternancia de sexos, bien por asimilar las plazas de Pleno a las de Catedrático.
  - **Agregado, interruptor OFF**: no está regulada expresamente; se aplica el art. 13.3.a y no el 13.3.b, previsto para Titular.
  - **Agregado, interruptor ON**: no está regulada expresamente; por interpretación se asimila Agregado a Titular y se aplica el art. 13.3.b.
  - Acta PDF (`exportarActaPDF()`): nueva sección "Criterio aplicado en el Bloque B", entre la tabla de composición y la traza.
  - Acta Excel (`construirHojaComposicion()`): fila(s) al pie de la hoja "Composición", tras una fila en blanco, con celdas combinadas A:K.
- **Anomalía cuando el art. 13.3.b no puede forzar la categoría Catedrático/Pleno** (p. ej., excepción aprobada por la CPU con menos Catedráticos/Pleno de los habituales en el Bloque B): `bloqueB_titular()` incorpora la función interna `elegirCP()`. Si en un paso en el que el artículo obliga a elegir un Catedrático/Pleno ya no queda ninguno, se selecciona la primera persona restante de género distinto y se registra el fallo. Se notifica en:
  - la **traza**, con la línea marcada "⚠ Anomalía";
  - un **banner en el resultado** (Paso 3);
  - el **acta PDF**, sección "Anomalías en la composición";
  - el **acta Excel**, fila al pie con prefijo "ANOMALÍA en la composición" en negrita.

  El mensaje indica el mínimo exigido (3 tras la 5ª elección, 4 tras la 6ª), cuántos Catedráticos/Pleno hay en el Bloque B de la propuesta y cuántos en la composición final, y en qué pasos no se pudo forzar la categoría.
- `calcularComposicion()` admite un sexto parámetro opcional `opciones` (`{ aplicar133b }`) y devuelve tres campos nuevos: `reglaBloqueB`, `notaCriterioB` y `anomaliasB`. Sin `opciones` el comportamiento es el de la v1.2.7, de modo que los tests y los casos congelados no se ven afectados.

### Changed
- El aviso de la traza sobre los pasos "forzado CP" / "refuerzo" (cifras fijas de 3 y 4, independientes del selector del 40% del Paso 2) se decide ahora por la regla efectivamente aplicada (`r.reglaBloqueB === 'art. 13.3.b'`) y no por la subcategoría: se muestra en Titular y en Agregado con el interruptor en ON.
- Número de versión mostrado en cabecera actualizado a "v1.2.8".

### Fixed
- **`bloqueB_titular()` (art. 13.3.b) devolvía solo 5 personas de Bloque B** cuando la propuesta tenía menos de 4 Catedráticos/Pleno en el Bloque B (p. ej., 3, que el criterio habitual del 40% con redondeo a la baja admite): al no encontrar candidato a forzar, el paso se omitía y la selección quedaba incompleta. Ahora la comisión se completa siempre con 6 personas y la situación se notifica como anomalía (ver "Added"). Afectaba a Titular, y desde esta versión también a Agregado con el interruptor en ON.

### Verified
- Sandbox de Node (`vm.createContext`) con un caso sintético en el que los Titulares/Agregados preceden a los Catedráticos en el Bloque B, de modo que 13.3.a y 13.3.b divergen:
  - Interruptor OFF: Agregado idéntico al de la v1.2.7 (art. 13.3.a).
  - Interruptor ON: Agregado idéntico al de Titular y al que daba la v1.2.6 (art. 13.3.b).
  - Pleno, Catedrático y Titular: sin cambios respecto a la v1.2.7; el parámetro `aplicar133b` se ignora en ellos.
  - Ayudante Doctor: sin cambios (art. 4.3), sin nota de criterio.
- 30.000 listas aleatorias de Bloque B para el fallo de la categoría forzada: con 4 o más Catedráticos/Pleno (≈18.000 listas) el resultado es idéntico al de la v1.2.7 y no aparece ninguna anomalía; con menos de 4 (≈12.000 listas) la composición tiene siempre 6 personas de Bloque B, incluye a todos los Catedráticos/Pleno disponibles y siempre se genera la anomalía.
- Prueba de interfaz (DOM simulado con `jsdom`): el interruptor aparece solo en Agregado; por defecto está en OFF; se reinicia al cambiar de subcategoría; la nota de criterio y las anomalías aparecen en pantalla, en el acta PDF y en el acta Excel (que se genera sin errores con `xlsx-js-style` 1.2.0).

### Known issues
- **Pendiente de re-verificar CASO-006** (Agregado bilingüe) con esta versión. En ese caso 13.3.a y 13.3.b daban el mismo resultado (ver v1.2.0), por lo que con cualquiera de las dos posiciones del interruptor no debería cambiar, pero no se ha contrastado con el CSV y la secuencia reales.
- La asimilación de Agregado a Titular (interruptor ON) y de Pleno a Catedrático es una **interpretación**, no una mención expresa del art. 13; conviene recogerla en las aclaraciones prácticas.
- La anomalía de la categoría forzada solo se detecta al calcular la composición (Paso 3). El Paso 2 no avisa todavía de que el Bloque B de una propuesta de Titular o de Agregado tenga menos de 4 Catedráticos/Pleno (el selector del 40% admite un mínimo de 3).
- La validación del 40% de Catedrático/Pleno por bloque (art. 12.4.d) sigue aplicándose a Agregado en `validarPropuesta()`, independientemente del interruptor; no se ha modificado.
- La presentación en un navegador real (maquetación del interruptor y de los banners) no se ha comprobado visualmente; solo se verificó el HTML generado.
