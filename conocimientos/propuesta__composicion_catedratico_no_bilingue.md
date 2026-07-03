Se hace un unico sorteo y luego se ordena segun los bloques para una plaza no bilingue de Catedratico

Sorteo:9 11 16 10 14 17 6 5 12 8 4 7 15 13 3 1 2

Luego se ordenan los bloques:
Bloque A: 6 5 8 4 7 3 1 2
Bloque B: 9 11 16 10 14 17 12 15 13

La mayoria de las propuestas que tengo tienen los 8 primeros integrantes de la UPV/EHU, pero he encontrado una en la que no.

Esta es la propuesta:
1		Vázquez	Jiménez	María Lidia	UPV/EHU	Catedrática de Universidad

2		Lanz	Rivera	Juan José	UPV/ EHU	Catedrático de Universidad

3		Ibarraran 	Vigalondo	Amaya	UPV/ EHU	Catedrática de Universidad

4		Ruiz	Arzalluz	Iñigo	UPV/ EHU	Catedrático de Universidad

5		Luengo	López	Jorge Augusto	Universidad Pablo de Olavide	Catedrático de Universidad

6		Bueno	García	Antonio	UNIVERSIDAD DE VALLADOLID (UVA)	Catedrático de Universidad

7		Bueno	Alonso	Josefina	Universitat d'Alacant	Catedrática de Universidad

8		Cortijo	Talavera	Adela	Universitat de València	Catedrática de Universidad

9		Carriedo	López	María Lourdes	Universidad Complutense	Catedrática de Universidad

10		Sanz	Hernández 	Teófilo	Universidad de Burgos	Catedrático de Universidad

11		Ramos	Gay 	Ignacio	Universitat de València	Catedrático de Universidad

12		Iñarrea 	Las Heras 	Ignacio 	Universidad de la Rioja 	Catedrático de Universidad

13		Suárez 	Pascual 	María-Pilar 	Universidad Autónoma de Madrid 	Catedrática de Universidad

14		López 	Díaz 	Montserrat 	Universidad de Santiago de Compostela 	Catedrática de Universidad

15		Pérez	Pérez	Concepción	Universidad de Sevilla	Catedrática de Universidad

16		Renouprez		Martine	Universidad de Cádiz	Catedrática de Universidad

17		González 	Fernández 	Francisco 	Universidad de Oviedo 	Catedrático de Universidad

Este es el ordenamiento:
Sorteo	Ordenación bloques	DNI/NAN	1er. APELLIDO / 1.ABIZENA	2º APELLIDO / 2.ABIZENA	NOMBRE / IZENA	UNIVERSIDAD /UNIBERTSITATEA

9	6	0	Bueno	García	Antonio	UNIVERSIDAD DE VALLADOLID (UVA)

11	5	0	Luengo	López	Jorge Augusto	Universidad Pablo de Olavide

16	8	0	Cortijo	Talavera	Adela	Universitat de València

10	4	0	Ruiz	Arzalluz	Iñigo	UPV/ EHU

14	7	0	Bueno	Alonso	Josefina	Universitat d'Alacant

17	3	0	Ibarraran 	Vigalondo	Amaya	UPV/ EHU

6	1	0	Vázquez	Jiménez	María Lidia	UPV/EHU

5	2	0	Lanz	Rivera	Juan José	UPV/ EHU

12	9	0	Carriedo	López	María Lourdes	Universidad Complutense

8	11	0	Ramos	Gay 	Ignacio	Universitat de València

4	16	0	Renouprez	0	Martine	Universidad de Cádiz

7	10	0	Sanz	Hernández 	Teófilo	Universidad de Burgos

15	14	0	López 	Díaz 	Montserrat 	Universidad de Santiago de Compostela
 
3	17	0	González 	Fernández 	Francisco 	Universidad de Oviedo
 
1	12	0	Iñarrea 	Las Heras 	Ignacio 	Universidad de la Rioja
 
13	15	0	Pérez	Pérez	Concepción	Universidad de Sevilla

2	13	0	Suárez 	Pascual 	María-Pilar 	Universidad Autónoma de Madrid

Y este el resultado:

UPV/EHU - TIT	4	0	IÑIGO RUIZ ARZALLUZ	T	UPV/ EHU
UPV/EHU - TIT	8	0	ADELA CORTIJO TALAVERA	T	UNIVERSITAT DE VALÈNCIA
EXT-TIT	        9	0	MARÍA LOURDES CARRIEDO LÓPEZ	T	UNIVERSIDAD COMPLUTENSE
EXT-TIT	        11	0	IGNACIO RAMOS GAY 	T	UNIVERSITAT DE VALÈNCIA
EXT-TIT	        16	0	MARTINE RENOUPREZ 0	T	UNIVERSIDAD DE CÁDIZ
					
UPV/EHU-SUP	    3	0	AMAYA IBARRARAN  VIGALONDO	S	UPV/ EHU
UPV/EHU-SUP	    6	0	ANTONIO BUENO GARCÍA	S	UNIVERSIDAD DE VALLADOLID (UVA)
UPV/EHU-SUP	    1	0	MARÍA LIDIA VÁZQUEZ JIMÉNEZ	S	UPV/EHU
UPV/EHU-SUP	    5	0	JORGE AUGUSTO LUENGO LÓPEZ	S	UNIVERSIDAD PABLO DE OLAVIDE
EXT-SUP	        10	0	TEÓFILO SANZ HERNÁNDEZ 	S	UNIVERSIDAD DE BURGOS
EXT-SUP	        14	0	MONTSERRAT  LÓPEZ  DÍAZ 	S	UNIVERSIDAD DE SANTIAGO DE COMPOSTELA 
EXT-SUP	        17	0	FRANCISCO  GONZÁLEZ  FERNÁNDEZ 	S	UNIVERSIDAD DE OVIEDO

NOTAS:
Gracias por el ejemplo real — es justo lo que necesitaba para verificar esto con datos, no solo con la letra de la norma. He rastreado tu caso a mano y descubro **tres cosas importantes**, una de las cuales corrige lo que te dije en el turno anterior.

## 1. Retracto mi recomendación anterior: es un único sorteo, no dos

Comprobé tu secuencia: el sorteo `9,11,16,10,14,17,6,5,12,8,4,7,15,3,1,13,2` filtrado solo por los números 1–8 da exactamente tu "Bloque A: 6,5,8,4,7,3,1,2", y filtrado por 9–17 da exactamente tu "Bloque B". Es decir: **un solo sorteo de 17 bolas**, y luego cada bloque conserva el orden relativo en que salieron sus miembros. La lectura literal del art. 13.1 ("dos sorteos") no se corresponde con la práctica real que muestras. Me equivoqué al recomendarte separar en dos urnas — lo dejo sin implementar.

## 2. El bloque se determina por número de orden, no por universidad — y esto revela un fallo real en mi código

Tu caso confirma que **Bloque A = números de orden 1–8, Bloque B = 9–17**, independientemente de la universidad real de cada persona. Prueba definitiva: el resultado etiqueta a Adela Cortijo Talavera (nº 8, Universitat de València) como **"UPV/EHU-TIT"**, no "EXT-TIT". El código actual usa `isUPV(universidad)` para todo — bloques, validaciones y hasta la etiqueta `CODIGO` de exportación —, así que con una propuesta como esta habría calculado mal: Bloque A de solo 4 personas (las UPV reales) y Bloque B de 13, en vez de 8/9.

## 3. Al corregir el punto 2, aparece un segundo fallo que no había detectado

Recalculé tu ejemplo a mano con la regla correcta (art. 13.2.2, plaza no bilingüe) sobre el pool de Bloque A reordenado `[6,5,8,4,7,3,1,2]`:

- **a.1** exige "primera persona **perteneciente a la UPV/EHU**" → debe ser el nº 4 (Ruiz Arzalluz), no el nº 6 (Bueno García, externo, que es simplemente el primero de la lista).
- Mi función `elegePareja` para el caso no-bilingüe toma literalmente `pool[0]` como "primera", **sin comprobar que sea UPV/EHU**. Funciona bien en Ayudante Doctor porque ahí el pool ya viene pre-filtrado solo-UPV, pero en Acuerdo 2024 (donde el Bloque A puede mezclar externos) esto habría elegido mal a la primera persona del par titular y de cada par suplente.

Con la corrección (exigir `isUPV` en la "primera" siempre, más bilingüe si aplica), reproduzco tu resultado exacto en los 6 puestos del Bloque A (titulares 4 y 8; suplentes 3, 6, 1 y 5) y también el Bloque B (titulares 9, 11, 16; suplentes 10, 14, 17) con la alternancia simple de género ya implementada — sin cambios ahí.

## Antes de tocar el código, una confirmación

Para el caso bilingüe (que no está en tu ejemplo), el art. 12.1.A dice *"en cualquier caso, al menos 2 personas de las propuestas serán de la UPV/EHU"* como suelo mínimo incluso si se completa con externos. Para el caso bilingüe son 8 miembros de la UPV/EHU bilingües, o asi ha sido en los casos que he visto.