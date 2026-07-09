# 🚗⚡ Segmentación de Vehículos y Análisis de Emisiones (DGT)

Este repositorio alberga un proyecto de Ciencia de Datos y Aprendizaje No Supervisado enfocado en la estructuración, análisis y agrupación del parque móvil basándose en los datos oficiales de homologación. El objetivo final es identificar clústeres de vehículos según su eficiencia y tecnología (térmicos, híbridos y eléctricos) bajo el ciclo **WLTP**.

---

## 📋 Estado Actual del Proyecto y Hoja de Ruta

El desarrollo sigue la metodología clásica de un pipeline de Data Science. El estado actual de las fases es el siguiente:

- [x] **Fase 1: Data Understanding & Calidad del Dato** - Auditoría del millón de registros y mapeo de la matriz de nulos.
  - Validación de nulos lógicos por incompatibilidad tecnológica (ej. cilindrada/combustible a `0.0` en eléctricos).
- [x] **Fase 2: Feature Engineering & Preparación**
  - Creación de un pipeline de preparación automatizado (`def preparacion()`).
  - Reducción de la alta dispersión mediante binning estratégico (agrupación de 75 marcas en 6 grupos competitivos, simplificación de combustibles y normativas Euro).
  - One-Hot Encoding controlado para evitar la maldición de la dimensionalidad.
- [x] **Fase 3: Validación Estadística Pre-Modelado**
  - Análisis de multicolinealidad mediante la Matriz de Correlación de Pearson.
  - Test de Kaiser-Meyer-Olkin (KMO Global: `0.6316`) para medir la adecuación muestral.
  - Test de Esfericidad de Bartlett ($\chi^2$: `6.040.526`, $p$-value: `0.0000`) confirmando la viabilidad del PCA.
- [ ] **Fase 4: Reducción Dimensional (PCA)** 🚧 *Siguiente paso*
  - Análisis de la varianza explicada acumulada para seleccionar el número óptimo de componentes principales.
- [ ] **Fase 5: Clustering con K-Means** 🕒 *Pendiente*
  - Aplicación del método del Codo (Elbow Method) y Análisis de Silueta (Silhouette Score) para determinar la $K$ óptima.
  - Entrenamiento, asignación de clústeres y contraste con las etiquetas actuales de la DGT.

---

## 📦 Estructura del Repositorio

* `01_data_preprocessing_PCA_Clustering.ipynb`: Jupyter Notebook principal con todo el código estructurado y documentado.
* `README.md`: Documentación del estado del arte del proyecto.
* `.gitignore`: Configuración de Git para excluir los datos pesados del control de versiones.

---

## 🛠️ Requisitos para Ejecución Local

Debido a las políticas de tamaño de GitHub, el dataset original (`data_coches2024.csv`, ~234 MB) **no está subido al repositorio**. Para replicar el análisis localmente:

1. Clona este repositorio.
2. Descarga el dataset oficial de emisiones desde la **Agencia Europea del Medio Ambiente (EEA)** en el siguiente enlace: [EEA Datahub Item](https://www.eea.europa.eu/en/datahub/datahubitem-view/fa8b1229-3db6-495d-b18e-9c9b3267c02b).
3. Crea una carpeta llamada `data/` en la raíz de tu proyecto local.
4. Renombra el archivo descargado como `data_coches2024.csv` (o asegúrate de que coincida con la ruta de tu notebook) y deposítalo dentro de dicha carpeta.
5. Asegúrate de tener instalado el entorno ejecutando:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn factor-analyzer
