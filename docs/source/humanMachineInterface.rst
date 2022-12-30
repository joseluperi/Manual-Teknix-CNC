Interfaz de Usuario
###################
      
En esta sección se describen las funcionalidades y modo de operación de interfaz de usuario.
Básicamente se puede dividir a la interfaz en su pantalla táctil principal por una parte y el teclado, botones y perillas por otro.

.. _teclados:

Teclado y botones
=================

El teclado y botones configura la parte física de la interfaz de usuario. En su versión usual, el control cuenta con los siguientes elementos.

**Botón de emergencia**

El botón de emergencia está ubicado en una posición accesible para el operador. En caso de una emergencia se deberá presionar el botón, lo que hará
que el control numérico frene lo más rápido posible el husillo y el movimiento de la máquina. En caso de emergencia todas las funciones que se manejen por el 
PLC (Controlador Lógico Programable) de la máquina pueden ser llevadas al modo de seguridad con el que se configuren.
Para desactivar el accionamiento del botón de emergencia el operador debe girarlo, lo que hará que salga de su posición retraída. 
Desactivar el botón de emergencia no sacará a la máquina del estado de emergencia ni iniciará el giro del husillo o del movimiento.
Luego de la activación de la emergencia no es necesario realizar el referenciado de los ejes nuevamente.

.. figure:: images/emergencyButton.png
   :width: 150
   
   Botón de parada de emergencia

**Rueda para Jogging**

La rueda para jogging se utiliza para cambiar la posición de forma manual, permite mover el eje seleccionado en ambos sentidos de forma intuitiva.
La velocidad de movimiento y por ende la diferencia de posición que representa cada pulso de la rueda se elige con el selector de escala que se describe a continuación.
Para que funcione el controlador debe estar en modo manual y sin errores pendientes de confirmación.

.. figure:: images/joggingWheel.png
   :width: 150
   
   Botón de parada de emergencia

**Selector de escala**

Se utiliza para seleccionar la escala con la que trabaja la rueda de jogging. Para movimientos más largos elija escalas más grandes y para posicionar con
mayor presición elija escalas más pequeñas.

.. figure:: images/scaleSelector.png
   :width: 90
   
   Selector de escala

**Selector de eje**

Se utiliza para seleccionar el eje que se moverá mediante la rueda de jogging cuando el controlador esté en modo de movimiento manual.

.. figure:: images/axisSelector.png
   :width: 110
   
   Selector de escala


**Perilla de override de velocidad de avance**

.. figure:: images/knobFeedOverride.png
   :width: 110
   
   Perilla de override de velocidad de avance

La perilla de override permite reducir la velocidad de avance real respecto a la velocidad de avance programada. La escala elegible va en un rango desde el 0 al 100 %.


Pantalla Táctil
===============

La pantalla táctil brinda las funcionalidades de manejo y edición de archivos; visualización del estado de máquina; editor de decalajes,
incluido un gestor de herramientas; ingreso de código G manual directo y visualizador de alarma y mensages, entre otras.
Las funcionalidades y modos de operación se decribe en las siguientes secciones.


.. _pantallaMaquina:

Pantallas de Máquina
====================


La pantalla inicial al iniciar el control es la pantalla de máquina, en donde se puede ver el estado general de la misma.

.. figure:: images/HMIscreenMachine.png
   :width: 750
   
   Pantalla principal de máquina

En la parte superior posee una barra horizontal que cuando no hay alarmas activas tiene la leyenda TEKNIX. 

Abajo de la barra superior, en el sector izquierdo se ven las posiciones actuales de los ejes y la distancia que deberán recorrer los mismos para llegar al punto final de la próxima instrucción.
Estas coordenadas se pueden ver en el sistema de coordenadas de la máquina o en el sistema de coordenadas de la pieza vigente. Para cambiar la visualización entre el sistema 
de coordenadas de máquina y de pieza se utilizan los botones *MCS* y *WCS* ubicados en la barra lateral de la derecha.

En la parte inferior de esta sección se muestra el sistema coordenado activo, es decir con el que se referencian los comandos de posición.

Abajo de la barra superior, en el sector derecho esta pantalla muestra la información sobre la herramienta actual, incluyendo: número de herramienta; descripción; filo seleccionado; orientación; 
radio de filo y decalajes. Abajo de la información de la herramienta se muestra la velocidad de avance actual y la programada, en las unidades correspondiente y el override.
Abajo de esto se muestra la velocidad de husillo actual y programada, con un símbolo que indica si está frenado o en qué sentido está girando.

Abajo de estas secciones se muestra el programa en ejecución. Si no ha sido seleccionado un programa para su ejecución esta parte de la pantalla estará vacía.

En el extremo inferior esta pantalla muestra una barra horizontal en donde se muestran íconos, cuyos rebordes se remarcan de verde cuando están activos.
De izquierda a derecha se muestra si está activa:

   * Emergency Stop - Parada de emergencia
   * Power - Energizado
   * Home All - Referenciado de ejes
   * SBL - 
   * Spindle Cw - Husillo girando en sentido horario
   * Spindle Cw - Husillo frenado
   * Spindle Ccw - Husillo girando en sentido antihorario

En el nivel superior se muestra el botón *Set WO* que permite modificar los decalajes del sistema de coordenadas actual, pantalla que se muestra en la siguiente figura.

.. figure:: images/HMIscreenSetWorkOffset.png
   :width: 750
   
   Edición de decalajes de sistemas coordenados actual


En el extremo derecho la pantalla tiene una barra vertical con botones. Esta barra se encuentra en diferentes pantallas en las que las acciones de los botones cambian según
el contexto.

En esta pantalla están activos los botones:

   * Active G Codes
   * MCS / WCS

En cuanto al botón *MCS / WCS* como ya se mencionó se utiliza para cambiar el sistema coordenado para la visualización de la posición actual.

Al presionar en el boton *Active G Codes* se despliega un listado de los códigos activos en cada estado modal, que se muestra en la siguiente figura.

.. figure:: images/HMIscreenMachineActiveGcodes.png
   :width: 750
   
   Pantalla principal de máquina, códigos activos

En la parte superior de la barra lateral derecha se muestran dos íconos. El de la izquierda muestra qué pantalla está activa y el de la derecha muestra qué modo de operación está activo.
Los íconos y su significado se muestran en las siguientes figuras.

.. figure:: images/HMImachineIcon.png
   :width: 35
   
   Símbolo de Pantalla de Máquina

.. figure:: images/HMIoffsetIcon.png
   :width: 35
   
   Símbolo de Pantalla de Decalajes

.. figure:: images/HMIeditorIcon.png
   :width: 35
   
   Símbolo de Pantalla de Editor

.. figure:: images/HMIprogramsIcon.png
   :width: 35
   
   Símbolo de Pantalla de Programas

.. figure:: images/HMIdiagnosisIcon.png
   :width: 35
   
   Símbolo de Pantalla de Diagnóstico

.. figure:: images/HMIjoggingIcon.png
   :width: 35
   
   Símbolo de Modo de Jogging

.. figure:: images/HMImdaIcon.png
   :width: 35
   
   Símbolo de Modo de Input Manual Directo

.. figure:: images/HMIautoIcon.png
   :width: 35
   
   Símbolo de Modo de Automático

Al presionar sobre estos íconos se activa el menú principal, pantalla que se muestra en la siguiente figura.

.. figure:: images/HMIscreenMenu.png
   :width: 750
   
   Menu principal

En la barra inferior del menú principal se encuentra de izquierda a derecha el botón *Machine* que lleva a la pantalla de máquina descripta en esta sección.
Luego se encuentra *OFFSETS* que lleva a la pantalla de Decalajes. El siguiente botón es *EDITOR* que lleva a la pantalla de edición de programas. 

Todas estas pantallas y su uso se muestran en las siguientes secciones.





   .. _HMIoffset:


Pantalla de Decalajes
=====================


**Editor de herramientas**


.. figure:: images/HMItoolList.png
   :width: 750
   
   Editor de herramientas



.. figure:: images/HMItoolWear.png
   :width: 750
   
   Desgaste de herramientas


.. figure:: images/HMItoolStorage.png
   :width: 750
   
   Almacén de herramientas


**Decalajes de sistemas coordenados**

.. figure:: images/HMIworkOffset.png
   :width: 750
   
   Decalajes de sistemas coordenados


**Variables de usuario**


.. figure:: images/HMIuserVariable.png
   :width: 750
   
   Variables de usuario



.. _editProgramas:


Editor de Programas
===================

en donde se abren, editan los archivos de código G 



.. figure:: images/HMIscreenEditor.png
   :width: 750
   
   Listado de achivos



.. figure:: images/HMIscreenEditorOpenedFile.png
   :width: 750
   
   Editor de achivos



.. figure:: images/HMIscreenEditorMark.png
   :width: 750
   
   Editor de achivos, selección de líneas


.. figure:: images/HMIscreenEditor2files.png
   :width: 750
   
   Editor de achivos, varios archivos


Pantalla de Programa
====================



.. figure:: images/HMIscreenProgram.png
   :width: 750
   
   Pantalla de programa




.. _diagnostico:

Diagnóstico
===========





.. figure:: images/HMIdiagnosis.png
   :width: 750
   
   Pantalla de diagnóstico


Jogging
=======



Referenciado
============






Ingreso Manual Directo
======================



.. figure:: images/HMImanualDirectInput.png
   :width: 750
   
   Pantalla para ingreso manual directo


Modo Automático
===============


.. figure:: images/HMIautomatic.png
   :width: 750
   
   Pantalla en modo de ejecución automático




Búsqueda de Línea
-----------------


.. figure:: images/HMIblockSearch.png
   :width: 750
   
   Búsqueda de línea, solicitud para ejecutar








