# CASO-002 - Comisión de Selección para Catedrático/a de Universidad (bilingüe)

## Estado

**Caso sintético de referencia — verificado, no oficial.**

A diferencia de CASO-001 (que corresponde a una resolución oficial real), este caso se ha
construido durante una sesión de depuración para servir de prueba de regresión del motor de
sorteo y del motor de validación del Reglamento de 26 de septiembre de 2024 (Acuerdo 2024),
subcategoría Catedrático/a, perfil bilingüe.

El resultado se ha verificado dos veces de forma independiente:

1. Aplicando manualmente el art. 13.2.1 y el art. 13.3.a paso a paso sobre la lista reordenada.
2. Ejecutando el motor de sorteo real extraído de `validador.html` (funciones
   `bloqueA_Acuerdo2024`, `bloqueB_alternando`, `calcularComposicion`) tras corregir los bugs 1-4
   detectados en esta misma sesión (categoría por igualdad exacta, rama 13.2.1/13.2.2 no
   parametrizada por subcategoría, duplicación entre Bloque A y B, y variantes de categoría
   —siglas, género, euskera— no reconocidas).

Ambas vías coinciden exactamente. Debe usarse como caso de referencia para detectar regresiones
en el motor de Acuerdo 2024, especialmente en la rama de Catedrático.

---

# Objetivo

Comprobar el procedimiento completo de composición de una Comisión de Selección de una plaza de
**Catedrático/a de Universidad** (Acuerdo 2024) a partir de:

- la propuesta inicial de 17 personas (Bloque A: nº 1-8 de la UPV/EHU; Bloque B: nº 9-17 externas);
- el resultado del sorteo;
- la aplicación de las reglas de negocio (art. 12 y art. 13 del Acuerdo 2024).

---

# Contexto

## Tipo de plaza

Catedrático/a de Universidad — Acuerdo de 26 de septiembre de 2024 (BOPV 10/10/2024).

## Área de conocimiento

385 - Física Aplicada

## Perfil lingüístico

Bilingüe

---

# Datos de entrada

## Propuesta inicial

La propuesta inicial está formada por **17 personas**, numeradas 1 a 8 en el Bloque A (UPV/EHU)
y 9 a 17 en el Bloque B (externas):

| Nº | Nombre y apellidos | Universidad | Categoría | Situación | Perfil ling. | Sexo |
|----|---|---|---|---|---|---|
| 1 | María Asunción Illarramendi Leturia | UPV/EHU | Catedrático de Universidad | ACTIVO | BILINGÜE | MUJER |
| 2 | María Arantzazu Mendioroz Astigarraga | UPV/EHU | Catedrático de Universidad | ACTIVO | NO BILINGÜE | MUJER |
| 3 | Agustín Salazar Hernández | UPV/EHU | Catedrático de Universidad | ACTIVO | NO BILINGÜE | HOMBRE |
| 4 | Alberto Oleaga Páramo | UPV/EHU | Catedrático de Universidad | ACTIVO | NO BILINGÜE | HOMBRE |
| 5 | Rolindes Balda de la Cruz | UPV/EHU | Catedrático de Universidad | ACTIVO | NO BILINGÜE | MUJER |
| 6 | María Luisa Fernández Gubieda Ruiz | UPV/EHU | Catedrático de Universidad | ACTIVO | NO BILINGÜE | MUJER |
| 7 | Nerea Zabala Unzalu | UPV/EHU | Catedrático de Universidad | ACTIVO | BILINGÜE | MUJER |
| 8 | Alfredo García Arribas | UPV/EHU | Catedrático de Universidad | ACTIVO | NO BILINGÜE | HOMBRE |
| 9 | Consuelo Cid Tortuero | Universidad de Alcalá de Henares | Catedrático de Universidad | ACTIVO | — | MUJER |
| 10 | Adriano Campo Bagatín | Universidad de Alicante | Catedrático de Universidad | ACTIVO | — | HOMBRE |
| 11 | Miguel Ángel Satorre Aznar | Universidad Politécnica de Alicante | Catedrático de Universidad | ACTIVO | — | HOMBRE |
| 12 | Ricardo López Antón | Universidad de Castilla-La Mancha (UCLM) | Catedrático de Universidad | ACTIVO | — | HOMBRE |
| 13 | Laura Palacio Martínez | Universidad de Valladolid (UVA) | Catedrático de Universidad | ACTIVO | — | MUJER |
| 14 | Ana María Laguna Luna | Universidad de Córdoba (UCO) | Catedrático de Universidad | ACTIVO | — | MUJER |
| 15 | Isidro Alberto Pérez Bartolomé | Universidad de Valladolid (UVA) | Catedrático de Universidad | ACTIVO | — | HOMBRE |
| 16 | Verónica Salgueiriño Maceiras | Universidad de Vigo (UVI) | Catedrático de Universidad | ACTIVO | — | MUJER |
| 17 | Eduardo García Ortega | Universidad de León (ULE) | Catedrático de Universidad | ACTIVO | — | HOMBRE |

Todas las personas pertenecen al área 385 - Física Aplicada.

## Resultado del sorteo

Orden obtenido (sorteo único de 17 bolas):

9 → 11 → 16 → 10 → 14 → 17 → 6 → 5 → 12 → 8 → 4 → 7 → 15 → 3 → 1 → 13 → 2

---

# Procedimiento aplicado

1. Reordenar las 17 personas según el orden del sorteo.
2. **Bloque A** (art. 13.2.1, régimen general — aplica siempre a Catedrático, sea o no bilingüe
   la plaza): sobre las 8 personas UPV/EHU dentro de la lista reordenada, elegir la pareja
   titular (primera persona bilingüe de la UPV/EHU + primera de género distinto) y repetir el
   proceso dos veces más para los 4 suplentes.
3. **Bloque B** (art. 13.3.a): sobre las 9 personas externas, elegir la primera de la lista y
   alternar género hasta completar 6; las 3 primeras son titulares, las 3 últimas suplentes.
   Se excluye explícitamente a cualquier persona ya asignada en el Bloque A (no aplica en este
   caso concreto, porque el Bloque A de Catedrático solo toma personas UPV/EHU, pero es la
   comprobación de la corrección del bug 3 de esta sesión).

---

# Resultado esperado

## Miembros titulares

### UPV/EHU (Bloque A)

| Nº | Nombre | Perfil ling. | Sexo |
|----|---|---|---|
| 7 | Nerea Zabala Unzalu | BILINGÜE | MUJER |
| 8 | Alfredo García Arribas | NO BILINGÜE | HOMBRE |

### Universidades externas (Bloque B)

| Nº | Nombre | Universidad |
|----|---|---|
| 9 | Consuelo Cid Tortuero | Universidad de Alcalá de Henares |
| 11 | Miguel Ángel Satorre Aznar | Universidad Politécnica de Alicante |
| 16 | Verónica Salgueiriño Maceiras | Universidad de Vigo (UVI) |

## Miembros suplentes

### UPV/EHU (Bloque A)

| Nº | Nombre | Perfil ling. | Sexo |
|----|---|---|---|
| 1 | María Asunción Illarramendi Leturia | BILINGÜE | MUJER |
| 4 | Alberto Oleaga Páramo | NO BILINGÜE | HOMBRE |
| 6 | María Luisa Fernández Gubieda Ruiz | NO BILINGÜE | MUJER |
| 3 | Agustín Salazar Hernández | NO BILINGÜE | HOMBRE |

### Universidades externas (Bloque B)

| Nº | Nombre | Universidad |
|----|---|---|
| 10 | Adriano Campo Bagatín | Universidad de Alicante |
| 14 | Ana María Laguna Luna | Universidad de Córdoba (UCO) |
| 17 | Eduardo García Ortega | Universidad de León (ULE) |

**Total: 5 titulares + 7 suplentes = 12 personas, todas distintas** (comprobación explícita del
bug 3: ninguna persona debe repetirse entre Bloque A y Bloque B).

---

# Validación esperada (además de la composición)

Este caso, tal como está construido, **no debería superar la validación del Paso 2 sin
excepción CPU**, y eso es intencional: sirve también para comprobar que el motor de validación
detecta correctamente la anomalía:

- **Anomalía esperada:** "Capacidad bilingüe/trilingüe insuficiente" — el Bloque A tiene solo 2
  de 8 personas bilingües (nº 1 y 7), y el mínimo exigido a Catedrático en plaza bilingüe es de
  **5 de 8** (art. 12.1.A — distinto del 100 % que exige el mismo artículo para Pleno/Agregado,
  art. 12.2).
- El resto de comprobaciones (numeración 1-17, tamaño 8+9, situación administrativa "Activo",
  área de conocimiento única, categoría "Catedrático de Universidad" en las 17 personas, paridad
  de género ≥4 en cada bloque) deben quedar conformes.

Si se marca la anomalía de bilingüismo como excepción CPU, el sorteo debe poder ejecutarse y
producir exactamente la composición descrita arriba.

---

# Reglas aplicadas

- Art. 12.1.A — Bloque A: 8 personas UPV/EHU, mínimo 4 mujeres.
- Art. 12.1.A — Bilingüismo en Bloque A para Catedrático: mínimo 5 de 8 (no 100 %, a diferencia
  de Pleno/Agregado).
- Art. 12.1.B — Bloque B: 9 personas externas, mínimo 4 mujeres.
- Art. 12.4.a — Categoría: Catedrático/a de Universidad en ambos bloques.
- Art. 13.2.1 — Sorteo y emparejamiento del Bloque A (régimen general, aplicable a Catedrático
  sea o no bilingüe la plaza).
- Art. 13.3.a — Sorteo y alternancia de género del Bloque B.
- Art. 11.9 — Situación administrativa de servicio activo.

---

# Documentación asociada

- Excel de propuesta aportado por el usuario en esta sesión (17 filas, columnas completas
  incluyendo perfil lingüístico y sexo).
- Orden de sorteo aportado por el usuario.
- Traza y composición verificadas manualmente y por simulación del motor real de
  `validador.html` en esta misma sesión.

---

# Fuente normativa

- Reglamento de concursos de acceso a Cuerpos Docentes Universitarios y selección y
  contratación de Profesorado Pleno y Agregado — Acuerdo de 26 de septiembre de 2024
  (BOPV 10/10/2024), arts. 11, 12 y 13.
