![image](https://user-images.githubusercontent.com/116558787/197547402-7aea89ce-1cf8-4156-830a-a0a822622aa3.png)
# RETO 1: Identificación de Eventos
## GRUPO_70: Ramón Sieira Martínez (SDG Group), Jose Divasón (Universidad de La Rioja) y Francisco Javier Martínez de Pisón (Universidad de La Rioja)
 - Inicialmente nos encontramos con el problema de analizar la base de datos y entenderla. Necesitamos bastante tiempo en entender un poco cómo eran las señales.
 - Nos dimos cuenta de que las señales tenían un ruido de fondo, provocando que fuera difícil identificar los eventos.
 - Debido a ello y dado además que era un problema de detección de eventos, inmediatamente pensamos en la utilización del modelo SED. Dicho modelo SED utiliza la misma métrica que se está usando en la competición. Lo más interesante es que incorpora una capa de atención basada en transformers. 
De esta forma, la clave es que podemos hacer que el modelo preste atención en diferentes zonas del espectro. Es una técnica que usada con éxito desde hace varios años, siendo muy muy popular en competiciones de KAGGLE, donde ha mejorado notablemente el estado del arte anterior.
 - Partiendo de ese modelo, y partiendo del análisis con diferentes técnicas de pre-procesado, estuvimos probando diferentes transformadas también y vimos que las dos que más información aportaba eran la transformar de Fourier y la CQT (es también conocido que en algunas en algunas competiciones este tipo de transformadas de señal han funcionado muy bien). 
 - Nuestra idea consiste en incorporar dos modelos dentro del modelo SED: dos modelos de capas de convolución basados en las redes B3 y B0 de EfficientNet. Hemos incorporado los dos modelos dentro del propio modelo SED y luego hemos utilizado dos capas de atención, una para cada modelo. 
 - Finalmente la concatenación es el valor máximo para cada tramo, es decir, para cada "frame" del audio. Por lo tanto, elegimos la probabilidad máxima que nos da cada uno de los dos modelos.
 - Se alcanzaron niveles de validacion de f1 micro de 0.22.
 - USAR el notebook 0115_MODELO_SIMPLIFICADO_EFFB6_SCORE_0.221195
### MODELO SED: Basado en modelos CNN pero incluye un transformer que “presta atención” a zonas específicas de la imagen. 
![image](https://user-images.githubusercontent.com/116558787/197606751-7ec89915-7ab4-4647-a93d-aa2e12e74f8b.png)

### FOURIER y CQT como tranformadores
![image](https://user-images.githubusercontent.com/116558787/197638943-9946f1f8-eed2-40bb-b9c9-36d5e9136f08.png)
![image](https://user-images.githubusercontent.com/116558787/197638945-ad4ba897-88e7-4c9c-9259-da85a1ea9909.png)

