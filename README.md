# # PRACTICA 2 - ANALISIS ESTRUCTURAL DE PROTEINAS CON ALPHAFOLD

**Asignatura:** Bioinformatica  
**Grado:** Bioinformatica / Ciencia e Ingenieria de Datos  
**Universidad:** Universidad de Las Palmas de Gran Canaria (ULPGC)

**Autores:**  
- Raul Mendoza  
- Adrian Ojeda  

---

## DESCRIPCION GENERAL

En esta practica se realiza un analisis estructural de una proteina utilizando
los modelos predichos por **AlphaFold**. El objetivo es aprender a trabajar con
estructuras tridimensionales de proteinas, evaluar la calidad de la prediccion
y comparar el modelo computacional con una estructura experimental real.

La proteina seleccionada por el grupo es:

- **Nombre:** SUMO1 (Small Ubiquitin-like Modifier 1)  
- **UniProt:** P63165  
- **PDB experimental:** 1A5R  

Todo el desarrollo se ha realizado en un cuaderno Jupyter (`.ipynb`) que permite
ejecutar cada paso de forma secuencial y visualizar los resultados directamente.

---

## REQUISITOS

Para ejecutar correctamente esta practica es necesario disponer de:

- Python 3.9 o superior  
- BioPython  
- py3Dmol  
- requests  
- numpy  
- matplotlib  
- Jupyter Notebook  

Instalacion de dependencias:

```bash
pip install biopython py3Dmol requests numpy matplotlib
```

---

## BLOQUE 1: OBTENCION DE LA SECUENCIA (FASTA)

En primer lugar se descarga la secuencia de la proteina desde **UniProt**
utilizando su identificador. A partir del fichero FASTA se comprueba:

- la longitud total de la secuencia,
- el encabezado,
- y los primeros aminoacidos.

Este paso permite verificar que la secuencia utilizada es correcta antes de
pasar al analisis estructural.

---

## BLOQUE 2: DESCARGA DEL MODELO ALPHAFOLD

El modelo estructural se obtiene desde **AlphaFold DB** usando la API oficial.
En lugar de construir manualmente la URL del fichero (lo que puede provocar
errores 404), se consulta primero la prediccion asociada al identificador
UniProt y se descarga la URL correcta del modelo.

El notebook es robusto y soporta:
- modelos en formato PDB,
- modelos en formato mmCIF.

---

## BLOQUE 3: VISUALIZACION 3D DE LA ESTRUCTURA

La estructura de la proteina se visualiza en 3D utilizando la libreria
`py3Dmol`, representandola en modo *cartoon*. Esta visualizacion permite
apreciar la forma global de la proteina y su organizacion secundaria.

---

## BLOQUE 4: ANALISIS DE pLDDT

Se extraen los valores de **pLDDT** del modelo AlphaFold. Estos valores,
almacenados como B-factor, indican la confianza de la prediccion para cada
residuo.

A partir de ellos se calcula:
- pLDDT medio global,
- porcentaje de residuos con pLDDT superior a 70.

Ademas, se genera una grafica de pLDDT por residuo para identificar regiones
bien definidas y regiones potencialmente flexibles.

---

## BLOQUE 5: COLOREADO DE LA ESTRUCTURA POR pLDDT

La estructura se colorea siguiendo el esquema clasico de AlphaFold:

- Azul: pLDDT muy alto (>= 90)
- Cian: pLDDT alto (70-90)
- Amarillo: pLDDT intermedio (50-70)
- Naranja/Rojo: pLDDT bajo (< 50)

Este paso facilita la interpretacion visual de la calidad estructural del
modelo.

---

## BLOQUE 6: COMPARACION CON ESTRUCTURA EXPERIMENTAL (1A5R)

Se descarga la estructura experimental 1A5R desde el **RCSB PDB** y se compara
con el modelo AlphaFold.

La comparacion se realiza:
- alineando los atomos Cα,
- calculando el RMSD entre ambas estructuras,
- visualizando ambas estructuras superpuestas.

Esta comparacion permite evaluar hasta que punto el modelo AlphaFold reproduce
la estructura experimental.

---

## BLOQUE 7: MAPA DE DISTANCIAS INTERNAS

Finalmente se construye una matriz de distancias Cα–Cα del modelo AlphaFold.
Este mapa permite analizar la compacidad de la proteina y relacionar regiones
estructurales con los valores de pLDDT obtenidos anteriormente.

---

## ESTRUCTURA DEL PROYECTO

- `Bioinformatica_ULPGC_AlphaFold_SUMO1_P63165_ARREGLADO.ipynb`  
  Cuaderno principal con todo el desarrollo de la practica.

- `data_sumo1/`  
  Directorio con los ficheros descargados (FASTA, modelos AlphaFold y PDB
  experimental).

---

## CONCLUSIONES

En esta practica se ha aprendido a:

- Obtener y manejar modelos estructurales predichos por AlphaFold.
- Evaluar la calidad de una prediccion mediante pLDDT.
- Visualizar estructuras 3D de proteinas.
- Comparar modelos computacionales con estructuras experimentales reales.
- Interpretar mapas de distancias internas.

Esta practica consolida los conceptos basicos de bioinformatica estructural y
sirve como base para analisis mas avanzados de proteinas.
