# Creando un MOSFET N

Vamos a crear nuestro primer MOSFET-N con Magic. Se construye dibujando **2 rectángulos**: uno para marcar las **zonas N**, y otro para el **polisilicio** de la **puerta**. A partir de estos dos rectángulos, magic calcula los parámetros necesarios para la fabricación del mosfet

Lo construiremos **de forma incremental**, a la vez que aprendemos las diferentes opciones de Magic, y practicamos con ellas
  
## Dibujando una Zona N mínima

La **zona N mínima** que podemos dibujar está determinada por el **tamaño del grid**, que lo hemos fichado en 0.050um x 0.050um (50nm x 50nm). Este es el tamaño que tiene la **caja** actual. Pulsamos `ctrl-z` para verlo centrado y a su mayor tamaño

![Zona N](images/zona-n-01-min.png)

Nos fijamos que se cumples **las reglas DRC** (básicamente porque NO hay diseñado nada todavía)

Para dibujar una **zona N** en la caja actual, ejecutamos este comando: `paint ndiffusion`. Esto es lo que nos aparece en la consola de magic:

![Zona N](images/zona-n-02-min2.png)

En la ventana del diseño vemos que la caja se pone de **color verde**, y en los cuadrados del grid superior y derecho aparece un **patrón de puntitos**

![Zona N con errores](images/zona-n-03-min3.png)

También observamos que el **DRC FALLA**: Hay 2 errores. Esto es debido a que **NO se puede construir una zona N tan pequeña**, con la tecnología sky130, sino que hay unas **dimensiones mínima**. Pero vamos a investigar sobre esto

Para ver el diseño completo, pinchamos en **windows/full view** o bien apretamos la tecla `v`

![Zona N](images/zona-n-erros.png) 

Ahora se ven todas las cuadrículas nuevas. Por la parte superior hay 2 que indican la **presencia de errores**, y por la parte derecha hay otras 2 también de errores. Los patrones de relleno de estas capas se pueden ver en la parte derecha. Ahí vemos las capas `ndifussion` y `errors`

![Zona N capas](images/zona-n-layers.png)


## Viendo los errores de DRC

Para ver los errores pinchamos en **Options/DRC Manager**

![DRC errors](images/zona-n-drc-errors-1.png)

Se nos abre una ventana nueva, donde nos indica la regla que se está violando: `Diffusion width < 0.15um (diff/tap.1)`

![DRC errors](images/zona-n-drc-errors-2.png)

Lo que significa es que la zona de difusión N tiene **unas dimensiones menores que las mínimas permitidas**. Las mínimas son de **0.15um**. Esto es lo que nos indican las cuadrículas de la capa de error: Al menos, tanto **la anchura** como **la altura** de la zona n tiene que ocupar **3 cuadrículas**


## Ampliando la anchura de la zona N

Vamos a solucionar primero **el problema de la anchura**. La anchura actual es de **0.050um**, pero debe ser al menos de **0.150um**. Situamos el puntero del ratón cerca de la zona donde queremos que se sitúe la **esquina superior derecha** de la **nueva caja** y pulsamos el **botón derecho del ratón**

![Zona N width](images/zona-n-width-1.png)

Se dibuja una **nueva caja** que mantiene la izquina inferior izquierda en el mismo sitio que antes, pero sitúa la esquina superior derecha en el nuevo punto (alineado con la cuadrícula)

Ahora pintamos la nueva zona, ejecutando el comando `paint ndiffusion`, igual que antes

![Zona N width](images/zona-n-width-2.png)

Ahora sólo queda **1 error de DRC**. Se muestra en la capa errors las cuadrículas que deberían ser zonas de difusión n, es decir, hay que ampliar la altura para que sea de al menos 0.150um

## Ampliando la altura de la Zona N

Repetimos el proceso. Con el **botón derecho** seleccionamos el punto de la cuadrícula donde queremos que se sitúe **la esquina superior derecha** de la caja

![Zona N height](images/zona-n-height-1.png)

Y la convertimos en zona de difusión n. Ahora ya sí se cumplen las reglas DRC, y **no hay errores**

![Zona N height](images/zona-n-height-2.png)

Hemos dibujado la **zona N mínima**



## Zona N definitiva

Cuando creamos un mosfet N, **la zona N tiene que ser más grande**, para cumplir con todas las **reglas de diseño**. Su tamaño tiene que ser al menos de **0.650um x 0.450um**. Así que la vamos a crear desde 0

Partimos del estado anterior, donde la caja rodea toda la zona N. Ejecutamos el comando `erase` y la zona desaparece, pero la caja sigue estando

![Zona N final](images/zona-n-final-1.png)

Ahora vamos a poner una zona N de 0.65 x 0.45 (um) en el origen. Utilizamos el comando `box 0 0 0.65 0.45` seguido de `paint ndiffusion`

![Zona N final](images/zona-n-final-2.png)

La Zona N definitiva está lista

## Colocando el Polisilicio

Lo siguiente es colocar **la zona de polisilicio** que atraviesa la zona N, para generar las **dos zonas N**, una a la izquierda y otra a la derecha, y la conexión con la puerta. Para no violar las reglas DRC, el polisilicio debe **sobresalir 0.15um** por arriba y por abajo

Primero marcamos la casilla donde va a estar la **esquina inferior izquierda** del polisilicio. Esto lo hacemos apretando el **botón izquierdo** del ratón

![alt text](images/polisilicio-01.png)


Se sitúa la caja actual con su esquina inferior izquierda en la cuadrícula indicada, ajustada al grid. Ahora posicionamos el ratón en la **esquina superior derecha** de la zona donde queremos que esté el polisicio

![alt text](images/polisilicio-02.png)

Apretamos el **botón derecho** y aparece la nueva caja

![alt text](images/polisilicio-03.png)


Escribimos `paint polysilicon` para convertirla en la zona de polisilicio

![alt text](images/polisilicio-04.png)


En la pantalla gráfica vemos el polisilicio. Observamos que **NO HAY ERRORES DE DRC**

![alt text](images/polisilicio-05.png)


¡Ya tenemos la base de nuestro primer MOSFET!

En el MOSFET N hay **3 capas**:

* **ndifussion**: Las 2 zonas N, que aparecen delimitadas por el polisilicio. Se dibuja una única zona N y **magic calcula** las dos a partir de la intersección con el polisilicio
* **polysilicon**: La capa de polisilicio que hemos dibujado. Magic calcula su intersección con la zona N y divide esta capa en dos zonas. Una de polisilio puro, que sobresale por la zona N y la zona de intersección que conforma la siguiente capa (ntransistor)
* **ntransistor**: Es la capa de **intersección** entre la zona N y el polisilicio. En la fabricación del chip esta zona se **dopa** para que haya muchos electrones libres y la puerta del transistor conduzca

![alt text](images/polisilicio-06.png)



## Mostrando/ocultando capas

Todas las **capas** definidas en la tecnología Sky130A se encuentran en el **panel de la derecha**, como ya hemos visto. Es posible ocultar las capas visibles, así como volver a mostrarlas. Para **ocultar** hay que pinchar en la capa correspondiente usando **el botón derecho del ratón**

En esta imagen vemos cómo se ha ocultado la capa `ntransistor`. Podemos ver que efectivamente ahora la zona N se ha dividido en 2 zonas N

![alt text](images/layers.png)

Para volver a **visualizar** cualquier capa basta con pinchar en la capa y usar **el botón izquierdo**


## Conectando la fuente

Vamos a aprender a realizar **conexiones a la fuente** y **el drenador**, que son iguales. Ambos parten de la capa `ndiffusion`

El punto de partida es una zona N cruzada por el polisilicio, como en el apartado anterior, pero con la geometría ligeramente cambiada: **más espacio en las zonas N** para que quepan los contactos nuevos que vamos a añadir. Ampliar esta zona es algo que ya sabemos hacer, y se deja como ejercicio. Para saber las dimensiones exactas, sólo hay que **contar cuadrículas** de la rejilla

![alt text](images/source-01.png)

El objetivo es **conectar la zona N de la fuente** con un **contacto metálico**, que es el que sale fuera del chip. Las conexiones están en **capas independientes** a mayor altura que el substrato. Estas capas de conexión están separadas, y son independientes. Por eso hay que añadir **contactos** entre ellas, que reciben el nombre de **vías**

La cantidad de capas de interconexión y de vías a diferentes niveles depende de la tecnología usada. Para el caso de **sky130**, que es el que estamos utilizando, la información se encuentra en una figura en este enlace de Tinytapeout: [Skywater’s 130 nm](https://tinytapeout.com/siliwiz/resistors/). Se reproduce aquí la figura para tenerla más a mano:


![alt text](images/source-03-sky130-map.png)


En esta figura se **definen** todos los parámetros de esta tecnología, así como las **diferentes capas**. Como hemos visto en magic, la cosa es más compleja, y existen muchas más capas, pero en este tutorial iremos resumiento la información necesaria, para simplificarlo todo

Este es el **modelo 3D** con las capas que tenemos de partida

![alt text](images/source-02-3D.svg)


Las capas de conexionado están a diferentes niveles. Para pasar de una a otra hay que utilizar **las vías**. La primera capa que hay se denomina `li` en la documentación (local interconection). Su uso es para realizar **conexiones locales** dentro del diseño actual. Se definen conexiones locales como aquellas que NO salen al exterior. Típicamente son **conexiones cortas**. A nivel de fabricación se usa un material especial (Nitruro de titanio) que soporta altas temperaturas


![alt text](images/source-03-mosfet-n-li-3D.svg)


🚧 DEBUG 🚧


La capa `li` recibe el nombre de `locali` en magic. Para acceder a ella hay que colocar una **vía**. Las vías de conexión a li dependen del material que hay en la capa 0. En nuestro caso el material es tipo N y la vía tiene que ser capaz de conectarse bien a ese material. Por ello a nivel genérico estas vías, las que van del sustrato al bus `li` reciben el nombre genérico de `licon` (Conexiones a li). Pero en la práctica hay que usar tipos diferentes según el material del sustrato

Como la fuente es tipo n, tenemos que usar en magic la capa `ndcontact`, que define un **contacto** entre el sustrato y li. Magic además genera las capas intermedias necesarias para realizar este contacto, pero no necesitamos entrar en tantos detalles

Así que vamos a colocar el contacto `ndcontact`. Colocamos la caja como se indica en esta figura. El tamaño mínimo del contacto es de 4x4 cuadros del grid

![](https://github.com/Obijuan/Learn-open-silicon/blob/main/wiki/Log/images/2026-08-18_04-magic-tutorial-mosfet-n-ndcontact1.png)  

Pinchamos con **el botón central del ratón** en la capa `ndcontact`. Nos aparece el contacto. En magic todos los contactos tiene una cruz. 

![](https://github.com/Obijuan/Learn-open-silicon/blob/main/wiki/Log/images/2026-08-18_05-magic-tutorial-mosfet-n-ndcontact2.png)  

Además observamos que aparecen **errores de DRC**. Son debidos a que todavía NO hemos metido la capa **locali**. Nos indican que esta capa no tiene el área mínima requerida (claro, al no estar, tiene área 0), y que tampoco hay un solape entre el contacto y esta área

![](https://github.com/Obijuan/Learn-open-silicon/blob/main/wiki/Log/images/2026-08-18_06-magic-tutorial-mosfet-n-ndcontact3.png)  

Colocamos la caja como se indica en la figura para crear la **capa locali**. Tiene que tener un tamaño lo suficientemente grande como para contener el `ndcontact` y también la vía que pondremos después para conectar con la capa metal1

![](https://github.com/Obijuan/Learn-open-silicon/blob/main/wiki/Log/images/2026-08-18_07-magic-tutorial-mosfet-n-li1.png)  

Nos aparece la **capa locali**. Ahora ya NO hay errores de DRC

![](https://github.com/Obijuan/Learn-open-silicon/blob/main/wiki/Log/images/2026-08-18_08-magic-tutorial-mosfet-n-li2.png)  




## Conectando la puerta

## Conexión con el sustrato

## Conexión con el drenador



