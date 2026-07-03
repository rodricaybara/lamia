# Reglas de negocio

## Objetivo

Este directorio contiene las reglas de negocio del proyecto.

Las reglas representan una interpretación funcional de la normativa oficial y constituyen la principal fuente de información para la implementación del software.

No contienen código ni detalles técnicos.

La normativa original continúa siendo la fuente de verdad y permanece en el directorio `docs`.

---

# Organización

Cada regla se almacena en un documento independiente.

Formato recomendado:

REG-XXX_Nombre_Regla.md

Ejemplo:

REG-001_Composicion_Comision.md

---

# Contenido de una regla

Cada regla debe incluir:

- Objetivo
- Descripción
- Fuente normativa
- Regla o reglas de negocio
- Excepciones (si existen)
- Relación con otras reglas
- Casos relacionados

---

# Buenas prácticas

- Una regla debe describir una única responsabilidad.
- No duplicar información entre reglas.
- Si una regla depende de otra, referenciarla.
- No incluir ejemplos extensos; deben almacenarse en `casos`.
- No incluir decisiones de implementación.

---

# Relación con el proyecto

Las reglas describen **qué debe cumplir la aplicación**, pero no **cómo implementarlo**.