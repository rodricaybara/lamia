# CASO-005 - Comisión de Selección para Profesorado Titular (bilingüe)

## Estado

**Verificado por análisis normativo — NO validado contra la plantilla oficial**

A diferencia de CASO-001 y CASO-004, este caso **no** puede marcarse como "Validado" en el sentido de "coincide con la plantilla oficial", porque la plantilla oficial de esta plaza aplica un algoritmo incorrecto en el Bloque B (ver más abajo). El resultado esperado que se documenta aquí ha sido obtenido y verificado artículo por artículo aplicando el motor de `validador.html` (art. 13.2.1 en Bloque A, art. 13.3.b en Bloque B), y es la composición correcta conforme al Acuerdo de 26 de septiembre de 2024.

Debe utilizarse como caso de referencia para regresión de la subcategoría Titular en perfil bilingüe. No debe congelarse ni compararse frente a la plantilla oficial de esta plaza, que se sabe defectuosa.

---

# Objetivo

Describir el procedimiento completo seguido para construir una Comisión de Selección de una plaza de Profesorado Titular, perfil lingüístico bilingüe, a partir de:

- la propuesta inicial de miembros;
- el resultado del sorteo;
- la aplicación de las reglas de negocio (art. 12 y art. 13 del Acuerdo 26/09/2024).

Este caso constituye una referencia funcional para comprobar el comportamiento del sistema en la ruta Titular + bilingüe, y en particular la interacción entre el art. 13.2.1 (Bloque A, régimen general) y el art. 13.3.b (Bloque B, forzado de categoría Catedrático/Pleno).

---

# Contexto

## Tipo de plaza

Titular (Acuerdo 26/09/2024)

## Código de plaza

TUC8/1-D00144-9

## Área de conocimiento

90 - Cirugía (Bloque A incluye también 443-Histología, 315-Farmacología, 50-Biología Celular, 653-Otorrinolaringología, 610-Medicina, 645-Ginecología, áreas afines dentro de la misma especialidad médica)

## Perfil lingüístico

Bilingüe

## Particularidad del caso

Las 8 personas del Bloque A son de la UPV/EHU y tienen capacidad bilingüe/trilingüe (8 de 8), por lo que no se activa ninguna anomalía en el Paso 2 relativa al art. 12.1.A (mínimo 5 de 8 para Catedrático/Titular en plaza bilingüe).

---

# Datos de entrada

## Propuesta inicial

La propuesta inicial está formada por **17 personas**.

### Bloque A (nº 1-8, todas UPV/EHU, todas bilingües)

| Nº | Nombre | Categoría | Sexo |
|----|--------|-----------|------|
| 1 | Ana Isabel Alonso Varona | Catedrática | Mujer |
| 2 | Maria Isabel Ulibarri Marcos | Titular | Mujer |
| 3 | María Dolores Boyano López | Catedrática | Mujer |
| 4 | Irene Diez Itza | Titular | Mujer |
| 5 | Fernando José Unda Rodríguez | Catedrático | Hombre |
| 6 | Francisco Santaolalla Montoya | Catedrático | Hombre |
| 7 | Guillermo Ruiz Irastorza | Titular | Hombre |
| 8 | Ignacio García-Alonso Montoya | Titular | Hombre |

### Bloque B (nº 9-17, todas externas, no bilingües)

| Nº | Nombre | Universidad | Categoría | Sexo |
|----|--------|-------------|-----------|------|
| 9 | Antonio Jose Torres García | Universidad Complutense de Madrid (UCM) | Catedrático | Hombre |
| 10 | Julio Ángel Mayol Martínez | Universidad Complutense de Madrid (UCM) | Catedrático | Hombre |
| 11 | Ignacio María González Pinto Arrillaga | Universidad de Oviedo (UOV) | Catedrático | Hombre |
| 12 | Felicito Enrique García-Álvarez García | Universidad de Zaragoza (UZA) | Titular | Hombre |
| 13 | Rosa María Martí Laborda | Universidad de Lleida (UDL) | Catedrática | Mujer |
| 14 | Ana María Gómez Martínez | Universidad Complutense de Madrid (UCM) | Titular | Mujer |
| 15 | María Yaiza Lopiz Morales | Universidad Complutense de Madrid (UCM) | Titular | Mujer |
| 16 | María Begoña Quintana Villamandos | Universidad Complutense de Madrid (UCM) | Titular | Mujer |
| 17 | Eloy Espín Basany | Universidad Autónoma de Barcelona (UAB) | Titular | Hombre |

---

## Resultado del sorteo

Orden obtenido (secuencia única de 17 bolas):

1 → 8 → 10 → 6 → 5 → 14 → 12 → 7 → 13 → 3 → 9 → 11 → 17 → 15 → 4 → 2 → 16

Este orden se filtra por número de orden para obtener la lista reordenada de cada bloque, sin alterar el orden relativo:

- **Bloque A reordenado** (nº 1-8, en orden de aparición): 1, 8, 6, 5, 7, 3, 4, 2
- **Bloque B reordenado** (nº 9-17, en orden de aparición): 10, 14, 12, 13, 9, 11, 17, 15, 16

---

# Procedimiento aplicado

1. Partir de la propuesta inicial (17 personas, Bloque A = nº 1-8, Bloque B = nº 9-17).
2. Aplicar el orden del sorteo, filtrado por posición para obtener la lista reordenada de cada bloque de forma independiente.
3. **Bloque A** (art. 13.2.1, régimen general — aplica siempre a Catedrático y Titular, con o sin bilingüismo):
   - Pareja titular: primera persona UPV/EHU bilingüe de la lista restante + primera persona de género distinto.
   - Se repite dos veces más para obtener 4 suplentes.
4. **Bloque B** (art. 13.3.b, específico de Titular y Agregado):
   - 1ª persona: primera de categoría Catedrático/Pleno.
   - 2ª persona: siguiente de género distinto.
   - 3ª/4ª: si no hay más de una persona Catedrático/Pleno en el tribunal titular provisional, se refuerza con otra persona Catedrático/Pleno y a continuación una de género distinto.
   - 5ª persona: se fuerza una persona Catedrático/Pleno si el conjunto no alcanza aún el mínimo de 3.
   - 6ª persona: se fuerza una persona Catedrático/Pleno si el conjunto no alcanza aún el mínimo de 4.
5. Verificar el cumplimiento de todas las reglas de negocio (Paso 2 de `validador.html`, 0 anomalías en este caso).
6. Obtener la composición definitiva.

---

# Resultado esperado

## Miembros titulares

### UPV/EHU

| Nº | Nombre | Categoría |
|----|--------|-----------|
| 1 | Ana Isabel Alonso Varona | Catedrática |
| 8 | Ignacio García-Alonso Montoya | Titular |

### Universidades externas

| Nº | Nombre | Universidad | Categoría |
|----|--------|-------------|-----------|
| 10 | Julio Ángel Mayol Martínez | Universidad Complutense de Madrid (UCM) | Catedrático |
| 14 | Ana María Gómez Martínez | Universidad Complutense de Madrid (UCM) | Titular |
| 13 | Rosa María Martí Laborda | Universidad de Lleida (UDL) | Catedrática |

---

## Miembros suplentes

### UPV/EHU

| Nº | Nombre | Categoría |
|----|--------|-----------|
| 6 | Francisco Santaolalla Montoya | Catedrático |
| 3 | María Dolores Boyano López | Catedrática |
| 5 | Fernando José Unda Rodríguez | Catedrático |
| 4 | Irene Diez Itza | Titular |

### Universidades externas

| Nº | Nombre | Universidad | Categoría |
|----|--------|-------------|-----------|
| 12 | Felicito Enrique García-Álvarez García | Universidad de Zaragoza (UZA) | Titular |
| 9 | Antonio Jose Torres García | Universidad Complutense de Madrid (UCM) | Catedrático |
| 11 | Ignacio María González Pinto Arrillaga | Universidad de Oviedo (UOV) | Catedrático |

---

## Verificación del art. 13.3.b sobre el conjunto final de Bloque B

Personas de Bloque B en el resultado final (titulares + suplentes): 10, 14, 13, 12, 9, 11.

Catedrático/Pleno entre ellas: 10, 13, 9, 11 → **4 de 6**, cumpliendo el mínimo exigido tras la 6ª elección (art. 13.3.b).

---

# Discrepancia conocida con la plantilla oficial de esta plaza

La plantilla oficial de esta plaza (TUC8/1-D00144-9) aplica en Bloque B el algoritmo simple del art. 13.3.a (alternancia de género pura, sin restricción de categoría), en vez del art. 13.3.b que corresponde a Titular. Con ese algoritmo incorrecto, la plantilla obtiene:

- Titulares Bloque B: 10, 14, **12**
- Suplentes Bloque B: **13**, 9, **15**

Catedrático/Pleno en ese conjunto: 10, 13, 9 → solo **3 de 6**, incumpliendo el mínimo de 4 exigido por el art. 13.3.b.

Esta discrepancia se ha observado de forma consistente en seis casos reales de Titular analizados hasta la fecha (TUC8/1-D00039-25, TUC8/1-D00144-9 [dos veces], TUC8/1-D00310-29, TUC8/1-D00237-25), siempre con el mismo patrón: la plantilla aplica 13.3.a en vez de 13.3.b en Bloque B. Bloque A, en cambio, ha coincidido siempre entre plantilla y validador.

**Por este motivo, la plantilla oficial de este caso no debe usarse como fuente de verdad**; el resultado documentado en la sección "Resultado esperado" de este documento —obtenido y verificado con `validador.html`— es el que debe usarse como referencia de regresión.

---

# Reglas aplicadas

Durante este caso intervienen, al menos, las siguientes reglas:

- REG-001 - Número de miembros.
- REG-002 - Procedencia institucional.
- REG-003 - Categorías académicas (incluye el mínimo del 40% de Catedrático/Pleno, art. 12.4.c).
- REG-004 - Área de conocimiento.
- REG-005 - Equilibrio de género.
- REG-006 - Requisitos lingüísticos (art. 12.1.A: mínimo 5 de 8 en Bloque A para Titular bilingüe).
- REG-007 - Situación administrativa.

---

# Validaciones esperadas

La aplicación deberá verificar que:

- La Comisión se construye respetando el orden del sorteo, filtrado por bloque según posición (nº 1-8 / nº 9-17), no por afiliación.
- Bloque A se resuelve con el régimen general del art. 13.2.1 (Titular usa siempre esta ruta, igual que Catedrático).
- Bloque B se resuelve con el art. 13.3.b, garantizando un mínimo de 3 Catedrático/Pleno tras la 5ª elección y 4 tras la 6ª, con prioridad de categoría sobre alternancia de género en caso de conflicto.
- Todos los integrantes cumplen los requisitos de situación administrativa.
- Se respeta la composición Bloque A (nº 1-8) / Bloque B (nº 9-17).
- Las categorías académicas son válidas para Titular (Catedrático/a o Titular de Universidad).
- Se cumple el mínimo del 40% de Catedrático/Pleno en cada bloque (art. 12.4.c) sobre la propuesta original.
- Se cumple el requisito de bilingüismo del Bloque A (mínimo 5 de 8, art. 12.1.A; en este caso 8 de 8).
- Se respeta el equilibrio de género (mínimo 4 mujeres en cada bloque de la propuesta).
- La Comisión generada coincide exactamente con la composición documentada en este caso, y NO con la de la plantilla oficial de esta plaza en lo relativo a Bloque B.

---

# Resultado esperado para el validador

Si la aplicación recibe la propuesta inicial y el orden del sorteo indicados en este caso, deberá generar exactamente la Comisión descrita en la sección "Resultado esperado".

Cualquier diferencia deberá considerarse un error de implementación. La coincidencia con la plantilla oficial de esta plaza en Bloque B, en cambio, indicaría un error (regresión al algoritmo incorrecto 13.3.a).

---

# Documentación asociada

- Propuesta de la CPU (17 personas), plaza TUC8/1-D00144-9.
- Orden del sorteo (secuencia única de 17 bolas).
- Plantilla oficial de esta plaza (documentada aquí únicamente como ejemplo de discrepancia conocida, no como fuente de verdad).

---

# Fuente normativa

- Acuerdo de 26 de septiembre de 2024 (BOPV 10/10/2024), arts. 11, 12 y 13.
- Composición de las Comisiones de Selección.