# P4 Amazon Warehouse

## Objetivo 🎯
El objetivo de esta práctica es programar un robot estilo Roomba para que sea capaz de mover estanterías de un sitio a otro en un almacén.

## Transformación de coordenadas 📐📏
Como en la práctica anterior, tenemos que convertir las coordenadas del mapa a las coordenadas de Gazebo y viceversa. Para ello, he creado dos funciones que transforman rápidamente esas coordenadas conociendo las medidas del mapa y las dimensiones del mundo.

## Planificación con OMPL
Para la planificación de rutas hemos utilizado la biblioteca OMPL, que nos proporciona algoritmos de planificación aleatorios. Para ello requerimos de una función de validación en la cual indicamos si un estado es válido o no. Esta es la parte más difícil del algoritmo. Por ello, mi función recibe un parámetro de tamaño, que corresponde a las dimensiones del robot. Con ello elaboro un cuadrado con el cual verifico que no colisione con ningún obstáculo. 

Esto no es tan sencillo, ya que hay que tener en cuenta la rotación del robot en cada estado. Por ello, nuestro cuadrado considera una matriz de rotación asociada. De este modo, cuando el robot coge la estantería, basta con cambiar las dimensiones del robot para que, en vez de ser un cuadrado, sea un rectángulo.

En cuanto al tipo de *planner*, he utilizado `og.RRTConnect()`. Este no es el más óptimo que he encontrado, pero sí el más robusto y rápido. Si lo que queremos es optimización de la ruta, deberíamos usar `og.RRTstar()`, que minimiza la distancia de la ruta.

![image](https://github.com/user-attachments/assets/246fa4af-c40a-4900-a503-88c3028204b7)
![image](https://github.com/user-attachments/assets/cdbffcda-12c0-443c-91e1-cb129cae6bdf)
![image](https://github.com/user-attachments/assets/bac98711-fc97-469a-aaee-b1927ec4bc9e)


## Locomoción
Para la locomoción, la verdad es que ha sido bastante fácil, ya que el *planner* nos proporciona una serie de puntos con los cuales debemos alinearnos y dirigirnos. Como dato curioso, hay que ignorar siempre el primer punto, ya que corresponde a nuestra localización actual. Respecto al *yaw*, solo es necesario tener en cuenta el final, ya que únicamente nos interesa la orientación final del robot, no la de los pasos intermedios.

## Problemas
- **Movimiento de la estantería**: en ocasiones, cuando la estantería está levantada y tratamos de girar con el robot, esta se mueve sin motivo aparente.
- **Elevación de la plataforma**: tras ejecutar el código más de una vez en la página web, esta se queda bloqueada y no consigo que baje. Tengo que reiniciar la web.
- **Planificación de la estantería**: este problema surgió ya que, cuando el robot ya tiene la estantería levantada, le resulta imposible encontrar un plan para ir a cualquier sitio, ya que se encuentra encerrado dentro de la estantería. Por ello, lo que hice fue borrar en el mapa las patas de la estantería una vez esta estaba levantada.

## Demostración
https://youtu.be/eOzIqXXaWbQ





