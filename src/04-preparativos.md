# Preparativos iniciales

Antes de diseñar nuestro **primer MOSFET-N**, vamos a ir **configurando** Magic, así como aprendiendo su **interfaz**

Magic es un programa **antiguo**, aunque muy potente. Por ello la interfaz resulta actualmente un poco **exraña**. Sin embargo, cuando se aprenden sus fundamentos, resulta **muy sencilla**

PERO es **muy importante** leer esta documetanción y NO intentar hacer nada por tu cuenta

## Ventana principal

Al arrancar Magic como se indica en el apartado anterior, nos aparece **la ventana principal**

![Ventana principal](images/main-window-01.png)


Esta es la pantalla donde haremos nuestro **diseño**. Vamos a destacar algunos de los elementos de la interfaz

* **DRC**: Reglas de diseño. Se indica si se están violando o no las reglas de diseño del chip, con la tecnología actual. Inicialmente no hay diseño, y por eso no se están violando ninguna de las reglas de diseño. Aparece un check en verde
* **Nombre del diseño** actualmente cargado. Por defecto es **UNLOADED**
* **Tecnología**: Sky130A
* **Bloque cursor**: Zona del chip con la zona **activa**, donde afectarán los diferentes comandos que se usen

Una cosa muy importante es que los elementos de diseño dentro del chip siempre son **zonas rectangulares**. Por eso el cursor es un bloque, que puede tener las dimensiones que le demos, pero siempre es **un rectángulo**. No es posible crear otras geometrías diferentes a rectángulos

El **bloque cursor** lo vamos a nombre como **la caja**

Las unidades por defecto que vamos a utilizar son **micrómetros** (µm), que en magic se usa el **prefijo um**. Las dimensiones de la caja por defecto, la que aparece al inicio son de **0.010um x 0.010um**


## Haciendo zoom

Cuando se trabaja con programas de diseño visuales, es importantísimo conocer el manejo de la **cámara**, y saber cómo acercarse para ver detalles, alejarse para ver más información, así como centrar la vista actual. En Magic todo esto se realiza **mediante teclas**. NO SE HACE CON EL RATÓN, como en los programas modernos

> [!NOTE]
> Recordemos que Magic es un programa desarrollado hace décadas, donde todavía el ratón era un elemento que podía NO estar presente en los ordenadores. Por eso está todo pensado para hacerse con el teclado

Para **hacer zoom** y acercarnos a un detalle de nuestro diseño pulsamos en la tecla `z`. Vemos que ahora **la caja** se ve más grande

![Zoom in](images/zoom-01-zoom-in.png)

Para **alejar el zoom** (zoom out) y visualizar más información de nuestro diseño pulsamos `shift-z`

![Zoom out](images/zoom-02-zoom-out.png)

Podemos **centrar** la caja con la tecla `ctrl-z`

![Zoom center](images/zoom-03-center.png)


Aunque conviene tener siempre en la cabeza estas teclas, también se encuentran disponibles en el menú **windows**
![Center](images/zoom-04-window-.png)


## Configurando el grid
## Midiendo el tamaño de la caja
## Guardando el diseño en un fichero
  
