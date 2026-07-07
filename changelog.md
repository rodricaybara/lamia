# Changelog

Todas las novedades notables de este proyecto se documentan en este fichero.

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/).

---

## [1.0.0] — 2026-07-07

Primera versión estable del validador. Cubre la validación de propuestas y el cálculo de
composición de Comisión de Selección para:

- **Profesorado Ayudante Doctor** (Acuerdo Consejo de Gobierno, 11 junio 2024).
- **Catedrático** y **Pleno** (Acuerdo 26/09/2024, BOPV 10/10/2024), en perfil bilingüe y
  no bilingüe.

Titular y Agregado quedan fuera de esta versión (deshabilitados en la interfaz, previstos
para v1.1).

### Added

- Parseo de la propuesta desde Excel (`.xlsx`), con detección de cabeceras por nombre y
  posición de respaldo (`crearIndiceColumnas`), y detección automática del código de plaza
  desde el título del fichero.
- Motor de validación (`validarPropuesta()`) que comprueba, según el reglamento aplicable:
  numeración 1–17 sin huecos ni duplicados, tamaño y proporción de bloques, situación
  administrativa, área de conocimiento, equilibrio de género, capacidad bilingüe/trilingüe
  y categoría académica — con mensajes de anomalía referenciados al artículo aplicable y
  sugerencia de corrección.
- Mecanismo de excepción CPU: cualquier anomalía puede marcarse como validada por la
  Comisión de Planificación Universitaria, con referencia de acta, sin bloquear el sorteo.
- Motor de sorteo (`calcularComposicion()`) que reordena la propuesta según el resultado
  del sorteo público y aplica el algoritmo de formación de pareja/alternancia de género
  correspondiente a cada bloque y cada régimen normativo, con traza paso a paso de cada
  decisión y su artículo de referencia.
- Entrada del sorteo por bolas individuales o como secuencia de texto.
- Exportación a Excel y PDF (vía impresión del navegador) tanto del informe de validación
  como del acta de composición final, con DNI enmascarado en pantalla.
- Cuatro casos de referencia congelados como regresión: CASO-001 (Ayudante Doctor),
  CASO-002 (Catedrático bilingüe), CASO-003 (Pleno bilingüe), CASO-004 (Pleno no
  bilingüe).

### Fixed

Bugs detectados y corregidos durante el desarrollo, acumulados hasta esta versión:

- Comparación de categoría por igualdad de cadena exacta, que bloqueaba todas las
  propuestas de Acuerdo 2024; sustituida por comparación de subcadena normalizada.
- Regla de emparejamiento del Bloque A (art. 13.2.1 vs. 13.2.2) aplicada según el perfil
  bilingüe en vez de según la subcategoría: Catedrático usa siempre 13.2.1; Pleno/Agregado
  usa 13.2.2 solo cuando la plaza no es bilingüe.
- Duplicación silenciosa de personas entre Bloque A y Bloque B cuando el art. 13.2.2
  incorporaba candidatos externos al Bloque A, que el Bloque B volvía a seleccionar por su
  cuenta al no excluir a quienes ya se habían usado — corregido separando la lista
  reordenada en dos sublistas por posición (nº 1–8 / nº 9–17) antes de aplicar el
  algoritmo de cada bloque.
- Reconocimiento de variantes de categoría (femeninas, abreviaturas, euskera) que fallaba
  con formas como "Catedrática", "CU", "TU" o "Katedraduna" — corregido con
  `normalizarCategoria()` y comparación por raíz léxica (`CATEDRATIC`, `PLEN`, etc.) en vez
  de por palabra completa.
- `validarPropuesta()` calculaba el Bloque A/B por afiliación institucional (`isUPV()`) en
  vez de por posición para Acuerdo 2024, dando conteos incorrectos de UPV/EHU en Bloque A
  y de paridad de género — corregido usando `getBloquesPropuesta()` de forma consistente
  en toda la aplicación; se añadió además una comprobación explícita de personas UPV/EHU
  coladas en el Bloque B (no permitido por art. 12.1.B).
- Categoría llegando como cadena compuesta con género flexionado (p. ej. "PROFESORA
  CATEDRATICA") en vez de la palabra clave aislada — resuelto con `esCategoria()` sobre
  raíces léxicas, y una etiqueta separada (`categoriasLabel`) para que los mensajes de
  error sigan siendo legibles.
- Etiquetado del código de fila ("UPV/EHU" vs. "EXT") calculado por afiliación individual
  en vez de por bloque de origen: las personas externas que completan el Bloque A (art.
  12.3) se mostraban como "EXT" en vez de "UPV/EHU" — corregido con el helper
  `codigoBloque()`, que distingue por posición en Acuerdo 2024 y por afiliación en
  Ayudante Doctor.

### Known issues

- La cita del artículo para la situación administrativa en plazas de Ayudante Doctor
  referencia por ahora el art. 11.9 del reglamento de Acuerdo 2024 (incorrecto para ese
  caso); pendiente de corregir con el texto completo del reglamento de Ayudante Doctor.
- No se ha podido contrastar este validador contra la plantilla Excel oficial como fuente
  fiable: se ha detectado que dicha plantilla desalinea las columnas de nombre y
  universidad en las filas de suplentes (ver CASO-004). El validador se apoya en la
  verificación manual del articulado y en los casos de referencia congelados, no en la
  plantilla.

### Not included in this version

- Profesorado Titular y Agregado (art. 12.4.c/d y art. 13.3.b, con los umbrales del 40%
  de Catedrático/Pleno) — deshabilitados en la interfaz, previstos para v1.1.