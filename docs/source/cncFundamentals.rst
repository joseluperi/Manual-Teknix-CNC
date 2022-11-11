Fundamentos de CNC
==================

En esta sección se describen los elementos del lenguage de código G, su estructura, comandos y expresiones.

.. _estrCNC:

Estructura del Código G
-----------------------

El lenguaje de código G está conformado por líneas de código, también llamadas bloques. Cada línea puede incluir comandos para realizar varias cosas. Las líneas pueden ser agrupadas en un 
archivo que define una rutina o pueden ser agrupadas para formar subrutinas o funciones.
Una línea típica de código consiste en una numeración opcional al comienzo seguida de uno o más términos, también llamados palabras. Un término consiste en una letra seguida de un número 
o algo que se evalúa y se convierte en un número. Ese término puede dar un comando o proveer un argumento a un comando.
| Por ejemplo G1 X30 es una línea de código con dos términos. G1 es un comando que solicita el movimiento en línea recta a la velocidad programada a determinado punto, y X30 provee un 
argumento que especifica que la coordenada X debe ser de 30 en el punto al final del movimiento.
| La mayoría de los comandos empieza con la letra G o con la letra M, que hacen referencia a comandos Generales y Misceláneos respectivamente.
| Los programas no poseen un indicador de inicio y fin. Un programa puede estar en un solo archivo o puede estar repartido
en varios archivos. Se pueden utilizar los comandos M2 o M30 opcionalmente para indicar el fin de un programas.

Formato
^^^^^^^

Una línea de comando está compuesta de los siguientes elementos, en orden, con un límite de 256 caracteres:

* Un caracter opcional,la barra ( / ) que indica bloques de comentarios.
* Un número de línea que es opcional.
* Un número variable de términos, parámetros y comentarios
* Un marcador de fin de línea

Cualquier término que no esté explícitamente permitido producirá un error.
| Los espacios y tabulaciones están permitidos en cualquier parte del código y no modifican el significado del mismo,
esto hace que algunos aspectos extraños sean correctos. por ejemplo:
| G0X +12. 5Y70 es equivalente a G0 x+12.5 Y70 o G0 X 12.5 Y 70.
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
|   I   | Distancia relativa en X para círculos y ciclos fijos G87              |
+-------+-----------------------------------------------------------------------+
|   J   | Distancia relativa en Y para círculos y ciclos fijos G87              |
+-------+-----------------------------------------------------------------------+
|   K   | Distancia relativa en Z para círculos y ciclos fijos G87              |
|       | Fracción de movimiento de husillo para movimientos sincronizados G33  |
+-------+-----------------------------------------------------------------------+
|   L   | Parámetros genericos para G10, M66 y otros                            |
+-------+-----------------------------------------------------------------------+
|   M   | Misceláneos                                                           |
+-------+-----------------------------------------------------------------------+
|   N   | Número de línea                                                       |
+-------+-----------------------------------------------------------------------+
|   P   | Tiempo de espera para ciclos con G4                                   |
|       | Código usado con G10                                                  |
+-------+-----------------------------------------------------------------------+
|   Q   | Incremento de velocidad de avance en ciclos G73, G83                  |
+-------+-----------------------------------------------------------------------+
|   R   | Radio de círculo o plano de ciclo fijo                                |
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

Números
^^^^^^^

Las siguientes reglas se aplican para los números (explícitos), en las que un dígito es un caracter del 0 al 9.

Un número consiste de un signo + o signo - que es opcional, seguido de ningún a muchos dígitos, luego puede tener 
un punto decimal seguido de ningún a muchos dígitos, siempre y cuando el número tenga al menos un dígito en alguna parte.

Hay dos tipos de números, decimales y enteros, que se diferencian por poseer un punto decimal respectivamente.
Los números pueden tener un número variable de dígitos, siempre que respeten el límite del largo de línea máximo, aunque
se utilizarán alrededor de 17 cifras significativas.
Se asume que un número sin signo es positivo.

Parámetros
^^^^^^^^^^

El lenguage CNC permite el uso de parámetros, lo que en otros lenguajes de programación se conoce como variables. Existen varios tipos de parámetros que tienen diferentes propósitos,
que se describen a continuación. El único valor soportado como parámetros son los números de punto flotante, no hay parámetros con valores lógicos, de texto o enteros en el código G.
Sin embargo, se pueden utilizar expresiones con operadores lógicos (AND, OR, XOR) y operadores de comparación (EQ, NE, GT, GE, LT, LE) y operadores que soportan aritmética de enteros
como MOD, ROUND, FUP y FIX.
| Los parámetros difieren en su sintáxis, ámbito (scope), comportamiento cuando no están inicializados, modo, persistencia y propósito de uso.

Sintáxis
""""""""

   Hay tres tipos de apariencia sintáctica:
   
   * Numerada - #4711
   * Por nombre, local - #<valorlocal>
   * Por nombre, global - #<_valorglobal>

Ámbito (Scope)
""""""""""""""

El ámbito a scope de un parámetro es 
Operadores

Inicialización
""""""""""""""

Modo
""""

Persistencia
""""""""""""


Syntax
There are three kinds of syntactic appearance:

numbered - #4711

named local - #<localvalue>

named global - #<_globalvalue>

Scope
The scope of a parameter is either global, or local within a subroutine. Subroutine parameters and local named variables have local scope. Global named parameters and numbered parameters starting from number 31 are global in scope. RS274/NGC uses lexical scoping - in a subroutine only the local variables defined therein, and any global variables are visible. The local variables of a calling procedure are not visible in a called procedure.

Behavior of uninitialized parameters
Uninitialized global parameters, and unused subroutine parameters return the value zero when used in an expression.

Uninitialized named parameters signal an error when used in an expression.

Mode
Most parameters are read/write and may be assigned to within an assignment statement. However, for many predefined parameters this does not make sense, so they are are read-only - they may appear in expressions, but not on the left-hand side of an assignment statement.

Persistence
When LinuxCNC is shut down, volatile parameters lose their values. All parameters except numbered parameters in the current persistent range [1] are volatile. Persistent parameters are saved in the .var file and restored to their previous values when LinuxCNC is started again. Volatile numbered parameters are reset to zero.

Intended Use
user parameters:: numbered parameters in the range 31..5000, and named global and local parameters except predefined parameters. These are available for general-purpose storage of floating-point values, like intermediate results, flags etc, throughout program execution. They are read/write (can be assigned a value).

subroutine parameters - these are used to hold the actual parameters passed to a subroutine.

numbered parameters - most of these are used to access offsets of coordinate systems.

system parameters - used to determine the current running version. They are read-only.

Comportamiento Modal
--------------------




.. _lenguajeCNC:

Elementos del Lenguaje
----------------------

.. _ejemploCNCbasico:

Ejemplo Básico de Programación
------------------------------

.. _comandosPosicion:

Comandos de Posición
--------------------


.. _comandosMovimiento:

Comandos de Movimiento
----------------------


.. _controlAvance:

Control de Avance
-----------------


.. _controlHusillo:

Control de Husillo
------------------


.. _interPLCconCNC:

Interacción de PLC/CNC
-----------------------


.. _ejemploCNCintermedio:

Ejemplo Intermedio de Programación
----------------------------------


