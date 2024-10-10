# P1 vacuum_cleaner 🏎🧹​

## Objetivo 🎯
El objetivo de esta práctica es programar una aspiradora de gama alta de tal forma de que sea capaz de hacer barridos de forma eficiente y sin dejarse zonas sin cubrir

Esto lo realizaremos atraves de un algoritmo conocido como BSA que permite recorrer un mapa de celdillas de una forma eficiente

## Escala 📐​📏​

El primer problema al que nos tenemos que enfrentar es al de ser capaz de atraves de una imagen png, ser capaces de saber donde esta el robot 
Para ello lo que he hecho a sido ir moviendo el robot a distinos puntos del mapa en los cuales, el pixel era conocido y la posicon del robot tambien. Esto lo he podido realizar gracias a que con un poco de maña, se puede consegir saber el pixel exacto por ejemplo de las esquinas.
Todas esta mediciones son con el fin de conseguir una matriz de homografia que se capaz de dados las coredenadas del mapa, vevolver las del mundo y viceversa y aplicamos su inversa

## Mapa de celdillas 🗺️

Para que el algoritmo BSA funcione, el mapa tiene que estar dividido en celdillas. Por tanto he tendo que dividir el mapa en celdillas en este caso de 20 pixeles ya que despues de varias pruebas, es un numero el cual he encontrado adecuado para que el robot no deje huecos en el barrido, ni pase dos veces por el mismo sitio
Por tanto una vez teniendo el mapa deividido en celdas de 20x20 solo queda saber si son obstaculos, y para ello he decidido que si existia algun pixel negro en esa celdilla, toda la celdilla seria negra ya que el robot podria chocar si pasara por ahi

## Contrucion del path 🛤️​

Como he dicho antes, el algorimo que se proporciona es BSA pero en mi caso he encontrado una "variante" que en vez de realizar espirales, realiza zig zags que en el caso de este mapa en concreto me ha parecido mas optimo.
Esto lo he conseguido estableciendo un oren de prioridades a las direciones posibles que puede tomar el robot. Ademas de eso he añadido tambien un estado de "busqueda de vecinos" en el cual cuando no tiene mas vecinos a los que ir porque se ha quedo atrapado, busca el vecino memorizado mas cercano.
Esto tambien puede ser un problema ya que si entre el vecino y la pisocion del rebot se encontrara una pared este no sabria de que modo esquivarla, por ello he añadido el famoso y conocido algoritmo BFS que es capaz de encontar el path mas optimo hacia el vecino teniendo en cuenta los obstaculos

[Screencast from 10-10-2024 07:12:00 PM.webm](https://github.com/user-attachments/assets/84a93ae5-c22c-4872-bca3-acf78b43a251)


## Locomocion 🚗​

Una vez tenemos el path de las celdilla que te tenemos que seguir es sencillo ya que basta con alinear el robot con la siguiente celdilla usando el aungulo y la distancia euclidea. Una vez estamos mirando a la celdilla es tan sencillo como comandar velocidad hasta llegar a ella. Una vez estamos encima de ella volvemos ha hacer lo mismo con la siguiente.

## Problemas ⚙️​

### Mueble de la habitacion 
Tras varias pruebas y errores me di cuenta de que el mueble que esta en la habitacion esta mal mapeado en la imagen, ya qye deberia estar 40 pixeles mas o menso a la derecha. Para solucionar este problema simplemente añadi yo esas celdilla como ocupadas a mano

### Engorde de los obstaculos 
Despues de que el robot se quedara encajado varias veces al lado de la mesilla del dormitorio, entre las patas de la mesa... Decidi en engordar los obstaculos en una celdila en cada direcion, pero claro esto hacia que el robot no llegara a algunos sitios. Por tanto despues de varias pruebas, es solo necesario engordarlos en el Sur.

![image](https://github.com/user-attachments/assets/31cf0125-551d-4735-a91c-b771d0321050)








  





