# Analisis para la compañía Sweet Lift, Prediccion de demanda

## Objetivo

La compañía Sweet Lift Taxi ha recopilado datos históricos sobre pedidos de taxis en los aeropuertos. Para atraer a más conductores durante las horas pico, necesitamos predecir la cantidad de pedidos de taxis para la próxima hora. 

Se está buscando que la métrica RECM en el conjunto de prueba **no debe ser superior a 48**.

## Estructura del Proyecto

El repositorio está organizado de la siguiente manera:

- **/datasets**: Contiene los datos brutos (`raw`) y los datos listos para ser procesados para la creacion del modelo(`pre-processed`).
- **/files/outputs**: Guarda los resultados del proyecto, como el modelo entrenado (`models`), imagenes (`images`)
- **/src**: Contiene el código fuente modularizado en scripts de Python.
- **`requirements.txt`**: Lista de dependencias del proyecto.
- En la raiz del proyecto se encuentran los archivos principales para la ejecución y prueba del mismo.

## Preparando el ambiente virtual
Por favor considerar el ejecutar las siguientes instrucciones para manejar el workspace dentro de un ambiente virtual:

```
mkdir venv
python3 -m venv venv
source venv/bin/activate
user$ pip install --upgrade pip
user$ python -m pip install -r requirements.txt
```

## Como ejecutar el proyecto

Se puede controlar las secciones del proceso a ejecutar por medio de variables dentro del modulo **params** en la raiz del proyecto segun se requiera. 

- preprocess_required = True/False
- training_required = True/False

Para la ejecucion del pipeline, es suficiente con la siguiente linea en raiz del proyecto:

```
python project_pipeline.py 

```
## Modelo Final y Resultados del entrenamiento

<!-- TODO: ajustar los resultados acorde al proyecto -->

El modelo final es un `CatBoost` optimizado. Las siguientes fueron las metricas obtenidas:

<img width="2000" height="600" alt="model_evaluation" src="https://github.com/user-attachments/assets/b04abc7e-df73-4eb1-86f3-289b0153e37a" />

|        |train|test|
|--------------|-----|----|
|F1 Score      |0.63 |0.59|
|Accuracy Score|0.82 |0.81|
|Recall Score  |0.57 |0.54|
|APS           |0.72 |0.65|
|ROC AUC       |0.87 |0.84|