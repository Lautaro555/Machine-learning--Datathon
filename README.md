# Machine-learning--Datathon

En este proyecto se utilizan 2 datasets con datos de un centro medico y el objetivo es entrenar un modelo de machine learning con el dataset de entrenamiento para luego predecir la columna objetivo del dataset de test. Posteriormente se evalua la precision del modelo usando como metrica el Recall y Accuracy, aunque se le dara prioridad al recall.

---

## **Descripción del dataset**

- Available Extra Rooms in Hospital: Habitaciones adicionales disponibles en el hospital. Una habitación no es igual a un paciente, pueden ser individuales o compartidas.
- Department: Área de atención a la que ingresa el paciente.
- Ward_Facility_Code: Código de la habitación del paciente.
- doctor_name: Nombre de el/la doctor/a a cargo del paciente.
- staff_available: Cantidad de personal disponible al momento del ingreso del paciente.
- patientid: Identificador del paciente.
- Age: Edad del paciente.
- gender: Género del paciente.
- Type of Admission: Tipo de ingreso registrado según la situación de ingreso del paciente.
- Severity of Illness: Gravedad de la enfermedad/condición/estado del paciente al momento del ingreso.
- health_conditions: Condiciones de salud del paciente.
- Visitors with Patient: Cantidad de visitantes registrados para el paciente.
- Insurance: Indica si la persona posee o no seguro de salud.
- Admission_Deposit: Pago realizado a nombre del paciente, con el fin de cubrir los costos iniciales de internación.
- Stay (in days): Días registrados de estancia hospitalaria.

La columna a predecir en el archivo de test es "Stay (in days)", donde se utiliza valor 0 para las estadias menores o iguales a 8 dias y valor 1 para las estadias mayores a 8 dias.

---

### **Paso 1**

Como primer medida se cargan los dataset y se evaluan los datos para su trabajo con el modelo. Se utiliza OneHotEncoder para transformar las variables categoricas a numeros y luego se mantienen solo las 10 columnas que tienen mayor correlacion con la columna target. Estos dataset modificados se guardan en un nuevo archivo.
Estos pasos se encuentran detallados en el archivo EDA.ypynb de la carpeta data_cleansing.

### **Paso 2**

Se utiliza un jupyter notebook para trabajar con los modelos. Primero se eligen los modelos a utilizar, en este caso fueron:

* **Regresion logistica:**
  Se utiliza para predecir la probabilidad de un evento, en función de características o variables predictoras. Esta probabilidad se calcula a través de la aplicación de una función logística, que permite asignar pesos a cada una de las variables para estimar la probabilidad de un resultado.
* **GaussNB:**
  Utiliza los principios de la teoría de probabilidad para clasificar los datos según la distribución de probabilidad normal. Estima la probabilidad para cada clase y luego selecciona la clase con la probabilidad más alta.
* **XGBoosting**
  Utiliza una técnica de aprendizaje basada en árboles para entrenar los modelos. Esto significa que cada árbol aprende de los errores cometidos por los árboles anteriores para mejorar el rendimiento global del modelo.

Los modelos fueron elegidos en base a prueba y error de distintos modelos. Al final fueron elegidos los modelos que ofrecian un recall y accuracy aceptable con buen rendimiento. Algunos de los modelos que fueron descartados debido al tiempo que llevaba entrenarlos fueron SVC y K-nearest neigboor.

### **Paso 3**

Se hace un Test split en el dataset de entrenamiento y se toma un 20% de los datos para testeo del modelo. Luego se entrena cada modelo y se usan distintas metricas para evaluarlos por separados.

En este caso lo ideal seria usar GridSearch o cualquier herramienta similar para obtener los mejores hiperparametros de cada modelo, pero al priorizar la velocidad de ejecucion de todo el proceso opte por investigar sobre la documentacion de cada modelo y utilice distintos parametros para intentar conseguir los mejores resultados posibles.

### **Paso 4**

Para finalizar la parte de entrenamiento de los modelos se uso un metodo de ensamblado, en este caso se utilizo Voting el cual funciona al promediar los resultados de cada uno de los modelos para producir un resultado final.
Una vez obtenido el modelo final, se lo utiliza para la prediccion de los datos en la columna objetivo del dataset de testeo, y se guardan los valores obtenidos en una columna llamada "pred" en el archivo Lautaro555.csv tal como se pide en la consigna del trabajo.

Todos estos pasos se pueden ver en el archivo voting model.ypynb

# Conclusion

El resultado obtenido con este modelo, el cual fue evaluado con los datos reales, fue:

* Recall = 0.68
* Accuracy = 0.63

El modelo tiene un desempeño aceptable, pero no es excelente. Un recall de 0.68 significa que el modelo es capaz de identificar correctamente el 68% de los casos relevantes, mientras que un accuracy de 0.63 significa que el modelo es capaz de predecir correctamente el 63% de todas las predicciones. Estos resultados sugieren que el modelo es capaz de identificar correctamente los casos relevantes, pero no es tan preciso con respecto a todas las predicciones. Se necesitan mejoras para aumentar el nivel de precisión.

Algunas de las mejores podrian ser usar GridSearch para la optimizacion de los parametros de cada modelo, usar tecnicas como oversampling para aumentar el tamaño del dataset train de forma sintetica, utilizar técnicas de validación cruzada para evaluar mejor el comportamiento del modelo con nuevos datos o utilizar algoritmos de aprendizaje más avanzados para mejorar la precisión de las predicciones.

De todas formas debido a la rapidez con la que se ejecuta todo el modelo lo considero un resultado aceptable.
