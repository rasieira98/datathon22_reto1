![image](https://user-images.githubusercontent.com/116558787/197547402-7aea89ce-1cf8-4156-830a-a0a822622aa3.png)
# RETO 1: Identificación de Eventos
![image](https://user-images.githubusercontent.com/116558787/197640277-0f6defa8-3c84-47ec-bb77-9c935108914b.png)
 - Se alcanzaron niveles de validacion de test del f1 micro de 0.15. En este caso manteniendo la misma proporcion de clases que los datos de entrenamiento
## GRUPO_70: Ramón Sieira Martínez (SDG Group) José Divasón (Universidad de La Rioja) Francisco Javier Martínez de Pisón (Universidad de La Rioja)
 - Inicialmente nos encontramos con el problema de analizar la base de datos y entender un poco perdimos bastante tiempo en entender un poco como como eran las señales.
 - Nos dimos cuenta de que las señales tenía un un ruido un ruido de fondo y era difícil identificar los eventos después de eso.
 - Visto eso y visto ya que era un problema de la detección de eventos pues inmediatamente pensamos en la utilización del modelo SED: el modelo SED, utiliza la misma métrica que se está usando en la competición lo interesante es que incorpora una capa de atención basada en transformers. 
De esta forma lo interesante es que podemos hacer que el modelo preste atención en diferentes zonas del espectro y se ha usado bueno esa es una técnica que desde hace ya unos cuantos años ha sido muy popular, por ejemplo, en competiciones de KAGGLE porque se ha utilizado y ha mejorado bastante a lo que había en el estado del arte anterior.
 - Partiendo de ese modelo, y partiendo del análisis con diferentes técnicas de pre procesado, estuvimos probando diferentes transformadas también y vimos que las dos que más información aportaba eran la transformar de Fourier y la CQT. También cierto que en algunas en algunas competiciones este tipo de transformadas de señal han funcionado muy bien. 
 - La idea es incorporar dos modelos dentro del modelo SED, dos modelos de capas de convolución en este caso he basado asen la B3 y B0 lo hemos estado probando e incorpora esas dos capas esos dos modelos dentro del propio modelo SED y luego utilizar dos capas de atención una para cada modelo. 
 - Finalmente la con es el valor máximo para cada tramo para cada frame del audio. Es decir que elegimos la probabilidad máxima nos da cada uno de los dos modelos. El en el este modelo es bastante pesado y la idea que tenemos es muy interesante.

### MODELO SED: Basado en modelos CNN pero incluye un transformer que “presta atención” a zonas específicas de la imagen. 
![image](https://user-images.githubusercontent.com/116558787/197606751-7ec89915-7ab4-4647-a93d-aa2e12e74f8b.png)

### FOURIER y CQT como tranformadores
![image](https://user-images.githubusercontent.com/116558787/197638943-9946f1f8-eed2-40bb-b9c9-36d5e9136f08.png)
![image](https://user-images.githubusercontent.com/116558787/197638945-ad4ba897-88e7-4c9c-9259-da85a1ea9909.png)

