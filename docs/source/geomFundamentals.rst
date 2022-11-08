Fundamentos Geométricos
=======================

En esta sección se muestran las definiciones de sistemas de referencia; coordenadas absolutas y relativas; centros de coordenadas y decalajes que son necesarios para la correcta definición de las posiciones.

.. _sistCoords:

Sistemas coordenados
--------------------

A los efectos de que el control pueda interpretar los datos de posición, éstos deben estar referidos a un sistema coordenado de referencia. Normalmente se utilizan sistemas de referencia ortogonales cuyas componentes son los ejes X, Y y Z.

Regla de la Mano Derecha
^^^^^^^^^^^^^^^^^^^^^^^^

Los sistemas ortogonales utilizados son dextrógiro, es decir que siguen la regla de la mano derecha.

.. figure:: images/rigthHandRule.png
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

Coordenadas Relativas
^^^^^^^^^^^^^^^^^^^^^

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



