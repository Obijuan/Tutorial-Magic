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

## Polisilicio

## Mostrando/oculatando capas

## Conectando la fuente

## Conectando la puerta

## Conexión con el sustrato

## Conexión con el drenador



