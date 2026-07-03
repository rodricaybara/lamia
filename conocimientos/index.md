# Base de Conocimiento del Proyecto

## Objetivo

Esta carpeta contiene el conocimiento estructurado del proyecto.

Su finalidad es proporcionar a los agentes de IA una representación clara y organizada de la normativa, los procesos y las decisiones funcionales, evitando la lectura continua de la documentación oficial.

La documentación original permanece en la carpeta `docs` y constituye la fuente normativa de referencia.

---

# Organización

La base de conocimiento se divide en cinco áreas.

## Reglas

Describe las reglas de negocio que debe cumplir la aplicación.

Las reglas representan una interpretación estructurada de la normativa oficial.

No contienen código ni detalles de implementación.

---

## Procesos

Describe cómo se desarrolla cada procedimiento administrativo.

Los procesos indican el orden de las actuaciones y las reglas que intervienen en cada fase.

---

## Entidades

Define los conceptos utilizados en la normativa.

Por ejemplo:

- Comisión
- Plaza
- Candidato
- Departamento

Las entidades no contienen reglas.

---

## Casos

Contiene ejemplos reales correctamente resueltos.

Su finalidad es ayudar a interpretar correctamente la normativa y servir de referencia durante el desarrollo.

Siempre que exista un caso resuelto deberá utilizarse como apoyo antes de consultar la documentación oficial.

---

## Decisiones

Documenta las decisiones tomadas durante el desarrollo del proyecto.

No forman parte de la normativa.

Explican por qué se ha elegido una determinada solución cuando existen varias alternativas posibles.

---

# Orden recomendado de consulta

Los agentes de IA deben consultar la información siguiendo este orden:

1. INDEX.md
2. Reglas
3. Procesos
4. Entidades
5. Casos
6. Decisiones
7. Documentación oficial (`docs`) únicamente cuando la información necesaria no exista en esta base de conocimiento.

---

# Principios

La información no debe duplicarse.

Cada concepto debe existir en un único lugar.

La documentación oficial continúa siendo la fuente de verdad.

La base de conocimiento representa una interpretación funcional de dicha documentación para facilitar el desarrollo del software.

---

# Mantenimiento

Siempre que cambie la normativa:

1. Actualizar las reglas afectadas.
2. Revisar los procesos relacionados.
3. Actualizar los casos si fuera necesario.
4. Adaptar la implementación del software.

Nunca modificar directamente el código sin haber actualizado previamente esta base de conocimiento.