# DEC-001 - Arquitectura funcional de Lamia

## Estado

**Aprobada**

Fecha: 03/07/2026

---

# Contexto

Lamia es una aplicación cuyo objetivo es asistir en la composición de las Comisiones de Selección de la UPV/EHU conforme a la normativa vigente.

Durante el análisis del dominio se identificó que la aplicación debe resolver dos problemas claramente diferenciados:

1. Construir una Comisión de Selección a partir de una propuesta de personas y del resultado del sorteo.
2. Verificar que la Comisión obtenida cumple todos los requisitos establecidos por la normativa.

Aunque ambas tareas están relacionadas, representan responsabilidades distintas y deben mantenerse desacopladas.

---

# Problema

Si la lógica de selección y la lógica de validación se mezclan en un único bloque de código:

- aumenta la complejidad;
- resulta más difícil localizar errores;
- las modificaciones normativas afectan a más partes del sistema;
- disminuye la reutilización del código.

---

# Alternativas consideradas

## Alternativa A

Implementar todo el procedimiento en un único algoritmo.

**Ventajas**

- Implementación inicial sencilla.

**Inconvenientes**

- Código difícil de mantener.
- Alta dependencia entre componentes.
- Difícil depuración.

---

## Alternativa B

Separar la generación de la Comisión de la validación normativa.

**Ventajas**

- Responsabilidades claramente diferenciadas.
- Mayor facilidad para mantener la aplicación.
- Permite reutilizar el motor de validación.
- Facilita la realización de pruebas.
- Hace más sencilla la incorporación de nuevas reglas.

**Inconvenientes**

- Requiere una estructura ligeramente más organizada.

---

# Decisión adoptada

Lamia se estructurará en dos motores funcionales independientes.

## Motor de selección

Responsable de construir la Comisión de Selección.

Sus entradas son:

- propuesta de miembros;
- resultado del sorteo;
- tipo de plaza;
- normativa aplicable.

Su salida es una propuesta de Comisión de Selección.

Este motor implementa el procedimiento administrativo.

No decide si la Comisión es válida.

---

## Motor de validación

Responsable de comprobar que una Comisión cumple todas las reglas de negocio.

Verifica, entre otros aspectos:

- número de miembros;
- procedencia institucional;
- categorías académicas;
- área de conocimiento;
- equilibrio de género;
- requisitos lingüísticos;
- situación administrativa.

Su salida será un conjunto de incidencias, advertencias o la confirmación de que la Comisión cumple la normativa.

---

# Flujo funcional

```text
Propuesta de miembros
          +
Resultado del sorteo
          │
          ▼
 Motor de selección
          │
          ▼
Comisión generada
          │
          ▼
 Motor de validación
          │
          ▼
Resultado de la validación
          │
          ▼
Generación de informe
```

---

# Relación con la base de conocimiento

El motor de selección utilizará principalmente:

- procesos;
- casos de referencia.

El motor de validación utilizará principalmente:

- reglas de negocio;
- entidades.

La documentación oficial (`docs`) únicamente se consultará cuando la información necesaria no esté disponible en la base de conocimiento.

---

# Consecuencias

Esta arquitectura permite:

- mantener desacopladas la generación y la validación;
- facilitar la evolución de la aplicación cuando cambie la normativa;
- reutilizar el motor de validación en otros proyectos;
- desarrollar y probar ambos motores de forma independiente.

---

# Documentación relacionada

## Entidades

- Comisión de Selección

## Procesos

- Propuesta de Comisión de Selección

## Casos

- CASO-001 - Profesor Ayudante Doctor

## Reglas

- REG-001 a REG-007

---

# Observaciones

Esta decisión define la arquitectura funcional del proyecto.

No impone ninguna arquitectura técnica concreta ni condiciona el lenguaje de programación, el framework o la organización interna del código.

Podrá mantenerse aunque la implementación tecnológica evolucione en el futuro.