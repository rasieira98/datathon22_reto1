![image](https://user-images.githubusercontent.com/116558787/197547402-7aea89ce-1cf8-4156-830a-a0a822622aa3.png)
# RETO 1: Identificación de Eventos
## GRUPO_70: Ramón Sieira Martínez (SDG Group), Jose Divasón (Universidad de La Rioja) y Francisco Javier Martínez de Pisón (Universidad de La Rioja)
 - Inicialmente nos encontramos con el problema de analizar la base de datos y entenderla. Necesitamos bastante tiempo en entender un poco cómo eran las señales.
 - Nos dimos cuenta de que las señales tenían mucho ruido de fondo, provocando que fuera muy difícil identificar los eventos. Este fue uno de los retos más importantes.
 - Debido a ello y dado además que era un problema de detección de eventos, inmediatamente pensamos en la utilización del modelo SED. Dicho modelo utiliza la misma métrica que se está usando en la competición. Lo más interesante del [modelo SED](https://tut-arg.github.io/sed_eval/tutorial.html) frente a los modelos tradicionales de visión es que incorpora una capa de atención basada en transformers de modo que el modelo presta atención a diferentes zonas del espectrograma. El modelo SED es una técnica usada con éxito desde hace varios años y mejoró sustancialmente el estado del arte relacionado con el la identificación en audio. Este modelo se popularizó en competiciones de audio de KAGGLE.
 - Partiendo de ese modelo, y partiendo del análisis con diferentes técnicas de pre-procesado, estuvimos probando diferentes transformadas y vimos que las dos que más información aportabba eran la FFT y la CQT (que en otras competiciones de Kaggle de audio y trtamiento de señal ha funcionado muy bien). 
 - El preprocesado en el dataloader fue vital. Para el entrenamiento, un 50% de las veces se se seleccionaban los tramos donde estaban los eventos y se escalaban al tamaño de la imagen deseado según el modelo Efficientnet a usar. Si el evento era mayor de tres segundos, se elegia un tramos entre 1 y 3 segundos del mismo. El otro 50% se escogia aleatoriamente entre 1 y 3 segundos. Las etiquetas correspondian a las cuatro clases más la clase ruido. Para la validación, se utilizó una ventana de 2 segundos con paso de 2 segundos.
 - Nuestra idea consistió en incorporar dos modelos dentro del modelo SED: dos modelos de capas de convolución basados en las redes Efficientnet-ns. El mejor modelo final utilizaba una Efficientnet-B6_ns. Se incorporaron dos redes Efficientnet dentro del propio modelo SED, una aprendia de la FFT y la otra del CQT. Posteriormente, se utilizaba dos capas de atención, una para cada modelo.
 - La combinación de los dos modelos se realizó a partir del valor máximo para cada tramo, es decir, para cada "frame" del audio. Por lo tanto, elegimos la probabilidad máxima que nos da para cada uno de los dos modelos interno.
 - El entrenamiento se realizó con un 80% de los audios, un 10% para validar y el otro 10% para la base de datos de Testeo.
 - La inferencia fué otro problema dificil de resolver. Para calcular los thresholds de cada clase, se utlizó la base de datos de testeo.
 - Se alcanzaron niveles de validacion de f1 micro de 0.3010 en el ranking de la competición.
 - USAR el notebook MODELO_SED_DOBLE_BALANCEADO_B6_0.301094
### MODELO SED: Basado en modelos CNN pero incluye un transformer que “presta atención” a zonas específicas de la imagen. 
![image](https://user-images.githubusercontent.com/116558787/197606751-7ec89915-7ab4-4647-a93d-aa2e12e74f8b.png)

### FOURIER y CQT como tranformadores
![image](https://user-images.githubusercontent.com/116558787/197638943-9946f1f8-eed2-40bb-b9c9-36d5e9136f08.png)
![image](https://user-images.githubusercontent.com/116558787/197638945-ad4ba897-88e7-4c9c-9259-da85a1ea9909.png)

