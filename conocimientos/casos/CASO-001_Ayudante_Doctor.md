# CASO-001 - Comisión de Selección para Profesor Ayudante Doctor

## Estado

**Validado**

Este caso corresponde a una propuesta oficial cuya composición final fue obtenida conforme a la normativa vigente.

Debe utilizarse como caso de referencia durante el desarrollo y validación de Lamia.

---

# Objetivo

Describir el procedimiento completo seguido para construir una Comisión de Selección de una plaza de Profesor Ayudante Doctor a partir de:

- la propuesta inicial de miembros;
- el resultado del sorteo;
- la aplicación de las reglas de negocio.

Este caso constituye una referencia funcional para comprobar el comportamiento del sistema.

---

# Contexto

## Tipo de plaza

Profesor Ayudante Doctor

## Área de conocimiento

260 - Escultura

## Perfil lingüístico

Bilingüe

---

# Datos de entrada

## Propuesta inicial

La propuesta inicial está formada por **17 personas**.

Cada propuesta incluye:

- Número de orden.
- Identificación.
- Nombre y apellidos.
- Universidad.
- Categoría académica.
- Situación administrativa.
- Área de conocimiento.
- Perfil lingüístico.
- Sexo.

La relación completa se conserva como documentación asociada al caso.

---

## Resultado del sorteo

Orden obtenido:

14 → 12 → 5 → 8 → 17 → 3 → 13 → 11 → 7 → 16 → 9 → 1 → 4 → 6 → 10 → 15 → 2

Este orden determina la prioridad de selección de los miembros de la Comisión.

---

# Procedimiento aplicado

El procedimiento seguido es el siguiente:

1. Partir de la propuesta inicial.
2. Aplicar el orden obtenido en el sorteo.
3. Seleccionar los miembros respetando dicho orden.
4. Verificar el cumplimiento de todas las reglas de negocio.
5. Obtener la composición definitiva de la Comisión.

---

# Resultado esperado

## Miembros titulares

### UPV/EHU

| Nº | Nombre | Categoría |
|----|---------|-----------|
| 5 | Amaia Lekerikabeaskoa Gaztañaga | Agregado |
| 1 | Augusto Zubiaga Garate | Agregado |

### Universidades externas

| Nº | Nombre | Universidad | Categoría |
|----|---------|-------------|-----------|
| 14 | Tatiana Sentamans Gómez | Universidad Miguel Hernández | Catedrática |
| 12 | Juan Carlos Román Redondo | Universidad de Vigo | Titular |
| 17 | María José Zanon Cuenca | Universidad Miguel Hernández | Catedrática |

---

## Miembros suplentes

### UPV/EHU

| Nº | Nombre | Categoría |
|----|---------|-----------|
| 8 | Oihana Garro Larrañaga | Agregado |
| 6 | Jon Macareno Ramos | Agregado |
| 3 | Iratxe Larrea Príncipe | Agregado |
| 2 | Isusko Vivas Ziarrusta | Catedrático |

### Universidades externas

| Nº | Nombre | Universidad | Categoría |
|----|---------|-------------|-----------|
| 11 | Miguel Molina Alarcón | Universitat Politècnica de València | Catedrático |
| 13 | María Josefa Zárraga Llorens | Universitat Politècnica de València | Titular |
| 16 | Juan Francisco Gómez de Albacete | Universidad Miguel Hernández | Titular |

---

# Reglas aplicadas

Durante este caso intervienen, al menos, las siguientes reglas:

- REG-001 - Número de miembros.
- REG-002 - Procedencia institucional.
- REG-003 - Categorías académicas.
- REG-004 - Área de conocimiento.
- REG-005 - Equilibrio de género.
- REG-006 - Requisitos lingüísticos.
- REG-007 - Situación administrativa.

---

# Validaciones esperadas

La aplicación deberá verificar que:

- La Comisión se construye respetando el orden del sorteo.
- Todos los integrantes cumplen los requisitos de situación administrativa.
- Se respeta la composición UPV/EHU / Universidades externas.
- Las categorías académicas son válidas.
- El área de conocimiento es correcta.
- Se cumplen los requisitos lingüísticos.
- Se respeta el equilibrio de género cuando resulte exigible.
- La Comisión generada coincide exactamente con la composición oficial.

---

# Resultado esperado para Lamia

Si la aplicación recibe la propuesta inicial y el orden del sorteo indicados en este caso, deberá generar exactamente la Comisión descrita en este documento.

Cualquier diferencia deberá considerarse un error de implementación o una discrepancia con la normativa.

---

# Documentación asociada

- Propuesta oficial de miembros.
- Resultado oficial del sorteo.
- Comisión definitiva.

---

# Fuente normativa

- Reglamento de Selección y Contratación del Personal Investigador.
- Composición de las Comisiones de Selección.
- Expediente oficial de la plaza.