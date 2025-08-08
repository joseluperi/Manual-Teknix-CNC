Fundamentos de las Máquinas CNC
################################

Esta sección describe brevemente las máquinas de control numérico desde el punto de vista del controlador.

.. _mechComps:

Componentes Mecánicos
=====================

Una máquina de control numérico tiene varios componentes mecánicos que pueden ser manejados por el control o 
que afectan la manera en que el controlador funciona. Aquí se describen los componentes que interactúan con el 
controlador. Los comonentes que no interactúan directamente con el controlador no se describen aquí, incluso si
afectan el control, como los botones de Jogging.

Ejes
----

Cualquier máquina de CNC tiene uno o más ejes. Las diferentes máquinas tienen diferentes combinaciones de ejes.
Por ejemplo una máquina de fresado de 4 ejes puede tener los ejes XYZA o XYZB. Un torno típicamente tiene los 
ejes XZ, pero puede tener además un eje Y. Si el husillo del torno se puede mover de forma coordinada con los otros
ejes, generalmente se lo denomica eje C.

**Ejes Lineales Primarios**

Los ejes X, Y y Z producen movimientos lineales en direcciones ortogonales.

**Ejes Lineales Secundarios**

Los ejes U, V y W producen movimientos lineales en direcciones ortogonales. Típicamente los ejes X y U son paralelos
así como los Y y V, y los Z y W.

**Ejes de Rotación**

Los ejes A, B y C producen movimientos angulares de rotación. Típicamente, el eje A rota alrededor de un eje paralelo al 
eje X, el B rota respecto a un eje paralelo al eje Y y el C rota respecto a un eje paralelo al eje Z.

Husillo
-------

Las máquinas de CNC tienen generalmente un husillo que hace girar una herramienta (en el caso de fresadoras) o un material 
(en el caso de tornos). El husillo puede o no ser controlado por el software de CNC. Este controlador ofrece soporta hasta 8
husillos, los que pueden ser individualmente controlados y pueden moverse simultáneamente a diferentes velocidades y direcciones.


Refrigerante
------------

Si una máquina tiene bombeo de refrigerante tipo niebla o líquido pueden ser controlados mediante código G.

Control de Override
-------------------

Una máquina de control numérico tiene generalmente perillas para manejar el override de la velocidad de avance. La función que cumple es 
darle al operario un manejo físico para poder disminuir la velocidad de avance, tanto en el modo automático como en el modo manual (Jogging).
Es usual que tabién posea un control de override de la velocidad de husillo.

Interruptor de Bloqueo de Código
--------------------------------

Es posible que las máquinas CNC tengan un interruptor que habilita o desahilita la lectura de código G que esté bloqueado. Para más información vea 
la :ref:`sección de interacciones <refBlockDelete>`.

Interruptor Opcional de Parada
------------------------------

Es posible también que la máquina tenga un interruptor para activar o desactivar pausas desde el código G. Para más información vea la 
:ref:`sección de interacciones <refStopSwitch>`.

Componentes de Control y Datos
==============================

Ejes Lineales
-------------

Los ejes X, Y a Z forman un sistema coordenado ortogonales dextrógiro (sigue la regla de la mano derecha). La posición de los mecanismos de
movimiento lineal se expresa mediante las coordenadas en cada eje.

Ejes Rotativos
--------------

La posición de los ejes rotacionales se mide en grados con sentido positivo en sentido antihorario visto desde el extremo positivo del eje 
X, y o Z correspondiente. La posición angular incrementa sin límites al girar en sentido antihorario (no vuelve a cero cada vez que da una
vuelta completa) y disminuye sin límites cunado gira en sentido horario. Esta notación se utiliza independiente de si existe un límite mecánico 
de los ejes.

Punto de Control
----------------

El punto de control es el punto cuya posición y movimiento se controla. Cuando el decalaje de herramienta es cero, este punto se ubica en el 
eje del husillo a cierta distancia fija del extremo del husillo (también se lo llama punto de origen), usualmente cerca del extremo del 
portaherramienta. La ubicación del punto de control se puede desplazar fuera a lo largo del eje del husillo especificando un valor positivo 
para el largo de herramienta. En fresadoras, este valor es normalmente el largo de herramienta actualmente en uso, para que el punto de control se corrresponda
con el filo de la herramienta. En los tornos, el largo de herramienta se debe especificar en las direcciones de los ejes X y Z, y el punto de control se
ubica en la punta de la herramienta o bien ligeramente afuera de la misma, en la intersección de las caras del inserto.

Movimiento Lineal Coordinado
----------------------------

Para mover la herramienta a lo largo de una trayectoria especificada el controlador necesita coordinar el movimiento de varios ejes.
Para que el movimiento siga una trayectoria recta entre dos puntos, en cada punto del movimiento cada eje debe avanzar proporcionalmente 
lo mismo entre su posición inicial y final. A su vez se producen aceleraciones sobre esa dirección de movimiento. La velocidad alcanzada
depende de la velocidad programada; del límite de velocidad de la máquina o a veces se ve limitada por la velocidad máxima de uno de los 
ejes, en esos casos, todos los ejes se mueven mas lento para mantener la línea recta de la trayectoria.

.. _refMachineFeedRate:

Velocidad de Avance
-------------------

La velocidad a la que se mueve el punto de control en movimientos a velocidad constante puede ser determinada por el usuario. En el controlador
la velocidad de avance se interpreta en una de las siguientes formas (a no ser que esté activo la velocidad de avance por inversa del tiempo o
avance por revolución de husillo, casos que se pueden ver en la sección :ref:`Modos G93-G94-G95 <refG93>`).

* Si alguno de los ejes XYZ se mueve, F es la velocidad medida en cantidad de unidades por minuto en el sistema cartesiano XYZ, y todos los otros ejes (ABCUVW) se mueven de manera de arrancar y terminar de forma coordinada.

* De otro modo, si algún eje UVW se mueve, F es la velocidad medida en cantidad de unidades por minuto en el sistema cartesiano UVW, y todos los otros ejes (ABC) se mueven de manera de arrancar y terminar de forma coordinada.

* De lo contrario, el movimiento es puramente rotacional y F es la velocidad de rotación en grados por minuto en el sistema pseudo cartesiano ABC.

Refrigerante
------------

El bombeo de refrigerante ya sea en forma de niebla o líquido pueden ser encendidos independientemente. Ver la sección :ref:`Modos M7-M8-M9 <refM7>`.

Pausa
-----

Una máquina CNC puede ser programada para realizar una pausa (no realizar movimientos) por un determinado tiempo. El uso más común es utilizar pausas para
permitir el corte de las virutas, ya que el husillo queda girando en la espera. Independientemente del modo de control (ver sección de :ref:`Trayectoria <refTrajectoryMode>`)
de trayectoria la máquina frenará exatamente en la posición del punto programado anterior a la pausa, como si estuviera en el modo de seguimiento. 

Unidades
--------

Las unidades utilizadas para las distancias a lo largo de los ejes X, Y y Z pueden ser medidas en milímetros o en pulgadas. Las unidades para todas los otros 
parámetros involucradas en el control de la máquina no pueden ser cambiadas. Los diferentes parámetros utilizan unidades específicas. 
La posición de los ejes rotacionales se miden en grados. La velocidad de avance se miden en la unidad de longitud activa por minuto, o grados por minuto, o 
unidades de longitud por revolución de husillo, como se lo describe en la sección :ref:`G93 <refG93>`.

Plano de trabajo
----------------

Siempre hay un plano de trabajo seleccionado, que debe ser el plano XY, el plano YZ o el plano XZ de la máquina. 
Este plano de trabajo se utiliza para, entre otras cosas, orientar las correcciones de posición debido al largo y radio de herramienta, tmabién se utiliza para definir
cotas de despeje en ciclos cerrados.
Para más información ver las secciones :doc:`toolCompensation` y :ref:`G80 a G89 <refG80>`.

Cambiador de Herramientas
-------------------------

La mayoría de las máquinas CNC poseen un cambiador de herramientas en donde se almacenan las herramientas a utilizar. Algunos son en posiciones fijas, otros poseen un 
carusel o son de otro tipo. Una diferencia desde el punto de vista del controlador es si las posiciones de cada herramienta es fija o intercambiable.

Cambio de Herramientas
----------------------

Es posible en la mayoría de las máquinas programar en el código G un cambio de herramienta que la máquina realiza de manera automática.

Cambiador de Piezas
-------------------

Algunas máquinas poseen un cambiador de piezas, que permite realizar la operación de carga/descarga de una pieza mientras se está mecanizando otra pieza simultáneamente.
Luego de la finalización del ciclo, la pieza a trabajar entra a la zona de mecanizado y la pieza finalizada sale para su descarga.

.. _refTrajectoryMode:

Modo de Control de Trayectoria
------------------------------

Las máquinas CNC pueden ser programadas para ejecutar uno de los siguientes 3 modos de control de trayectoria. 1. Modo de posicionamiento preciso y frenado, 2. Modo de 
posicionamiento preciso o 3. Modo de suavizado de trayectoria. En el primer modo el movimiento se frena en cada punto programado. En el segundo la máquina sigue la 
trayectoria de la manera más precisa posible, frenando o bajando la velocidad cerca de vértices y en el modo de suavizado, la trayectoria puede ser redondeada cerca 
de los vértices para intentar seguir la velocidad de avance programada.
Para más información ver las secciones :ref:`G61 y G64 <refG61>`.


Interacción con Interruptores y Perillas
========================================

El controlador interactúa con varios interruptores y comandos. Las interacciones se describen brevemente en las siguientes secciones.

Perillas de Override
--------------------

El controlador interpreta los comandos *M48* y *M49* para deshabilitar y habilitar la influencia de las perillas de override.
Para ciertos movimientos, como el roscado, se desabilitan los controles de override automáticamente.

El controlador reacciona a los valores de los overrides cuando el control está activo.

Para más información ver las secciones :ref:`G48 y G49 <refM48>`.

.. _refBlockDelete:

Interruptor de Bloqueo de Líneas
--------------------------------

Si el interruptor de comentarios de líneas está activo, las líneas de código G que empiezan con una barra inclinada (caracter de bloque de línea)
no se interpretan. Si el interruptor está inactivo, éstas líneas son intepretadas y ejecutadas. Normalmente el interruptor de bloqueo de líneas debe
ser configurado antes de empezar a ejecutar el programa.

.. _refStopSwitch:

Interruptor Opcional de Parada
------------------------------

Si el interruptor está habilitado y se encuentra el cógido *M1*, la ejecución del programa se pausa.


Tabla de herramientas
=====================

La tabla de herramientas guarda la información de qué herramientas están disponibles en el cambiador de herramientas y en qué posiciones
se encuentran. El nombre del archivo, con extensión .tbl, que contiene a la tabla se encuentra en el archivo de configuración .ini::

   [EMCIO]
   
   # tool table file
   TOOL_TABLE = tooltable.tbl


Parámetros
==========

La máquina CNC mantiene una serie de parámetros numéricos que utiliza el sistema (*RS274NGC_MAX_PARAMETERS*). Muchos de estos parámetros 
tienen funciones específicas y son persistentes, es decir, no se borran al reinciar la máquina. Todos los parámetros están disponibles 
para su uso desde los programas de código G.
El formato del archivo de parámetros se muestra en la tabla siguiente. Cada línea línea del archivo contiene el número de índice del parámetros
en la primer columna y el valor del mismo en la segunda columna. La tercer columna se utiliza para comentarios pero no es leída por el controlador.
Los parámetros disponibles deben tener un índice desde 1 a 5400 y su numeración debe ser ascendente.

+----------------------+-----------------------+-----------------------------+
| Índice de Parámetro  | Valor de Parámetro    | Comentario                  |
+----------------------+-----------------------+-----------------------------+
|       5161           |  0.0                  | G28 Origen X                |
+----------------------+-----------------------+-----------------------------+
|       5162           |  0.0                  | G28 Origen Y                |
+----------------------+-----------------------+-----------------------------+

Para más información ver la sección de :ref:`Parámetros <refParameters>`.

















