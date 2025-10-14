# MODELDETECTIONDEPANS

Proyecto de detección automática de depresión y ansiedad mediante análisis de mensajes de texto utilizando técnicas de Machine Learning y análisis de sentimientos.

Autoras: Gisselle Barreto(gisselle96) y Kathia Garcia(kathia98).

## 📋 Descripción

Este proyecto implementa múltiples modelos de Machine Learning para la detección de señales de depresión y ansiedad en mensajes de texto. El análisis incluye características lingüísticas, emocionales, temporales y de medicamentos para proporcionar predicciones precisas.

## 🚀 Ejecución

### Google Colab

Este proyecto está diseñado para ejecutarse en **Google Colab**. Para comenzar:

1. Sube los notebooks (`.ipynb`) a tu Google Drive
2. Abre el notebook deseado con Google Colab
3. Sube los archivos de datos cuando a tu Drive y agrega los links donde se solicitan
4. Ejecuta las celdas secuencialmente

## 📊 Formatos de Archivos

### Archivos de Entrada

#### 1. `linkCsv.csv`
Archivo principal con los mensajes individuales y sus características.

**Formato esperado:**
```csv
id_message,message,date,subject_id,label,toxicity,sentiment,POS,NEG,NEU,alegría,tristeza,enojo,miedo,sorpresa,disgusto,yo,me,mi,mío,mía,mí,nosotros,nosotras,nos,nuestro,nuestra,nuestros,nuestras,hora,mes,horario_categoria,estacion_categoria,Med_depresion,Med_ansiedad,Medicamento_depresion,Medicamento_ansiedad,Xanax,Diazepam,Valium,Lorazepam,Alprazolam,MedDep,MedAns,num_palabras_largas,num_palabras_mayusculas,num_signos_puntuacion,num_palabras_primera_mayuscula,negaciones
1.0,"Hola, cómo estás",2024-01-15,user_001,0,0.02,positive,0.85,0.05,0.10,0.70,0.10,0.05,0.03,0.08,0.04,2,1,1,0,0,0,0,0,0,0,0,0,0,14,1,tarde,verano,0.0,no,0,0,0,0,0,0,0,0,0,2,1,2,1,0
```


**Columnas principales:**
- `id_message`: ID único del mensaje
- `message`: Texto del mensaje
- `date`: Fecha del mensaje (YYYY-MM-DD)
- `subject_id`: Identificador del usuario
- `label`: Etiqueta (0=sin depresión, 1=con depresión)
- `toxicity`: Nivel de toxicidad (0.0-1.0)
- `sentiment`: Sentimiento (positive/negative/neutral)
- `POS`, `NEG`, `NEU`: Scores de sentimiento
- Emociones: `alegría`, `tristeza`, `enojo`, `miedo`, `sorpresa`, `disgusto`
- Pronombres: `yo`, `me`, `mi`, `mío`, `mía`, `mí`, `nosotros`, etc.
- Variables temporales: `hora`, `mes`, `horario_categoria`, `estacion_categoria`
- Medicamentos: Columnas binarias para diferentes medicamentos

#### 2. `linkCsv.csv`
Archivo agregado con características por usuario.

**Formato esperado para los modelos:**
##### 📊 Ejemplo de Filas (Datos Reales del Dataset)

**Fila 1: Usuario con depresión**
| subject_id | toxicity | sentiment | POS | NEG | NEU | alegría | tristeza | enojo | miedo | yo | me | mi |
|------------|----------|-----------|-----|-----|-----|---------|----------|-------|-------|----|----|-----|
| subject10000 | 0.0175 | NEU | 0.1600 | 0.2937 | 0.5463 | 0.0852 | 0.0144 | 0.0110 | 0.0069 | 21 | 16 | 3 |

| Hora | Mes | Horario | Estacion | Med_depresion | Medicamento_depresion | label | num_palabras_largas | negaciones |
|------|-----|---------|----------|---------------|----------------------|-------|---------------------|------------|
| 23 | 12 | Noche | Cuarta estación | 0 | 0 | **1** | 43 | 3 |
### Archivos de Salida (Excel)

#### `linkXlsx.xlsx`
Archivo Excel con datos agregados por usuario.

**Estructura:**
- Mismas columnas que `linkCsv.csv`
- Una fila por usuario
- Valores promediados/sumados según el tipo de característica

## 🔧 Características Extraídas

### Características Lingüísticas
- Número de palabras largas
- Número de palabras en mayúsculas
- Número de palabras con primera letra mayúscula
- Número de signos de puntuación
- Cantidad de negaciones

### Características Emocionales
- 6 emociones básicas: alegría, tristeza, enojo, miedo, sorpresa, disgusto
- Análisis de sentimiento: positivo, negativo, neutral
- Nivel de toxicidad

### Características de Pronombres
- Uso de pronombres personales en primera persona (yo, me, mi, etc.)
- Uso de pronombres en primera persona plural (nosotros, nos, etc.)

### Características Temporales
- Hora del día
- Mes
- Categoría horaria (mañana/tarde/noche)
- Estación del año

### Características de Medicamentos
- Menciones de medicamentos para depresión
- Menciones de medicamentos para ansiedad
- Medicamentos específicos: Lorazepam, Valium, Diazepam, Alprazolam, Xanax

#### `linkCsv.csv`

##### Columnas de Identificación y Texto
| Columna | Tipo | Descripción | Ejemplo |
|---------|------|-------------|---------|
| `id_message` | Float | ID único del mensaje | 1245.0 |
| `message` | String | Texto del mensaje | "Me siento muy cansado hoy" |
| `date` | Date | Fecha del mensaje | 2024-03-15 |
| `subject_id` | String | Identificador del usuario | user_042 |
| `label` | Integer | Etiqueta (0=control, 1=con depresión, 2=con ansiedad) | 1 |

##### Columnas de Análisis de Sentimiento
| Columna | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| `toxicity` | Float | 0.0 - 1.0 | Nivel de toxicidad del mensaje |
| `sentiment` | String | - | Sentimiento general (positive/negative/neutral) |
| `POS` | Float | 0.0 - 1.0 | Score de sentimiento positivo |
| `NEG` | Float | 0.0 - 1.0 | Score de sentimiento negativo |
| `NEU` | Float | 0.0 - 1.0 | Score de sentimiento neutral |

##### Columnas de Emociones
| Columna | Tipo | Rango | Descripción |
|---------|------|-------|-------------|
| `alegría` | Float | 0.0 - 1.0 | Nivel de alegría detectado |
| `tristeza` | Float | 0.0 - 1.0 | Nivel de tristeza detectado |
| `enojo` | Float | 0.0 - 1.0 | Nivel de enojo detectado |
| `miedo` | Float | 0.0 - 1.0 | Nivel de miedo detectado |
| `sorpresa` | Float | 0.0 - 1.0 | Nivel de sorpresa detectado |
| `disgusto` | Float | 0.0 - 1.0 | Nivel de disgusto detectado |

##### Columnas de Pronombres (Primera Persona)
| Columna | Tipo | Descripción |
|---------|------|-------------|
| `yo`, `me`, `mi`, `mío`, `mía`, `mí` | Integer | Conteo de pronombres singulares |
| `nosotros`, `nosotras`, `nos`, `nuestro`, `nuestra`, `nuestros`, `nuestras` | Integer | Conteo de pronombres plurales |

##### Columnas Temporales
| Columna | Tipo | Descripción | Valores |
|---------|------|-------------|---------|
| `hora` | Integer | Hora del mensaje | 0-23 |
| `mes` | Integer | Mes del mensaje | 1-12 |
| `horario_categoria` | String | Categoría horaria | mañana/tarde/noche |
| `estacion_categoria` | String | Estación del año | primavera/verano/otoño/invierno |


##### Estructura de Columnas

| Categoría | Columnas | Descripción |
|-----------|----------|-------------|
| **Identificación** | `subject_id`, `label` | Usuario y etiqueta de depresión |
| **Sentimiento** | `toxicity`, `sentiment`, `POS`, `NEG`, `NEU` | Promedios de análisis de sentimiento |
| **Emociones** | `alegría`, `tristeza`, `enojo`, `miedo`, `sorpresa`, `disgusto` | Promedios de emociones detectadas |
| **Pronombres** | `yo`, `me`, `mi`, `mío`, `mía`, `mí`, `nosotros`, `nosotras`, `nos`, `nuestro`, `nuestra`, `nuestros`, `nuestras` | Suma total de uso de pronombres |
| **Medicamentos** | `Medicamento_depresion`, `Medicamento_ansiedad`, `Lorazepam`, `Valium`, `Diazepam`, `Alprazolam`, `Xanax`, `Med_depresion`, `Med_ansiedad`, `MedDep`, `MedAns` | Información agregada sobre medicamentos |
| **Temporal** | `Hora`, `Mes`, `Horario`, `Estacion` | Valores más frecuentes o promedios temporales |
| **Lingüísticas** | `num_palabras_largas`, `num_palabras_mayusculas`, `num_palabras_primera_mayuscula`, `num_signos_puntuacion`, `negaciones` | Suma total de características lingüísticas |


## 🤖 Modelos Implementados

- **Naive Bayes**: Modelo probabilístico baseline
- **Random Forest (RF)**: Ensemble de árboles de decisión
- **Gradient Boosting Machine (GBM)**: Boosting tradicional
- **Light Gradient Boosting Machine (LGBM)**: Versión optimizada de GBM
- **Support Vector Machine (SVM)**: Clasificador de máximo margen
- **K-Nearest Neighbors (KNC)**: Clasificador basado en proximidad
- **Bag of Words (BoW)**: Análisis de frecuencia de términos

## 📈 Pipeline de Procesamiento

1. **Extracción de Características** (Carpeta `Caracteristicas/`)
   - Cada notebook procesa un tipo específico de característica
   - Los resultados se consolidan en archivos agregados

2. **Agregación de Datos**
   - `AgregacionDatosporSujetos.ipynb`: Agrupa mensajes por usuario
   - Genera `Caracteristicas por usuario.csv` y `grouped_trainytrial.xlsx`

3. **Entrenamiento de Modelos** (Carpeta `Modelos/`)
   - Cada modelo tiene su propio notebook
   - Los modelos se evalúan y comparan

4. **Testing** (Carpeta `Test-Modelos/`)
   - Validación de los mejores modelos
   - Métricas de rendimiento

## 📋 Requisitos

```python
pandas
numpy
scikit-learn
lightgbm
xgboost
matplotlib
seaborn
openpyxl
```

## 📝 Notas Importantes

- Asegúrate de que los archivos CSV estén codificados en UTF-8
- Los archivos Excel deben tener extensión `.xlsx` o `.csv`
- La columna `label` es: 0 (control), 1 (con depresión) y 2 (con ansiedad)
- Los valores faltantes se manejan automáticamente en cada notebook


## 📄 Licencia

Este proyecto se encuentra bajo la licencia especificada en el archivo LICENSE.


**Nota**: Este es un proyecto de investigación académica. Los resultados deben ser interpretados por profesionales de la salud mental calificados.
