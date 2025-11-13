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
python3 -m venv .venv
source .venv/bin/activate
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

El modelo final es un `RandomForestRegressor` que da un mejor resultado sobre los datos de validación. 


El uso de un `GridSearchCV` para optimizar los hiperparámetros de múltiples modelos arrojaron los siguientes resultados consiguiendo los mejores hiperparametros para el entrenamiento:  

```python
Best Scores: {
    'LinearRegression': np.float64(-23.54183772334203), 
    'ExtraTreesRegressor': np.float64(-17.78691482058781), 
    'RandomForestRegressor': np.float64(-18.211009978532047)
}

Best Params: {
    'LinearRegression': {'fit_intercept': True}, 
    'ExtraTreesRegressor': {'bootstrap': False, 'max_depth': 24, 'n_estimators': 160, 'warm_start': True}, 
    'RandomForestRegressor': {'bootstrap': True, 'max_depth': None, 'n_estimators': 130, 'warm_start': False}
}

```

Así las metricas resultantes fueron las siguientes en los diferentes sets de datos:


<div>
<style>
    body .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    body .dataframe tbody tr th {
        vertical-align: top;
    }

    body .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>model</th>
      <th>set_name</th>
      <th>mse</th>
      <th>rmse</th>
      <th>r2_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td><b>ExtraTreesRegressor</b></td>
      <td>train</td>
      <td>0.028512</td>
      <td>0.168855</td>
      <td>0.999981</td>
    </tr>
    <tr>
      <th>4</th>
      <td>RandomForestRegressor</td>
      <td>train</td>
      <td>71.672147</td>
      <td>8.465940</td>
      <td>0.952040</td>
    </tr>
    <tr>
      <th>0</th>
      <td>LinearRegression</td>
      <td>train</td>
      <td>905.242597</td>
      <td>30.087250</td>
      <td>0.394255</td>
    </tr>
    <tr>
      <th>5</th>
      <td><b>RandomForestRegressor</b></td>
      <td>validation</td>
      <td>1832.722043</td>
      <td>42.810303</td>
      <td>0.466087</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ExtraTreesRegressor</td>
      <td>validation</td>
      <td>1860.194787</td>
      <td>43.129975</td>
      <td>0.458084</td>
    </tr>
    <tr>
      <th>1</th>
      <td>LinearRegression</td>
      <td>validation</td>
      <td>2757.472488</td>
      <td>52.511641</td>
      <td>0.196687</td>
    </tr>
  </tbody>
</table>
</div>