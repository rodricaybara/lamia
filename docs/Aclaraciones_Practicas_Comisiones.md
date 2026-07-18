# Aclaraciones prácticas de aplicación — Comisiones de Selección

## Naturaleza de este documento

Este documento **no es normativa**. Recoge interpretaciones y matices de aplicación práctica confirmados durante el desarrollo y validación artículo por artículo del motor de cálculo de comisiones (proyecto "Lamia" / `validador.html`), contrastados contra casos reales de sorteo y composición.

Ante cualquier discrepancia aparente entre este documento y la normativa marco (Acuerdo 26/09/2024, Reglamento de Profesorado Ayudante Doctor, etc.), **prevalece siempre la normativa**. Este documento debe tratarse como contexto adicional de apoyo, no como fuente de rango normativo.

Cada entrada indica el artículo o regla de referencia y, cuando existe, el caso real que la confirma.

---

## 1. Asignación de Bloque A / Bloque B: por posición, no por afiliación institucional

**Regla:** El Bloque A (posiciones 1–8) y el Bloque B (posiciones 9–17) se determinan **exclusivamente por el número de posición** que la persona ocupa en la lista de propuesta, **nunca** por si la persona pertenece o no a la UPV/EHU.

**Por qué es contraintuitivo:** Es habitual asumir que "Bloque A = personal UPV/EHU" y "Bloque B = personal externo", porque así es *en principio* como se construye la propuesta (art. 12.1.A y 12.1.B). Pero la excepción del art. 12.1.A permite incluir personas externas en posiciones del Bloque A, y eso no cambia el bloque al que pertenecen: siguen contando como Bloque A por ocupar una posición 1–8.

**Consecuencia práctica:** Al verificar una propuesta o resolver una alegación sobre composición de bloque, mirar siempre el número de posición, no la procedencia institucional de la persona.

**Aplica a:** todas las subcategorías del Acuerdo 26/09/2024 (Catedrático, Pleno, Titular, Agregado). Para Ayudante Doctor, la asignación de bloque sí se determina por afiliación institucional (régimen distinto).

---

## 2. Régimen general (art. 13.2.1) vs. régimen de pareja con exigencia de no-UPV (art. 13.2.2)

**Regla:**
- El **art. 13.2.1** (régimen general de emparejamiento) se aplica **siempre** a Catedrático, y también a Pleno/Titular/Agregado **cuando la plaza es bilingüe**.
- El **art. 13.2.2** (el segundo miembro de cada pareja debe ser obligatoriamente ajeno a la UPV/EHU) se aplica **únicamente** a Pleno/Agregado **no bilingüe**.

**Consecuencia práctica:** Antes de aplicar el art. 13.2.2 a una consulta, confirmar dos cosas: que la subcategoría es Pleno o Agregado (nunca Catedrático o Titular) y que la plaza **no** es bilingüe. Si falta cualquiera de las dos condiciones, se aplica el 13.2.1.

**Confirmado en:** CASO-003 (Pleno bilingüe, aplica 13.2.1), CASO-004 (Pleno no bilingüe, aplica 13.2.2), CASO-006 (Agregado bilingüe, aplica 13.2.1).

---

## 3. Bloque B de Titular/Agregado: prioridad de categoría (art. 13.3.b) sobre alternancia de género (art. 13.3.a)

**Regla:** En el Bloque B de Titular y Agregado, la exigencia de un mínimo de miembros con categoría de Catedrático/Pleno (3 y, después, 4 — valores fijos de origen estatutario, independientes del umbral del 40%) tiene **prioridad estricta** sobre la alternancia de género del art. 13.3.a.

**Aviso importante:** La plantilla Excel oficial del Vicerrectorado **aplica incorrectamente el art. 13.3.a** (alternancia simple, sin restricción de categoría) en lugar del 13.3.b en este supuesto. Un cálculo de composición de Bloque B para Titular o Agregado hecho con la plantilla oficial puede no ser fiable si hay tensión entre el criterio de categoría y la alternancia de género.

**Cómo detectar si hay tensión real:** Si en el Bloque B hay pocos Titulares/Agregados (la mayoría son Catedráticos/Plenos), los dos artículos suelen coincidir en el resultado y el error de la plantilla pasa desapercibido. La divergencia solo se hace visible cuando hay una proporción significativa de Titulares/Agregados en el Bloque B.

**Estado de verificación:**
- **Titular:** confirmado con CASO-005, tras corregir un fallo del motor (`bloqueB_titular()`) que producía 5 miembros de Bloque B en vez de 6.
- **Agregado:** **no confirmado de forma concluyente todavía.** CASO-006 tiene una distribución de categorías en el Bloque B (8 Catedráticos de 9) que hace que el art. 13.3.a y el 13.3.b coincidan en el resultado, por lo que este caso no permite distinguir cuál se está aplicando realmente. Se necesita un caso con más Titulares/Agregados en el Bloque B para confirmarlo.

**Consecuencia práctica:** Ante una consulta sobre composición de Bloque B de Titular o Agregado que involucre un cálculo hecho con la plantilla Excel oficial, advertir de esta posible discrepancia y recomendar verificación adicional si hay varios Titulares/Agregados en el Bloque B.

---

## 4. Errores conocidos adicionales de la plantilla Excel oficial

**Pleno no bilingüe — suplentes:** La plantilla oficial produce una composición incorrecta de suplentes para Pleno no bilingüe, debido a errores de mapeo entre filas y posiciones. Confirmado en CASO-004.

**Consecuencia práctica:** No dar por buena, sin contraste adicional, una composición de comisión calculada con la plantilla Excel oficial para plazas de Pleno no bilingüe o para el Bloque B de Titular/Agregado. Si hay dudas, remitir a verificación manual artículo por artículo.

---

## 5. Equivalencias de categoría para Agregado (no aplicables a Titular)

**Regla:** Las siguientes denominaciones de categoría se consideran equivalentes a Agregado/a en la UPV/EHU:
- Profesor/a Contratado/a Doctor/a (PDC)
- Laboral Permanente
- Permanente Laboral

**Importante — límite de la equivalencia:** Esta equivalencia aplica **únicamente** a efectos de la categoría Agregado. **No se extiende a la categoría Titular.** Una persona con categoría "Profesor/a Contratado/a Doctor/a" cuenta como Agregado/a a efectos de composición de comisión, pero no cuenta como Titular.

**Consecuencia práctica:** Es un punto frecuente de duda de aspirantes ("soy PDC, ¿puedo formar parte de/optar a una comisión de Titular?"). La respuesta depende de si la categoría exigida es Agregado (sí cuenta) o Titular (no cuenta).

**Reconocimiento de categoría en general:** El emparejamiento de categorías debe hacerse por raíz léxica del término (p. ej. `CATEDRATIC`, `KATEDRADUN`, `PLEN`), no por coincidencia exacta de cadena de texto, para cubrir variantes de género, abreviaturas y formas en euskera. Esto es relevante sobre todo para quien redacte o revise propuestas, menos para la resolución de consultas puntuales, pero puede ayudar a explicar por qué una denominación no estándar en una propuesta sigue siendo válida.

---

## Índice de casos de referencia utilizados

| Caso | Subcategoría | Relevante para |
|------|-------------|-----------------|
| CASO-001 | Ayudante Doctor | Régimen general de composición y sorteo |
| CASO-002 | Catedrático bilingüe | Régimen general art. 13.2.1 |
| CASO-003 | Pleno bilingüe | Art. 13.2.1 vs 13.2.2 |
| CASO-004 | Pleno no bilingüe | Art. 13.2.2; error de la plantilla oficial en suplentes |
| CASO-005 | Titular | Art. 13.3.b confirmado en Bloque B |
| CASO-006 | Agregado bilingüe | Art. 13.3.b no concluyente; equivalencias de categoría |
