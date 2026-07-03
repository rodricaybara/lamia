# Entidad: Candidato

## Objetivo

Representar la participación de una persona en un procedimiento de selección como aspirante a una plaza convocada.

La entidad Candidato describe la información específica asociada a una candidatura y complementa a la entidad Persona.

---

# Descripción

Un Candidato es una Persona que participa en una convocatoria para optar a una plaza.

La condición de candidato existe únicamente dentro del contexto de una convocatoria determinada.

Una misma Persona podrá ser candidata en distintas convocatorias a lo largo del tiempo.

---

# Finalidad

Representar la candidatura presentada por una persona y toda la información necesaria para su evaluación durante el procedimiento de selección.

---

# Atributos principales

| Atributo | Descripción |
|----------|-------------|
| Persona | Persona que presenta la candidatura. |
| Convocatoria | Convocatoria en la que participa. |
| Plaza | Plaza a la que opta. |
| Fecha de solicitud | Fecha de presentación de la candidatura. |
| Estado de la candidatura | Situación de la candidatura dentro del procedimiento. |
| Documentación presentada | Documentación aportada por la persona candidata. |
| Méritos | Méritos alegados para su valoración. |
| Resultado de la evaluación | Resultado obtenido durante el procedimiento. |

---

# Relaciones

La entidad Candidato se relaciona con:

- Persona
- Convocatoria
- Plaza
- Comisión de Selección

---

# Procesos relacionados

El candidato interviene en los siguientes procesos:

- Presentación de solicitudes.
- Admisión de candidaturas.
- Evaluación de méritos.
- Realización de pruebas.
- Resolución del procedimiento.

---

# Reglas relacionadas

Las reglas aplicables dependerán de la convocatoria y de la normativa correspondiente.

Entre otras:

- requisitos de participación;
- documentación obligatoria;
- valoración de méritos;
- realización de pruebas;
- causas de exclusión.

---

# Casos relacionados

Pendiente.

---

# Fuente normativa

- Reglamento de Selección y Contratación del Personal Investigador.
- Convocatoria correspondiente.