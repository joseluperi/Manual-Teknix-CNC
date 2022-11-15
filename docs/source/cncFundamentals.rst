Fundamentos de CNC
##################

En esta sección se describen los elementos del lenguage de código G, su estructura, comandos y expresiones.

.. _estrCNC:

Estructura del Código G
=======================

| El lenguaje de código G está conformado por líneas de código, también llamadas bloques. Cada línea puede incluir comandos para realizar varias cosas. 
| Las líneas pueden ser agrupadas en un archivo que define una rutina o pueden ser agrupadas para formar subrutinas o funciones. 
| Una línea típica de código consiste en una numeración opcional al comienzo seguida de uno o más términos, también llamados palabras. Un término consiste en una letra
  seguida de un número o algo que se evalúa y se convierte en un número. Ese término puede dar un comando o proveer un argumento a un comando. 
| Por ejemplo G1 X30 es una línea de código con dos términos. G1 es un comando que solicita el movimiento en línea recta a la velocidad programada a determinado punto, y X30 provee un 
  argumento que especifica que la coordenada X debe ser de 30 en el punto al final del movimiento. 
| La mayoría de los comandos empieza con la letra G o con la letra M, que hacen referencia a comandos Generales y Misceláneos respectivamente. 
| Los programas no poseen un indicador de inicio y fin. Un programa puede estar en un solo archivo o puede estar repartido
  en varios archivos. Se pueden utilizar los comandos M2 o M30 opcionalmente para indicar el fin de un programas. 

Formato
-------

Una línea de comando está compuesta de los siguientes elementos, en orden, con un límite de 256 caracteres:

* Un caracter opcional, la barra ( / ) que indica bloques de comentarios. 
* Un número de línea que es opcional. 
* Un número variable de términos, parámetros y comentarios. 
* Un marcador de fin de línea. 

| Cualquier término que no esté explícitamente permitido producirá un error. 
| Los espacios y tabulaciones están permitidos en cualquier parte del código y no modifican el significado del mismo,
  esto hace que algunos aspectos extraños sean correctos, por ejemplo: 
| G0X +12. 5Y70 es equivalente a G0 x+12.5 Y70 y a G0 X 12.5 Y 70. 
| Las líneas vacías también están permitidas, no tienen efecto en el código. 
| El uso de maýusculas o minúsculas es indiferente y no cambia el significado. 
| El número de línea se forma con la letra N seguido de un número entero, opcionalmente seguido de un punto y otro número entero. 
  Por ejemplo, N103 y N103.12 son números de línea válidos. Pueden estar repetidos y estar definidos en orden creciente o no, aunque 
  la práctica usual es evitarlos o en caso de utilizarlos definirlos en orden creciente. 
| Los términos están formados por cualquier letra de las que se muestarn en la siguente tabla: 

+-------+-----------------------------------------------------------------------+
| Letra |  Significado                                                          |
+=======+=======================================================================+
|   A   | Eje A de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   B   | Eje B de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   C   | Eje C de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   D   | Radio de compensación de herramienta                                  |
+-------+-----------------------------------------------------------------------+
|   F   | Velocidad de avance                                                   |
+-------+-----------------------------------------------------------------------+
|   G   | Función general (tabla de grupos modales)                             |
+-------+-----------------------------------------------------------------------+
|   H   | Índice de longitud de herramienta                                     |
+-------+-----------------------------------------------------------------------+
|   I   | Distancia relativa en X para círculos y ciclos cerrados G87           |
+-------+-----------------------------------------------------------------------+
|   J   | Distancia relativa en Y para círculos y ciclos cerrados G87           |
+-------+-----------------------------------------------------------------------+
|   K   | Distancia relativa en Z para círculos y ciclos cerrados G87           |
|       |                                                                       |
|       | Fracción de movimiento de husillo para movimientos sincronizados G33  |
+-------+-----------------------------------------------------------------------+
|   L   | Parámetros genericos para G10, M66 y otros                            |
+-------+-----------------------------------------------------------------------+
|   M   | Misceláneos                                                           |
+-------+-----------------------------------------------------------------------+
|   N   | Número de bloque                                                      |
+-------+-----------------------------------------------------------------------+
|   P   | Tiempo de espera para ciclos con G4                                   |
|       | Código usado con G10                                                  |
+-------+-----------------------------------------------------------------------+
|   Q   | Incremento de velocidad de avance en ciclos G73, G83                  |
+-------+-----------------------------------------------------------------------+
|   R   | Radio de círculo o plano de ciclo cerrado                             |
+-------+-----------------------------------------------------------------------+
|   S   | Velocidad de Husillo                                                  |
+-------+-----------------------------------------------------------------------+
|   T   | Selección de herramienta                                              |
+-------+-----------------------------------------------------------------------+
|   U   | Eje U de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   V   | Eje V de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   W   | Eje W de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   X   | Eje X de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   Y   | Eje Y de máquina                                                      |
+-------+-----------------------------------------------------------------------+
|   Z   | Eje Z de máquina                                                      |
+-------+-----------------------------------------------------------------------+

Algunas de estas letras (I,J,K,L,P,R) pueden tener diferentes significados de acuerdo al contexto. Las letras que se refieren a nombres de ejes no son válidos en una
máquina que no tiene ese eje.

Números
-------

| Las siguientes reglas se aplican para los números (explícitos), en las que un dígito es un caracter del 0 al 9.
| Un número consiste de un signo + o signo - que es opcional, seguido de ningún a muchos dígitos, luego puede tener 
  un punto decimal seguido de ningún a muchos dígitos, siempre y cuando el número tenga al menos un dígito en alguna parte.
| Hay dos tipos de números, decimales y enteros, que se diferencian por poseer o no un punto decimal.
| Los números pueden tener un número variable de dígitos, siempre que respeten el límite del largo de línea máximo, aunque
  se utilizarán alrededor de 17 cifras significativas.
| Se asume que un número sin signo es positivo.

Secuencia
---------

A los efectos de mantener el formato de los bloques lo más claros posibles es recomendable seguir el siguiente orden:

+-------------+------------------------------------------------------------------------+
| Término     | Significado                                                            |
+=============+========================================================================+
| N           | Número de bloque                                                       |
+-------------+------------------------------------------------------------------------+
| G           | Función de preparación                                                 |
+-------------+------------------------------------------------------------------------+
| X, Y, Z     | Datos de posición                                                      |
+-------------+------------------------------------------------------------------------+
| F           | Velocidad de avance                                                    |
+-------------+------------------------------------------------------------------------+
| S           | Velocidad de husillo                                                   |
+-------------+------------------------------------------------------------------------+
| T           | Herramienta                                                            |
+-------------+------------------------------------------------------------------------+
| D           | Corrección de herramienta                                              |
+-------------+------------------------------------------------------------------------+
| M           | Función miscelánea                                                     |
+-------------+------------------------------------------------------------------------+
| H           | Función auxiliar                                                       |
+-------------+------------------------------------------------------------------------+

Nota: Ciertos términos pueden usarse repetidamente en un bloque (ej. G..., M..., H... )

Comportamiento Modal
--------------------

Muchos de los comandos causan un cambio del modo en el cotrolador, ese modo queda activado hasta que otro comando lo cambia explícitamente o implícitamente. Éstos comandos son
llamados comandos modales. Por ejemplo, si se prende el bombeo de refrigerante, permanece prendido hasta que explícitamente se lo apaga. Los comandos de movimiento también son 
modales. Si se define un comando G1 (movimiento lineal) en una línea, por ejemplo, será ejecutado nuevamente en las líneas siguientes si uno o más términos modifican posiciones 
de ejes, a no ser que se defina un comando en las líneas siguientes que explícitamente cancele el movimiento.

Los comandos no modales tienen efecto sólo en la línea en la que están definidos. Por ejemplo, G4 (espera) es no modal.

Grupos Modales
--------------

Los comandos modales está clasificados en grupos modales, en los que sólo un comando del grupo puede estar activo en determinado momento. En general los grupos modales contienen 
comandos para los que es lógicamente imposible que dos elementos tengan efecto al mismo tiempo, como por ejemplo medidas en milímetros y medidas en pulgadas. Una máquina puede
tener activos varios modos al mismo tiempo, con un modo de cada grupo modal aplicados. Los grupos modales se muestran en la siguiente tabla:

Tabla de Grupos Modales para códigos G

+---------------------------------------------------+--------------------------------------------------------------+
| Tipo de Grupo Modal                               | Términos del Grupo                                           |
+===================================================+==============================================================+
| Códigos no modales (Grupo 0)                      | G4, G10, G28, G30, G52, G53, G92, G92.1, G92.2, G92.3        |
+---------------------------------------------------+--------------------------------------------------------------+
| Movimiento (Grupo 1)                              | G0, G1, G2, G3, G33, G38.n, G73, G76, G80, G81               |
|                                                   | G82, G83, G84, G85, G86, G87, G88, G89                       |
+---------------------------------------------------+--------------------------------------------------------------+
| Selección de plano (Grupo 2)                      | G17, G18, G19, G17.1, G18.1, G19.1                           |
+---------------------------------------------------+--------------------------------------------------------------+
| Modo de distancia (Grupo 3)                       | G90, G91                                                     |
+---------------------------------------------------+--------------------------------------------------------------+
| Modo de distancia de círculos IJK (Grupo 4)       | G90.1, G91.1                                                 |
+---------------------------------------------------+--------------------------------------------------------------+
| Modo de velocidad de avance (Grupo 5)             | G93, G94, G95                                                |
+---------------------------------------------------+--------------------------------------------------------------+
| Unidades (Grupo 6)                                | G20, G21                                                     |
+---------------------------------------------------+--------------------------------------------------------------+
| Compensación de radio de herramienta (Grupo 7)    | G40, G41, G42, G41.1, G42.1                                  |
+---------------------------------------------------+--------------------------------------------------------------+
| Largo de herramienta (Grupo 8)                    | G43, G43.1, G49                                              |
+---------------------------------------------------+--------------------------------------------------------------+
| Modo de retorno de ciclos cerrados (Grupo 10)     | G98, G99                                                     |
+---------------------------------------------------+--------------------------------------------------------------+
| Sistemas de coordenadas (Grupo 12)                | G54, G55, G56, G57, G58, G59, G59.1, G59.2, G59.3            |
+---------------------------------------------------+--------------------------------------------------------------+
| Modo de control (Grupo 13)                        | G61, G61.1, G64                                              |
+---------------------------------------------------+--------------------------------------------------------------+
| Velocidad de husillo (Grupo 14)                   | G96, G97                                                     |
+---------------------------------------------------+--------------------------------------------------------------+
| Modo de diametral de tornos (Grupo 15)            | G7, G8                                                       |
+---------------------------------------------------+--------------------------------------------------------------+

Tabla de Grupos Modales para códigos M

+---------------------------------------------------+--------------------------------------------------------------+
| Tipo de Grupo Modal                               | Términos del Grupo                                           |
+===================================================+==============================================================+
| Parada (Grupo 4)                                  | M0, M1, M2, M30, M60                                         |
+---------------------------------------------------+--------------------------------------------------------------+
| Husillo (Grupo 7)                                 | M3, M4, M5                                                   |
+---------------------------------------------------+--------------------------------------------------------------+
| Refrigerante (Grupo 8)                            | (M7 M8 pueden estar ambos activos), M9                       |
+---------------------------------------------------+--------------------------------------------------------------+
| Control de override (Grupo 9)                     | M48, M49                                                     |
+---------------------------------------------------+--------------------------------------------------------------+
| Grupo definido por el usuario (Grupo 10)          | M100 - M199                                                  |
+---------------------------------------------------+--------------------------------------------------------------+

Para varios de los modos, cuando una máquina está lista para aceptar comandos, un elemento del grupo debe estar en efecto. Hay configuraciones por defecto para estos modos.
Cuando la máquina se prende o se reinicializa, los valores por defecto se activan.
El grupo 1 es el grupo de movimiento. Un comando de este grupo debe estar siempre en efecto, el que es llamado modo de movimiento vigente.
Es un error escribir código G del grupo 1 y código G del grupo 0 en la misma línea si ambos hacen referencia a ejes. Si hay un término del grupo 1 implícitamente en efecto 
en una línea (al ser definido en alguna línea anterior) y el comando del grupo 0 que hace referencia al eje en la misma línea, la actividad del código G del grupo 1 se suspende
para esa línea. 

Comentarios
-----------

Es posible agregar comentarios a las líneas del código G que ayudan a esclarecer la intención del programador. Los comentarios pueden ser escritos en la línea mediante el uso de 
los paréntesis () o estar al final de la línea utilizando el signo de punto coma ; .
Los comentarios pueden utilizarse entre los términos pero no entre un término y su correspondiente parámetro.
Por ejemplo S0, S100 (determinar velocidad) F200 (velocidad) es válido, pero S(velocidad)100 F(velocidad) 200 no es correcto.

Hay algunos comentarios activos que **parecen** comentarios pero causan alguna acción, como (debug,..) o (print,..). Si hay varios comentarios en una línea, sólo el último comentario
será interpretado según estas reglas. Por lo tanto un comentario normal seguido de un comentario activo tendrá el efecto de desactivar el comentario activo. For ejemplo (foo)(debug,#1)
mostrará el valor del parámetro #1, sin embargo (debug,#1)(foo) no lo hará.

Un comentario definido por un punto coma es por definición el último comentarioen esa línea y será interpretado con la sintáxis de comentarios activos.

Mensajes
--------

Es posible mostrar un mensaje al operador desde el código con la función MSG(), por ejemplo MSG('Programa en ejecución') mostrará 'Programa en ejecución' al usuario. Si se requiere
una confirmación del operador para avanzar se puede utilizar el comando POPUP() que mostará el mensaje al operador en una ventana emergente y bloqueará la ejecución del programa
hasta que el operador confirme.


Parámetros
----------

| El lenguage CNC permite el uso de parámetros, lo que en otros lenguajes de programación se conoce como variables. Existen varios tipos de parámetros que tienen diferentes propósitos,
  que se describen a continuación. El único valor soportado como parámetros son los números de punto flotante, no hay parámetros con valores lógicos, de texto o enteros en el código G.
| Sin embargo, se pueden utilizar expresiones con operadores lógicos (AND, OR, XOR) y operadores de comparación (EQ, NE, GT, GE, LT, LE) y operadores que soportan aritmética de enteros
  como MOD, ROUND, FUP y FIX.
| Los parámetros difieren en su sintáxis, ámbito (scope), comportamiento cuando no están inicializados, modo, persistencia y propósito de uso.

**Sintáxis**

   Hay tres tipos de apariencia sintáctica:
   
   * Parámetro Numerad0  #4711
   * Parámetro por nombre, local  #<valorlocal>
   * Parámetro por nombre, global  #<_valorglobal>

**Ámbito (Scope)**

Los parámetros o variables son normalmente creadas y desechadas en la ejecución del código. El ámbito o scope de un parámetro es la parte del código donde un parámetro existe
la variable, éste puede ser Global, o Local dentro de una subrutina. Los parámetros creados dentro de una subrutina tienen scope o ámbito local, es decir que la variable existen dentro
de la subrutina pero la rutina que llama a esa subrutina no puede acceder a la misma. En cambio, las variables globales pueden ser accesibles en todo el código.

**Inicialización**

| Los parámetros o variables globales no inicializadas y parámetros de subrutina no usados dan el valor 0 cuando se los usa en una expresión.
| Los parámetros por nombre no inicializados dan error al ser usados en una expresión.

**Modo**

La mayoría de los parámetros son de lectura y escritura, sin embargo existen algunos parámetros predefinidos que no deben cambiar que son sólo de escritura. 
Pueden ser utilizados en una expresión pero no se les puede asignar un valor.

**Persistencia**

Al apagar el control numérico los parámetros volátiles pierden su valor. Todos los parámetros salvo los parámetros numerados son volátiles. Los parámetros persistentes
se guardan en un archivo con formato .var y sus valores son restaurados a sus valores pervios cuando el control se reinicia. Los parámetros volátiles son reiniciados a 
valor cero.

**Propósito**

* Parámetros de usuario
   | Parámetros numerados en el rango de 31 a 5000 y parámetros por nombre globales y locales, salvo los predefinidos.
   | Éstos están disponibles para propósitos generales, como guardar valores de punto flotante, resultados intermedios, etc. en la ejecución de u 
     programa.
   | Son de lectura y escritura.
* Parámetros de subrutinas
   Se utilizan para guardar los valores de los parámetros vigentes para pasarlos a un subrutina.
* Parámetros numerados
   La mayoría se utilizan para acceder a los decalajes de los sistemas de coordenadas.
* Parámetros de sistema 
   Usados para acceder a la versión del sistema que se utiliza. Son de solo lectura.

Expresiones
-----------

Las expresiones están formadas por una serie de caracteres que empiezan con un corchete izquierdo ( [ ) y terminan con un corchete derecho ( ] ). En el medio tiene números,
parámetros, operaciones matemáticas y/u otras expresiones. Las expresiones son evaluadas a un número. Las expresiones son evaluadas cuando se lee la línea, antes de la ejecución.
Un ejemplo es la expresión [1 + acos[0] - [#3 ** [4.0/2]]].

**Comparación y operadores lógicos**

+--------------------+--------------------------+
| Operador           | Significado              |
+====================+==========================+
| == o EQ            | Igual a                  |
+--------------------+--------------------------+
| <> O NE            | Desigual a               |
+--------------------+--------------------------+
| > o GE             | Mayor o igual a          |
+--------------------+--------------------------+
| < o GT             | Mayor a                  |
+--------------------+--------------------------+
| < o LE             | Menor o igual a          |
+--------------------+--------------------------+
| < o LT             | Menor a                  |
+--------------------+--------------------------+
| & o AND            | Y                        |
+--------------------+--------------------------+
| \| o OR            | O (inclusivo)            |
+--------------------+--------------------------+
| \^ o XOR           | O (exclusivo)            |
+--------------------+--------------------------+
| ! o NOT            | Negación                 |
+--------------------+--------------------------+

**Precedencia**

Los operadores están divididos en varios grupos de acuerdo a su precedencia. Si se definen juntas varias operaciones de diferente precedencia en una expresión 
(por ejemplo 2.0 / 3 * 1.5 - 5.5 / 11.0 ) se ejecutan las operaciones con mayor precedencia primero y luego las de menor precedencia. Si una expresión contiene 7
más de una operación con el mismo nivel de precedencia, se ejecuta de izquierda a derecha. Por ende, el ejemplo es equivalente a  [[[2.0/3]*1.5]-[5.5/11.0]], lo
que es equivalente a [1.0-0.5] que da como resultado 0.5.
Las operaciones lógicas y de módulo son ejecutadas para cualquier número real, no solo enteros. El número cero es quivalente al falso lógico, y cualquier número no 
nulo es equivalente al verdadero lógico.

+----------------------+-------------+
| Grupos de operadores | Precedencia |
+======================+=============+
| \**                  | Mayor       |
+----------------------+-------------+
| \* \/ MOD            |             |
+----------------------+-------------+
| \+ \-                |             |
+----------------------+-------------+
| EQ NE GT GE LT LE    |             |
+----------------------+-------------+
| AND OR XOR NOT       | Menor       |
+----------------------+-------------+

**Igualdades de punto flotante**

El lenguage permite solo valores de punto flotante, por lo que la presición en la representación de números reales es acotada. Es por esto que la igualdad o desigualdad de
dos valores de punto flotante es inherentemente problemática. El interpretador resuelve este problema al considerar que dos valores son iguales si la diferencia entre ambos 
es menor a 0.0001. Este valor se define como una variable persistente.

**Funciones**

+-------------------+-----------------------------------------------------------+
|       Función     |         Resultado                                         |
+===================+===========================================================+
|  ATAN[arg]/[arg]  | Inversa de la tangente en los cuatro cuadrantes           |
+-------------------+-----------------------------------------------------------+
|      ABS[arg]     | Valor absoluto                                            |
+-------------------+-----------------------------------------------------------+
|     ACOS[arg]     | Inversa del coseno                                        |
+-------------------+-----------------------------------------------------------+
|     ASIN[arg]     | Inversa del seno                                          |
+-------------------+-----------------------------------------------------------+
|      COS[arg]     | Coseno                                                    |
+-------------------+-----------------------------------------------------------+
|      EXP[arg]     | Número e elevando a la potencia dada                      |
+-------------------+-----------------------------------------------------------+
|      FIX[arg]     | Truncamiento a próximo entero hacia abajo                 |
+-------------------+-----------------------------------------------------------+
|    ROUND[arg]     | Truncamiento a entero más próximo                         |
+-------------------+-----------------------------------------------------------+
|       LN[arg]     | Logaritmo natural                                         |
+-------------------+-----------------------------------------------------------+
|      SIN[arg]     | Seno                                                      |
+-------------------+-----------------------------------------------------------+
|     SQRT[arg]     | Raíz cuadrada                                             |
+-------------------+-----------------------------------------------------------+
|      TAN[arg]     | Tangente                                                  |
+-------------------+-----------------------------------------------------------+
|    EXIST[arg]     | Existencia de un parámetro numerado                       |
+-------------------+-----------------------------------------------------------+

.. _practicasCNC:

Buenas prácticas
----------------

* Utilice una presición apropiada
   Use al menos 3 dígitos luego del punto decimal cuando las unidades están en milímetros y por los menos 4 cuando están en pulgadas.

* Utilice el espaciado consistentemente
   El código G es más legible cuando por lo menos hay un espacio antes de cada término. Mientras que se permiten espacios en el medio de los números, no hay razón para hacerlo.

* Use definición del centro de arcos
   La definición del centro de arcos de círculos por medio de coordenadas (I,J,K en vez de R) se comporta de manera más consistente que los arcos definidos por su radio, partiularmente
   para ángulos cercanos a 180 o 360 grados.

* Use preambulos para definir los grupos modales
   La correcta ejecución del programa generalmente depende de la configuración de los modos. Asegúrese de que al principio de su programa estén definidos, ya que los modos pueden 
   ser acarreados de programas previos y desde comandos de la interfaz. 

Ejemplo de preambulo de modos::

   G17 G20 G40 G49 G54 G80 G90 G94

G17 define el plano de trabajo XY, G20 selecciona pulgadas, G40 cancela la compensación diametral, G49 cancela el decalaje por largo de herramienta, G54 para utilizar el sistema
de coordenadas 1, G80 cancela los ciclos cerrados, G90 define coordenadas absolutas y G94 define avance en distancia/minutos.

* No defina demasiadas cosas en una línea
   Si bien la sección :ref:`ordenEjecucionCNC` se muestra para referencia, no tenga en cuenta lo indicado en esta sección para escribir todo en una línea. 
   Es más claro y legible escribir lo mismo en varias líneas separadas.

* No defina y use un parámetro en el misma línea
   No defina y use un parámetro en el misma línea, a pesar de que la semántica esté bien utilizada. Actualizar el valor de una variable usando #1=[#1+#2] está permitido.

* No use numeración de líneas
   El uso de los números de línea no ofrece ventaja alguna. Cuando se reportan números de líneas en los mensajes de error se hace referencia al número de línea del archivo, 
   no a los números de línea definidos por el código G.


Mensajes de Errores Comunes
---------------------------

* Código G fuera de ámbito
   Se utilizó un código G mayor a G99, el rango de códigos G es de 0 a 99. Además no todos los números entre 0 y 99 son códigos válidos.

* Código G no reconocido
   Se ha utilizado un código G que no forma parte del lenguaje.

* I,J,K sin Gx a utilizar
   Los términos I,J,K deben ser utilizados en la misma línea que el código G.
   
* No se puede utilizar un valor de posición de eje sin un código G que lo utilice
   Los valores de posición de ejes no se pueden especificar en una línea sin un código G modal que esté vigente o bien un código G en la misma línea.

* Archivo finalizado sin signo de terminación ( % ) o programa terminado
   Todo código G debe tener un M2 o M30 en la última línea o estar limitado por un signo de porcentaje %.

.. _tablaCodigosG:

Tabla de Referencia - Códigos G
===============================

En esta sección se detallan los códigos G y su forma de uso. En la descripción se utiliza el guión (-) para denotar un valor real y 
los signos (<>) para denotar un item opcional.
Si se utiliza la siguiente expresión L- significa que en el código se debe utilizar por ejemplo L20 y se hará referencia a ese valor 
como el *valor L*. De igual manera se hace con cualquier otra letra.
En estos prototipos de código G la palabra *ejes* se utiliza para cualquier eje que esté en su configuración.
Un valor opcionalserá escrito de esta forma *<L->*.
Un valor real podrá ser:

* Un número explícito, *4*
* Una expresión, *[2+4]*
* Un parámetro, *#88*
* Una función escalar, *acos[0]*

En la mayoría de los casos, si se utiliza la palabra *eje* (cualquiera o todos de *X Y Z A B C U V W*, especifica un punto de destino.

Las posiciones de ejes están en sus sistemas de coordenadas activos,  a no ser que explícitamente se describa que hacen referencia al sistema de
coordenadas absolutas.

En donde la posición de un eje es opcional, cualquier valor omitido significa que el eje retiene su posición original.

Todos los items que en los prototipos de código G no sea descripto comomopcional es una valor requerido.

Los valores de las siguientes letras son dados frecuentemente como números. A no ser que se describa otra cosa, los números
explícitos pueden ser valores reales. Por ejemplo, *G10 L2* puede ser equivalente a *G[2*5]L[1+1]*. Si el valor del parámetro
100 fuera 2, *G10 L#100* tendría el mismo significado.

Si L- está escrito en la forma de prototipo el signo - frecuentemente está referido al *número L*, y así para cualquier otra letra.

+-------------------------------+-------------------------------------------------------------------+
|       Comando                 | Descripción                                                       |
+===============================+===================================================================+
|  :ref:`G0 <refG0>`            | Movimiento coordinado rápido                                      |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G1 <refG1>`            | Movimiento coordinado con velocidad de avance                     |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G2 G3 <refG2>`         | Movimiento de Arco de Círculo o Helicoidal                        |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G4 <refG4>`            | Espera                                                            |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G5 <refG5>`            | Spline Cúbico                                                     |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G5.1 <refG5.1>`        | Spline Cuadrático                                                 |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G5.2 <refG5.2>`        | Bloque de NURBS                                                   |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G7 <refG7>`            | Modo Diametral (para torneado)                                    |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G8 <refG8>`            | Modo Radial (para torneado)                                       |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G10 L1 <refG10L1>`     | Definición de Parámetros de Herramienta                           |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`G10 L2 <refG10L2>`     | Definición de de Sistema Coordinado                               |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G10 L10 <refG10L10>`    | Definición de Parámetros de Herramienta                           |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G10 L11 <refG10L11>`    | Definición de Parámetros de Herramienta                           |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G10 L20 <refG10L20>`    | Definición de de Sistema Coordinado                               |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G17-G19.1 <refG17>`     | Selección de Plano de Trabajo                                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G20 G21 <refG20>`       | Selección de Unidades                                             |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G28 G28.1 <refG28>`     | Ir a posición Predeterminada                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G30 G30.1 <refG30>`     | Ir a posición Predeterminada                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G33 <refG33>`           | Movimiento Sincronizado de Husillo                                |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G33.1 <refG33.1>`       | Roscado Rígido                                                    |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G38.n <refG38>`         | Sondeo                                                            |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G40 <refG40>`           | Compensación de Radio de Herramienta Desactivada                  |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G41 G42 <refG41>`       | Compensación de Radio de Herramienta                              |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G41.1 G42.1 <refG41.1>` | Compensación Dinámica de Radio de Herramienta                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G43 <refG43>`           | Compensación de Largo de Herramienta                              |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G43.1 <refG43.1>`       | Compensación Dinámica de Largo de Herramienta                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G43.2 <refG43.2>`       | Compensación Adicional de Largo de Herramienta                    |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G49 <refG49>`           | Cancelar Compensación de Largo de Herramienta                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G52 <refG52>`           | Posición del Sistema de Coordenadas Local                         |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G53 <refG53>`           | Posición en Sistema de Coordenadas de Máquina                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G54-G59.3 <refG54>`     | Selección de Sistema de Coordenadas Local                         |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G61 <refG61>`           | Modo de Posicionamiento Exacto                                    |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G61.1 <refG61.1>`       | Modo de Frenado en Posición Exacta                                |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G64 <refG64>`           | Suavizado de Trayectoria                                          |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G73 <refG73>`           | Ciclo de Perforado con Ruptura de Viruta                          |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G74 <refG74>`           | Ciclo de Roscado Izquierdo con Espera                             |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G76 <refG76>`           | Ciclo de Roscado de Varias Pasadas (Torneado)                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G80 <refG80>`           | Cancelación de Ciclo Cerrado                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G81 <refG81>`           | Ciclo de Perforado                                                |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G82 <refG82>`           | Ciclo de Perforado con Espera                                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G83 <refG83>`           | Ciclo de Perforado Profundo                                       |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G84 <refG84>`           | Ciclo de Roscado Derecho con Espera                               |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G85 <refG85>`           | Ciclo de Perforado con Velocidad de Salida                        |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G86 <refG86>`           | Ciclo de Perforado, Freno de Husillo y Velocidad Rápida de Salida |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G89 <refG89>`           | Ciclo de Perforado, Espera y Velocidad de Salida                  |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G90 G91 <refG90>`       | Modo de Distancia Absoluta o Relativa                             |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G90.1 G91.1 <refG90.1>` | Modo de Distancia de Arcos Absoluta o Relativa                    |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G92 <refG92>`           | Definir Posición de Sistema de Coordenadas en Punto Actual        |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G92.1 G92.2 <refG92.1>` | Resetear Posición de Sistema de Coordenadas                       |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G92.3 <refG92.3>`       | Restablecer Posición de Sistema de Coordenadas de G92             |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G93 G94 G95 <refG93>`   | Modo de Avance                                                    |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G96 G97 <refG96>`       | Modo de Control de Husillo                                        |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`G98 G99 <refG98>`       | Nivel de Retorno de Ciclos Cerrados                               |
+-------------------------------+-------------------------------------------------------------------+




.. _refG0:

G0 Movimiento Rápido
--------------------

Ejemplo de preambulo de modos::

   G0 ejes

Ejecuta un movimiento coordinado rápido en línea recta, donde todas las posiciones de ejes son opcionales. El G0 es opcional
si el modo de movimiento es G0. Este comando se usa típicamente para posicionarse en determinado lugar.

**Velocidad de Avance Rápido**

**Ejemplo**:

   G90 (modo de coordenadas absolutas)
   G0 X10 Y-23.5 (movimiento lineal rápido desde la posición actual a X10 Y-23.5)
   M2 (fin de programa)

* Ver las secciones :ref:`G90 <refG90>` y :ref:`M2 <refM2>` para más información.

Si la compensación de herramienta está activa, el movimiento del descripto en el ejemplo, ver :ref:`Compensación de Herramienta <refM2>`

.. _refG1:

G1 Movimiento Lineal
--------------------

.. _refG2:

G2 G3 Movimiento Arco de Círculo o Helicoidal
---------------------------------------------

.. _refG4:

G4 Espera
---------

.. _refG5:

G5 Spline Cúbico
----------------

.. _refG5.1:

G5.1 Spline Cuadrático
-----------------------

.. _refG5.2:

G5.2 G5.3 Bloque de NURBS
-------------------------

.. _refG7:

G7 Modo Diametral (para torneado)
---------------------------------

.. _refG8:

G8 Modo Radial (para torneado)
---------------------------------

.. _refG10L1:

G10 L1 Definición de Parámetros de Herramienta
----------------------------------------------

G10 L1 sets the tool table for the P tool number to the values of the words.

A valid G10 L1 rewrites and reloads the tool table.

.. _refG10L2:

G10 L2 Definición de Sistema Coordinado
---------------------------------------

.. _refG10L10:

G10 L10 Definición de Parámetros de Herramienta
-----------------------------------------------

.. _refG10L11:

G10 L11 Definición de Parámetros de Herramienta
-----------------------------------------------


.. _refG10L20:

G10 L20 Definición de Sistema Coordinado
----------------------------------------


.. _refG17:

G17-G19.1 Selección de Plano de Trabajo
---------------------------------------


.. _refG20:

G20 G21 Selección de Unidades
------------------------------


.. _refG28:

G28 G28.1 Ir a posición Predeterminada
--------------------------------------

.. _refG30: 

G30 G30.1 Ir a posición Predeterminada
--------------------------------------

.. _refG33:

G33 Movimiento Sincronizado de Husillo
--------------------------------------

.. _refG33.1:

G33.1 Roscado Rígido
---------------------

.. _refG38:

G38.n Sondeo
------------


.. _refG40:

G40.n Compensación de Radio de Herramienta Desactivada
------------------------------------------------------

.. _refG41:

G41 G42 Compensación de Radio de Herramienta
--------------------------------------------


.. _refG41.1:

G41.1 G42.1 Compensación Dinámica de Radio de Herramienta
---------------------------------------------------------



.. _refG43:

G43 Compensación de Largo de Herramienta
-----------------------------------------


.. _refG43.1:

G43.1 Compensación Dinámica de Largo de Herramienta 
---------------------------------------------------

.. _refG43.2:

G43.2 Compensación Adicional de Largo de Herramienta 
----------------------------------------------------



.. _refG49:

G49 Cancelar Compensación de Largo de Herramienta 
-------------------------------------------------


.. _refG52:

G52 Posición del Sistema de Coordenadas Local
---------------------------------------------


.. _refG53:

G53 Posición en Sistema de Coordenadas de Máquina
-------------------------------------------------

.. _refG54:

G54-G59.3 Selección de Sistema de Coordenadas Local
---------------------------------------------------




.. _refG61:

G61 Modo de Posicionamiento Exacto
----------------------------------



.. _refG61.1:

G61.1 Modo de Frenado en Posición Exacta
----------------------------------------

.. _refG64:

G64 Suavizado de Trayectoria
----------------------------


.. _refG73:

G73 Ciclo de Perforado con Ruptura de Viruta
--------------------------------------------


.. _refG74:

G74 Ciclo de Roscado Izquierdo con Espera
-----------------------------------------

.. _refG76:

G76 Ciclo de Roscado de Varias Pasadas (Torneado)
-------------------------------------------------

.. _refG80:

G80 Cancelación de Ciclo Cerrado
--------------------------------

.. _refG81:

G81 Ciclo de Perforado
----------------------

.. _refG82:

G82 Ciclo de Perforado con Espera
----------------------------------


.. _refG83:

G83 Ciclo de Perforado Profundo
-------------------------------
.. _refG84:

G84 Ciclo de Roscado Derecho con Espera
---------------------------------------

.. _refG85:

G85 Ciclo de Perforado con Velocidad de Salida
----------------------------------------------

.. _refG86: 

G86 Ciclo de Perforado, Freno de Husillo y Velocidad Rápida de Salida
---------------------------------------------------------------------

.. _refG89:

G89 Ciclo de Perforado, Espera y Velocidad de Salida
----------------------------------------------------

.. _refG90:

G90 G91 Modo de Distancia Absoluta o Relativa
---------------------------------------------

.. _refG90.1:

G90.1 G91.1 Modo de Distancia de Arcos Absoluta o Relativa
----------------------------------------------------------

.. _refG92:

G92 Definir Posición de Sistema de Coordenadas en Punto Actual
--------------------------------------------------------------

.. _refG92.1:

G92.1 G92.2 Resetear Posición de Sistema de Coordenadas
-------------------------------------------------------

.. _refG92.3:

G92.3 Restablecer Posición de Sistema de Coordenadas de G92
-----------------------------------------------------------

.. _refG93:

G93 G94 G95 Modo de Avance
--------------------------

.. _refG96:

G96 G97 Modo de Control de Husillo
----------------------------------

.. _refG98:

G98 G99 Nivel de Retorno de Ciclos Cerrados
-------------------------------------------



.. _tablaCodigosM:

Tabla de Referencia - Códigos M
===============================

+-------------------------------+-------------------------------------------------------------------+
|       Comando                 | Descripción                                                       |
+===============================+===================================================================+
|  :ref:`M0 M1 <refM0>`         | Pausa de Programa                                                 |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M2 M30 <refM2>`        | Fin de Programa                                                   |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M60 <refM60>`          | Pausa de Cambio de Palet                                          |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M3 M4 M5 <refM3>`      | Control de Husillo                                                |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M6 <refM6>`            | Cambio de Herramienta                                             |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M7 M8 M9 <refM7>`      | Control de Refrigerante                                           |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M19 <refM19>`          | Orientación de Husillo                                            |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M48 M49 <refM48>`      | Activar / Desactivar Override de Avance y Husillo                 |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M50 <refM50>`          | Control de Override de Avance                                     |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M51 <refM51>`          | Control de Override de Husillo                                    |
+-------------------------------+-------------------------------------------------------------------+
|  :ref:`M52 <refM52>`          | Control Adaptativo de Avance                                      |
+-------------------------------+-------------------------------------------------------------------+

| :ref:`M10 L10 <refM10L10>`    | Definición de Parámetros de Herramienta                           |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M10 L11 <refM10L11>`    | Definición de Parámetros de Herramienta                           |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M10 L20 <refM10L20>`    | Definición de de Sistema Coordinado                               |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M17-M19.1 <refM17>`     | Selección de Plano de Trabajo                                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M20 M21 <refM20>`       | Selección de Unidades                                             |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M28 M28.1 <refM28>`     | Ir a posición Predeterminada                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M30 M30.1 <refM30>`     | Ir a posición Predeterminada                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M33 <refM33>`           | Movimiento Sincronizado de Husillo                                |
+-------------------------------+-------------------------------------------------------------------+




.. _ordenEjecucionCNC:

Orden de ejecución de Comandos
==============================

El orden de ejecución de los comandos en una línea no está definido por el lugar de cada comando dentro de la línea, sino por el orden en la siguiente lista:

+-------------------------------------------------------------------------------+
|       Orden de ejecución                                                      |
+===============================================================================+
| Comentarios (incluyendo mensajes)                                             |
+-------------------------------------------------------------------------------+
| Modo de velocidad de avance (G93, G94)                                        |
+-------------------------------------------------------------------------------+
| Velocidad de avance (F)                                                       |
+-------------------------------------------------------------------------------+
| Velocidad de husillo (S)                                                      |
+-------------------------------------------------------------------------------+
| Selección de herramienta (T)                                                  |
+-------------------------------------------------------------------------------+
| HAL pin I/O (M62-M68)                                                         |
+-------------------------------------------------------------------------------+
| Cambiar herramienta (M6) y definición de herramienta (M61)                    |
+-------------------------------------------------------------------------------+
| Prender / apagar husillo (M3, M4, M5)                                         |
+-------------------------------------------------------------------------------+
| Guardar estado (M70, M73), reestablecer estado (M72), invalidar estado (M71)  |
+-------------------------------------------------------------------------------+
| Prender / apagar refrigerante (M7, M8, M9)                                    |
+-------------------------------------------------------------------------------+
| Habilitar / desahilitar overrides (M48, M49, M50, M51, M52, M53)              |
+-------------------------------------------------------------------------------+
| Comandos definidos por el usurario (M100-M199)                                |
+-------------------------------------------------------------------------------+
| Espera (G4)                                                                   |
+-------------------------------------------------------------------------------+
| Selección de plano activo (G17,G18,G19)                                       |
+-------------------------------------------------------------------------------+
| Selección de unidades (G20,G21)                                               |
+-------------------------------------------------------------------------------+
| Activar / desactivar radio de compensación de herramienta (G40, G41, G42)     |
+-------------------------------------------------------------------------------+
| Activar / desactivar largo de compensación de herramienta (G43, G49)          |
+-------------------------------------------------------------------------------+
| Selección de sistema coordinado (G54, G55, G56, G57, G58, G59, G59.1-G59.9)   |
+-------------------------------------------------------------------------------+
| Definir modo de control de trayectoria (G61, G61.1, G64)                      |
+-------------------------------------------------------------------------------+
| Selección de modo de distancia (G90, G91)                                     |
+-------------------------------------------------------------------------------+
| Selección de modo de reflejo (G98, G99)                                       |
+-------------------------------------------------------------------------------+
| Ir a posición de referencia (G28, G30), modificar sistema coordenado (G10)    |
| o seleccionar decalaje de ejes (G52, G92, G92.1, G92.2, G94)                  |
+-------------------------------------------------------------------------------+
| Selección de modo de distancia (G90, G91)                                     |
+-------------------------------------------------------------------------------+
| Parada (M0, M1, M2, M30, M60)                                                 |
+-------------------------------------------------------------------------------+










.. _ejemploCNCbasico:

Ejemplo de Programación
========================


.. _interPLCconCNC:

Interacción de PLC/CNC
=======================



