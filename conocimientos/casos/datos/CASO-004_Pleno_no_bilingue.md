# CASO-004 - Comisión de Selección para Profesorado Pleno (no bilingüe)

## Estado

**Validado**

Este caso corresponde a una propuesta real de Departamento para una plaza de Profesorado
Pleno, perfil **no bilingüe**. La composición de referencia de este documento es la que
genera `validador.html` (una vez corregidos los dos bugs descritos más abajo), verificada
manualmente por Fernando siguiendo el Acuerdo 26/09/2024 artículo por artículo.

**No se usa la plantilla Excel oficial como fuente de este caso.** Al comparar ambas
salidas se detectó que la plantilla tiene un fallo de desalineación conocido: las columnas
"Nombre y apellidos" / "Universidad" de las filas de suplentes no corresponden a la
persona real de esa fila (categoría, área, perfil y sexo sí quedan correctamente atados al
número de la propuesta; nombre/universidad muestran los de otra fila). Este patrón ya se
había detectado antes con la plantilla en otro contexto (mapeo por posición de fila en vez
de por número), y ha quedado confirmado de nuevo aquí. Por eso este caso se congela con los
datos del validador, no con los de la plantilla.

Debe utilizarse como caso de referencia congelado (regresión) para el régimen de
Acuerdo 26/09/2024, subcategoría Pleno, perfil **no bilingüe** (art. 13.2.2 / art. 12.3),
análogo a CASO-002 (Catedrático bilingüe) y CASO-003 (Pleno bilingüe).

---

# Objetivo

Describir el procedimiento completo seguido para construir una Comisión de Selección de
una plaza de Profesorado Pleno no bilingüe a partir de:

- la propuesta inicial de miembros (17 personas, Bloque A nº 1–8 / Bloque B nº 9–17);
- el resultado del sorteo;
- la aplicación de las reglas de negocio (art. 12.3 y art. 13.2.2 / 13.3.a del Acuerdo
  26/09/2024).

Este caso, además, sirvió para detectar y corregir dos bugs del motor de sorteo y de
presentación (ver sección "Bugs detectados y corregidos").

---

# Contexto

## Tipo de plaza

Catedrático · Pleno · Titular · Agregado (Acuerdo 26/09/2024) — subcategoría **Pleno**

## Código de plaza

PLC8L1-D00166-2

## Área de conocimiento

230 - Economía Financiera y Contabilidad (Bloque B y mayoría del Bloque A; nº3 pertenece
al área afín 95 - Comercialización e Investigación de Mercados)

## Perfil lingüístico

No bilingüe

---

# Datos de entrada

## Propuesta inicial

La propuesta inicial está formada por **17 personas**: 8 en el Bloque A (nº 1–8) y 9 en
el Bloque B (nº 9–17). Fichero de referencia: `propuesta_pleno_no_bilingue.csv`.

Conforme al art. 12.3 (Pleno/Agregado no bilingüe), el Bloque A no exige que las 8
personas sean de la UPV/EHU: basta un mínimo de 2 y máximo de 4. En esta propuesta el
Bloque A tiene exactamente **4 personas UPV/EHU** (nº1, 2, 3, 4) y **4 externas**
(nº5, 6, 7, 8) — dentro del rango permitido.

---

# Procedimiento aplicado

1. Partir de la propuesta inicial (Bloque A: nº 1–8; Bloque B: nº 9–17).
2. Aplicar el orden obtenido en el sorteo para reordenar la lista completa.
3. **Separar la lista reordenada en dos sublistas por posición** — Bloque A (nº 1–8) y
   Bloque B (nº 9–17), conservando el orden de extracción dentro de cada una — antes de
   aplicar el algoritmo de cada bloque (ver "Bugs detectados y corregidos", bug 1).
4. Bloque A — art. 13.2.2 (régimen específico de Pleno/Agregado no bilingüe):
   - Pareja titular: primera persona UPV/EHU de la lista reordenada **del Bloque A**, y a
     continuación primera persona de género distinto **y externa a la UPV/EHU**, también
     dentro del Bloque A.
   - Se repite el proceso dos veces más, con la lista de personas restantes del Bloque A,
     para obtener las 4 personas suplentes.
5. Bloque B — art. 13.3.a: primera persona de la lista reordenada **del Bloque B** y,
   alternando género, cinco personas más de ese mismo bloque.
6. Verificar el cumplimiento de todas las reglas de negocio.
7. Obtener la composición definitiva de la Comisión.

Un orden de sorteo que reproduce el resultado de este caso (construido para verificar el
fix, consistente con la propuesta):

`4 → 3 → 5 → 6 → 1 → 8 → 7 → 2 → 9 → 16 → 11 → 10 → 15 → 14 → 12 → 13 → 17`

---

# Resultado esperado (según el validador, tras los fixes)

## Miembros titulares

### Bloque A

| Nº | Nombre | Universidad | Categoría | Sexo |
|----|---------|-------------|-----------|------|
| 4 | Jon Landeta Rodríguez | UPV/EHU | Catedrático | Hombre |
| 5 | Sara Fernández López | Universidad de Santiago de Compostela | Catedrática | Mujer |

### Bloque B

| Nº | Nombre | Universidad | Categoría | Sexo |
|----|---------|-------------|-----------|------|
| 9 | Esteban Romero Trías | Universidad de Granada (UGR) | Catedrático | Hombre |
| 16 | Begoña Gutiérrez Nieto | Universidad de Zaragoza (UZA) | Catedrática | Mujer |
| 11 | José Pedro Martí Pellón | Universidad Complutense de Madrid (UCM) | Catedrático | Hombre |

---

## Miembros suplentes

### Bloque A

| Nº | Nombre | Universidad | Categoría | Sexo |
|----|---------|-------------|-----------|------|
| 3 | Vanessa Apaolaza Ibañez | UPV/EHU | Catedrática | Mujer |
| 6 | Lázaro Rodríguez Ariza | Universidad de Granada (UGR) | Catedrático | Hombre |
| 1 | Leire San José Ruiz de Aguirre | UPV/EHU | Catedrática | Mujer |
| 8 | Carlos López Gutiérrez | Universidad de Cantabria (UCN) | Catedrático | Hombre |

### Bloque B

| Nº | Nombre | Universidad | Categoría | Sexo |
|----|---------|-------------|-----------|------|
| 10 | Carmen Inés Ruiz de la Rosa | Universidad de La Laguna | Catedrática | Mujer |
| 15 | Antonio Terceño Gómez | Universidad Rovira i Virgili (URV) | Catedrático | Hombre |
| 14 | Myriam García Olalla | Universidad de Cantabria (UCN) | Catedrática | Mujer |

Nota de etiquetado: el "Código" de cada fila (UPV/EHU vs. EXT) se asigna por **bloque de
origen** (posición 1–8 = UPV/EHU, 9–17 = EXT), no por afiliación individual — así, nº5, 6
y 8 aparecen como "UPV/EHU-TIT/SUP" pese a ser de universidades externas, por pertenecer
al Bloque A (ver bug 2).

---

# Bugs detectados y corregidos en este caso

## Bug 1 — Duplicación de personas entre Bloque A y Bloque B

**Síntoma:** antes del fix, la persona nº16 (Begoña Gutiérrez Nieto) resultaba
seleccionada simultáneamente como segunda titular del Bloque A y como titular del Bloque
B; nº9 y nº11 también se duplicaban entre bloques.

**Causa raíz:** `calcularComposicion()` pasaba la lista reordenada completa (17 personas)
tanto a `bloqueA_Acuerdo2024()` como a `bloqueB_alternando()`. El art. 13.1 exige dos
sorteos independientes (uno por bloque) y los arts. 13.2/13.3 operan explícitamente sobre
"la lista reordenada del bloque A" / "del bloque B" — listas disjuntas por diseño. Al no
separar la lista combinada de 17 en sus dos sublistas por posición (nº 1–8 / nº 9–17)
antes de aplicar cada algoritmo, el Bloque A podía alcanzar personas numeradas en el rango
del Bloque B (posible en Pleno/Agregado no bilingüe porque el art. 12.3 permite completar
el Bloque A con externos), y el Bloque B las volvía a seleccionar sin saber que ya
estaban usadas.

Con Ayudante Doctor y con Catedrático/Pleno **bilingüe** el bug no se manifestaba porque
el Bloque A queda filtrado a UPV/EHU exclusivamente (arts. 12.1.A/12.2), sin solape
posible con el Bloque B.

**Fix:** en `calcularComposicion()`, para `tipoPlaza === 'acuerdo2024'`, se separa la
lista reordenada en `listaReordenadaA` (nº 1–8) y `listaReordenadaB` (nº 9–17),
conservando el orden de extracción dentro de cada una, antes de invocar
`bloqueA_Acuerdo2024()` y `bloqueB_alternando()` respectivamente.

## Bug 2 — Etiquetado de "Código" por afiliación individual en vez de por bloque

**Síntoma:** las personas externas que completan el Bloque A (nº5, 6, 8 en este caso)
aparecían etiquetadas como "EXT-TIT"/"EXT-SUP" en vez de "UPV/EHU-TIT"/"UPV/EHU-SUP".

**Causa raíz:** `filaTabla()`, `exportarActaExcel()` y `exportarActaPDF()` calculaban el
código a partir de `isUPV(p.universidad)` (afiliación real de la persona), en vez de a
partir del bloque de origen. El art. 12.3 permite completar el Bloque A con personal
externo, pero esa persona sigue perteneciendo administrativamente al "bloque UPV/EHU" a
efectos del acta.

**Fix:** nuevo helper `codigoBloque(p, tipoPlaza)` — para `acuerdo2024` calcula el código
por posición (nº 1–8 → "UPV/EHU", nº 9–17 → "EXT"); para `ayudante_doctor` mantiene el
cálculo por afiliación (`isUPV`), ya que en ese reglamento el Bloque A es exclusivamente
UPV/EHU y ambos criterios coinciden.

---

# Reglas aplicadas

- REG-001 - Número de miembros (17 personas, 8+9).
- REG-002 - Procedencia institucional (Bloque A por posición 1–8, admite externos por
  art. 12.3; Bloque B exclusivamente externo).
- REG-003 - Categorías académicas (Catedrático/a o Pleno).
- REG-004 - Área de conocimiento (área 95 en Bloque A como área afín, no bloqueante).
- REG-005 - Equilibrio de género (mínimo 4 mujeres en cada bloque).
- REG-006 - Requisitos lingüísticos (no aplica, plaza no bilingüe).
- REG-007 - Situación administrativa (todos "Activo").

---

# Validaciones esperadas

- El Bloque A (nº 1–8) tiene entre 2 y 4 personas UPV/EHU (art. 12.3); en este caso, 4.
- Ninguna persona aparece simultáneamente en el Bloque A y en el Bloque B de la
  composición final.
- El código de bloque (UPV/EHU vs. EXT) se asigna por posición de origen, no por
  afiliación individual.
- La comisión generada coincide exactamente con la tabla de "Resultado esperado" de este
  documento.

---

# Documentación asociada

- `propuesta_pleno_no_bilingue.csv` — propuesta oficial de miembros.
- Composición de referencia: la de este documento (generada por `validador.html` tras los
  fixes descritos), verificada manualmente contra el Acuerdo 26/09/2024.
- **No usar** `comision_pleno__no_bilingue.csv` ni el PDF asociado de la plantilla Excel
  como referencia: contienen el fallo de desalineación de columnas descrito arriba.

---

# Fuente normativa

- ACUERDO de 26 de septiembre de 2024 (BOPV 10/10/2024), arts. 11, 12.3, 13.1, 13.2.2 y
  13.3.a.
- `resumen_composicion_pleno_no_bilingue.md`, `resumen_propuesta_pleno_no_bilingue.md`.