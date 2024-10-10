# P1 vacuum_cleaner 🏎🧹​

## Objetivo 🎯
El objetivo de esta práctica es programar una aspiradora de gama alta de tal forma que sea capaz de hacer barridos de forma eficiente y sin dejar zonas sin cubrir.

Esto lo realizaremos a través de un algoritmo conocido como BSA, que permite recorrer un mapa de celdillas de una forma eficiente.

## Escala 📐​📏​

El primer problema al que nos tenemos que enfrentar es el de ser capaces, a través de una imagen PNG, de identificar dónde está el robot. Para ello, lo que he hecho ha sido mover el robot a distintos puntos del mapa donde el píxel era conocido y la posición del robot también. Esto lo he podido realizar gracias a que, con un poco de habilidad, se puede conseguir identificar el píxel exacto, por ejemplo, en las esquinas.  
Todas estas mediciones tienen el fin de obtener una matriz de homografía que sea capaz de, dadas las coordenadas del mapa, devolver las del mundo y viceversa, aplicando su inversa.

## Mapa de celdillas 🗺️

Para que el algoritmo BSA funcione, el mapa tiene que estar dividido en celdillas. Por lo tanto, he tenido que dividir el mapa en celdillas, en este caso de 20 píxeles, ya que después de varias pruebas, es un número que he encontrado adecuado para que el robot no deje huecos en el barrido ni pase dos veces por el mismo sitio.  
Por lo tanto, una vez dividido el mapa en celdas de 20x20, solo queda determinar si son obstáculos. Para ello, he decidido que, si existe algún píxel negro en esa celdilla, toda la celdilla será negra, ya que el robot podría chocar si pasara por allí.

## Construcción del path 🛤️​

Como he mencionado antes, el algoritmo que se proporciona es BSA, pero en mi caso he encontrado una "variante" que, en vez de realizar espirales, realiza zigzags, lo cual me ha parecido más óptimo para este mapa en concreto.  
Esto lo he conseguido estableciendo un orden de prioridades a las direcciones posibles que puede tomar el robot. Además, he añadido también un estado de "búsqueda de vecinos", en el cual, cuando no tiene más vecinos a los que ir porque se ha quedado atrapado, busca el vecino memorizado más cercano.  
Esto también puede ser un problema, ya que, si entre el vecino y la posición del robot se encuentra una pared, este no sabría cómo esquivarla. Por ello, he añadido el famoso y conocido algoritmo BFS, que es capaz de encontrar el camino más óptimo hacia el vecino teniendo en cuenta los obstáculos.

## Locomoción 🚗​

Una vez tenemos el camino de las celdillas que tenemos que seguir, es sencillo, ya que basta con alinear el robot con la siguiente celdilla usando el ángulo y la distancia euclidiana. Una vez estamos mirando hacia la celdilla, es tan sencillo como comandar velocidad hasta llegar a ella. Una vez estamos encima de ella, volvemos a hacer lo mismo con la siguiente.

## Problemas ⚙️​

### Mueble de la habitación  
Tras varias pruebas y errores, me di cuenta de que el mueble que está en la habitación está mal mapeado en la imagen, ya que debería estar 40 píxeles más o menos a la derecha. Para solucionar este problema, simplemente añadí esas celdillas como ocupadas a mano.

### Engrosamiento de los obstáculos  
Después de que el robot se quedara encajado varias veces al lado de la mesilla del dormitorio, entre las patas de la mesa, decidí engrosar los obstáculos una celdilla en cada dirección. Sin embargo, esto hacía que el robot no llegara a algunos sitios. Por lo tanto, después de varias pruebas, descubrí que solo era necesario engrosarlos en el Sur.
