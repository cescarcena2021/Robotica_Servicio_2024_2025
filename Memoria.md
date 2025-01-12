# P3 Autoparking

## Objetivo
El objetivo de esta práctica es conseguir que el coche sea capaz de realizar un aparcamiento en línea de forma autónoma. 

## Alineación con la carretera
Lo primero en esta práctica es alinearse de forma correcta con la carretera, de tal forma que el coche sea capaz de circular pegado a los coches, detectando con el láser lateral si hay sitios libres o no.  
Para ello, me he estado fijando en las medidas del láser lateral, de tal forma que se mantenga a 1 metro de los coches, detectando si hay huecos libres. En el video demostrativo, podemos ver cómo, nada más arrancar, el coche comienza a pegarse a los coches de su derecha.

## Búsqueda de aparcamiento
Esto, la verdad, ha sido sencillo, ya que simplemente basta con tomar lecturas del láser lateral; en mi caso, de 50 a 130 grados. Si todas estas medidas del láser están libres, eso significa que el coche entra dentro del hueco y que es capaz de aparcar ahí.

## Aparcamiento
Para el proceso de aparcamiento, he usado el típico procedimiento de aparcamiento que se enseñaría en cualquier autoescuela.  
![image](https://github.com/user-attachments/assets/8155465a-a18b-4ee0-bef0-dd60f34616c1)

El primer paso sería alinearse con el coche de delante o, en caso de que no exista coche delante, avanzar una distancia considerable.  
En segundo lugar, como podemos ver en la imagen, hay que girar las ruedas mientras vamos marcha atrás, hasta detectar que estamos en una buena posición respecto al coche de atrás.  
En tercer lugar, con las ruedas rectas, retrocedemos lo necesario para poder enderezar el coche sin rozar al coche de delante, en caso de que exista. Continuando con este paso, seguimos retrocediendo con las ruedas giradas en sentido contrario hasta que estemos a una distancia prudente respecto al coche de detrás.  
Finalmente, cuando ya nos encontramos en esta posición, solo queda ir hacia delante y hacia atrás de forma consecutiva, girando las ruedas en ambos sentidos, para dejar el coche en una posición de aparcamiento óptima.

## Robustez
Para que esta práctica sea buena y robusta, el coche debe aparcar tanto en sitios grandes como en sitios pequeños, con coches delante y detrás, y sin ellos. En mi caso, he conseguido lo siguiente:

- [x] Aparcamiento predeterminado.
- [x] Aparcamiento en un sitio más pequeño.
- [x] Aparcamiento sin un coche delante. 
- [ ] Aparcamiento sin coche detrás.

Este último no lo he conseguido desarrollar, ya que, en mi caso, necesito tener algún coche de apoyo para poder alinearme con la carretera, saber qué dirección tomar, y cuándo empezar a realizar la maniobra de aparcamiento.

## Demostración
https://youtu.be/9e0KgSAW1p0
