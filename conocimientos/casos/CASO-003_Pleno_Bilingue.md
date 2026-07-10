# CASO-003 - Comisión de Selección para Profesorado Pleno (bilingüe)

## Estado

**Validado**

Este caso corresponde a una propuesta real de Departamento para una plaza de Profesorado
Pleno, perfil bilingüe. El resultado de la composición ha sido verificado ejecutando el
motor de sorteo (`calcularComposicion`) tal y como está implementado en `validador.html`,
y coincide exactamente, persona a persona y en el mismo orden, con la comisión oficial
resultante.

Debe utilizarse como caso de referencia congelado (regresión) para el régimen de
Acuerdo 26/09/2024, subcategoría Pleno, perfil bilingüe — análogo a CASO-002 para
Catedrático bilingüe.

---

# Objetivo

Describir el procedimiento completo seguido para construir una Comisión de Selección de
una plaza de Profesorado Pleno bilingüe a partir de:

- la propuesta inicial de miembros (17 personas, Bloque A 1–8 / Bloque B 9–17);
- el resultado del sorteo;
- la aplicación de las reglas de negocio (art. 12 y art. 13 del Acuerdo 26/09/2024).

---

# Contexto

## Tipo de plaza

Catedrático · Pleno · Titular · Agregado (Acuerdo 26/09/2024) — subcategoría **Pleno**

## Código de plaza

PLC8L1-D00039-1

## Área de conocimiento

755 - Química Física (Bloque A y mayoría del Bloque B; ver nota sobre áreas afines más
abajo)

## Perfil lingüístico

Bilingüe

---

# Datos de entrada

## Propuesta inicial

La propuesta inicial está formada por **17 personas**: 8 en el Bloque A (nº 1–8, todas de
la UPV/EHU) y 9 en el Bloque B (nº 9–17, todas externas). Fichero de referencia:
`propuesta_pleno_bilingue.csv`.

Nota sobre la columna "Cuerpo-Categoría": en esta propuesta real llega como texto
compuesto con género flexionado — "Profesor Catedratico", "Profesora Catedratica",
"Profesor Pleno" — y no como la palabra clave aislada ("Catedrático", "Pleno"). Este
caso fue precisamente el que puso de manifiesto que el check de categoría de
`validarPropuesta()` debía compararse por raíz léxica normalizada (`CATEDRATIC`, `PLEN`)
y no por igualdad exacta ni por la palabra completa "CATEDRATICO" (que no reconoce por
subcadena la forma femenina "CATEDRATICA").

Nota sobre área de conocimiento: la propuesta incluye 4 códigos de área distintos (755,
760, 750, 555), todos dentro del ámbito de Química. Esto genera un aviso ("Requiere
criterio") por uso de áreas afines, no un bloqueante.

## Resultado del sorteo

Orden obtenido (bolas 1–17, sorteo único reordenado por bloques según la práctica habitual
descrita en `resumen_composicion_catedratico_no_bilingue.md`):

9 → 11 → 16 → 10 → 14 → 17 → 6 → 5 → 12 → 8 → 4 → 7 → 15 → 3 → 1 → 13 → 2

---

# Procedimiento aplicado

1. Partir de la propuesta inicial (Bloque A: nº 1–8, todos UPV/EHU; Bloque B: nº 9–17,
   todos externos).
2. Aplicar el orden obtenido en el sorteo para reordenar la lista completa.
3. Bloque A — régimen general art. 13.2.1 (Pleno bilingüe usa el mismo régimen que
   Catedrático, no el art. 13.2.2 específico de Pleno/Agregado no bilingüe):
   - Pareja titular: primera persona UPV/EHU bilingüe de la lista reordenada, y a
     continuación primera persona de género distinto.
   - Se repite el proceso dos veces más para obtener las 4 personas suplentes.
4. Bloque B — art. 13.3.a: primera persona externa de la lista reordenada y, alternando
   género, cinco personas externas más.
5. Verificar el cumplimiento de todas las reglas de negocio.
6. Obtener la composición definitiva de la Comisión.

---

# Resultado esperado

## Miembros titulares

### Bloque A (UPV/EHU)

| Nº | Nombre | Categoría | Sexo |
|----|---------|-----------|------|
| 6 | Olatz Zuloaga Zubieta | Profesora Catedrática | Mujer |
| 4 | Jose Javier López Pestaña | Profesor Catedrático | Hombre |

### Bloque B (externos)

| Nº | Nombre | Universidad | Categoría |
|----|---------|-------------|-----------|
| 9 | Ignacio Nilo Tuñón García de Vicuña | Universitat de València | Profesor Catedrático |
| 16 | Ana María Graña Rodríguez | Universidad de Vigo | Profesora Catedrática |
| 11 | José Albadalejo Pérez | Universidad de Castilla-La Mancha | Profesor Catedrático |

---

## Miembros suplentes

### Bloque A (UPV/EHU)

| Nº | Nombre | Categoría | Sexo |
|----|---------|-----------|------|
| 5 | María Teresa Insausti Peña | Profesora Catedrática | Mujer |
| 3 | Jon Mattin Matxain Beraza | Profesor Pleno | Hombre |
| 8 | María Coro De la Caba Ciriza | Profesora Catedrática | Mujer |
| 1 | Jose Luis Vilas Vilela | Profesor Catedrático | Hombre |

### Bloque B (externos)

| Nº | Nombre | Universidad | Categoría |
|----|---------|-------------|-----------|
| 14 | Clara Gómez Clari | Universitat de València | Profesora Catedrática |
| 10 | Franciso Monroy Muñoz | Universidad Complutense de Madrid | Profesor Catedrático |
| 17 | Elena Jiménez Martínez | Universidad de Castilla-La Mancha | Profesora Catedrática |

---

# Reglas aplicadas

Durante este caso intervienen, al menos, las siguientes reglas:

- REG-001 - Número de miembros (17 personas, 8+9).
- REG-002 - Procedencia institucional (Bloque A por posición 1–8, no por afiliación).
- REG-003 - Categorías académicas (Catedrático/a o Pleno, matching por raíz léxica).
- REG-004 - Área de conocimiento (aviso por áreas afines, no bloqueante).
- REG-005 - Equilibrio de género (mínimo 4 mujeres en cada bloque).
- REG-006 - Requisitos lingüísticos (100% del Bloque A con capacidad bilingüe, art. 12.2).
- REG-007 - Situación administrativa (todos "Activo").

---

# Validaciones esperadas

La aplicación deberá verificar que:

- La numeración es 1–17 sin huecos ni duplicados.
- El Bloque A (nº 1–8) y el Bloque B (nº 9–17) se determinan por posición, no por
  afiliación institucional.
- Las 8 personas del Bloque A tienen capacidad bilingüe/trilingüe (art. 12.2, 100%
  exigido para Pleno/Agregado bilingüe).
- Todas las personas cumplen la categoría exigida (Catedrático/a o Pleno) pese a llegar
  con variantes de género en el texto de la categoría.
- Se respeta el mínimo de 4 mujeres en cada bloque.
- La Comisión generada por el motor de sorteo coincide exactamente con la composición
  oficial descrita en este documento.

---

# Documentación asociada

- `propuesta_pleno_bilingue.csv` — propuesta oficial de miembros.
- `comision_pleno_bilingue.csv` — comisión definitiva de referencia.
- Orden de sorteo: ver sección "Resultado del sorteo" arriba.

---

# Fuente normativa

- ACUERDO de 26 de septiembre de 2024 (BOPV 10/10/2024), arts. 11, 12 y 13.
- `resumen_composicion_pleno_bilingue.md`, `resumen_propuessta_pleno_bilingue.md`.