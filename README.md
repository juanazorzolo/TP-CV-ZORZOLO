# 🐾 Sistema de Detección y Clasificación de Razas de Perros

Este proyecto implementa un sistema completo de visión por computadora capaz de detectar y clasificar razas de perros a partir de imágenes. Se desarrolla en cuatro etapas que abarcan desde un buscador por similitud hasta un pipeline de detección y anotación automática usando modelos de Deep Learning.


## 🧱 Estructura del Proyecto

El trabajo está dividido en **cuatro etapas**, cada una incrementando las capacidades del sistema:

### ✅ Etapa 1: Buscador de Imágenes por Similitud

- Se utiliza una **ResNet50 preentrenada** para extraer vectores de características (embeddings) de las imágenes del dataset.
- Se indexan los vectores en una **base de datos vectorial** usando **FAISS**.
- A través de **Gradio**, el usuario puede subir una imagen y obtener las 10 más similares.
- Se predice la raza del perro por **voto mayoritario** entre las imágenes recuperadas.
- Se evalúa el sistema con la métrica **NDCG@10**, obteniendo un desempeño destacado.

### ✅ Etapa 2: Entrenamiento y Comparación de Modelos de Clasificación

- Entrenamiento de dos modelos:
  - Modelo A: **Fine-tuning de ResNet18** sobre las 70 razas.
  - Modelo B: **CNN personalizada** entrenada desde cero.
- Cálculo de métricas: **Precisión, Exactitud, Recall, F1-Score, Sensibilidad y Especificidad**.
- Se integra a Gradio la opción de elegir entre ambos modelos para la búsqueda por similitud.

### ✅ Etapa 3: Pipeline de Detección y Clasificación en Imágenes Complejas

- Se integra un modelo **YOLOv8 preentrenado** para detectar perros en escenas del mundo real.
- Por cada perro detectado, se extrae el recorte y se clasifica su raza con el mejor modelo de la Etapa 2.
- La aplicación muestra la imagen original con **bounding boxes** y etiquetas con la raza predicha.

### ✅ Etapa 4: Evaluación, Optimización y Anotación Automática

- Se evalúa el pipeline completo usando un conjunto de imágenes anotadas manualmente.
- Métricas calculadas: **mAP, IoU, Precisión, Recall y F1-Score**.
- Optimización del pipeline:
  - **Cuantización de pesos (FP32 a INT8)**
  - **Conversión a ONNX / TensorRT**
  - Se mide la mejora en **velocidad de inferencia**.
- Se desarrolla un **script de anotación automática** que genera etiquetas en formato **YOLOv5 (.txt)** y **COCO (.json)** para datasets nuevos.



## 📦 Dataset

- **Nombre**: [70 Dog Breeds Image Dataset (Kaggle)](https://www.kaggle.com/datasets/gpiosenka/70-dog-breedsimage-data-set)
- **Distribución**: `train/`, `valid/`, `test/`
- **Clases**: 70 razas distintas de perros


## 🧠 Tecnologías y Librerías

- Python 3.10+
- PyTorch / torchvision
- FAISS
- Gradio
- Ultralytics YOLOv8
- OpenCV / PIL / NumPy
- ONNX / TensorRT (opcional)
- Google Colab (desarrollo y entrenamiento)



## 🚀 ¿Cómo ejecutar el proyecto?

### 1. Cloná el repositorio

```bash
git clone https://github.com/juanazorzolo/TP-CV-ZORZOLO.git
cd nombre_repositorio
```

### 2. Instalá dependencias

pip install -r requirements.txt

### 3. Configurá el acceso a Kaggle (si corrés localmente)

1. Subí tu archivo kaggle.json en la carpeta raíz
2. Ejecutá

mkdir -p ~/.kaggle

cp kaggle.json ~/.kaggle/

chmod 600 ~/.kaggle/kaggle.json


### 4. Ejecutá la app en Gradio
python app.py

## 🗃️ Estructura del Repositorio

📁 app/                  # Código de la app Gradio

📁 models/               # Modelos entrenados

📁 annotations/          # Anotaciones manuales y automáticas

📁 notebooks/            # Notebooks de desarrollo y pruebas

📁 utils/                # Funciones auxiliares (preprocesamiento, métricas, etc.)

📄 app.py                # App principal

📄 requirements.txt      # Dependencias

📄 README.md             # Este archivo

## 📝 Informe
Se adjunta un informe detallado en PDF donde se explican:
- Decisiones de diseño
- Métricas de evaluación
- Desafíos encontrados y soluciones
- Conclusiones generales sobre aplicabilidad real del sistema

## 👤 Autor
Juana Zorzolo Rubio 

Estudiante de Tecnicatura Universitaria en IA

Año: 2025
