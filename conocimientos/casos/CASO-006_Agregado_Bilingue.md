# CASO-006 - Comisión de Selección para Profesorado Agregado (bilingüe)

## Estado

**Analizado, no decisivo.**

Este caso ha sido verificado con el motor extraído en Node.js (Bloque A y Bloque B), y su composición coincide con la de la plantilla oficial. No obstante, **no permite confirmar ni descartar** la necesidad del algoritmo del art. 13.3.b para Agregado, porque la distribución de categorías del Bloque B (8 Catedráticos de 9) hace que el algoritmo simple (art. 13.3.a) y el algoritmo con restricción de categoría (art. 13.3.b) coincidan en el resultado.

Debe conservarse como caso de referencia de "régimen bilingüe de Bloque A + Bloque B sin tensión de categoría", pero **se necesita un caso adicional con más Titulares/Agregados en el Bloque B** para congelar la implementación del art. 13.3.b en Agregado (de forma análoga a los casos pendientes de Titular: TUC8/1-D00039-25 y TUC8/1-D00144-9).

---

# Objetivo

Describir el procedimiento completo seguido para construir una Comisión de Selección de una plaza de Profesorado Agregado (bilingüe) a partir de:

- la propuesta inicial de miembros;
- el resultado del sorteo;
- la aplicación de las reglas de negocio del Acuerdo 26/09/2024.

---

# Contexto

## Tipo de plaza

Profesorado Agregado

## Código de plaza

AGC8L1-D00331-20

## Área de conocimiento

175 / 140 / 165 / 135 / 130 (varias, Derecho — ver detalle de la propuesta)

## Perfil lingüístico

Bilingüe

---

# Datos de entrada

## Propuesta inicial

17 personas numeradas (Bloque A: nº 1-8, Bloque B: nº 9-17):

### Bloque A (nº 1-8, UPV/EHU, todos bilingües)

| Nº | Nombre | Categoría | Sexo |
|----|--------|-----------|------|
| 1 | Jose Francisco Etxeberria Guridi | Catedrático | Hombre |
| 2 | Miren Edurne Terradillos Ormaechea | Catedrática | Mujer |
| 3 | Aitor Zurimendi Isla | Catedrático | Hombre |
| 4 | Juan Ignacio Ugartemendia Eceizabarrena | Catedrático | Hombre |
| 5 | Maria Elena Leiñena Mendizabal | Profesora Titular | Mujer |
| 6 | Rosa Ochoa-Errarte Goicoechea | Agregada | Mujer |
| 7 | Miren Igone Altzelai Uliondo | Agregada | Mujer |
| 8 | Mikel Mari Karrera Egialde | Profesor Titular | Hombre |

### Bloque B (nº 9-17, externos)

| Nº | Nombre | Universidad | Categoría | Sexo |
|----|--------|-------------|-----------|------|
| 9 | Ana Diaz Martinez | U. Santiago de Compostela | Catedrática | Mujer |
| 10 | Angel Rebolledo Varela | U. Santiago de Compostela | Catedrático | Hombre |
| 11 | Marta Carballo Fidalgo | U. Santiago de Compostela | Profesora Titular | Mujer |
| 12 | Javier Barcelo Domenech | U. Alicante | Catedrático | Hombre |
| 13 | Jose Ramon De Verda Beamonte | U. València | Catedrático | Hombre |
| 14 | Cristina De Amunategui Rodriguez | U. Complutense de Madrid | Catedrática | Mujer |
| 15 | Antoni Vaquer Aloy | U. Lleida | Catedrático | Hombre |
| 16 | Mª Ángeles Egusquiza Balmaseda | U. Pública de Navarra | Catedrática | Mujer |
| 17 | Eduardo Vazquez de Castro | U. Cantabria | Catedrático | Hombre |

## Resultado del sorteo

Orden obtenido:

2 → 4 → 3 → 1 → 5 → 8 → 6 → 7 → 12 → 9 → 17 → 16 → 13 → 10 → 11 → 15 → 14

---

# Verificación de la propuesta (Paso 2)

- Bloques 8 (A) + 9 (B): correcto (art. 12.1).
- Bloque A: 100% bilingüe (8/8) — cumple art. 12.2 (Agregado/Pleno bilingüe exige el 100%, no el mínimo de 5/8 de Catedrático).
- Mujeres en Bloque A: 4 (mínimo exigido) ✓.
- Mujeres en Bloque B: 4 (mínimo exigido) ✓.
- Umbral 40% CP (Catedrático/Pleno) por bloque, art. 12.4.d:
  - Bloque A: 4 de 8 = 50% ✓
  - Bloque B: 8 de 9 = 89% ✓

---

# Procedimiento aplicado y resultado

## Bloque A (art. 13.2.1 — régimen general, aplica por ser plaza bilingüe; el art. 13.2.2 solo aplica a Pleno/Agregado *no* bilingüe)

**Titulares:** nº 2 (Miren Edurne Terradillos Ormaechea), nº 4 (Juan Ignacio Ugartemendia Eceizabarrena)

**Suplentes:** nº 3 (Aitor Zurimendi Isla), nº 5 (Maria Elena Leiñena Mendizabal), nº 1 (Jose Francisco Etxeberria Guridi), nº 6 (Rosa Ochoa-Errarte Goicoechea)

**Fuera de comisión:** nº 8, nº 7

## Bloque B (art. 13.3.b — mecanismo de categoría, generalizado desde Titular a Agregado)

**Titulares:** nº 12 (Catedrático), nº 9 (Catedrática), nº 17 (Catedrático)

**Suplentes:** nº 16 (Catedrática), nº 13 (Catedrático), nº 11 (Profesora Titular)

CP totales en el conjunto final del Bloque B: 5 de 6 (mínimo exigido: 4) ✓

> **Nota de verificación cruzada:** el algoritmo simple del art. 13.3.a (alternancia de género sin restricción de categoría, el que aplica hoy el motor a todas las subcategorías del Acuerdo 2024) produce, para este caso concreto, **exactamente el mismo resultado**. La coincidencia se debe a la escasa presencia de Titulares en este Bloque B (solo 1 de 9), no a que ambos artículos sean equivalentes. Este caso, por tanto, **no permite validar por sí solo** la implementación del art. 13.3.b para Agregado.

---

# Reglas aplicadas

- REG-001 - Número de miembros.
- REG-002 - Procedencia institucional.
- REG-003 - Categorías académicas.
- REG-004 - Área de conocimiento.
- REG-005 - Equilibrio de género.
- REG-006 - Requisitos lingüísticos.
- REG-007 - Situación administrativa.

---

# Pendiente

- Confirmar con un caso real de Agregado con más Titulares/Agregados en el Bloque B que el art. 13.3.b (mecanismo de categoría) diverge del art. 13.3.a (mecanismo simple) y que el motor implementado resuelve correctamente ese caso.
- Congelar este caso (CASO-006) solo tras verificación manual artículo por artículo por parte de Fernando, siguiendo la disciplina de casos congelados del proyecto.

---

# Fuente normativa

- Reglamento de concursos de acceso a Cuerpos Docentes Universitarios y selección y contratación de Profesorado Pleno y Agregado — Acuerdo 26 de septiembre de 2024 (BOPV 10/10/2024), arts. 11, 12, 13.