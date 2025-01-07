# P5 Marker Localization

# Objetivo 
El objetivo de esta práctica es localizar el robot en una habitación basándonos única y exclusivamente de las marcas QR que encontramos en la pared

Para que esto sea posible, tenemos que resolver la matriz de transformacion del mundo de gazebo a la camara del robot. esto lo podemos conseguir resolviendo las siguientes tres matrices. primeramente, hay que resolver la Madrid que va del mundo a los marcadores para resolver así la posición de estos en el mundo. Seguidamente, tendremos que resolver la matriz de los marcadores a la cámara para ubicarlos dentro del espacio del robot. Y una vez has tenido estas dos matrices simplemente nos quedaría resolver la matriz de la cámara al robot para ubicarnos y obtener la localización estimada en base a la marca visuales.

# Matriz mundo-Qr
para la matiz del mundo a los marcadores QR primeramente debemos crear una matriz de rotación 3 × 3 en el eje z. El ángulo de esta dependerá del yaw dado en el diccionario, según el ID de cada baliza. por otro lado para el vector de traslación usaremos como primera componente, la X que nos da el diccionario, como segunda componente la Y que nos proporciona el diccionario y por último como Z usaremos un valor constante, ya que todas estas etiquetas están a la misma altura, la cual es 0,8. teniendo tanto la matriz de rotación como el vector de traslación, simplemente nos queda unirlo en una 4x4 añadiéndole un poco de papping de tal forma que quede como la siguiente.

# Matriz Qr-camara
resolver esta Madrid primeramente, tenemos que encontrar los QR en la imagen. Para ello. Yo he usado la función que viene dada en la documentación del ejercicio. con ello podemos obtener las esquinas de cada etiqueta y usando la función solvePNP de OpenCV, Podemos sacar tanto el vector de rotación como el vector de traslación. en este caso, nuestro vector de rotación no tiene la forma deseada, ya que nosotros queremos que tenga forma 3 × 3 y la función solvePNP nos lo devuelve en 1 × 3. para ello usaremos la función Rodrígues la cual nos convierte este vector a una matriz 3 × 3 como la matriz de el apartado anterior. teniendo esto, simplemente deberíamos seguir los pasos del apartado anterior para resolver la matriz 4 x 4, pero con ello tendríamos la matriz que va de la cámara a los marcadores. Por ello tendríamos que invertir esta matriz para obtener la matriz que nosotros queremos que es la que va del marcador a la cámara.
además, después de varias pruebas me di cuenta de que los ejes del mundo de gazebo y los ejes de OpenCV no eran exactamente los mismos. Por ello esta matriz después de invertirla hay que aplicarle una rotación de -90° en Z y otra rotación de -90° en X, para que estos ejes coincidan y las transformaciones sean correctas.

# Matriz camara-robot
para resolver esta matriz es muy sencillo, ya que simplemente basta con mirar en los archivos del Turtlebot3 donde está ubicada la cámara dentro del robot .concretamente dentro de los archivos SDF podemos ver que las posiciones de la cámara respecto a la base del robot son

# Matriz final
para obtener esta matriz, basta con multiplicar en orden las tres matrices anteriores. es la primera matriz tres será la matriz de rotación, de la cual obtendremos el yaw y por otro lado de las componentes de la derecha, obtendremos el vector de traslación de las cuales obtendremos las coordenadas X Y Z del robot.


# Demostracion
