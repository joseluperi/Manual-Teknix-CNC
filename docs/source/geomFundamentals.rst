Fundamentos Geométricos
=======================

En esta sección se muestran las definiciones de sistemas de referencia; coordenadas absolutas y relativas; centros de coordenadas y 
decalajes que son necesarios para la correcta definición de las posiciones.

.. _sistCoords:

Sistemas coordenados
--------------------

A los efectos de que el control pueda interpretar los datos de posición, éstos deben estar expresados en un sistema coordenado 
de referencia. Normalmente se utilizan sistemas de referencia ortogonales cuyas componentes son los ejes X, Y y Z.

Regla de la Mano Derecha
^^^^^^^^^^^^^^^^^^^^^^^^

Los sistemas ortogonales utilizados son dextrógiros, es decir que siguen la regla de la mano derecha.

.. figure:: images/rightHandRule.png
   :width: 200
   
   Regla de la mano derecha.
   
   * El dedo pulgar apunta en la dirección del eje X positivo.
   * El dedo índice apunta en la dirección del eje Y positivo.
   * El dedo medio apunta en la dirección del eje Z positivo.
   
Normalmente para operaciones de fresado el plano horizontal corresponde al plano contenido por los ejes X e Y.

.. figure:: images/millingCoordSys.png
   :width: 200
   
   Sistema coordenado para fresado.

Normalmente para operaciones de torneado el eje del husillo correspode al eje Z.

.. figure:: images/turningCoordSys.png
   :width: 200
   
   Sistema coordenado para torneado. 


Coordenadas Absolutas
^^^^^^^^^^^^^^^^^^^^^

Cuando se utilizan coordenadas absolutas, las posiciones están referidas al origen del sistema coordenado de referencia.
| Aplicado al movimiento de herramientas significa la posición a la que se moverá la herramienta.

Ejemplo para fresado

.. figure:: images/absoluteMillingCoords.png
   :width: 200
   
   P1 corresponde a X20 Y35
   P2 corresponde a X50 Y60
   P3 corresponde a X70 Y20

Ejemplo para torneado

.. figure:: images/absoluteTurningCoords.png
   :width: 200
   
   P1 corresponde a X25 Z-7.5
   P2 corresponde a X40 Z-15
   P3 corresponde a X40 Z-25
   P4 corresponde a X60 Z-35

Coordenadas Relativas
^^^^^^^^^^^^^^^^^^^^^

Frecuentemente nos encontramos con planos que tienen cotas relativas, es decir que la posición de un punto está referido a otro punto.
Para poder evitar la conversión a cotas absolutas se pueden utilizar coordenadas relativas, que refieren a la posición de la definición
del punto previo. 
| Aplicado al movimiento de herramientas significa la distancia que la herramienta se trasladará.

Ejemplo para fresado

.. figure:: images/relativeMillingCoords.png
   :width: 200
   
   P1 corresponde a X20 Y35 ; (respecto al origen de coordenadas)
   P2 corresponde a X30 Y20 ; (respecto a P1)
   P3 corresponde a X20 Y-35 ; (respecto a P2)

Ejemplo paratorneado

.. figure:: images/relativeTurningCoords.png
   :width: 200
   
   G90 P1 corresponde a X25 Z-7.5; (respecto al origen de coordenadas)
   G91 P2 corresponde a X15 Z-7.5 ; (respecto a P1)
   G91 P3 corresponde a Z-10 ; (respecto a P2)
   G91 P4 corresponde a X20 Z-10 ; (respecto a P3)

Nota: Cuando DIAMOF o DIAM90 está activo, la posición se programa con la dimensión del radio con G91.

Planos de Trabajo
^^^^^^^^^^^^^^^^^

Al programar es necesario especificar el plano en el que se está trabajado para que el sistema de control realizar los cálculos geométricos y pueda utilizar de manera correcta los decalajes de herramientas. 
El plano de trabajo se definen por medio de los códigos G17, G18 o G19 y su definición queda determinada por los dos ejes del sistema coordenado que lo contienen.

* G17 es el plano definido por los ejes X e Y.
* G18 es el plano definido por los ejes X e Z.
* G19 es el plano definido por los ejes Y e Z.

.. figure:: images/planesMilling.png
   :width: 200
   
   Planos de trabajo para fresado.

.. figure:: images/planesTurning.png
   :width: 200
   
   Planos de trabajo para torneado.


.. _centrosCoords:


Centros de Coordenadas
----------------------


.. _centrosCoords:


Posición de Sistemas de Referencia
----------------------------------

.. _decaPieza:

Decalaje de Pieza
-----------------

.. _decaHerram:

Decalaje de Herramientas
------------------------



