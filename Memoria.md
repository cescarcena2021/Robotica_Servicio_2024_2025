# P2 Rescue pepole ​

## Objetivo 🎯
El objetivo de esta práctica es programar un dron de tal forma que este sea capaz de encontar a personas perdidas en el mar y mandar su ubicacion para su posterior rescate 

## Transfotmacion de cooredenadas 📐​📏​

En primer lugar tenemos que saber el lugar donde estan mas o menos las personas, esto se nos proporciona en la practica ya que nos dicen que las cooredenadas actuales del barco son 40º16’48.2” N, 3º49’03.5” W
y nos dicen que las presonas estan cerca de 40º16’47.23” N, 3º49’01.78” W. Por tanto lo primero que hice fue pasar eso a cooredenadas de mi mapa, y para ello use el trasnformador que se nos proporciona en la [practica](http://rcn.montana.edu/Resources/Converter.aspx)
y conclui que las cordendas eran las siguientes "Coordenadas del barco" E-430492 N-4459162 y "Coordenadas de la personas" E-430532 N-4459125 por tanto haciendo una resta llege a la conclusion de que la zona donde
estaban las persona en el mapa de gazebo era en [40,-37]

## Algoritmo de cobertura 🗺️

Para hacer la busqueda de las personas lo que hice fue hacer un algortimo de espiral crecinete el cual seria capaz de encontar a cualquier persona en el radio de la espiral. Para ello simplemente elegi un
tamaño de lado y este se va incrementando cada dos giros, consighiendo asi hacer una espiral cuadrada que cubra todo el area.

## Detection de las perosnas 

Para saber si nuestra camara enfoca a personas o no, use el algoritmo de detecion de caras Haar Cascades, el cual atraves de varios pequeños filtros, es capaz de detectar caras en una imagen. Pero esto no fue tan 
sencillo ya que una vez lo fui a probar, me dicuenta de que solo detectaba a "Obama" lo cual me parecio raro ya que la camara pasaba por delante de todas las personas, pero solo lo detectaba a el. Despues de varias
prubas me di cuenta de que solo lo detectaba a el ya que era el unico que estaba bien orientado respecto a la imagen, por tanto mi solucion fue rotar la imagen constantemenete para cubrir todos los possobles angulos

![image](https://github.com/user-attachments/assets/ad2819ae-6348-4b9a-b4c1-9317516a3027)

![image](https://github.com/user-attachments/assets/eccd4c86-618c-454f-939e-85de4612b05d)

![image](https://github.com/user-attachments/assets/7216dd68-2699-4ede-9066-6bfb6a119be5)

![image](https://github.com/user-attachments/assets/e52a315b-9d6e-4d12-9e1d-dc7dd580b1ae)

![image](https://github.com/user-attachments/assets/b437ebaf-ecb3-442c-ba2c-68650b39f363)




##  Problema de coordenadas🚗​

Una vez hemos detectado a la persona, tenemos que saber sus coordenadas exactas, y en un primer momento se me ocurrio simplemete obtener la posicion del dron, pero claro si la persona se detecta en una esquina de
la camara la posicion del dron y la posion real de la persona no seria la misma. Por ello dedidi bajar la alrura del dorn, de tal forma que las caras detectadas si
estarian exactemente debajo del dron, por tanto las coordenadas serian mas exactas.

## Aterrizaje

Cuando al dron se le esta acabando la bateria este decide volverse al barco y aterriza. Ya que no contamos con una funcion que nos proporcione la bateria del dron, he decido simular esto con un contador el cual
cuando han pasado 15 min desde que el dron despego, este "se queda sin bateria" y decide volver al barco para ser cargado.

## Demostracion 




