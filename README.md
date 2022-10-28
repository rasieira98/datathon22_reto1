![image](https://user-images.githubusercontent.com/116558787/197547402-7aea89ce-1cf8-4156-830a-a0a822622aa3.png)
# RETO 1: Identificación de Eventos
## GRUPO_70: Ramón Sieira Martínez (SDG Group), Jose Divasón (Universidad de La Rioja) y Francisco Javier Martínez de Pisón (Universidad de La Rioja)
 - Inicialmente nos encontramos con el problema de analizar la base de datos y entenderla. Necesitamos bastante tiempo en entender un poco cómo eran las señales.
 - Nos dimos cuenta de que las señales tenían mucho ruido de fondo, provocando que fuera muy difícil identificar los eventos. Este fue uno de los retos más importantes.
 - Debido a ello y dado además que era un problema de detección de eventos, inmediatamente pensamos en la utilización del modelo SED. Dicho modelo utiliza la misma métrica que se está usando en la competición. Lo más interesante del modelo SED frente a los modelos tradicionales de visión es que incorpora una capa de atención basada en transformers de modo que el modelo presta atención a diferentes zonas del espectrograma. El modelo SED es una técnica usada con éxito desde hace varios años y mejoró sustancialmente el estado del arte relacionado con el la identificación en audio. Este modelo se popularizó en competiciones de audio de KAGGLE.
 - Partiendo de ese modelo, y partiendo del análisis con diferentes técnicas de pre-procesado, estuvimos probando diferentes transformadas también y vimos que las dos que más información aportaba eran la transformar de Fourier y la CQT (es también conocido que en algunas en algunas competiciones este tipo de transformadas de señal han funcionado muy bien). 
 - Nuestra idea consiste en incorporar dos modelos dentro del modelo SED: dos modelos de capas de convolución basados en las redes B3 y B0 de EfficientNet. Hemos incorporado los dos modelos dentro del propio modelo SED y luego hemos utilizado dos capas de atención, una para cada modelo. 
 - Finalmente la concatenación es el valor máximo para cada tramo, es decir, para cada "frame" del audio. Por lo tanto, elegimos la probabilidad máxima que nos da cada uno de los dos modelos.
 - Se alcanzaron niveles de validacion de f1 micro de 0.3010.
 - USAR el notebook MODELO_SED_DOBLE_BALANCEADO_B6_0.301094
### MODELO SED: Basado en modelos CNN pero incluye un transformer que “presta atención” a zonas específicas de la imagen. 
![image](https://user-images.githubusercontent.com/116558787/197606751-7ec89915-7ab4-4647-a93d-aa2e12e74f8b.png)

### FOURIER y CQT como tranformadores
![image](https://user-images.githubusercontent.com/116558787/197638943-9946f1f8-eed2-40bb-b9c9-36d5e9136f08.png)
![image](https://user-images.githubusercontent.com/116558787/197638945-ad4ba897-88e7-4c9c-9259-da85a1ea9909.png)

