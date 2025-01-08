# P5 Marker Localization

## Objetivo

El objetivo de esta práctica es localizar el robot en una habitación basándonos única y exclusivamente en las marcas QR que encontramos en la pared.

Para que esto sea posible, tenemos que resolver la matriz de transformación del mundo de Gazebo a la cámara del robot. Esto lo podemos conseguir resolviendo las siguientes tres matrices. Primeramente, hay que resolver la matriz que va del mundo a los marcadores para determinar la posición de estos en el mundo. Seguidamente, tendremos que resolver la matriz de los marcadores a la cámara para ubicarlos dentro del espacio del robot. Una vez tengamos estas dos matrices, simplemente nos quedaría resolver la matriz de la cámara al robot para ubicarnos y obtener la localización estimada en base a las marcas visuales.

## Matriz Mundo-QR

Para la matriz del mundo a los marcadores QR, primeramente debemos crear una matriz de rotación 3×3 en el eje Z. El ángulo de esta dependerá del *yaw* dado en el diccionario, según el ID de cada baliza. Por otro lado, para el vector de traslación usaremos como primera componente la X que nos da el diccionario, como segunda componente la Y que nos proporciona el diccionario y, por último, como Z, usaremos un valor constante, ya que todas estas etiquetas están a la misma altura, la cual es 0.8. 

Teniendo tanto la matriz de rotación como el vector de traslación, simplemente nos queda unirlo en una matriz 4×4, añadiéndole un poco de *padding*, de tal forma que quede como la siguiente:

$$
\begin{bmatrix}
cos(α) & -sin(α) & 0 & X \\
sin(α) & cos(α) & 0 & Y \\
0 & 0 & 1 & Z \\
0 & 0 & 0 & 1
\end{bmatrix}
$$


## Matriz QR-Cámara

Para resolver esta matriz, primeramente tenemos que encontrar los QR en la imagen. Para ello, he usado la función que viene dada en la documentación del ejercicio. Con ello, podemos obtener las esquinas de cada etiqueta y, usando la función `solvePNP` de OpenCV, podemos calcular tanto el vector de rotación como el vector de traslación. 

En este caso, nuestro vector de rotación no tiene la forma deseada, ya que queremos que tenga forma 3×3 y la función `solvePNP` nos lo devuelve en 1×3. Para ello, usaremos la función `Rodrigues`, la cual convierte este vector a una matriz 3×3 como en el apartado anterior. Teniendo esto, simplemente deberíamos seguir los pasos del apartado anterior para resolver la matriz 4×4. Sin embargo, con ello obtendríamos la matriz que va de la cámara a los marcadores. Por lo tanto, tendríamos que invertir esta matriz para obtener la matriz que nosotros queremos, que es la que va del marcador a la cámara.

Además, después de varias pruebas, me di cuenta de que los ejes del mundo de Gazebo y los ejes de OpenCV no eran exactamente los mismos. Por ello, a esta matriz, después de invertirla, hay que aplicarle una rotación de -90° en Z y otra rotación de -90° en X para que estos ejes coincidan y las transformaciones sean correctas.

## Matriz Cámara-Robot

Resolver esta matriz es muy sencillo, ya que simplemente basta con mirar en los archivos del TurtleBot3 dónde está ubicada la cámara dentro del robot. Concretamente, dentro de los archivos SDF podemos ver que las posiciones de la cámara respecto a la base del robot son: x: 0.069 y: -0.047 z: -0.107 yaw: 0 


## Matriz Final

Para obtener esta matriz, basta con multiplicar en orden las tres matrices anteriores. La primera de ellas será la matriz de rotación, de la cual obtendremos el *yaw*. Por otro lado, de las componentes de la derecha obtendremos el vector de traslación, del cual obtendremos las coordenadas X, Y y Z del robot.

## Demostración

![image](https://github.com/user-attachments/assets/a1146d31-c2d3-4e89-926d-07463c1b0f18)

