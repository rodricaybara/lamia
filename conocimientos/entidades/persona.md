# Entidad: Persona

## Objetivo

Representar a una persona física que participa en un procedimiento de selección o contratación regulado por la normativa de la UPV/EHU.

La entidad Persona define la información común necesaria para identificar a cualquier participante en el procedimiento, independientemente del papel que desempeñe.

No describe las funciones ni responsabilidades asociadas a un rol concreto.

---

# Descripción

Una Persona es cualquier individuo que interviene en un procedimiento de selección.

Dependiendo del contexto, una misma persona podrá desempeñar distintos roles, como:

- Miembro de una Comisión de Selección.
- Persona candidata.
- Presidente o Presidenta de una Comisión.
- Secretario o Secretaria.
- Vocal.

La entidad Persona únicamente representa la identidad y los datos generales compartidos por todos ellos.

---

# Finalidad

Disponer de una representación única de las personas que participan en los distintos procedimientos administrativos.

Esta entidad evita duplicar información cuando una misma persona interviene en diferentes convocatorias o desempeña distintos roles.

---

# Atributos principales

| Atributo | Descripción |
|----------|-------------|
| Documento identificativo | DNI, NIE o documento equivalente. |
| Nombre | Nombre de la persona. |
| Primer apellido | Primer apellido. |
| Segundo apellido | Segundo apellido, cuando exista. |
| Sexo | Sexo utilizado para aplicar determinadas reglas de composición. |
| Universidad | Universidad o institución de pertenencia. |
| Categoría académica | Categoría profesional de la persona. |
| Situación administrativa | Situación administrativa en el momento del procedimiento. |
| Área de conocimiento | Área de conocimiento a la que pertenece. |
| Perfil lingüístico | Perfil lingüístico, cuando resulte aplicable. |

---

# Relaciones

La entidad Persona puede estar relacionada con:

- Comisión de Selección.
- Candidato.
- Convocatoria.
- Universidad.
- Área de conocimiento.
- Departamento.
- Instituto.

---

# Procesos relacionados

La entidad Persona interviene en distintos procesos, entre ellos:

- Propuesta de Comisión de Selección.
- Presentación de solicitudes.
- Evaluación de candidaturas.
- Resolución del procedimiento.

---

# Reglas relacionadas

Las reglas aplicables dependerán del rol que desempeñe la persona dentro del procedimiento.

Por ejemplo:

- requisitos para formar parte de una Comisión;
- requisitos para participar como candidato;
- requisitos relativos a la categoría académica;
- situación administrativa;
- perfil lingüístico.

---

# Casos relacionados

- CASO-001 - Profesor Ayudante Doctor.

---

# Fuente normativa

- Reglamento de Selección y Contratación del Personal Investigador.
- Composición de las Comisiones de Selección.
- Resto de normativa aplicable.