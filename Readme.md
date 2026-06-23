### 

### Diplomatura Inteligencia Artificial

###### Universidad de Palermo

###### 



Alumno: Gonzalez Marta Elizabeth



Fecha: Junio26

\------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------







### Practico 2





###### **Objetivo del Proyecto**





El objetivo del presente trabajo consiste en desarrollar un modelo de Machine Learning capaz de predecir si una persona es fumadora o no fumadora, utilizando información demográfica, antropométrica y clínica.



La variable objetivo es:



&#x09;		**smoking**



donde:



&#x09;		**0 = No fumador**

&#x09;		**1 = Fumador**





La métrica principal de evaluación definida por la consigna es:



&#x09;		**F1-Score para la clase 1 (fumadores)**





\---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------





###### **Orden de Ejecución de las Notebooks**



Nota: posicionarse en el repositorio notebooks, y luego ejecutar en el siguiente orden:



1\. Ejecutar 01\_Analisis\_Inicial.ipynb

2\. Ejecutar 02\_EDA.ipynb

3\. Ejecutar 03\_Preprocesamiento.ipynb

4\. Ejecutar 04\_Entrenamiento.ipynb

5\. Ejecutar 05\_Validacion.ipynb

6\. Ejecutar 06\_Prediccion.ipynb



\---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------





###### **Metodología Aplicada**





Se siguió el siguiente flujo de trabajo:



Análisis Inicial

&#x20;       	↓

&#x20;      		EDA

&#x20;       		↓

&#x09;		Preprocesamiento

&#x20;       			↓

&#x09;			Feature Engineering

&#x20;       				↓

&#x09;				Entrenamiento

&#x20;       					↓

&#x09;					Validación

&#x20;       						↓

&#x09;						Predicción





\---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



###### **Descripción de las Notebooks**





###### **Notebook 01 - Análisis Inicial**





Se realizo una exploración preliminar del conjunto de datos:

* Carga del dataset.
* Revisión de estructura.
* Identificación de tipos de datos.
* Análisis de valores faltantes.
* Verificación de registros duplicados.
* Análisis inicial de la variable objetivo.



**Hallazgos:**

* Dataset compuesto por aproximadamente 50.000 registros.
* Variables clínicas, demográficas y antropométricas.
* No se detectaron valores nulos significativos.
* No se observaron problemas relevantes de calidad de datos.
* El dataset presentaba condiciones adecuadas para su utilización.





###### **Diccionario de Datos**



Variable		Descripción			Es Nulo		Tipo

\--------------------------------------------------------------------------------

ID			Identificador			Not null	Int64

gender			Género				Not null	Object

age			Edad				Not null	Int64

height(cm)		Altura				Not null	Int64

weight(kg)		Peso				Not null	Int64

waist(cm)		Circunferencia cintura		Not null	Float64

eyesight(left)		Visión izquierda		Not null	Float64

eyesight(right)		Visión derecha			Not null	Float64

hearing(left)		Audición izquierda		Not null	Float64

hearing(right)		Audición derecha		Not null	Float64

systolic		Presión sistólica		Not null	Float64

relaxation		Presión diastólica		Not null	Float64

fasting blood sugar	Glucemia			Not null	Float64

Cholesterol		Colesterol			Not null	Float64

triglyceride		Triglicéridos			Not null	Float64

HDL			Colesterol HDL			Not null	Float64

LDL			Colesterol LDL			Not null	Float64

hemoglobin		Hemoglobina			Not null	Float64

urine protein		Proteína en orina		Not null	Float64

serum creatinine	Creatinina			Not null	Float64

AST			Aspartato aminotransferasa	Not null	Float64

ALT			Alanina aminotransferasa	Not null	Float64

Gtp			Gamma GT			Not null	Float64

oral			Examen oral			Not null	Object

dental caries		Dental caries			Not null	Int64

tartar			Sarro dental			Not null	Object

smoking			Variable objetivo		Not null	Int64





###### **Notebook 02 - Análisis Exploratorio de Datos (EDA)**

&#x20;



Para comprender la distribución de las variables y detectar patrones relacionados con el hábito de fumar, se realizaron las siguiente tareas:

* Actividades realizadas
* Análisis univariado.
* Histogramas.
* Boxplots.
* Pairplots.
* Matriz de correlación.
* Mutual Information.
* Comparación entre fumadores y no fumadores.



**Hallazgos principales:**



* Se observó que las variables con mayor asociación respecto al target fueron:

&#x09;Variable	Correlación

&#x09;height(cm)	0.396

&#x09;hemoglobin	0.396

&#x09;weight(kg)	0.301

&#x09;triglyceride	0.251

&#x09;Gtp	        0.236

&#x09;waist(cm)	0.225



También se identificó que:

* Los fumadores presentan niveles más elevados de hemoglobina.
* Los fumadores presentan mayores niveles de triglicéridos.
* Los fumadores presentan mayores niveles de Gtp.
* Las variables antropométricas muestran capacidad predictiva.
* Distribución de la variable objetivo
* No fumadores: \~63%
* Fumadores: \~37%



* Se observó un desbalance moderado, aunque no crítico.







###### **Notebook 03 - Preprocesamiento y Feature Engineering**

&#x20;



Preparación de los datos para el entrenamiento de modelos predictivos:

* Limpieza
* Eliminación de la variable ID.
* Verificación de duplicados.
* Verificación de valores faltantes.
* Feature Engineering



* Se generaron nuevas variables con potencial capacidad predictiva.



* Variables creadas:

&#x09;

&#x09;BMI



&#x09;Índice de Masa Corporal:



&#x09;BMI = peso / altura²

&#x09;WHR



&#x09;Relación cintura-altura:



&#x09;WHR = cintura / altura

&#x09;chol\_hdl\_ratio



&#x09;Relación colesterol total / HDL.



&#x09;tri\_hdl\_ratio



&#x09;Relación triglicéridos / HDL.



* Tratamiento de Outliers



&#x09;Se detectaron valores extremos principalmente en: triglyceride, AST, ALT, Gtp



* Se aplicó Winsorización utilizando:



&#x09;				Percentil 1

&#x09;				Percentil 99



&#x09;Justificación: 			Esta técnica permitió reducir la influencia de valores extremos sin eliminar observaciones.



* Resultado



&#x09;Dataset final:



&#x09;50.000 registros

&#x09;29 variables predictoras

&#x09;1 variable objetivo







###### **Notebook 04 - Entrenamiento y Optimización**

&#x20;



Se Entrenaron distintos algoritmos y se selecciono el modelo con mejor desempeño.



Modelos evaluados:

* Logistic Regression
* Random Forest
* Gradient Boosting



Métrica utilizada:

&#x09;		F1 Score



Resultados



Modelo	F1 Score

* Logistic Regression	0.6666
* Gradient Boosting	0.6959
* Random Forest	0.7353



Modelo seleccionado:

&#x09;		**Random Forest**



Motivo de la elección:



El modelo Random Forest obtuvo el mayor valor de F1-Score, superando en aproximadamente



* 10% a la Regresión Logística.
* 4% a Gradient Boosting.



Dado que la métrica de evaluación definida para el proyecto fue el F1-Score de la clase fumador (target = 1), este modelo logró el mejor equilibrio entre precisión y recall.





La Regresión Logística obtuvo el menor desempeño ( F1 = 0.6666) debido a que el EDA mostró:



* Distribuciones no normales.
* Variables sesgadas.
* Interacciones complejas entre indicadores clínicos.
* Presencia de relaciones no lineales detectadas mediante Mutual Information.



Y este modelo asume una relación esencialmente lineal entre las variables predictoras y la probabilidad de pertenecer a una clase, por lo que no aplica en este caso.





Por otro lado, el hábito de fumar no depende de una única variable, sino de la interacción simultánea de múltiples factores clínicos, por ejemplo:



* Una persona puede presentar triglicéridos elevados sin ser fumadora.
* Otra puede presentar hemoglobina elevada y ser fumadora.
* La combinación de varias variables incrementa significativamente la capacidad predictiva.



Los árboles de decisión que conforman el bosque permiten capturar este tipo de patrones complejos de forma natural.





###### 

###### **Notebook 05 - Validación**

&#x20;



Se evaluó la capacidad de generalización del modelo seleccionado.



Resultados obtenidos:

&#x09;		Classification Report



Clase fumador:



Métrica			Valor

Precision		0.71

Recall			0.76

F1 Score		0.74

Accuracy Global 	0.80





Validación Cruzada



Resultados:

* F1 promedio = 0.7367
* Desvío estándar = 0.0019



Interpretación:

El modelo mostró un comportamiento muy estable en todas las particiones evaluadas. 

El rendimiento se mantiene consistente entre distintas particiones de los datos.







###### **Notebook 06 - Predicción**

&#x20;



Se aplico el modelo entrenado sobre datos no etiquetados.



Se efectuaron las siguientes tareas:

* Carga del dataset de predicción.
* Aplicación de las mismas transformaciones utilizadas durante el entrenamiento.
* Carga del modelo entrenado.
* Generación de predicciones.
* Exportación del archivo final.
* Resultado



Predicciones generadas:



&#x09;		5692 registros



Distribución:



&#x09;Clase		Cantidad

&#x09;No fumador	3520

&#x09;Fumador		2172







\---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------





###### **Optimizaciones Realizadas**



Durante el proyecto se implementaron diversas mejoras para maximizar el rendimiento predictivo.



1\. Feature Engineering



Se incorporaron variables derivadas:



* BMI
* WHR
* chol\_hdl\_ratio
* tri\_hdl\_ratio



Estas variables permitieron representar mejor relaciones fisiológicas y metabólicas.





2\. Tratamiento de Outliers



Se aplicó Winsorización para reducir el impacto de observaciones extremas.





3\. Comparación de Modelos



Se evaluaron múltiples algoritmos:



* Regresión Logística
* Random Forest
* Gradient Boosting



permitiendo seleccionar la mejor alternativa basada en evidencia empírica.





4\. Validación Cruzada



Se utilizó Cross Validation para evaluar la estabilidad del modelo y minimizar el riesgo de conclusiones sesgadas.





5\. Evaluación de Sobreajuste y Subajuste



Análisis de Sobreajuste:



No se observaron evidencias significativas de sobreajuste.



La principal evidencia es la similitud entre:



F1 Test = 0.7353

F1 Cross Validation = 0.7367



La diferencia es mínima:



≈ 0.0014



lo que indica una adecuada capacidad de generalización.





Análisis de Subajuste



Tampoco se observaron señales de subajuste.



El modelo logró:



* Recall elevado para la clase fumador.
* F1 superior a los modelos alternativos.
* Accuracy cercana al 80%.



Estos resultados sugieren que el modelo fue capaz de capturar patrones relevantes presentes en los datos.



\---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------





##### **Conclusiones**



El proyecto permitió desarrollar un modelo predictivo para identificar fumadores a partir de información clínica y antropométrica.



Los principales hallazgos indican que variables relacionadas con:



* Hemoglobina
* Triglicéridos
* Gtp
* Peso corporal
* Circunferencia de cintura



presentan una asociación significativa con el hábito de fumar.



El modelo Random Forest obtuvo el mejor desempeño, alcanzando:



&#x09;F1 Score = 0.7353



y mostrando una optima estabilidad mediante validación cruzada.





Los resultados obtenidos permiten concluir que fuer necesario aplicar una combinación de análisis exploratorio, ingeniería de características, tratamiento de outliers y selección adecuada de modelos.



