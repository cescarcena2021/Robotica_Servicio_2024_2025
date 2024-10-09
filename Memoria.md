# P1 vacuum_cleaner 🏎️

## Objetivo 🎯
El objetivo de esta práctica es programar una aspiradora de gama alta de tal forma de que sea capaz de hacer barridos de forma eficiente y sin dejarse zonas sin cubrir

Esto lo realizaremos atraves de un algoritmo conocido como BSA que permite recorrer un mapa de celdillas de una forma eficiente

## Escala ⚜️​

El primer problema al que nos tenemos que enfrentar es al de ser capaz de atraves de una imagen png, ser capaces de saber donde esta el robot 
Para ello lo que he hecho a sido ir moviendo el robot a distinos puntos del mapa en los cuales, el pixel era conocido y la posicon del robot tambien. Esto lo he podido realizar gracias a que con un poco de maña, se puede consegir saber el pixel exacto por ejemplo de las esquinas.
Todas esta mediciones son con el fin de conseguir una matriz de homografia que se capaz de dados las coredenadas del mapa, vevolver las del mundo y viceversa y aplicamos su inversa

## Mapa de celdillas

Para que el algoritmo BSA funcione, el mapa tiene que estar dividido en celdillas. Por tanto he tendo que dividir el mapa en celdillas en este caso de 20 pixeles ya que despues de varias pruebas, es un numero el cual he encontrado adecuado para que el robot no deje huecos en el barrido, ni pase dos veces por el mismo sitio
Por tanto una vez teniendo el mapa deividido en celdas de 20x20 solo queda saber si son obstaculos, y para ello he decidido que si existia algun pixel negro en esa celdilla, toda la celdilla seria negra ya que el robot podria chocar si pasara por ahi

## Contrucion del path

Como he dicho antes, el algorimo que se proporciona es BSA pero en mi caso he encontrado una "variante" que en vez de realizar espirales, realiza zig zags que en el caso de este mapa en concreto me ha parecido mas optimo.
Esto lo he conseguido estableciendo un oren de prioridades a las direciones posibles que puede tomar el robot. Ademas de eso he añadido tambien un estado de "busqueda de vecinos" en el cual cuando no tiene mas vecinos a los que ir porque se ha quedo atrapado, busca el vecino memorizado mas cercano.
Esto tambien puede ser un problema ya que si entre el vecino y la pisocion del rebot se encontrara una pared este no sabria de que modo esquivarla, por ello he añadido el famoso y conocido algoritmo BFS que es capaz de encontar el path mas optimo hacia el vecino teniendo en cuenta los obstaculos

## Locomocion

Una vez tenemos el path de las celdilla que te tenemos que seguir es sencillo ya que basta con alinear el robot con la siguiente celdilla usando el aungulo y la distancia euclidea. Una vez estamos mirando a la celdilla es tan sencillo como comandar velocidad hasta llegar a ella. Una vez estamos encima de ella volvemos ha hacer lo mismo con la siguiente.

## Problemas 

### Mueble de la habitacion 
Tras varias pruebas y errores me di cuenta de que el mueble que esta en la habitacion esta mal mapeado en la imagen, ya qye deberia estar 40 pixeles mas o menso a la derecha. Para solucionar este problema simplemente añadi yo esas celdilla como ocupadas a mano

### Engorde de los obstaculos 
Despues de que el robot se quedara encajado varias veces al lado de la mesilla del dormitorio, entre las patas de la mesa... Decidi en engordar los obstaculos en una celdila en cada direcion, pero claro esto hacia que el robot no llegara a algunos sitios. Por tanto despues de varias pruebas, es solo necesario engordarlos en el Sur.


![image](https://github.com/cescarcena2021/RoboticaMovil2023-2024/assets/102520602/d12ba1b4-56cc-4fb9-83d8-cd307dbe7556)

Pero a esto hay que añadirle una complicación, ya que en la vida real, el mundo no es plano. Existen multitud de obstáculos que un coche no puede atravesar, y es lo que pasa en este caso con las paredes del mapa. Estas paredes necesitan tener un coste muy grande en el gradiente para evitar que el coche las atraviese. De tal forma que el gradiente que ya teníamos, más el reajuste de costes a las paredes, debería quedar algo así:

![image](https://github.com/cescarcena2021/RoboticaMovil2023-2024/assets/102520602/0b64c1c4-d7ff-4cbf-8928-75cb07185fd9)

## Algoritmo de búsqueda 🔍

Como algoritmo de busqueda he usado con cola de prioridad con BFS (breadth first serch) la cual va expandiendo en las 8 direcciones y va asignado pesos a los vecinos. Cuando este llega a un obstáculo deja de espandir y cuando encuentra el coche termina.

## Obtención del camino 👌​
Para saber por dónde tenemos que ir, es muy sencillo una vez tenemos el mapa de costes, ya que simplemente hay que escoger el camino más corto posible basandonos en los pesos.
En este caso, se puede ver cómo el camino claramente es la línea verde

![image](https://github.com/cescarcena2021/RoboticaMovil2023-2024/assets/102520602/ae50a680-49a0-4284-8d03-a9927b7cbc66)


## Navegación 🛥️​

Una vez que tenemos el camino, la navegación es relativamente sencilla. La técnica que he usado ha sido recorrer el camino punto por punto, es decir, voy del punto A al punto B, y cuando ya estoy en B, voy al C y así sucesivamente hasta llegar al objetivo. Para ir de un punto a otro, primero me he centrado en la orientación.

* **Orientación**: Para abordar el tema de la orientación, he utilizado la arcotangente que relaciona el ángulo del coche respecto al siguiente punto. Y una vez que conocemos ese error, simplemente se va corrigiendo poco a poco hasta que este error sea prácticamente inexistente. Cuando estamos perfectamente alineados con el punto, ya podemos ir hacia él

![image](https://github.com/cescarcena2021/RoboticaMovil2023-2024/assets/102520602/1c9cd2d2-e767-4919-8bbb-28aec2ac7e9c)


* **Distancia**: Para determinar la distancia, también he utilizado un teorema matemático, en este caso, el teorema de Pitágoras. Con este teorema, podemos calcular los llamados catetos, que son la diferencia en x y en y de los puntos, para posteriormente obtener la hipotenusa, que en este caso es la distancia entre puntos. Con esto, ya somos capaces de saber la distancia a la que estamos y si hemos alcanzado el objetivo. En caso de que alcancemos el objetivo, iremos a por el siguiente.

![image](https://github.com/cescarcena2021/RoboticaMovil2023-2024/assets/102520602/95134e4e-b381-4fda-8726-2ccec6aa7c34)


## Problemas ⁉️​

* **Cambio de coordenadas**: Durante la práctica, he dedicado varias horas a entender que el problema, en ocasiones, estaba en el uso incorrecto de las coordenadas. No solo las coordenadas del mapa son distintas a las del mundo, sino que también es necesario invertir las coordenadas del objetivo, ya que la x y la y están intercambiadas. Para imprimir el camino, también he necesitado invertir cada x y cada y del camino para que se "printeara" de forma correcta.

```python
# Invertir las cordenadas del target para pasarlos a cordenadas del mapa
target[0], target[1] = target[1], target[0]

....

# Invertimos las cordenandas
  print_path = [(point[1], point[0]) for point in path]
```

* **Cercanía a los muros**: Como en cualquier algoritmo de navegación profesional, el robot es tratado como un punto, pero no lo es. Este tiene unas dimensiones dependiendo de cada robot y, si lo tratáramos como un punto sin hacer nada más, rasparía con las paredes e intentaría siempre ir pegado a ellas. Para ello, una buena técnica es engordar los obstáculos. De esta forma, salvamos las distancias entre los límites del coche y las paredes. Por ello, he creado esta función para que reciba la lista de obstáculos y los aumente el factor deseado dependiendo del robot.


## Demostración 🚕​

[Screencast from 06-16-2024 08:29:41 PM.webm](https://github.com/cescarcena2021/RoboticaMovil2023-2024/assets/102520602/ae713c9e-a2df-4b4c-a733-4dbec029166d)




  





