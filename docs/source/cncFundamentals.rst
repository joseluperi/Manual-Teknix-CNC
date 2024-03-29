Fundamentos del Código G
########################

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
| Los términos están formados por cualquier letra de las que se muestran en la siguente tabla: 

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

.. admonition:: Nota

   Ciertos términos pueden usarse repetidamente en un bloque (ej. G..., M..., H... )

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


.. _refComentarios:

Comentarios
-----------

Es posible agregar comentarios a las líneas del código G que ayudan a esclarecer la intención del programador. Los comentarios pueden ser escritos en la línea mediante el uso de 
los paréntesis () o estar al final de la línea utilizando el signo de punto coma ; .
Los comentarios pueden utilizarse entre los términos pero no entre un término y su correspondiente parámetro.
Por ejemplo S0, S100 (determinar velocidad) F200 (velocidad) es válido, pero S(velocidad)100 F(velocidad) 200 no es correcto.

Hay algunos comentarios activos que **parecen** comentarios pero causan alguna acción, como *(debug,..)* o *(print,..)*. Si hay varios comentarios en una línea, sólo el último comentario
será interpretado según estas reglas. Por lo tanto un comentario normal seguido de un comentario activo tendrá el efecto de desactivar el comentario activo. For ejemplo *(foo)(debug,#1)*
mostrará el valor del parámetro #1, sin embargo *(debug,#1)(foo)* no lo hará.

Un comentario definido por un punto coma es por definición el último comentario en esa línea y será interpretado con la sintáxis de comentarios activos.

Rastreo de Eventos (Logging)
----------------------------

Una funcionalidad útil para almacenar información de eventos ocurridos es grabarlos a un archivo, para esto se pueden utilizar los siguientes comandos:

* *(LOGOPEN,nombredearchivo.txt)* abre el archivo con el nombre definido. Si el archivo ya existe se trunca.
* *(LOGAPPEND,nombredearchivo)* abre el archivo con el nombre definido. Si el archivo ya existe la información se agrega al final.
* *(LOGCLOSE)* cierra el archivo con el nombre definido.
* *(LOG,)* escribe lo que sigue a continuación de la coma si el archivo está abierto. Soporta la escritura de valores de parámetros.

Mensajes
--------

Es posible mostrar un mensaje al operador desde el código con la función *MSG()*, por ejemplo *MSG('Programa en ejecución')* mostrará 'Programa en ejecución' al usuario. Si se requiere
una confirmación del operador para avanzar se puede utilizar el comando *POPUP()* que mostará el mensaje al operador en una ventana emergente y bloqueará la ejecución del programa
hasta que el operador confirme.

Imprimir Mensajes
-----------------

*(PRINT,)* los mensajes se muestran en la consola. Soporta la escritura de valores de parámetros.


Mensajes de Depuración (Debug)
------------------------------

*(DEBUG,)* muestra un mensaje como *(MSG,)* con la capacidad de mostrar valores de los parámetros. La forma de hacerlo se muestra en la sección de Valores en Mensajes más abajo.


Valores en Mensajes
-------------------

En las funcionalidades *DEBUG*, *PRINT* y *LOG*, se pueden escribir los valores de los parámetros en el mensaje.

Por ejemplo, para imprimir el valor de una variabla global a la consola.

**Ejemplo de Valores de Parámetros**::

   (print,endmill dia = #<_endmill_dia>)
   (print,value of variable 123 is: #123)

Dentro de estos comentarios las secuencias como *#123* son reemplazadas por el valor del parámetro 123.
Las sequencias como *#<nombre de parametro>* son reemplazadas por el valor del parametro con el nombre *nombre de parámetro*. En los nombres de parámetros se eliminan los espacios, 
por lo que *<nombre de parametro>* se convertirá en *#<nombredeparametro>*.

.. _fileReq:

Requerimientos de Archivo
-------------------------

El archivo de Código G debe contener una o más líneas de código y estar finalizado con un comando de *Fin de Programa (M2 o M30)*. Cualquier línea luego del comando de Fin de Programa 
se ignora. Si no se utiliza el comando de Fin de Programa, se puede utilizar un par de símbolos *%*, el primer símbolo *%* en la primer línea del archivo, seguido de una o más líneas de 
código y el segundo símbolo *%*. Los comandos luego del segundo símbolo *%* no serán evaluados.

.. admonition: Precaución
   :class: warning

   Utilizar los símbolos *%* para encerrar Código G no tiene el mismo efecto que un comando de Fin de Programa ya que quedará activos los modos de operación que tenía la máquina al momento
   de ejecución del segundo símbolo. Por ejemplo, el husillo puede quedar girando, la bomba de refrigerante quedar encendida y los decalajes activos. Por lo que si no utiliza un preámbulo 
   en el principio del siguiente código a ejecutar se pueden producir situaciones peligrosas

.. _refParameters:

Parámetros
----------

| El lenguage CNC permite el uso de parámetros, lo que en otros lenguajes de programación se conoce como variables. Existen varios tipos de parámetros que tienen diferentes propósitos,
  que se describen a continuación. El único valor soportado como parámetros son los números de punto flotante, no hay parámetros con valores lógicos, de texto o enteros en el código G.
| Sin embargo, se pueden utilizar expresiones con operadores lógicos (AND, OR, XOR) y operadores de comparación (EQ, NE, GT, GE, LT, LE) y operadores que soportan aritmética de enteros
  como MOD, ROUND, FUP y FIX.
| Los parámetros difieren en su sintáxis, ámbito (scope), comportamiento cuando no están inicializados, modo, persistencia y propósito de uso.

**Sintáxis**

   Hay tres tipos de apariencia sintáctica:
   
   * Parámetro Numerado  #4711
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

Parámetros numerados
--------------------


**Persistencia de parámetros numerados**

Los parámetros numerados se especifican con el símbolo # seguido de un número entero entre 1 y 5602. El parámetro es referido por su número y su valor es cualquier número
guardado en ese parámetro.
Un valor se guarda en un parámetro con el signo igual =, por ejemplo::

   #3 = 15 (guarda el número 15 en el parámetro 3)

El guardado del valor en el parámetro no tiene efecto hasta que todos los valores de los parámetros en la misma línea se han evaluada. Por ejemplo, si el parámetro
3 tenía un valor de 15 y se interpreta la línea *#3=6 G1 X#3* se realizará un movimiento lineal a un punto con X igual a 15 y luego el valor del parámetro 3 se cambiará 
a 6.

El símbolo # tiene precedencia respeto a otras operaciones, por ejemplo, *#1+2* se intepreta como el número del parámetro 1 más 2 unidades. Para especificar el valor de
un parámetro cuyo número es el resultado de una operación se debe utilizar corchetes, por ejemplo *#[1+2]* hace referencia al valor del parámetro 3. El símbolo # puede 
estar repetido, por ejemplo *##2* significa el valor del parámetro cuyo número es el valor del parámetro 2.

* *31-5000* Parámetros de usuario de códigos G. Estos parámetros son globales en el código G y están disponibles para su uso. Volátiles.

* *5061-5069* Coordenadas de un procedimiento de sondeo G38 (X, Y, Z, A, B, C, U, V & W). Las coordenadas están en el sistema en el que se ejecutó G38. Volátiles.

* *5070* Resultado de procedimiento G38: 1 si fue exitoso, 0 si la sonda no se accionó. Utilizado con G38.3 y G38.5. Volátil.

* *5161-5169* Origen G28 de X, Y, Z, A, B, C, U, V & W. Persistentes.

* *5181-5189* Origen G30 de X, Y, Z, A, B, C, U, V & W. Persistentes.

* *5210* 1 si está activo el decalaje de G52 o G92, 0 de lo contrario. Volátil por defecto; persistente si DISABLE_G92_PERSISTENCE = 1 en la sección [RS274NGC] del archivo .ini.

* *5211-5219* Decalaje compartido de G52 y G92 para X, Y, Z, A, B, C, U, V & W. Volátil por defecto; persistente si  DISABLE_G92_PERSISTENCE = 1 en la sección [RS274NGC] del archivo .ini..

* *5220* Número de sistema coordenado 1 - 9 para G54 - G59.3. Persistente.

* *5221-5230* Sistema coordenado 1, G54 para X, Y, Z, A, B, C, U, V, W & R. R denotes the XY rotation angle around the Z axis. Persistent.

* *5241-5250* Sistema coordenado 2, G55 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5261-5270* Sistema coordenado  3, G56 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5281-5290* Sistema coordenado  4, G57 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5301-5310* Sistema coordenado  5, G58 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5321-5330* Sistema coordenado  6, G59 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5341-5350* Sistema coordenado  7, G59.1 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5361-5370* Sistema coordenado  8, G59.2 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5381-5390* Sistema coordenado  9, G59.3 para X, Y, Z, A, B, C, U, V, W & R. Persistente.

* *5399* Resultado de *M66* - Verificar o esperar a input. Volátil.

* *5400* Número de herramienta. Volátil.

* *5401-5409* Decalajes de herramientas para X, Y, Z, A, B, C, U, V & W. Volátil.

* *5410* Diámetro de herramienta. Volátil.

* *5411* Ángulo frontal de herramienta. Volátil.

* *5412* Ángulo trasero de herramienta. Volátil.

* *5413* Orientación de herramienta. Volátil.

* *5420-5428* Posición relativa actual en el sistema coordinado activo incluyendo todos los decalajes y las unidades activas para  X, Y, Z, A, B, C, U, V & W, Volátil.

* *5599* Bandera de control de salidas para depuración (DEBUG,). 1 = activo, 0 = inactivo; defecto = 1. Volátil.

* *5600* Indicador de falla de cambiador de herramienta. Utilizado con el componente iocontrol-v2. 1: cambiador en falla, 0: normal. Volátil.

* *5601* Indicador de falla de cambiador de herramienta. Utilizado con el componente iocontrol-v2. Refleja el valor de la razón de falla del cambiador del tesitgo (pin) de HAL. Volátil.


Parámetros de Subrutinas
------------------------

Los parámetros en el rango *1-30* son parámetros locales de llamadas a subrutinas. Estos parámetros son locales a la subrutina y son volátiles.
Para más información ver la sección de :ref:`códigos O <refOcodes>`.

Parámetros con Nombre
---------------------

Los parámetros con nombre funcionan de la misma manera que los parámetros numerados pero son más fáciles de leer. Todos los nombres de parámetros son convertidos
a minúscula y se les quitan los espacios y tabulaciones, por lo que *<parametro>* y *<P a R am	etro>* refieren al mismo parámetro. Los nombres de los parámetros deben ser
encerados por los símbolos *< >*.
*#<parametro con nombre> es un parámetro con nombre local. Por defecto un parámetro con nombre es local al ámbito (scope) en el que es asignado. No se puede acceder a un 
parámetro con nombre fuera de la subrutina. Esto significa que dos subrutinas pueden utilizar cada una un parámetro con el mismo nombre sin la posibilidad de que una 
subrutina sobreescriba el valor del parámetro de la otra.
#<_parámetro con nombre global> es un parámetro con nombre global. Se definen utilizando el símbolo *_* como primer caracter. Es accesible desde subrutinas y su valor puede 
ser cambiado desde las subrutina que sea accesible desde la función que las llama. 
Desde el punto de vista del ámbito se comportan igual a los parámetros numerados. No se guardan en archivos.

**Declaración de parámetros con nombre globales**

::

   #<_diam_fresa> = 0.049


**Referencia a parámetros globales previamente definidos**

::

   #<_radio_fresa> = [#<_diam_fresa>/2.0]

**Parámetros mixtos (literales y con nombre)**

::

   o100 call [0.0] [0.0] [#<_desbaste_interno>-#<_diam_fresa>] [#<_profundidadZ>] [#<_velocidadDeAvance>]

Los parámetros con nombre se crean cunado se les asigna un valor por primera vez.
Se produce un error si se utiliza un parámetro con nombre que no existe dentro de una expresión, o se lo utiliza a la derecha de la asignación.
Al imprimir el valor de un parámetro con nombre inexistente con *(DEBUG, <parametro_inexistente>* se mostrará el símbolo *#*.
Los parámetros globales, como así también los parámetros locales asignados en el nivel global, seguirán existinendo aún cunado el programa finaliza,
y sus valores estarán disponibles cuando el programa se ejecute nuevamente.
La función *EXIST* se puede utilizar para conocer si existe un parámetro con determinado nombre.


.. _refNamedPredefParam:

Parámetros con Nombre Predefinidos
----------------------------------

Los siguientes parámetros globales de solo lectura están disponibles a los efectos de acceder al estado interno del controlador. Pueden ser utilizados 
en cualquier expresión, por ejemplo, controlar el flujo de la ejecución de un programa.

* *#<_line>* Al correr un archivo de código G retorna el número de línea actual.

* *#<_motion_mode>* Retorna el estado actual del modo de movimiento:

+---------------------+--------------------------+
| Modo de movimiento  | Valor de retorno         |
+---------------------+--------------------------+
|   G1                |          10              |
+---------------------+--------------------------+
|   G2                |          20              |
+---------------------+--------------------------+
|   G3                |          30              |
+---------------------+--------------------------+
|   G33               |          330             |
+---------------------+--------------------------+
|   G38.2             |          382             |
+---------------------+--------------------------+
|   G38.3             |          383             |
+---------------------+--------------------------+
|   G38.4             |          384             |
+---------------------+--------------------------+
|   G38.5             |          385             |
+---------------------+--------------------------+
|   G5.2              |          52              |
+---------------------+--------------------------+
|   G73               |          730             |
+---------------------+--------------------------+
|   G76               |          760             |
+---------------------+--------------------------+
|   G80               |          800             |
+---------------------+--------------------------+
|   G81               |          810             |
+---------------------+--------------------------+
|   G82               |          820             |
+---------------------+--------------------------+
|   G83               |          830             |
+---------------------+--------------------------+
|   G84               |          840             |
+---------------------+--------------------------+
|   G85               |          850             |
+---------------------+--------------------------+
|   G86               |          860             |
+---------------------+--------------------------+
|   G87               |          870             |
+---------------------+--------------------------+
|   G88               |          880             |
+---------------------+--------------------------+
|   G89               |          890             |
+---------------------+--------------------------+

* *#<_plane>* retorna el valor designado al plano de trabajo activo:

+---------------------+--------------------------+
|   Plano de trabajo  | Valor de retorno         |
+---------------------+--------------------------+
|   G17               |          170             |
+---------------------+--------------------------+
|   G18               |          180             |
+---------------------+--------------------------+
|   G19               |          190             |
+---------------------+--------------------------+
|   G17.1             |          171             |
+---------------------+--------------------------+
|   G18.1             |          181             |
+---------------------+--------------------------+
|   G19.1             |          191             |
+---------------------+--------------------------+

* *#<_ccomp>* Retorna el estado de la compensación de herramienta:

+---------------------+--------------------------+
|   Modo              | Valor de retorno         |
+---------------------+--------------------------+
|   G40               |          400             |
+---------------------+--------------------------+
|   G41               |          410             |
+---------------------+--------------------------+
|   G41.1             |          411             |
+---------------------+--------------------------+
|   G42               |          420             |
+---------------------+--------------------------+
|   G42.1             |          421             |
+---------------------+--------------------------+

* *#<_metric>* Retorna 1 si *G21* está activo, sino 0.

* *#<_imperial>* Retorna 1 if *G20* está activo, sino 0.

* *#<_absolute>* Retorna 1 if *G90* está activo, sino 0.

* *#<_incremental>* Retorna 1 if *G91* está activo, sino 0.

* *#<_inverse_time> *Retorna 1 si el modo de avance inverso *G93* está activo, sino 0.

* *#<_units_per_minute>* Retorna 1 si el modo de avance en unidades/minuto *G94* está activo, sino 0.

* *#<_units_per_rev>* Retorna 1 si el modo de unidades/revolucion *G95* está activo, sino 0.

* *#<_coord_system>* Retorna a un número de punto flotante del sistema coordenado actual *G54..G59.3*. Por ejemplo si el sistema activo es *G55* retorna un valor de 550.00000 y si es *G59.1* el valor de retorno es 591.000000.


+---------------------+--------------------------+
|   Modo              | Valor de retorno         |
+---------------------+--------------------------+
|   G54               |          540             |
+---------------------+--------------------------+
|   G55               |          550             |
+---------------------+--------------------------+
|   G56               |          561             |
+---------------------+--------------------------+
|   G57               |          570             |
+---------------------+--------------------------+
|   G58               |          580             |
+---------------------+--------------------------+
|   G59               |          590             |
+---------------------+--------------------------+
|   G59.1             |          591             |
+---------------------+--------------------------+
|   G59.2             |          592             |
+---------------------+--------------------------+
|   G59.3             |          593             |
+---------------------+--------------------------+

* *#<_tool_offset>* Retorna 1 si el decalaje de herraimienta está activo *G43*, sino 0.

* *#<_retract_r_plane>* Retorna 1 si *G98* está definido, sino 0.

* *#<_retract_old_z>* Retorna 1 si *G99* está definido, sino 0.


Parámetros de Sistema
---------------------


* *#<_spindle_rpm_mode>* Retorna 1 si el modo de husillo etá en RPM *G97*, sino 0.

* *#<_spindle_css_mode>* Retorna 1 si el modo de velocidad superficial constante *G96* está activo, sino 0.

* *#<_ijk_absolute_mode>* Retorna 1 si el modo de distancia absoluta para arcos *G90.1* está activo, sino 0.

* *#<_lathe_diameter_mode>* Retorna 1 si la configuración de torno y el modo diametral *G7* está activo, sino 0.

* *#<_lathe_radius_mode>* Retorna 1 si la configuración de torno y el modo radial *G8* está activo, sino 0.

* *#<_spindle_on>* Retorna 1 si el husillo está girando *M3* o *M4*, sino 0.

* *#<_spindle_cw>* Retorna 1 si la dirección de giro del husillo es horario *M3*, sino 0.

* *#<_mist>* Retorna 1 si la bomba de refrigerante de niebla *M7* está prendido.

* *#<_flood>* Retorna 1 si la bomba de refrigerante líquido *M8* está prendido.

* *#<_speed_override>* Retorna 1 si el override de velocidad de husillo *M48* o *M51 P1* está activo, sino 0.

* *#<_feed_override>* Retorna 1 si el override de velocidad de avance *M48* or *M50 P1* está activo, sino 0.

* *#<_adaptive_feed>* Retorna 1 si el modo de avance adaptativo *M52* or *M52 P1* está activo, sino 0.

* *#<_feed_hold>* Retorna 1 si el interruptor de avance está activo *M53 P1*, sino 0.

* *#<_feed>* Retorna el valor configurado de *F*, no la velocidad de avance real.

* *#<_rpm>* Retorna el valor configurado de *S*, no la velocidad de husillo real.

* *#<_x>* Retorna la coordenada relativa del eje X incluyendo todos los decalajes. Al igual que #5420.

* *#<_y>* Retorna la coordenada relativa del eje Y incluyendo todos los decalajes. Al igual que #5421.

* *#<_z>* Retorna la coordenada relativa del eje Z incluyendo todos los decalajes. Al igual que #5422.

* *#<_a>* Retorna la coordenada relativa del eje A incluyendo todos los decalajes. Al igual que #5423.

* *#<_b>* Retorna la coordenada relativa del eje B incluyendo todos los decalajes. Al igual que #5424.

* *#<_c>* Retorna la coordenada relativa del eje C incluyendo todos los decalajes. Al igual que #5425.

* *#<_u>* Retorna la coordenada relativa del eje U incluyendo todos los decalajes. Al igual que #5426.

* *#<_v>* Retorna la coordenada relativa del eje V incluyendo todos los decalajes. Al igual que #5427.

* *#<_w>* Retorna la coordenada relativa del eje W incluyendo todos los decalajes. Al igual que #5428.

* *#<_current_tool>* Retorna el numero de herramienta actual en el husillo. Al igual que #5400.

* *#<_current_pocket>* Retorna el lugar de guardado de la herramienta actual.

* *#<_selected_tool>* Retorna el número de la herramienta seleccionada luego de un código *T*. Valor por defecto -1.

* *#<_selected_pocket>* Retorna el lugar de guardado de la herramietna seleccionada luego de un código *T*. Valor por default -1.

* *#<_value>* Retorna el valor de retorno del último *código-O* o *endsub*. Valor por default 0 si no se definió. Inicializada a 0 en inicio de programa.

* *#<_value_returned>* 1.0 if the last O-word return or endsub returned a value, 0 otherwise. Cleared by the next O-word call.

* *#<_task>* - 1.0 si la instancia del interpretador es parte de una tarea de mecanizado, 0.0 de lo contrario.

* *#<_call_level>* Nivel actual de los procedimientos de *códiog-O*. Para depuración.

* *#<_remap_level>* Nivel actual de remapeo del stack. Cada remapeo de un bloque agrega un nivel al stack. Para depuración.


Testigos de HAL y valores INI
-----------------------------

Si el archivo de configuración .ini está configurado de esta forma, el código G tendrá acceso a los valores de entrada del archivo .ini y al valor de los testigos
del HAL (Capa de abstraccion de Hardware).

*#<_ini[sección]nombre>* Returna el valor del ítem correspondiente del archivo de configuración .ini. Por ejemplo, si el archivo .ini tiene esta definición::

   [SETUP]
   XPOS = 3.145
   YPOS = 2.718

Podrá referir al parámetro *#<_ini[setup]xpos>* y al *#<_ini[setup]ypos>* en el código g.

La función *EXISTS* puede ser utilizada para verificar la existencia de una definición en el archivo .ini::

   o100 if [EXISTS[#<_ini[setup]xpos>]]
     (debug, [setup]xpos exists: #<_ini[setup]xpos>)
   o100 else
     (debug, [setup]xpos does not exist)
   o100 endif

El valor es leído desde el archivo .ini una sola vez y guardados por el interpretador. Estos valores son solo lectura, si se intenta asignar un valor resulta en error.
Los nombres no diferencian minúsculas/maypusculas, son convertidos a mayúsculas al consultar el archivo .ini.

* *#<_hal[Hal item]>* Permite al código G leer los valores de los testigos (pins) del HAL. El acceso mediante variables es solo lectura, la única forma de modificar las definiciones del HAL desde el código G se restringe a los códigos *M62-M65*, *M67*, *M68* y los códigos definidos por usuario *M100-M199*. Notar que el valor leído no se actualizará en tiempo real, típicamente se leerá el valor que existía cuando se inició la ejecución del código G. Es posible acceder al valor actualizado al forzar un valor con un comando *M66* modificado, *M66E0L0*.

Ejemplo::

   (debug, #<_hal[motion-controller.time]>)

Accede a los ítems del HAL como sólo lectura. Actualmente se puede acceder a los valores del HAL definidos en minúscula.

Se puede utilizar el comando *EXISTS* para verificar la existencia de un ítem de HAL::

   o100 if [EXISTS[#<_hal[motion-controller.time]>]]
     (debug, [motion-controller.time] exists: #<_hal[motion-controller.time]>)
   o100 else
     (debug, [motion-controller.time] does not exist)
   o100 endif


.. _refExpresions:

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

.. _refBinaryOps:

**Operadores Binarios**

Los operadores binarios aparecen sólo dentro de las expresiones. Existen cuatro tipos básicos de operaciones matemáticas: suma (+), resta (-), multiplicación (*) y división (/). Hay 
tres operadores lógicos: O no exclusivo (OR), O exclusivo (XOR) y el opreardor lógico Y (AND). La octava operación es la operación módulo, que devuelve el resto de la división (MOD). 
El noveno operador es la potencia (**), en donde el valor que la antecede es la base y el valor que la sucede es el exponente. Los operadores relacionales son la igualdad (EQ), inequidad (NEQ),
mayor que (GT), mayor o igual que (GE), menor que (LT) y menor o igual que (LE).


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

.. _refFunctions:

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

   G17 define el plano de trabajo XY
   G20 selecciona pulgadas
   G40 cancela la compensación diametral
   G49 cancela el decalaje por largo de herramienta
   G54 para utilizar el sistema de coordenadas 1
   G80 cancela los ciclos cerrados
   G90 define coordenadas absolutas 
   G94 define avance en distancia/minutos.

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

+-------------------------------+--------------------------------------------------------------------------+
|       Comando                 | Descripción                                                              |
+===============================+==========================================================================+
|  :ref:`G0 <refG0>`            | Movimiento coordinado rápido                                             |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G1 <refG1>`            | Movimiento coordinado con velocidad de avance                            |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G2 G3 <refG2>`         | Movimiento de Arco de Círculo o Helicoidal                               |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G4 <refG4>`            | Espera                                                                   |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G5 <refG5>`            | Spline Cúbico                                                            |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G5.1 <refG5.1>`        | Spline Cuadrático                                                        |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G7 <refG7>`            | Modo Diametral (para torneado)                                           |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G8 <refG8>`            | Modo Radial (para torneado)                                              |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G10 L1 <refG10L1>`     | Definición de Parámetros de Herramienta                                  |
+-------------------------------+--------------------------------------------------------------------------+
|  :ref:`G10 L2 <refG10L2>`     | Definición de de Sistema Coordinado                                      |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G10 L10 <refG10L10>`    | Definición de Parámetros de Herramienta en Punto Actual                  |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G10 L11 <refG10L11>`    | Definición de Parámetros de Herramienta en Punto Actual referido a G59.3 |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G10 L20 <refG10L20>`    | Definición de de Sistema Coordinado                                      |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G17-G19.1 <refG17>`     | Selección de Plano de Trabajo                                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G20 G21 <refG20>`       | Selección de Unidades                                                    |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G28 G28.1 <refG28>`     | Ir a posición Predeterminada                                             |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G30 G30.1 <refG30>`     | Ir a posición Predeterminada                                             |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G33 <refG33>`           | Movimiento Sincronizado de Husillo                                       |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G33.1 <refG33.1>`       | Roscado Rígido                                                           |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G38.n <refG38>`         | Sondeo                                                                   |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G40 <refG40>`           | Compensación de Radio de Herramienta Desactivada                         |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G41 G42 <refG41>`       | Compensación de Radio de Herramienta                                     |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G41.1 G42.1 <refG41.1>` | Compensación Dinámica de Radio de Herramienta                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G43 <refG43>`           | Compensación de Largo de Herramienta                                     |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G43.1 <refG43.1>`       | Compensación Dinámica de Largo de Herramienta                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G43.2 <refG43.2>`       | Compensación Adicional de Largo de Herramienta                           |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G49 <refG49>`           | Cancelar Compensación de Largo de Herramienta                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G52 <refG52>`           | Decalaje temporal del Sistema de Coordenadas Local                       |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G53 <refG53>`           | Posición en Sistema de Coordenadas de Máquina                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G54-G59.3 <refG54>`     | Selección de Sistema de Coordenadas Local                                |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G61 <refG61>`           | Modo de Posicionamiento Preciso                                          |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G61.1 <refG61.1>`       | Modo de Posicionamiento Preciso y Frenado                                |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G64 <refG64>`           | Suavizado de Trayectoria                                                 |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G73 <refG73>`           | Ciclo de Perforado con Ruptura de Viruta                                 |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G74 <refG74>`           | Ciclo de Roscado (Tapping) Izquierdo con Huelgo                          |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G76 <refG76>`           | Ciclo de Roscado (Threading) de Varias Pasadas                           |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G80 <refG80>`           | Cancelación de Ciclo Cerrado                                             |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G81 <refG81>`           | Ciclo de Perforado                                                       |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G82 <refG82>`           | Ciclo de Perforado con Espera                                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G83 <refG83>`           | Ciclo de Perforado Profundo                                              |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G84 <refG84>`           | Ciclo de Roscado (Tapping) Derecho con Espera                            |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G85 <refG85>`           | Ciclo de Perforado con Velocidad de Salida                               |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G86 <refG86>`           | Ciclo de Perforado, Freno de Husillo y Velocidad Rápida de Salida        |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G89 <refG89>`           | Ciclo de Perforado, Espera y Velocidad de Salida                         |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G90 G91 <refG90>`       | Modo de Distancia Absoluta o Relativa                                    |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G90.1 G91.1 <refG90.1>` | Modo de Distancia de Arcos Absoluta o Relativa                           |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G92 <refG92>`           | Definir Decalaje de Sistema de Coordenadas en Punto Actual               |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G92.1 G92.2 <refG92.1>` | Resetear Decalaje de Sistema de Coordenadas G92                          |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G92.3 <refG92.3>`       | Restablecer Decalaje de Sistema de Coordenadas G92                       |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G93 G94 G95 <refG93>`   | Modo de Avance                                                           |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G96 G97 <refG96>`       | Modo de Control de Husillo                                               |
+-------------------------------+--------------------------------------------------------------------------+
| :ref:`G98 G99 <refG98>`       | Nivel de Retorno de Ciclos Cerrados                                      |
+-------------------------------+--------------------------------------------------------------------------+




.. _refG0:

G0 Movimiento Rápido
--------------------

::

   G0 ejes

Ejecuta un movimiento coordinado rápido en línea recta, donde todas las posiciones de ejes son opcionales. El *G0* es opcional
si el modo de movimiento *G0* está activo. Este comando se usa típicamente para posicionarse en determinado lugar.

**Velocidad de Avance Rápido**

La velocidad de movimiento rápido se define en el parámetro MAX_VELOCITY del archivo .ini en la sección [TRAJ]. La velocidad máxima
para los movimientos rápidos puede ser mayor a la máxima velocidad individual de los ejes MAX_VELOCITY durante el movimiento coordinado
de varios ejes. La velocidad de traslación rápida puede ser menor a la velocidad de movimiento rápido de la trayectoria si algún eje
limita a ésta.

Si la compensación de herramienta está activa, el movimiento difiere del descripto en el ejemplo, ver sección de :doc:`toolCompensation`.

Si *G53* está definido en la misma línea, el movimiento también se ve modificado; ver sección :ref:`G53 <refG53>` para más información.

..

   La trayectoria de un movimiento rápido *G0* puede verse suavizado en los cambios de dirección y depende de la configuración de :doc:`trajectoryControl`.

Se produce un error si:

   * Hay una letra de eje sin un valor real
   * Se utiliza una letra de eje que no está configurado

**Ejemplo G0**

::

   G90 (modo de coordenadas absolutas)
   G0 X10 Y-23.5 (movimiento lineal rápido desde la posición actual a X10 Y-23.5)
   M2 (fin de programa)

* Ver las secciones :ref:`G90 <refG90>` y :ref:`M2 <refM2>` para más información.


.. _refG1:

G1 Movimiento Lineal
--------------------

::

   G1 ejes

Ejecuta un movimiento coordinado en línea recta a determinada velocidad de avance (para mecanizar o no), donde todas las posiciones de 
ejes son opcionales. El *G1* es opcional si el modo de movimiento *G1* está activo. Este comando se usa típicamente para 
mecanizar trasladandose en una recta desde el punto actual al punto definido.

Si la compensación de herramienta está activa, el movimiento difiere del descripto en el ejemplo, ver sección de :doc:`toolCompensation`.

Si *G53* está definido en la misma línea, el movimiento también se ve modificado; ver sección :ref:`G53 <refG53>` para más información.

Se produce un error si:

   * No se ha definido la velocidad de avance
   * Hay una letra de eje sin un valor real
   * Se utiliza una letra de eje que no está configurado

**Ejemplo G1**

.. figure:: images/g1example.png
   :width: 300

::

   G17 S400 M3 (plano de trabajo XY, velocidad de husillo 400 en sentido horario)
   G90 (modo de coordenadas absolutas)
   G0 X20 Y20 Z2 (aproximación a punto inicial)
   G1 Z-2 F40 (movimiento lineal Z-2 a una velocidad de avance de 40)
   X80 Y80 Z-15 (mecanizado en línea recta a punto final)
   G0 Z100 (retiro)
   M2 (fin de programa)

* Ver las secciones :ref:`G17 <refG17>`, :ref:`S <refS>`, :ref:`M3 <refG90>`, :ref:`G90 <refG90>`, :ref:`F <refF>` y :ref:`M2 <refM2>` para más información.


.. _refG2:

G2 G3 Movimiento Arco de Círculo o Helicoidal
---------------------------------------------

::

   G2 o G3 ejes distancias (definición de centro y punto final)
   G2 o G3 ejes R- (definición de radio y punto final)
   G2 o G3 distancias|R- <P-> (circulos completos)

Estos comandos generan un movimiento con forma de arco de círculo o un movimiento helicoidal a una velocidad de avance definida. 

Opciones para la definición:

* Centro de círculo y punto final en coordenadas absolutas o relativas
* Radio y centro de círculo
* Para ambas opciones anteriores el parámetro P- es opcional y permite círculos de varias vueltas

Los ejes del arco de círculo o helicoide deben ser paralelos a los ejes X, Y o Z del sistema de coordenadas de la máquina. El eje
de rotación (o equivalentemente el plano perpendicular al eje) se selecciona con :ref:`G17 <refG17>` (eje Z, plano XY), :ref:`G18 <refG17>`
(eje Y, plano XZ) o :ref:`G19 <refG17>` (eje X, plano YZ). 

Si el punto final se encuentra en el mismo plano de trabajo que el punto de inicio (posición actual) el comando resulta en un arco de círculo plano.

.. figure:: images/arc.png
   :width: 250
   
   Arco de Círculo


Para programar un helicoide incluya una componente de traslación en la dirección del eje de rotación, por ejemplo si *G17* está activo,
al incluir una palabra Z- habrá un movimiento perpendicular al plano del arco de círculo. Al ejecutar el movimiento, la componente fuera
del plano es proporcional al desarrollo del arco de círculo.

.. figure:: images/helix.png
   :width: 250
   
   Helicoide

Para programar un arco de círculo que describa más de una vuelta completa se utiliza el parámetro opcional *P-*, que especifica la cantidad
de vueltas completas. Si *P* no se define el comportamiento es equivalente a especificar *P1*, esto es, solo una vuelta completa o vuelta 
parcial se ejecuta. Por ejemplo, para una arco de 180 grados programado con P2, el movimiento resultante será de una revolución y media.
Es decir por cada valor por encima de 1 resulta una vuelta completa adicional. Se pueden definir movimientos helicoidales de varias vueltas,
que resultan útiles para mecanizar agujeros o roscas.

Si la compensación de herramienta está activa, el movimiento difiere del descripto en el ejemplo, ver sección de :doc:`toolCompensation`.

El centro del arco de círculo se da en coordenadas absolutas o relativas de acuerdo a los comandos :ref:`G90.1 G91.1 <refG90.1>` respectivamente.

Se produce un error si:

   * No se ha definido la velocidad de avance
   * La letra P no es un entero

*G2* se utiliza para movimientos en el sentido horario y *G3* para movimientos en sentido antihorario.
La referencia del sentido se toma respecto a la dirección positiva del eje alrededor del cual el movimiento circular ocurre.

De acuerdo al plano de trabajo activo los sentidos de giro resultan de la siguiente manera:

.. figure:: images/G2G3directionsForPlanes.png
   :width: 300

**Centro y punto final**

La definición mediante el centro del arco de círculo es más precisa que la definición por medio del radio por lo que su uso es más recomendable.

Se debe definir la posición del punto final y la del centro del círculo, opcionalmente el parámetro de cantidad de vueltas. No hay inconveniente en
que el punto final coincida con el punto inicial. 

El comando resulta en error si hay una diferencia significativa entre el radio inicial y final, por lo que se recomienda utilizar por lo menos 3 decimales
para la definición de los puntos.

Se puede definir la posición del centro en coordenadas relativas o absolutas:

   **Definición de posiciones relativas**
   
      Se define el centro del círculo como la posición relativa desde el punto de inicio (posición actual). Este modo está activado por defecto.
      
      Para arcos que no son múltiplos de 360 grados se debe definir la posición final de por lo menos algún eje Y la posición del centro de
      por lo menos un eje.
      
      Para arcos múltiplos de 360 no es necesario definir la posición final y se debe definir la posición del centro por lo menos en algún eje.
      El parámetro P es opcional y por defecto es 1.
      
      Para más información ver *Coordenadas relativas para arcos* :ref:`G91.1 <refG90.1>`.
   
   **Definición de posiciones absolutas**
   
      Se define el centro del círculo como la posición absoluta en el sistema de coordenadas activo.
      
      Para arcos que no son múltiplos de 360 grados se debe definir la posición final de por lo menos algún eje Y la posición del centro de
      círculo en ambos ejes.
      
      Para arcos múltiplos de 360 no es necesario definir la posición final y se debe definir la posición del centro en ambos ejes.
      El parámetro P es opcional y por defecto es 1.
      
      Para más información ver *Coordenadas absolutas para arcos* :ref:`G90.1  <refG90.1>`

   **Plano XY (G17)**

   ::
   
      G2 o G3 <X- Y- Z- I- J- P->
   
   * I- posición en X del centro
   * J- posición en Y del centro
   * Z- componente de helicoide
   * P- número de vueltas
   
   **Plano XZ (G18)**
   
   ::
   
      G2 o G3 <X- Z- Y- I- K- P->
   
   * I- posición en X del centro
   * K- posición en Z del centro
   * Y- componente de helicoide
   * P- número de vueltas

   **Plano YZ (G19)**

   ::

      G2 o G3 <Y- Z- X- J- J- P->

   * I- posición en Y del centro
   * K- posición en Z del centro
   * X- componente de helicoide
   * P- número de vueltas

Se produce un error si:

   * No se ha definido la velocidad de avance
   * No se definió la posición del centro
   * Cuando el arco es proyectado en el plano de trabajo, la distancia desde la posición inicial al centro y 
     la distancia desde el punto final al centro difieren más de 0.5 mm o 0.1% del radio.

El error *El radio al final difiere del radio al inicio* refiere a:

   * *Inicio* - la posición inicial
   * *Centro* - la posición del centro calculadas utilizando las letras i, j o k
   * *Fin* - el punto final programado
   * *r1* - radio desde el punto inicial al centro
   * *r2* - radio desde el punto final al centro

   **Ejemplos de Centro y punto final**

   Calcular las coordenadas de los arcos a mano puede ser dificil a veces. Una alternativa puede ser realizar el dibujo en un programa de CAD para
   obtener las coordenadas de los puntos inicial y final y del centro del círculo. 

   **Ejemplo - Cuarto de Círculo**

.. figure:: images/exampleG2a.png
   :width: 300

   Se pueden definir este arco de las siguientes maneras::

      G90 (coordenadas absolutas)
      G18 (plano de trabajo XZ)
      G0 X 15 Z 10 (punto inicial)
      (G91.1 activado por defecto)
      G2 X 40 Z 35 I25 F10
      M2 (fin de programa)

   ::

      G90 (coordenadas absolutas)
      G0 X 15 Z 10 (punto inicial)
      G18 (plano de trabajo XZ)
      G90.1 (coordenadas absolutas para centro de círculo)
      G2 X 40 Z 35 I15 K35 F10
      M2 (fin de programa)

   **Ejemplo - Helicoide**

.. figure:: images/exampleHelix.png
   :width: 300

   Se pueden definir este helicoide de la siguiente manera::

      G90 (coordenadas absolutas)
      G17 (plano de trabajo XY)
      G0 X 27.5 Y 32.99 Z3 (acercar a punto inicial)
      G90.1 (coordenadas absolutas para centro de círculo)
      G3 X 20 Y5 Z -20 I20 J20 P3 F10 (helicoide, centro de arco en (20,20), más dos vueltas completas hasta punto final)
      M2 (fin de programa)

**Radio y punto final**

   ::

      G2 o G3 <X- Y- Z-> R- <P->

   * R- radio del círculo

No es buena práctica utilizar este tipo de definición - radio y punto final - para describir arcos que sean similares a un círculo o a un semicírculo debido a
que pequeños cambios en la ubicación del punto final producen cambios muchos más grandes en la ubicación del centro del círculo. El efecto de magnificación
del error de redondeo puede producir mecanizados fuera de tolerancia. Por ejemplo, errores de ubicación del 1% del punto final produce errores del 7% 
en un punto a 90 grados. Para arcos similares a un círculo completo, este problema se magnifica. Para otros arcos, desde pequeños ángulos a 165 grados y de
195 a 345 grados esta opción es aceptable.

En este tipo de definición se debe determinar por lo menos una de las coordenadas del punto final en el plano de trabajo y el radio del círculo. Cuando el 
arco de círculo se define de esta manera siempre hay dos opciones compatibles, un arco de círculo más corto y un arco de mayor desarrollo. Para diferenciarlos 
se puede utilizar un valor del radio R positivo para indicar arcos menores a 180 grados mientras que valores negativos del radio indican arcos de más de 180 grados.

   Se produce un error si:

      * Se omiten ambas coordenadas del punto final en el plano de trabajo
      * El punto final es igual al punto inicial

**Ejemplo - Radio y punto final**


.. figure:: images/exampleG3radius.png
   :width: 300

   Se pueden definir estos arcos círculo de las siguientes maneras:

   ::

      G90 (coordenadas absolutas)
      G17 (plano de trabajo XY)
      G0 X30 Y40 (ir a punto inicial)
      G3 Y10 R16 F10 (arco de círculo corto)
      M2 (fin de programa)

   ::

      G90 (coordenadas absolutas)
      G17 (plano de trabajo XY)
      G0 X30 Y40 (ir a punto inicial)
      G3 Y10 R-16 F10 (arco de círculo largo)
      M2 (fin de programa)

.. _refG4:

G4 Espera
---------

::

   G4 P-

* *P-* tiempo de espera en segundos

El número *P* es el número de segundos que los ejes van a permanecer inmóviles. El valor es un punto flotante por lo que se pueden utilizar fracciones de 
segundos. El comando *G4* no afecta al refrigerante, husillo ni a las entradas / salidas.

**Ejemplo**

::

   G4 P0.5 (espera 0.5 segundos antes de proceder)

Se produce un error si:

* el número P es negativo o no está especificado

.. _refG5:

G5 Spline Cúbico
----------------

::

   G5 X- Y- <I- J-> P- Q-

* *I-* Coordenada relativa en X desde el punto inicial al primer punto de control
* *J-* Coordenada relativa en Y desde el punto inicial al primer punto de control
* *P-* Coordenada relativa en X desde el punto final al segundo punto de control
* *Q-* Coordenada relativa en Y desde el punto final al segundo punto de control

*G5* crea una curva del tipo B-spline cúbica en el plano XY sólo con los ejes X e Y. Tanto P como Q deben ser especificados para todo comando *G5*.

Para el primer comando *G5* de una serie de comandos *G5*, tanto I como J deben ser especificados. Para los comandos *G5* subsecuentes, es posible
especificar ambos, I y J, o ninguno de los dos. Si I y J no se especifican, la dirección inicial de la curva coincidirá con la dirección final de la
curva previa (como si los parámetros I y J fueran iguales y opuestas de los parámetros P y Q anteriores).

Por ejemplo, para programar una curva con forma de N:

**Ejemplo de spline cúbico inicial**::

   G90 G17
   G0 X0 Y0
   G5 I0 J3 P0 Q-3 X1 Y1

Un segundo segmento de con forma de N que se concatena suavemente con el primero puede programarse sin especificar I y J.

**Ejemplo de spline cúbico subsecuente**::

   G5 P0 Q-3 X2 Y2

Da un error si:

   * No se especifican ambos valores de P y Q
   * Solo se especifica un valor de I o J
   * I y J no se especifican en el primero de una serie de comandos *G5*
   * Se define algún eje que no sea X e Y
   * El plano de trabajo activo no es G17


.. _refG5.1:

G5.1 Spline Cuadrático
-----------------------

::

   G5.1 X- Y- I- J-

* *I-* Coordenada relativa en X desde el punto inicial al punto de control
* *J-* Coordenada relativa en Y desde el punto inicial al punto de control

*G5.1* crea una curva tipo B-spline cuadrática en el plano XY sólo con los ejes X e Y. No especificar I o J da un eje no 
especificado, por lo que ambos valores deben ser definidos.

Por ejemplo, si se desea programar una parábola que pase por el origen y por los puntos X-2 Y4 y X2 Y4:

**Ejemplo de spline cuadrático**::

   G90 G17
   G0 X-2 Y4
   G5.1 X2 I2 J-8

Da un error si:

   * Si ambos valores de I o J no se especifican o son 0
   * Se define algún eje que no sea X e Y
   * El plano de trabajo activo no es G17


.. _refG7:

G7 Modo Diametral (para torneado)
---------------------------------

::

   G7

El comando *G7* activa el modo diametral para el eje X de un torno. Cuando el modo diametral está activo el eje X se mueve
a la mitad de la distancia respecto al eje del husillo. Esto hace que se pueda definir como posición la cota que corresponde 
al diámetro de una pieza. Ver Figura :ref:`G7 G8 <refFigureG7G8>`


.. _refG8:

G8 Modo Radial (para torneado)
---------------------------------

::

   G8

El comando *G8* activa el modo radial (modo diametral inactivo) para el eje X de un torno. Cuando el modo radial está activo el eje X se mueve
a la distancia especificada respecto al eje del husillo. Esto hace que al definir como posición una cota, el diámetro de la pieza resulte
en el doble de la posición especificada. 

   **Ejemplo**

.. _refFigureG7G8:

.. figure:: images/diamOnOffg7g8.png
   :width: 300
   
   Modo diametral activo *G7* y modo radial (modo diametral inactivo) *G8*

   ::

      S2000 M3 (activar husillo)
      G8 (modo radial)
      G0 X10 Z0 (posición X = radio)
      G1 X10 Z-20 F0.5 (posición X = radio)
      G7 (modo diametral)
      G1 X50 Z-30 (posición X = diámetro)
      G1 X50 Z-55 (posición X = diámetro)

.. _refG10L1:

G10 L1 Definición de Parámetros de Herramienta
----------------------------------------------

::

   G10 L1 P- ejes <R- I- J- Q->

* *P-* número de herramienta
* *R-* radio de la herramienta
* *I-* ángulo frontal (torno)
* *J-* ángulo posterior (torno)
* *Q-* orientación (torno)

*G10 L1* define las dimensiones de la herramienta *P* en la tabla de herramienta a los valores utilizados en la línea.
Un comando *G10 L1* redefine los valores y recarga la tabla de herramientas, donde se almacena toda la información sobre la geometría de las mismas.

**Ejemplo**::

   G10 L1 P1 Z1.5 (define el decalaje en dirección Z desde el origen hasta el filo de la herramienta 1 a un valor 1.5)
   G10 L1 P2 R12.5 Q3 (ejemplo para torneado - define el radio de herramienta con un valor de 12.5 y orientación 3 para la herramienta 2)

Da un error si:
   
   * La compensación de herramienta está activa
   * El número *P* no se especifica
   * El número *P* no es un número de herramienta válido para la tabla de herramientas
   * El número P es 0.

Para más información sobre la orientación de herramientas ver la sección :doc:`toolCompensation`.

.. _refG10L2:

G10 L2 Definición de Sistema Coordinado
---------------------------------------

::

   G10 L2 P- <ejes R->

* *P-* sistema coordenado (0-9)
* *R-* rotación alrededor del eje Z

*G10 L2* define la posición del sistema de coordenadas *P* a los valores utilizados en la línea. Los valores definidos reemplazarán los valores existentes
grabados anteriormente para ese sistema de coordenadas. Los valores no especificados permanecerán sin cambios.

Utilice *P0* a *P9* para especificar el sistema de coordenadas.

+------------------+---------------------------+-------------------+
| Valor de *P*     | Sistema de Coordenadas    |    Código G       |
+==================+===========================+===================+
|         0        |        Activo             |        n/a        |
+------------------+---------------------------+-------------------+
|         1        |           1               |        G54        |
+------------------+---------------------------+-------------------+
|         2        |           2               |        G55        |
+------------------+---------------------------+-------------------+
|         3        |           3               |        G56        |
+------------------+---------------------------+-------------------+
|         4        |           4               |        G57        |
+------------------+---------------------------+-------------------+
|         5        |           5               |        G58        |
+------------------+---------------------------+-------------------+
|         6        |           6               |        G59        |
+------------------+---------------------------+-------------------+
|         7        |           7               |        G59.1      |
+------------------+---------------------------+-------------------+
|         8        |           8               |        G59.2      |
+------------------+---------------------------+-------------------+
|         9        |           9               |        G59.3      |
+------------------+---------------------------+-------------------+

Opcionalmente utilice *R* para indicar la rotación de los ejes XY alrededor del eje Z. El sentido de rotación es
antihorario visto desde la dirección positiva de Z.

Todos las definiciones de ejes son opcionales.

Si el modo de coordenadas incremental está activo (:ref:`G91  <refG90>`) no tiene efecto en el comando *G10 L2*.

Conceptos importantes:

   * *G10 L2 Pn* no cambia de sistema de coordenadas que se está utilizando para definir posiciones, para eso debe utilizar *G54-G59.3*
   * Cuando una rotación está en efecto, al mover un eje en modo de intervención manual (Jog) moverá solo ese eje en la dirección
     positiva o negativa pero no en la dirección rotada.
   * Si hay un decalaje temporal definido mediante :ref:`G52  <refG52>` o hay un decalaje definido mediante :ref:`G92  <refG92>` en 
     efecto anteriormente a *G10 L2*, permacerán en vigencia luego del comando.
   * Cuando se programa una rotación mediante *R*, cualquier :ref:`G52  <refG52>` o :ref:`G92  <refG92>` se aplica **luego** de la rotación.
   * El sistema de coordenadas uya posición se ve afectada por medio de una comando *G10* puede estar activo o inactivo en ese momento. 
     Si está activo, la nueva posición tiene efecto inmediato.

Da error si:

   * El número *P* no se puede evaluar en un entero en el rango 0 a 9
   * Se programa un eje que no está definido en la configuración

**Ejemplo**::

   G10 L2 X35.2 Y17.8

En la línea anterior se define la posición del sistema de coordenadas 1 (el que se selecciona con el comando *G54*) a los valores de X = 35.2
e Y = 17.8. Debido a que solo X e Y se han definido, el origen del sistema de coordenadas se mueve mientras que las otras coordenadas no se mueven.


.. admonition:: Nota
   :class: note

   Adicionalmente al decalaje o posición del sistema de coordenadas de pieza, se superpone el efecto de las funciones de transformación, que permiten
   trasladar, rotar, escalar o espejar el sistema de refererncia. Para más infromación ver la sección de :ref:`Transformación de Sistemas Coordenados  <transfCoords>`


.. _refG10L10:

G10 L10 Definición de Parámetros de Herramienta en Punto Actual
---------------------------------------------------------------

::

   G10 L10 P- eje <R- I- J- Q->

* *P-* número de herramienta
* *R-* radio de la herramienta
* *I-* ángulo frontal (torno)
* *J-* ángulo posterior (torno)
* *Q-* orientación (torno)

*G10 L10* cambia los valores de decalaje de la herramienta *P* en la tabla de herramientas para que si los decalajes se recargan, con la máquina en 
la posición actual y los decalajes activos que correspondan al sistema actual (*G5x* y *G52/G92*), las coordenadas actuales para los ejes determinados 
se conviertan en los valores dados. Los valores que no se especifican en el comando *G10 L10* no serán modificados. Este comando es útil particularmente
cuando se utiliza un sensor de contacto, como se describe en la sección :ref:`G38 <refG38>`.

**Ejemplo**::

   T1 M6 G43 (carga la herramienta 1 y sus decalajes)
   G10 L10 P1 Z1.5 (define la posición actual en Z para que sea 1.5)
   G43 (recarga los decalajes de la tabla ya cambiada)
   M2 (fin de programa)

* Para más información ver secciones :ref:`T  <refT>`, :ref:`M6  <refM6>`, :ref:`G43  <refG43>` y  :ref:`G43.1  <refG43>`.

Da un error si:

   * La compensación de herramienta está activa
   * El número *P* no se especifica 
   * El número *P* no es un número válido de la tabla de herramientas
   * El número *P* es 0


.. _refG10L11:

G10 L11 Definición de Parámetros de Herramienta en Punto Actual referido a G59.3
--------------------------------------------------------------------------------

::

   G10 L11 P- ejes <R- I- J- Q->

* *P-* número de herramienta
* *R-* radio de la herramienta
* *I-* ángulo frontal (torno)
* *J-* ángulo posterior (torno)
* *Q-* orientación (torno)

*G10 L11* es igual a *G10 L10* excepto por que en vez de definir los valores de acuerdo a los decalajes actuales, se definen de manera tal que las 
coordenadas actuales se conviertan a los valores dados si se recargan los nuevos valores de decalajes y la máquina se posiciona con el sistema de 
coordenadas *G59.3* sin los decalajes *G52*/*G92*.

Esto permite al usuario definir el sistema de coordenadas *G59.3* de acuerdo a un punto fijo de la máquina y luego usar ese punto independientemente 
de otros decalajes activos.

Da un error si:
   
   * La compensación de herramienta está activa
   * El número *P* no se especifica 
   * El número *P* no es un número válido de la tabla de herramientas
   * El número *P* es 0

   
.. _refG10L20:

G10 L20 Definición de Sistema Coordinado
----------------------------------------

::

   G10 L20 P- ejes

* *P-* número de herramienta

*G10 L20* es similar a *G10 L2* excepto que en vez de definir el valor en la tabla, define un valor calculado que hace que las coordenadas
actuales se conviertan en el valor dado.

**Ejemplo**:

   G10 L20 P1 X1.5 (define la posición actual en X como 1.5 para el sistema de coordenadas 1)

Da error si:

   * El número *P* no se puede evaluar en un entero en el rango 0 a 9
   * Se programa un eje que no está definido en la configuración


.. _refG17:

G17-G19.1 Selección de Plano de Trabajo
---------------------------------------

Estos comandos seleccionan el plano de trabajo:

   * *G17* - XY (por defecto)
   * *G18* - ZX
   * *G19* - YZ
   * *G17.1* - UV
   * *G18.1* - WU
   * *G19.1* - VW

En los planos Uv, Wu y VW no se pueden utilizar los arcos de círculos.

Es una buena práctica seleccionar el plano de trabajo en el preambulo de los archivo de código G.

El efecto de seleccionar el plano de traajo se muestra en las secciones sobre arcos :ref:`G2 G3 <refG2>`, :ref:`G81  <refG81>` y :ref:`G89 <refG89>`.


.. _refG20:

G20 G21 Selección de Unidades
------------------------------

   * *G20* - para utilizar pulgadas como unidades de longitud
   * *G21* - para utilizar milímetros como unidades de longitud

Es una buena práctica seleccionar las unidades en el preambulo de los archivo de código G.

.. _refG28:

G28 G28.1 Ir a posición Predeterminada
--------------------------------------

.. admonition:: Precaución
   :class: warning

   Solo use *G28* cuando se han referenciado los ejes (homing) a una posición repetible y la posición deseada *G28* ha sido guardada con *G28.1*

*G28* utiliza los valores guardados en los parámetros 5161 - 5169 como los ejes X Y Z A B C U V W como el punto final al cual moverse. Los valores
de los parámetros son coordenadas de máquinas *absolutas* en las unidades *originales* de la máquina como están especificadas en el archivo .ini.
Todos los ejes definidos en el archivo .ini serán movilizados cuando se ejecuta el comando *G28*. Si no hay posiciones guardades con *G28.1*, entonces
todos los ejes se posicionarán en el origen de la máquina.

   * *G28* realiza un movimiento rápido desde la posición actual a la posición *absoluta* definida por los valores de los parámetros 5161-5169
   * *G28 ejes* realiza un movimiento rápido a la posición definida en *ejes* inluyendo los decalajes, luego hace un movimiento rápido a la posición
     *absoluta* definida por los valores de los parámetros 5161-5169. Cualquier *eje* no especificado no se moverá
   * *G28.1* guarda la posición *absoluta* actual en los parámetros 5161-5169

**Ejemplo**::

   G28 Z2.5 (movimiento rápido a Z2.5 luego a la posición Z especificada en #5163)

Da un error si:

   * La compensación de herramienta está activa


.. _refG30: 

G30 G30.1 Ir a posición Predeterminada
--------------------------------------

.. admonition:: Precaución
   :class: warning

   Solo use *G30* cuando se han referenciado los ejes (homing) a una posición repetible y la posición deseada *G30* ha sido guardada con *G30.1*

El comando *G30* funciona igual al comando *G28* pero utiliza los valores guardados en los parámetros 5181 - 5189 como los ejes X Y Z A B C U V W como el punto final al cual moverse.
Los valores de los parámetros son coordenadas de máquinas *absolutas* en las unidades *originales* de la máquina como están especificadas en el archivo .ini.
Todos los ejes definidos en el archivo .ini serán movilizados cuando se ejecuta el comando *G30*. Si no hay posiciones guardades con *G30.1*, entonces
todos los ejes se posicionarán en el origen de la máquina.

.. admonition:: Nota

   Los parametros *G30* son usados para mover la herramienta cuando se utiliza el comando *M6* si *TOOL_CHANGE_AT_G30=1* está definido en la sección *[EMCIO]* del archivo .ini.

* *G30* realiza un movimiento rápido desde la posición actual a la posición *absoluta* definida por los valores de los parámetros 5181-5189
* *G30* *ejes* realiza un movimiento rápido a la posición definida en *ejes* inluyendo los decalajes, luego hace un movimiento rápido a la posición *absoluta* definida 
  por los valores de los parámetros 5181-5189. Cualquier *eje* no especificado no se moverá
* *G30.1* guarda la posición *absoluta* actual en los parámetros 5181-5189

**Ejemplo**::

   G30 Z2.5 (movimiento rápido a Z2.5 luego a la posición Z especificada en #5183)

Da un error si:

   * La compensación de herramienta está activa


.. _refG33:

G33 Movimiento Sincronizado de Husillo
--------------------------------------

::

   G33 X- Y- Z- K- $-

* K- distancia por revolución de husillo

El comando *G33* se utiliza para movimientos sincronizados de husillo en una dirección definida por XYZ, donde *K* determina la distancia que se mueve en esa dirección 
por cada revolución del husillo. Por ejemplo, empezando en *Z=0*, *G33 Z-1 K.0625* produce un movimiento de un pulgada (de estar activo *G20*) en dirección *Z* para 16 
revoluciones de husillo. Este comando podría ser parte de un programa para producir un roscado de 16 TPI (filetes por pulgada).

El argumento opcional *$* define cuál husillo es el que se sincroniza (por defecto el 0). Por ejemplo *G33 Z10 K1 $1* hará que el husillo 1 se mueva en sincronía con el valor
del testigo (pin) de HAL *spindle.N.revs*.

El movimiento sincronizado de husillo espera a los testigos (pins) de índice de husillo y husillo en velocidad, por lo que deben estar ambos activos. *G33* mueve el extremo
al punto final programado. El comando *G33* puede ser utilizado para realizar roscas cónicas.

Todos las palabras de ejes son opcionales, por lo menos una debe ser utilizada.

.. admonition:: Nota

   El valor *K* sigue la dirección descripta por *X- Y- Z-*. *K* no es paralera a Z si los valores X o Y del punto final del punto final son usados, por ejemplo para roscas cónicas.

**Información Técnica**

Al principio de un movimiento *G33*, el controlador utiliza la velocidad del husillo y los límites de aceleración de la máquina para calcular el tiempo de aceleración en la dirección
XYZ luego de que el testigo se active y determina la cantidad de grados que deberá rotar el husillo durante ese tiempo. Luego adiciona ese ángulo al testigo de posición y calcula 
la posición XYZ usando el ángulo corregido del husillo. Eso significa que la ubicación XYZ llegará a la posición adecuada al terminar de acelerar a la velocidad correcta, y que
podrá empezar a mecanizar adecuadamente el roscado.

**Conexiones de HAL**

El testigo (pin) de HAL *spindle.N.at-speed* debe tener valor *Verdadero* (true) para que empiece el movimiento. Adicionalmnete *spindle.N.revs* debe incrementarse en 1 para cada
revolución del husillo y el testigo *spindle.N.index-enable* debe estar conectado a un contador de encoder que resetea al *index-enable* en cada revolución.

**Ejemplo**::

   G90 (modo de coordenadas absolutas)
   G0 X1 Z0.1 (movimiento rápido)
   S100 M3 (arranca giro de husillo)
   G33 Z-2 K0.125 (mover eje Z a -2 a una velocidad de 0.125 por revolución)
   G0 X1.25 (movimiento rápido fuera de línea de trabajo)
   Z0.1 (movimiento rápido a la posición de inicio en Z)
   M2 (fin de programa)

Para más información ver secciones :ref:`G90 <refG90>`, :ref:`G0 <refG0>` y :ref:`M2 <refM2>`.

Da un error si:

   * Se omiten todas las palabras de ejes
   * El husillo no está en movimiento cuando el comando se ejecuta
   * El movimiento lineal requerido excede los límites de velocidad de la máquina debido a la velocidad del husillo


.. _refG33.1:

G33.1 Roscado Rígido
---------------------

::

   G33.1 X- Y- Z- K- I- $-

* *K-* distancia por revolución de husillo
* *I-* multiplicador de velocidad para retorno rápido, opcional
* *$-* selector del husillo, opcional|

.. admonition:: Precaución
   :class: warning

   Para roscado en Z solamente posicione previamente la ubicación de los ejes XY antes de llamar *G33.1* y solo utilice la palabra Z en el comando
   *G33.1*. Si las coordenadas especificadas no son las coordenadas actuales cuando se ejecuta *G33.1* para el roscado, el movimiento no se producirá
   sólo en el eje Z, sino que será un movimiento coordinado, sincronizado con el husillo, desde la posición actual a la posición especificada y de vuelta.

El comando *G33.1* se utiliza para roscado rígido (movimiento de husillo sincronizado con retorno), donde *K-* define la distancia de avance por cada revolución del husillo.

El roscado rígido posee la siguiente secuencia:

   #. Un movimiento desde la coordenada actual a la coordenada especificada, sincronizado con el husillo seleccionado y con el avance especificado, comenzando de acuerdo al pulso de ubicación del husillo.
   #. Al alcanzar el punto final un comando para invertir el giro del husillo y retroceder a una velocidad más elevada definida por el multiplicador.
   #. Continuación del movimiento coordinado más allá de la coordenada especificada hasta que el husillo efectivamente frene e invierta el giro.
   #. Continuación del movimiento coordinado de vuelta a la coordenada original
   #. Al alcanzar la coordenada original, un nuevo comando para invertir el giro del husillo
   #. Continuación del movimiento coordinado más allá de la coordenada original hasta que el husillo efectivamente frene e invierta el giro.
   #. Un movimiento *No sincronizado* de vuelta a la coordenada inicial.

Los movimientos sincronizados de husillo esperan al pulso de ubicación del husillo de forma que múltiples pasadas *G33.1* coinciden en su ubicación.

Todas las palabras de ejes son opcionales, pero por lo menos una debe utilizarse.

**Ejemplo**::

   G90 (modo de coordenadas absolutas)
   G0 X1 Y1 Z0.1 (movimiento rapido a punto inicial)
   S1000 M3 (arranca giro de husillo)
   G33.1 Z-0.75 K0.05 (roscado rígido de 20 filetes por pulgada de 0.75 de profundidad)
   M2 (fin de programa)

* Para más información ver secciones :ref:`G90 <refG90>`, :ref:`G0 <refG0>` :ref:`M2 <refM2>`.

Da un error si:

   * Se omiten todas las palabras de ejes
   * El husillo no está en movimiento cuando el comando se ejecuta
   * El movimiento lineal requerido excede los límites de velocidad de la máquina debido a la velocidad del husillo

.. _refG38:

G38.n Sondeo
------------

::

   G38.n ejes

* *G38.2* - sonda hacia la pieza, parar en caso de contacto, señal de error si falla
* *G38.3* - sonda hacia la pieza, parar caso de en contacto
* *G38.4* - sonda en contra de la pieza, parar al perder contacto, señal de error si falla
* *G38.5* - sonda en contra de la pieza, parar al perder contacto

.. admonition:: Importante

   No se puede utilizar la sonda o sensor de contacto hasta que la máquina esté configurada para trabajar con una señal de 
   entrada para la sonda. Esta señal debe estar conectada al testigo *motion.probe-input* en el archivo .hal. El comando *G38.n* 
   utiliza el testigo (pin) *motion.probe-input* para determinar cuando el sensor ha hecho (o ha perdido) contacto. *Verdadero*
   para sondas de contacto normal cerrado (tocando), *Falso* para sondas de contacto normal abierto.

Utilice el comando *G38.n* para implementar operaciones con sensores de contacto. Las palabras de ejes son opcionales, salvo que 
es necesario utiliza por lo menos una. Las posiciones de ejes definen el punto de destino hacia el que se moverá la sonda, empezando
por la posición actual. Si la sonda no hace contacto (o no deja de hacer contacto) al llegar a destino *G38.2* o *G38.4* emiten un 
error.

En respuesta a este comando la máquina mueve el punto de control (que debería estar en el centro de la esfera de la sonda) en línea
recta a la presente velocidad de avance hacia el punto programado. El movimiento se frena (dentro de los límites de aceleración) 
cuando el punto programado es alcanzado, o cuando se produce un cambio en el estado de la sonda, lo que ocurra primero.

Se puede utilizar un comentario con el formato *(PROBEOPEN filename.txt)* para abrir el archivo *filename.txt* y guardad los valores 
de las 9 coordenadas XYZABCUVW de cada procedimiento satisfactorio de búsqueda de contacto. El archivo debe ser cerrrado con 
*(PROBECLOSE)*. Para más información ver la sección de :ref:`refComentarios`.

Da un error si:

   * La posición actual es la misma que el punto programado
   * No se utiliza alguna palabra de eje
   * La compensación de herramienta está activa
   * La velocidad de avance es nula
   * La sonda ya está en el estado objetivo (activa para *G38.3* por ejemplo)


.. _refG40:

G40.n Compensación de Radio de Herramienta Desactivada
------------------------------------------------------

::

   G40

El comando *G40* desactiva la compensación de herramienta. Si la compensación de herramienta estaba activo, para que tenga efecto el siguiente
movimiento debe ser un movimiento lineal con un desplazamiento mayor al diámetro de la herramienta. En caso de no estar activo es posible 
utilizar este comando.

**Ejemplo de G40**::

   ; la posición actual es X1 luego de un movimiento compensado
   G40 (desactivar la compensación)
   G0 X14 (movimiento linea más largo que el diámetro de herramienta)
   M2 (fin de programa)

* Para más información ver secciones :ref:`G0 <refG0>` y :ref:`M2 <refM2>`

Da un error si:

   * Se utiliza un comando *G2/G3* a continuación de *G40*
   * El movimiento linealluego de desactivar la compensación es menor al diámetro de la herramienta.


.. _refG41:

G41 G42 Compensación de Radio de Herramienta
--------------------------------------------

::

   G41 <D-> (a la izquierda de la trayectoria programada)
   G42 <D-> (a la derecha de la trayectoria programada)

* *D-* número de herramienta

La palabra *D* es opcional, si no se define el radio de la herramienta cargada actual será utilizado (si no hay herramienta cargada y no se 
especifica la palabra *D* se utiliza un radio igual a cero).

Si se define la palabra *D*, hace referencia al número de herramienta del cuál se selecciona el radio de compensación. Normalmente es el número
de herramienta a utilizar (en cuyo caso el uso de la palabra *D* es redundante y no necesita ser utilizada), pero podría ser cualquier número 
válido de herramienta.

.. admonition:: Nota

   El comando *G41/G42* *D0* es especial. Su comportamiento difiere si la máquina tiene un cambiador de herramientas que permita cambios 
   aleatorios o no (ver sección de Cambios de Herramienta REFERENCIA ). En máquinas con cambiadores de herramientas 
   no aleatorios el comando *G41/G42* *D0* aplica el decalaje de la herramienta que está en uso o el decalaje nulo si no hay una herramienta
   cargada. En máquinas que tienen cambiadores aleatorios *G41/G42* *D0* aplica el decalaje de la herramienta T0 de la tabla de herramientas
   (o da error si la herramienta T0 no está definida en la tabla de herramientas).

Para activar la compensación de herramienta a la izquierda de la trayectoria utilice el comando *G41*. Este comando corre la ubicación real 
de la herramienta para que el filo se ubique sobre la línea programada, ubicándola a la izquierda visto desde el extremo positivo del eje 
perpendicular al plano.

Para activar la compensación de herramienta a la derecha de la trayectoria utilice el comando *G42*. Este comando corre la ubicación real 
de la herramienta para que el filo se ubique sobre la línea programada, ubicándola a la derecha visto desde el extremo positivo del eje 
perpendicular al plano.

El largo del movimiento debe ser igual omayor al radio de la herramienta. El movmimiento puede ser un movimiento rápido.

La compensación de herramienta puede ser realizado si el plano XY o el XZ está activos.

Los comandos *M100-M199* están permitidos al estar activa la compensación de herramienta.

El comportamiento de un centro de mecanizado cuando la compensación de herramienta está activa se describe en la sección
:doc:`toolCompensation`.

.. admonition:: Nota
   :class: note

   Cuando la compensación de herramienta está activa *G41/G42* no se permite realizar el cambios de herramientas ni de 
   filos de herramienta

Da un error si:

   * El número *D* no es válido o es 0
   * El plano YZ está activo
   * Se utiliza un comando para activar la compensación de herramienta cuando ya está activa


.. _refG41.1:

G41.1 G42.1 Compensación Dinámica de Radio de Herramienta
---------------------------------------------------------

::

   G41.1 D- <L-> (a la izquierda de la trayectoria programada)
   G42.1 D- <L-> (a la derecha de la trayectoria programada)

Los comandos *G41.1* y *G42.1* funcionan de la misma manera que los comandos *G41* y *G42* con la funcionalidad
agregada de poder programar el diámetro de la herramienta. La palabra *L* tiene por defecto el 0 si no se 
especifica.

Da un error si:

   * El plano YZ está activo
   * El número *L* no está en el rango de 0 a 9
   * El número *L* es usado cuando el plano XZ no está activo
   * Se utiliza un comando para activar la compensación de herramienta cuando ya está activa


.. _refG43:

G43 Compensación de Largo de Herramienta
-----------------------------------------

::

   G43 <H->

* *H-* número de herramienta (opcional)

El comando *G43* activa la compensación de largo de herramienta. *G43* cambia los movimientos subsiguientes al desplazar 
la posición de los ejes una magnitud igual a largo de la herramienta. Este comando no causa movimiento alguno. La próxima vez
que se mueva un eje con compensación el eje se desplaza a la ubicación compensada.

Un comando *G43* sin la palabra *H* utiliza la herramienta cargada en el último comando *Tn* *M6*.

El comando *G43* *Hn* utiliza el decalaje de la herramienta número *n*. 

.. admonition:: Nota

   El comando *G43* *H0* es especial. Su comportamiento difiere si la máquina tiene un cambiador de herramientas que permita cambios 
   aleatorios o no (ver sección de Cambios de Herramienta REFERENCIA ). En máquinas con cambiadores de herramientas 
   no aleatorios el comando *G43* *H0* aplica el largo de la herramienta que está en uso o un largo nulo si no hay una herramienta
   cargada. En máquinas que tienen cambiadores aleatorios *G43* *H0* aplica el largo de la herramienta T0 de la tabla de herramientas
   (o da error si la herramienta T0 no está definida en la tabla de herramientas).

**Ejemplo G43 H-**::

   G43 H1 (selecciona los decalajes utilizando los valores de la herramienta 1 de la tabla de herramientas)

Da un error si:

   * El número *H* no es un entero
   * El número *H* es negativo
   * El número *H* no es un número válido de herramienta (notar que el número 0 es válido en máquinas con cambiadores no aleatorios)


.. _refG43.1:

G43.1 Compensación Dinámica de Largo de Herramienta 
---------------------------------------------------

::

   G43.1 ejes

* El comando *G43.1* *ejes* modifica los movimientos subsiguientes al reemplazar el/los decalaje/s de ejes.
  Este comando no causa movimiento alguno. La próxima vez que se mueva un eje con compensación el eje se desplaza a la ubicación compensada.

**Ejemplo G43.1**::

   G90 (coordenadas absolutas)
   T1 M6 G43 (carga la herramienta 1 y el largo de herramienta, Z está en la cordenada 0 de máquina y DRO muestra Z1.5)
   G43.1 Z0.25 (cambia el decalaje de la herramienta en 0.25, ahora DRO muestra Z1.25)
   M2 (fin de programa)

* Para más información ver secciones :ref:`G90 <refG90>`, :ref:`T <refT>` y :ref:`M6 <refM6>`

Da error si:

   * El movimiento se programa en la misma línea que *G43.1*

.. admonition: Nota

   *G43.1* no modifica los datos de la tabla de herramientas


.. _refG43.2:

G43.2 Compensación Adicional de Largo de Herramienta 
----------------------------------------------------

::

   G43.2 H-

* G43.2 aplica un decalaje de largo de herramienta adicional y simultáneo

**Ejemplo G43.2**::

   G90 (coordenadas absolutas)
   T1 M6 (carga la herramienta 1)
   G43 (o G43 H1 - reemplaza todos los decalajes de herramientas con el decalaje de la herramienta 1)
   G43.2 H10 (también suma los decalajes de la herramienta 10)
   M2 (fin de programa)

Se puede sumar un número arbitrario de decalajes utilizando el comando *G43.2* varias veces. No se realizan suposiciones
sobre cuales son decalajes geométricos y cuales son decalajes por desgaste de la herramienta, o si se utiliza o no uno solo 
para cada tipo.
Como los otros comandos *G43*, *G43.2* no causa movimiento alguno. La próxima vez que se realice un movimiento coordinado de 
ejes, la posición de la punta de la herramienta será compensada en el punto final.

Da error si:

   * *H* no se especifica
   * El número de herramienta no existe en la tabla de herramientas

.. admonition: Nota

   *G43.2* no modifica los datos de la tabla de herramientas


.. _refG49:

G49 Cancelar Compensación de Largo de Herramienta 
-------------------------------------------------

* G49 cancela la compensación de largo de herramienta

Es válido programar este comando utilizando el mismo decalaje que ya está en uso. Es válido también programar este comando 
utilizando un largo de herramienta nulo si no hay alguno en uso.

.. _refG52:

G52 Posición del Sistema de Coordenadas Local
---------------------------------------------

::

   G52 ejes

*G52* es utilizado en una parte de un programa como un decalaje temporario del sistema coordenado local, referido al sistema
coordenado de la pieza.
Un ejemplo de uso se da cuando se mecanizan varias veces la misma geometría en diferentes ubicaciones de una pieza. Para cada
geometría, *G52* determina un punto de referencia local dentro del sistema coordinado de la pieza y se llama a un subprograma 
para mecanizar la geometría en una posición relativa a ese punto de referencia.
*G52 ejes* se utiliza para programar el decalaje de esos *ejes* para los sistemas de referencia de la pieza desde *G54* a 
*G59.3*. Como un decalaje local, *G52* se aplica adicionalmente luego del decalaje del sistema de referencia de la pieza, incluida
la rotación. Por ende, la geometría será mecanizada identicamente en cada parte, independientemente de la orientación de la pieza. 

.. admonition:: Precaución
   :class: warning

   Como un decalaje temporario, la definición en otros interpretadores No es persistente luego del reset de la máquina, un código *M02*
   o *M30*. Sin embargo en este controlador, *G52* comparte los parámetros con *G92*, lo que implica que la definición Es persistente. 
   Ver la sección de :ref:`Precauciones sobre Persistencia de G92 <refG92>`

.. admonition:: Precaución
   :class: warning

   *G52* y *G92* comparten los registros para la definición. Por lo tanto *G52* sobreescribe cualquier configuración mediante *G92*, y *G52*
   tendrá una definición persistente al reset de máquina cuando *G92* esté definido como persistente. Estas interacciones pueden resultar en 
   decalajes no previstos. Ver la sección de :ref:`Interacción entre G52 y G92 <refG92>`

Programar *G52 X10 Y25* cambia el decalaje del sistema coordenado de pieza actual, movíendolo 10 en la dirección X y 25 en la dirección Y.
Los ejes que no estén definidos en el comando, tal como el eje Z en el ejemplo previo, no se verán afectados, por lo que el decalaje *G52 Z*
permanecerá en efecto, de lo contrario el decalaje en Z será nulo.
El decalaje temporario puede ser cancelado con *G52 X0 Y0*.


.. _refG53:

G53 Posición en Sistema de Coordenadas de Máquina
-------------------------------------------------

::

   G53 ejes

*G53* realiza un movimiento lineal referido al sistema de coordenadas de la máquina en la misma línea en que se definen las coordenadas del 
la posición a la cual moverse. *G53 no es modal y debe ser definido en cada línea. En contraste para *G0* o *G1* no se requiere que se utilicen
en cada línea si uno de ellos está activo.
Por ejemplo, *G53 G0 X0 Y0 Z0* provocará un movimiento al origen de coordenadas de la máquina aún si hay un sistema de 
coordenadas con decalaje activo.

::

   G53 G0 X0 Y0 Z0 (movimiento lineal rápido al origen de máquina)
   G53 X2 (movimiento lineal rápido a la coordenada absoluta X2)

Da error si:

   * *G53* se utliliza sin *G0* o *G1* activos
   * *G53* se utiliza con la compensación de herramienta activo

.. _refG54:

G54-G59.3 Selección de Sistema de Coordenadas Local
---------------------------------------------------

* *G54* - Selección del sistema de coordenadas 1
* *G55* - Selección del sistema de coordenadas 2
* *G56* - Selección del sistema de coordenadas 3
* *G57* - Selección del sistema de coordenadas 4
* *G58* - Selección del sistema de coordenadas 5
* *G59* - Selección del sistema de coordenadas 6
* *G59.1* - Selección del sistema de coordenadas 7
* *G59.2* - Selección del sistema de coordenadas 8
* *G59.3* - Selección del sistema de coordenadas 9

Los sistemas de coordenadas guardan las posiciones de decalajes y rotación de los ejes en los siguientes parámetros.

+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
| Selección   | SC  |    X   |    Y   |    Z   |    A   |    B   |    C   |    U   |    V   |    W   |    R   |
+=============+=====+========+========+========+========+========+========+========+========+========+========+
|     G54     |  1  |  5221  |  5222  |  5223  |  5224  |  5225  |  5226  |  5227  |  5228  |  5229  |  5230  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G55     |  2  |  5241  |  5242  |  5243  |  5244  |  5245  |  5246  |  5247  |  5248  |  5249  |  5250  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G56     |  3  |  5261  |  5262  |  5263  |  5264  |  5265  |  5266  |  5267  |  5268  |  5269  |  5270  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G57     |  4  |  5281  |  5282  |  5283  |  5284  |  5285  |  5286  |  5287  |  5288  |  5289  |  5290  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G58     |  5  |  5301  |  5302  |  5303  |  5304  |  5305  |  5306  |  5307  |  5308  |  5309  |  5310  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G59     |  6  |  5321  |  5322  |  5323  |  5324  |  5325  |  5326  |  5327  |  5328  |  5329  |  5330  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G59.1   |  7  |  5341  |  5342  |  5343  |  5344  |  5345  |  5346  |  5347  |  5348  |  5349  |  5350  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G59.2   |  8  |  5361  |  5362  |  5363  |  5364  |  5365  |  5366  |  5367  |  5368  |  5369  |  5370  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+
|     G59.3   |  9  |  5381  |  5382  |  5383  |  5384  |  5385  |  5386  |  5387  |  5388  |  5389  |  5390  |
+-------------+-----+--------+--------+--------+--------+--------+--------+--------+--------+--------+--------+

Da error si:

   * Se selecciona un sistema de coordenadas mientras la compensación de herramientas está activa


.. _refG61:


G61 Modo de Posicionamiento Preciso
-----------------------------------

*G61* se utiliza para activar el posicionamiento preciso. Los movimientos serán más lentos o se detendrán de acuerdo a 
lo necesario a los efectos de llegar a la posición definida por cada punto. Si dos movimientos son colineares el movimiento
no se deterndrá.


.. _refG61.1:

G61.1 Modo de Posicionamiento Preciso y Frenado
-----------------------------------------------

*G61.1* provoca la detención del movimiento en todos los tramos sobre el punto final de cada segmento.

.. _refG64:

G64 Suavizado de Trayectoria
----------------------------

::

   G64 <P- <Q->>

* *P-* tolerancia del suavizado de trayectoria
* *Q-* tolerancia para algoritmo de direcciones sucesivas

El comando *G64*, sin parámetros *P* ni *Q*, realizará el movimiento con la velocidad más alta posible, sin considerar cuanto se
aleja el movimiento del punto programado.

* *G64* P- <Q-> - realizará los movimiento con una trayectoria suavizado con tolerancia, es decir que el movimiento entre tramos diferentes no se detendrá, sino que la trayectoria se suaviza en torno al punto intermedio, y la velocidad en esa transcición será la más alta posible sujeta a las restricciones que le imponen las tolerancias utilizadas. La velocidad especificada será reducida si es necesario para mantener las tolerancias especificadas. 

La tolerancia *P* indica la máxima desviación posible de la trayectoria en el entorno del punto intermedio respecto a la geometría 
definida por los comandos de movimiento. Cuando se especifica la tolerancia *P* es posible definir adicionalmente el parámetro de 
tolerancia *Q*. Cuando se especifican ambos parámetros de tolerancia, para una serie de movimientos lineales consecutivos con la misma
especificación de velocidad, se activa un algoritmo que bajo las condiciones correcta puede unificar diferentes tramos en uno solo. 
En los movimientos *G2*/*G3* en el plano XY (G17), si distancia máxima entre el arco y la recta que une sus extremos es menor a la 
tolerancia *P*, se reemplaza el arco por dos tramos rectos con suavizado con el algoritmo y el parámetro *Q*. De esta forma los movimientos
entre línea-arco, arco-arco y arc-línea, tal como línea-línea se pueden procesar con ese algoritmo. Esto implica una mejora en ciertos casos
para la ejecución de movimientos de contorno al simplificar la trayectoria.
Es válido programar este comando cuando el modo está ya activo. Para más información sobre la trayectoria ver la sección :doc:`trajectoryControl`.

Si *Q* no se especifica el comando tendrá el mismo comportamiento pero con el valor de *P* especificado.

Ejemplo de G64 P-::

   G64 P0.15 (activar el suavizado con una tolerancia de 0.15 unidades)

Es una buena práctica incluir las especificaciones del suavizado de trayectoria en el preámbulo del Código G.


.. _refG73:

G73 Ciclo de Perforado con Ruptura de Viruta
--------------------------------------------

::

   G73 X- Y- Z- R- Q- <L->

* *R-* posición de retracción en el eje Z
* *Q-* incremento relativo en el eje Z
* *L-* repeticiones

El comando *G73* produce un ciclo de perforado o fresado con ruptura de viruta. Este ciclo toma el valor de *Q-* que representa el incremento 
de la posición a lo largo del eje Z.

#. Movimiento preliminar

   * Si la posición en el eje Z es menor al valor de *R-*, el eje Z realiza un movimiento lineal rápido para tomar el valor de *R-*

   * Desplazamiento al valor de las coordenadas X e Y

#. Desplazamiento en el eje Z a la velocidad de avance actual hacia abajo, por el valor definido por *Q-* o a la posición *Z-*, el de menor profundidad
#. Desplazamiento corto rápido hacia arriba
#. Repetición de los pasos 2 y 3 hasta que se logra la posición Z en el paso 2
#. Desplazamiento rápido en Z a la posición *R-*

Da error si:

   * El número *Q* es negativo o nulo
   * El número *R* no se especifica


.. _refG74:

G74 Ciclo de Roscado (Tapping) Izquierdo con Huelgo
---------------------------------------------------

::

   G74 (X- Y- Z-) o (U- V- W-) R- L- P- $-

El ciclo *G74* se utiliza típicamente para realizar roscados con una herramienta de roscado (macho) con un mandril flotate, es decir que permite un cierto juego en la
dirección axial. Al llegar al final del roscado ejecuta una espera.

La secuencia de movimientos es la siguiente:

   #. Movmiento preliminar, como se describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Anula overrides de velocidad de husillo y velocidad de avance
   #. Frena el husillo seleccionado, definido por el parámetro *$*
   #. Activa la rotación del husillo en el sentido horario
   #. Espera por *P* segundos
   #. Mueve el eje Z a la velocidad de avance actual a la posición de despeje
   #. Activa la velocidad de husillo y velocidad de avance a los valores previos

El paso de la rosca resulta del valor de la velocidad de avance F dividido la velocidad de rotación del husillo S. 
Por ejemplo con valores S100 y F125 daría un paso de 1.25 mm por revolución.


.. _refG76:

G76 Ciclo de Roscado (Threading) de Varias Pasadas 
--------------------------------------------------

::

   G76 P- Z- I- J- R- K- Q- H- E- L- $-

* *P-* paso de la rosca en unidades de distancia por revolución
* *Z-* posición final del roscado. AL final de ciclo la herramienta quedará en esta posición

Las posiciones se definen relativas una la línea de referencia definida por la posición X inicial y la direcciónn Z.

.. figure:: images/thread.png
   :width: 250

.. admonition:: Nota
   :class: note

   Cuando el modo diametral está activo *G7* los valores de *I*, *J* y *K* son medidas de diámetros. Cuando el modo radial está activo *G8* los valores de *I*, *J* 
   y *K* son medidas de radios. 

* *I-* posición relativa de la cresta de los filetes de la rosca respecto a la línea de referencia. Para roscas externas se utilizan valores negativos mientras que para roscas internas se utilizan valores positivos.
* *J-* profundidad de corte inicial, con valor positivo. El primer corte del roscado se ubicará a una distancia *J* de la posición de la cresta de los filetes.
* *K-* profundidad del filete de la rosca, con valor positivo. La posición de corte final del roscado se ubicará a una distancia *J* de la posición de la cresta de los filetes.

   **Especificaciones Opcionales**

* *$-* número de husillo con el que se sincronizará el movimiento (por defecto 0). Por ejemplo si se utiliza *$1* el movimiento programado empezará cuando se active el *splindel.1.index-enable* y procederá en sincronía con el valor *spindle.1.revs*.
* *R-* factor de reducción de profundidad. *R1.0* define profundidades de corte constantes en las sucesivas pasadas. *R2.0* se utiliza para que el área de corte sea constante. Valores entre 1.0 y 2.0 implican profundidades decrecientes pero áreas crecientes. Valores mayores a 2.0 implican áreas decrecientes. Tenga en cuenta que valores de reducción altos causarán una gran cantidad de pasadas.
* *Q-* ángulo de deslizamiento compuesto en grados, describe la dirección de avance relativo entre sucesivas pasadas respecto a la línea de referencia. Se utiliza para que un un lado de la herramienta remueva más material que el otro. Un valor de *Q* positivo causa que el lado de ataque corte más material. Los valores que típicamnete se utilizan son de 29 a 30.
* *H-* número de pasadas de repaso adicionales. Es la cantidad de pasadas en la posición final para repaso de la rosca, si no se desean pasadas adicionales de puede programar *H0*.
* *E-* distancia a lo largo de la línea de referencia utilizada para la entrada y/o salida en ángulo. El ángulo será tal que la última pasada retrocede la profundidad del filete sobre la distancia definida por *E*. *E0.2* dará un ángulo para los primeros/últimos 0.2 unidades de longitud a lo largo de la rosca. Para un ángulo de 45 grados programe la entrada/salida con valores iguales de *E* y *K*.
* *L-* especifica cuales extremos tendrán ángulo de entrada/salida. Utilice *L0* para rosca sin entrada/salida en ángulo valor por defecto), *L1* para ángulo de entrada, *L2* para ángulo de salida y *L3* para ángulo de entrada y de salida.

La herramienta se mueve a las posiciones de X y Z antes de ejecutar el comando G76. La posición en X determina la línea de referencia y la posición de Z marcará el 
inicio del roscado.
El movimiento se frenará brevemente para sincronizar antes de cada pasada, por lo que se requiere una ranura para la entrada, salvo que en el comienzo de la rosca 
esté fuera del material a roscar o se utilice un ángulo de entrada.
Salvo que se utilice un ángulo de salida, el movimiento no estará sincronizado con la velocidad del husillo y se realizará con un movimiento lineal rápido. Cuando 
la velocidad del husillo es baja, el movimiento de salida tomará solo una fracción de una revolución. Si la velocidade del husillo se incrementa luego de 
varias pasadas las salidas sucesivas tomarán una proporción mayor de una revolución, resultando en profundidades de corte mayores. Esto puede evitarse 
utilizando una ranura para la salida o dejando constante la velocidad durante el roscado.
La posición final de la herramienta será el final de la línea de referencia. Un movimiento en Z de seguridad será necesario en roscados internos para extraer la 
herramienta del agujero. 

Da error si:

   * El plano activo no es XZ
   * Se especifican otros ejes como *X-* o *Y-*
   * El valor de reducción es menor a 1.0
   * *P-*, *J-*, *K-* o *H-* son negativos
   * *E-* es mayor a la mitad de la longitud de la línea de referencia

**Conexiones HAL**

Los testigos (pins) *spindle.N.at-speed* y *encoder.n.phaze-Z* para el husillo deben estar conectados en el archivo HAL antes de ejecutar *G76*.

**Información Técnica**

EL ciclo cerrado *G76* está basado en el comando *G33* de movimiento sincronizado de husillo.

**Ejemplo de G76**

::

   G0 Z-0.5 X0.2
   G76 P0.05 Z-1 I-.075 J0.008 K0.045 Q29.5 L2 E0.045

.. figure:: images/g76Example.png
   :width: 250

   Figura de ejemplo de G76

.. _refCannedCycles:

Ciclos Cerrados
---------------

Los ciclos cerrados se definen con los comandos entre *G81* y *G89*, mientras que la cancelación de ciclo cerrado se hace con el comando *G80*.
Todos los ciclos cerrados se ejecutan respecto al plano de trabajo seleccionado. En la mayoría de las descripciones de esta sección se asume que 
el plano de trabajo es el XY. El comportamiento para otros planos es análogo, con el debido cambio en el uso de los ejes.
Por ejemplo, en el plano *G17.1*, las operaciones del ciclo cerrado se realizarán en el eje W, y las posiciones o incrementos se realizarán en los ejes
U y V. En este caso deberá sustituir U, V y W por X, Y y Z en las instrucciones dadas.
Los ejes rotativos no están permitidos en los ciclos cerrados. Cuando un plano de trabajo está definido en los ejes XYZ, las palabras de ejes UVW no están
permitidas y viceversa.

**Palabras en Común**

Todos los ciclos cerrados usan los grupos X, Y, Z o U, V, W dependiendo del plano de trabajo seleccionado y las palabras *R*. Las palabras *R*, que generalmente 
hacen referencia a la posición de retracción, es perpendicular al plano de trabajo (eje Z para plano XY). Algunos ciclos cerrados utilizan argumentos adicionales.

**Palabras permanentes**

Para los ciclos cerrados, cuando el mismo ciclo se utiliza en diferentes líneas de código secuencialmente, hay palabras que deben definirse en la primera línea pero
que no es necesario utilizarlos en las siguientes líneas. A estos parámetros se los llama palabras permanentes. Su valor se mantiene en el resto de las líneas de código si 
no se cambia su valor explícitamente. El valor de *R* es siempre permanente. 

En el modo de distancia incremental, X, Y y R son tratados como incrementos desde la posición actual y el valor de Z como un incremente desde la posición Z antes de que el 
movimiento en Z ocurra. En el modo de distancia absoluta, X, Y, R y Z refieren en posiciones absolutas en el sistema coordenado actual.

**Repetición de Ciclo**

El parámetro opcional L representa el número de repeticiones. L=0 no está permitido. Si se utiliza esta opción, normalmente se utiliza el modo incremental de distancia, para que 
la misma secuencia de movimientos se repita en posiciones igualmente espaciadas. Cuando el valor de *L-* es mayor que 1 en el modo incremental con el plano XY seleccionado, las 
posiciones de X e Y se determinan sumando los valores de X e Y dados a las posiciones iniciales (en la primera repetición) o a los valores de fin de ciclo anterior (en las siguientes
repeticiones). Por ende, si se programa *L10* se realizarán 10 repeticiones. El primer ciclo estará a una distancia X e Y de la posición original. Las posiciones R y Z no cambiarán 
durante las repeticiones. El número L no es permanente. En modo de distancias absolutas, L mayor a 1 implica realizar el mismo ciclo en la misma posición. Si se omite la definición de 
L equivale a realizar el cilo 1 vez.

**Modo de Retracción**

La altura a la que se retrae el movimiento da cada ciclo (llamada altura de despeje) es determinada por el modo de retracción, ya sea a la posición original de Z (si ésta está arriba de la 
posición R y el modo de retracción es *G98*) o a la posición determinada por R. Ver la sección :ref:`G98 G99 <refG98>`.

**Errores de Ciclos Cerrados**

Da error si:

   * No hay alguna palabras de eje
   * Se utilizan palabras de ejes de ambos grupos (XYZ) o (UVW)
   * Se requiere un número P y el número P es negativo
   * Se utiliza un número L que no se puede evaluar a un entero positivo
   * Se utiliza un movimiento de algún eje rotativos
   * La velocidad de avance inversa está activa durante un ciclo cerrado
   * La compensación de herramienta está activa durante un ciclo cerrado

Si el plano XY está activo, el número Z es permanente y da un error si

   * El número Z no está definido y el mismo ciclo cerrado no estaba activo previamente
   * El número R es menor al número Z

Si otros planos están activos, las condiciones de error son análogas a las descriptas para el plano XY.

**Movimientos preliminares e intermedios**

Los movimientos preliminares son un conjunto de movimientos comunes a todas los ciclos cerrados de fresado.
Si la posición en el eje Z es menor al valor de *R-*, el eje Z realiza un movimiento lineal rápido para tomar el valor de *R-*
Esto sucede solo una vez, independientemente del valor de *L*.
Adicionalmente, al inicio del primer ciclo y en cada repetición, se realiza uno o los dos movimientos siguientes:

#. Desplazamiento rápido en el plano XY al valor de las coordenadas X e Y dados
#. Desplazamiento rápido a la posición *R*, si es que no está en esa posición

**¿Porqué usar Ciclos Cerrados?**

Es conveniente usar ciclos cerrados por lo menos por dos razones importantes. La primera razón es la simplicidad del código. Por ejemplo, la ejecución de un agujero 
podría requerir varias líneas de código para programarlo.

El ejemplo siguiente muestra cómo un ciclo cerrado se puede utilizar para ejecutar 8 agujeros con 5 líneas de código.

.. admonition:: Nota
   :class: note

   Los números de línea no son necesarios pero se utilizan para hacer referencia a los ejemplos

Ejemplo para 8 Agujeros::

   N100 G90 G0 X0 Y0 Z0 (desplazarse al origen)
   N110 G1 F10 X0 G4 P0.1
   N120 G91 G81 X1 Y0 Z-1 R1 L4 (ciclo cerrado de perforado)
   N130 G90 G0 X0 Y1
   N140 Z0
   N150 G91 G81 X1 Y0 Z-0.5 R1 L4 (ciclo cerrado de perforado)
   N160 G80 (cancelar ciclo cerrado)
   N170 M2 (fin de programa)

.. figure:: images/canned8holes.png
   :width: 250

Ejemplo para 12 Agujeros::

   N1000 G90 G0 X0 Y0 Z0 (desplazarse al origen)
   N1010 G1 F50 X0 G4 P0.1
   N1020 G91 G81 X1 Y0 Z-0.5 R1 L4 (ciclo cerrado de perforado)
   N1030 X0 Y1 R0 L3 (repetición de ciclo cerrado)
   N1040 X-1 Y0 L3 (repetición de ciclo cerrado)
   N1050 X0 Y-1 L2 (repetición de ciclo cerrado)
   N1060 G80 (cancelar ciclo cerrado)
   N1070 G90 G0 X0 (rapid move home)
   N1080 Y0
   N1090 Z0
   N1100 M2 (fin de programa)

En este ejemplo se muestra el uso del párametro *L* para repetir un conjunto de ciclos de perforado en las líneas de 
cógido subsiguientes dentro del modo *G81*. Aquí se realizan 12 agujeros utilizando 5 líneas de código en el modo de ciclo cerrado.

.. figure:: images/canned12holes.png
   :width: 250

La segunda razón para utilizar ciclos cerrados es que todos ellos producen movimientos preliminares y de fin de ciclo que se pueden anticipar y controlar
independientemente del punto de inicio del ciclo cerrado.


.. _refG80:

G80 Cancelación de Ciclo Cerrado
--------------------------------

*G80* cancela el modo de movimientos de ciclos cerrados. *G80* es parte del grupo modal 1, por lo que al programar cualquier otro código G del grupo modal se 
cancela el ciclo cerrado.

Da error si:

   * Se utilizan palabras de ejes cunado *G80* está activo.

Ejemplo de G80::

   G90 G81 X1 Y1 Z1.5 R2.8 (ciclo cerrado en coordenadas absolutas)
   G80 (cancelar ciclo cerrado)
   G0 X0 Y0 Z0 (movimiento lineal rápido al origen)

El código siguiente produce la misma posición final y modo de máquina que el código anterior.

::

   G90 G81 X1 Y1 Z1.5 R2.8 (ciclo cerrado en coordenadas absolutas)
   G0 X0 Y0 Z0 (cancela modo de ciclo cerrado y desplaza al origen)

La ventaja del primer código es resulta más evidente que el comando *G80* cancela el modo *G81*. En el primer código se debe programar el modo movimiento 
nuevamente con *G0* o cualquier otra palabra G de movimiento.

Si el modo de ciclo cerrado no se cancela con *G80* u otro comando, el ciclo cerrado intentará repetirse utilizando el siguiente bloque de código que contenga
alguna palabra X, Y o Z. El siguiente archivo perfora (G81) una serie de 8 agujeros.

Ejemplo 1 de G80::

   N100 G90 G0 X0 Y0 Z0 (coordinate home)
   N110 G1 X0 G4 P0.1
   N120 G81 X1 Y0 Z0 R1 (canned drill cycle)
   N130 X2
   N140 X3
   N150 X4
   N160 Y1 Z0.5
   N170 X3
   N180 X2
   N190 X1
   N200 G80 (turn off canned cycle)
   N210 G0 X0 (rapid move home)
   N220 Y0
   N230 Z0
   N240 M2 (program end)

.. admonition:: Nota
   :class: note

   Notar que la posición en Z cambia luego de los primeros 4 agujeros. También que es posible mover el puntero a una línea específica de código,
   ésta es una de las pocas situaciones en las que es útil definir los números de líneas de código.

.. figure:: images/exampleG80.png
   :width: 250

La utilización de *G80* en la l+inea N200 es opcional pero sin ésta es más dificil observar que los bloques entre N120 y N200 perteneces a un
ciclo cerrado.


.. _refG81:

G81 Ciclo de Perforado
----------------------

::

   G81 (X- Y- Z-) or (U- V- W-) R- L-

El ciclo *G81* se utiliza para realizar perforaciones y ejecuta las siguientes funciones:

   #. Movimiento preliminar, como se lo describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Movimiento en el eje Z a la velocidad de avance actual a la posición Z*
   #. Movimiento rápido a la posición de despeje de Z

**Ejemplo 1 de G81 con posición absoluta**

Suponga que la posición actual es (X1, Y2, Z3) y se ejecuta la siguiente línea::

   G90 G98 G81 X4 Y5 Z1.5 R2.8

Ésta línea llama al ciclo cerrado *G81* con posicionamiento absoluto *G90* y el modo de retracción *G98* una vez, por lo que se produce:

   #. Movimiento rápido paralelo al plano XY a X4, Y5
   #. Movimiento rápido del eje Z a Z2.8
   #. Movimiento del eje Z a velocidad de avance a Z1.5
   #. Movimiento rápido del eje Z a Z3 

.. figure:: images/exampleG81a.png
   :width: 250

**Ejemplo 2 de G81 con posición relativa**

Suponga que la posición actual es (X1, Y2, Z3) y se ejecuta la siguiente línea::

   G91 G98 G81 X4 Y5 Z-0.6 R1.8 L3

Ésta línea llama al ciclo cerrado *G81* con posicionamiento relativo *G91* y el modo de retracción *G98* solicitando que el ciclose repita 3 veces.
La posición inicial en el eje X será 5 (=1+4), en el eje Y será 7 (=2+5), la posición de despeje de Z será 4.8 (1.8+3) y la posición en Z será 
4.2 (=1.8+3). La posición anterior de Z es 3.

El movimiento preliminar será un movimiento rápido en el eje Z a (X1, Y2, Z4.8), debido a que la posición anterior de Z (3) es menor al despeje en Z (4.8).

La primer repetición consiste en 3 movimientos:

   #. Movimiento rápido paralelo al plano XY a X5 Y7
   #. Movimiento en el eje Z a velocidad de avance a Z4.2
   #. Movimiento rápido en el eje Z a Z4.8

La segunda repetición consiste en 3 movimientos. La posición X se modifica a 9 (=5+4) y la posición en Y igual a 12 (=7+5):

   #. Movimiento rápido paralelo al plano XY a X9 Y12 Z4.8
   #. Movimiento en el eje Z a velocidad de avance a X9 Y12 Z4.2
   #. Movimiento rápido en el eje Z a X9 Y12 Z4.8

La tercera repetición consiste en 3 movimientos. La posición X se modifica a 13 (=9+4) y la posición en Y igual a 17 (=12+5):

   #. Movimiento rápido paralelo al plano XY a X13 Y17 Z4.8
   #. Movimiento en el eje Z a velocidad de avance a X Y12 Z4.2
   #. Movimiento rápido en el eje Z a X13 Y17 Z4.8


.. figure:: images/exampleG81b.png
   :width: 250

**Ejemplo 3 de G81 con posición relativa**

Suponga que se ejecuta la primera línea con comando G81 pero con la posición desde es (X0, Y0, Z0)::

   G90 G98 G81 X4 Y5 Z1.5 R2.8

En este ejemplo la posición en Z anterior es menor al valor de R, no se modifica los movimientos, pero debido a que el valor inicial de Z es menor
que el valor especificado de R, se producirá un movimiento preliminar en el eje Z. 

.. figure:: images/exampleG81c.png
   :width: 250

**Ejemplo 4 de G81 con posición absoluta R > Z**

Para la siguiente línea de comando, iniciando desde el origen (X0, Y0, Z0)::

   G91 G98 G81 X4 Y5 Z-0.6 R1.8 L3

El interpretador adiciona a la coordenada Z0 el número R1.8 y realiza un movimiento rápido a esa posición. Luego de este movimiento inicial
el ejemplo produce el mismo resultado que en el ejemplo 3 con la profundidad final de Z de 0.6 por abajo del valor R.

.. figure:: images/exampleG81d.png
   :width: 250

**Ejemplo 5 de G81 con posición relativa R > Z**

Para la siguiente línea de comando, iniciando desde el origen (X0, Y0, Z0)::

   G90 G98 G81 X4 Y5 Z-0.6 R1.8

El interpretador adiciona a la coordenada Z0 el número R1.8 y realiza un movimiento rápido a esa posición, como en el ejemplo 4.
Luego del movimiento inicial en Z realiza un movimiento rápido a X4 Y5, por lo que la profundidad en Z está 0.6 por debajo del 
valor R. La función de repetición ejecutaría el movimiento en Z a la misma ubicación.


.. _refG82:

G82 Ciclo de Perforado con Espera
----------------------------------

::

   G82 (X- Y- Z-) or (U- V- W-) R- L- P-

El ciclo *G82* se utiliza para realizar perforaciones con un tiempo de espera en el fondo del agujero. Realizando:

   #. Movimiento preliminar, como se lo describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Movimiento en el eje Z a la velocidad de avance actual a la posición Z*
   #. Espera por un tiempo de P segundos
   #. Movimiento rápido a la posición de despeje de Z

El movimiento del ciclo cerrado *G82* es igual al del ciclo *G81* pero con el tiempo de espera al llegar al fondo del agujero. El tiempo
de espera queda definido por el parámetro *P-* del comando *G82*.


.. _refG83:

G83 Ciclo de Perforado Profundo
-------------------------------

::

   G83 (X- Y- Z-) or (U- V- W-) R- L- Q-

El ciclo cerrado *G83* se utiliza para realizar perforaciones profundas con ruptura de viruta. Las retracciones de este ciclo limpian el agujero 
de virutas y cortan las virutas largas (comunes al perforar aluminio). Este ciclo utiliza el número *Q* que representa una distancia incremental
de perforado a lo largo del eje Z. La/s retracción/es se realiza al plano de retracción incluso si está activo *G98* durante el perforado. La 
retracción final respetará las instrucciones de *G98*/*G99* en efecto. El comando *G83* funciona de manera similar a *G81* con el egregado de las
reracciones durante el ciclo para limpieza de virutas. Los movimientos que realiza son los siguientes:

   #. Movimiento preliminar, como se lo describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Movimiento en el eje Z a la velocidad de avance actual una distancia definida en *Q* o a la posición *Z*, la que sea de menor profundidad
   #. Movimiento rápido en el eje Z al plano de retracción especificado por el valor de *R*
   #. Movimiento rápido en el eje Z hasta la cota ya mecanizada.
   #. Repetición de los pasos 2, 3 y 4 hasta la posición especificada por *Z*
   #. Movimiento rápido para despeje del eje Z

Da un error si:

   * El número *Q* es negativo o nulo


.. _refG84:

G84 Ciclo de Roscado (Tapping) Derecho con Espera
-------------------------------------------------

::

   G84 (X- Y- Z-) o (U- V- W-) R- L- P- $-

El ciclo *G84* se utiliza típicamente para realizar roscados con una herramienta de roscado (macho) con un mandril flotate, es decir que permite un cierto juego en la
dirección axial. Al llegar al final del roscado ejecuta una espera.

La secuencia de movimientos es la siguiente:

   #. Movimiento preliminar, como se describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Anula overrides de velocidad de husillo y velocidad de avance
   #. Frena el husillo seleccionado, definido por el parámetro *$*
   #. Activa la rotación del husillo en el sentido horario
   #. Espera por *P* segundos
   #. Mueve el eje Z a la velocidad de avance actual a la posición de despeje
   #. Activa la velocidad de husillo y velocidad de avance a los valores previos

El paso de la rosca resulta del valor de la velocidad de avance F dividido la velocidad de rotación del husillo S. 
Por ejemplo con valores S100 y F125 daría un paso de 1.25 mm por revolución.


.. _refG85:

G85 Ciclo de Perforado con Velocidad de Salida
----------------------------------------------

::

   G85 (X- Y- Z-) or (U- V- W-) R- L-

El comando *G85* se utiliza para perforado o repasado, aunque también se puede utilizar para fresado. Realiza los siguientes movimientos:

   #. Movimiento preliminar, como se describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Movimiento en el eje Z a la velocidad de avance actual al valor definido por *Z*
   #. Retracción del eje Z a la velocidad de avance actual al valor *R* si es menor a la posición inicial Z
   #. Retracción a la velocidad de desplazamiento


.. _refG86: 

G86 Ciclo de Perforado, Freno de Husillo y Velocidad Rápida de Salida
---------------------------------------------------------------------

::

   G86 (X- Y- Z-) or (U- V- W-) R- L- P- $-

El comando *G86* se utiliza para perforado. Al llegar al final del roscado ejecuta una espera. Realiza los siguientes movimientos:

   #. Movimiento preliminar, como se describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Movimiento en el eje Z a la velocidad de avance actual al valor definido por *Z*
   #. Espera por *P* segundos
   #. Frena el husillo (seleccionado por el parámetro $)
   #. Retracción rápida del eje Z a la posición de despeje
   #. Activa el giro del husillo en la dirección que giraba anteriormente

Da error si:

   * El husillo no está girando antes de la ejecución del ciclo


.. _refG89:

G89 Ciclo de Perforado, Espera y Velocidad de Salida
----------------------------------------------------

::

   G89 (X- Y- Z-) or (U- V- W-) R- L- P-

El comando *G89* se utiliza para perforado. Al llegar al final del roscado ejecuta una espera. Realiza los siguientes movimientos:

   #. Movimiento preliminar, como se describe en la sección :ref:`Movimiento preliminar e intermedios <refCannedCycles>`
   #. Movimiento en el eje Z a la velocidad de avance actual al valor definido por *Z*
   #. Espera por *P* segundos
   #. Retracción del eje Z a la velocidad de avance actual a la posición de despeje


.. _refG90:

G90 G91 Modo de Distancia Absoluta o Relativa
---------------------------------------------

* *G90* se utiliza para activar el modo de definición de posiciones en distancias absolutas. En este modo los valores definidos para los ejes (X, Y, Z, A, B, C, U, V, W) generalmente representan posiciones respecto al sistema de coordenadas activo. Las exepciones a esta regla se describen explícitamente en la sección :ref:`G80-G89 <refCannedCycles>`.

* *G91* se utiliza para activar el modo de definición de posiciones relativos. En este modo las posiciones representan incrementos referidoa a la posición actual.

**Ejemplo de G90**

::

   G90 (activar modo de posición absoluta)
   G0 X2.5 (movimiento rápido a la coordenada X2.5 incluyendo los decalajes activos)

**Ejemplo de G90**

::

   G91 (activar modo de posición relativa)
   G0 X2.5 (movimiento rápido a lo largo del eje X una distancia de 2.5 desde la posición actual)


.. _refG90.1:

G90.1 G91.1 Modo de Distancia de Arcos Absoluta o Relativa
----------------------------------------------------------

* *G90.1* se utiliza para activar el modo de posiciones absolutas para los valores de I, J y K. Cuando *G90.1* está activo tanto I como J deben especificarse en los comandos *G2* y *G3* para el plano XY, o tnato los parámetros J y K deben especificarse para el plano XZ.

* *G91.1* se utiliza para activar el modo de posiciones relatvas para los valores de I, J y K. El comando *G91.1* retorna el modo de funcionamiento de los valores I, J y K a su comportamiento por defecto.


.. _refG92:

G92 Definir Decalaje de Sistema de Coordenadas en Punto Actual
--------------------------------------------------------------

::

   G92 ejes


.. admonition:: Precaución
   :class: warning

   Sólo utilice *G92* luego de que la máquina ha sido posicionada en el punto deseado

*G92* hace que el punto en el que se encuentra la máquina tenga las coordenadas especificadas en los ejes incluidos en el comando, sin ejecutar movimiento. 
Se puede especificar sólo un eje o todos, los decalajes de los ejes que no se especifican serán nulos.

Cuando se ejecuta *G92* el origen de todos los sistemas de coordenadas (G53 a G59.3) se mueven la misma distancia. Los valores se modifican de tal forma que 
el punto en el que se encuentra la máquina adoptará los valores definidos por el comando en los ejes especificados.

*G92* utiliza los valores guardados en los parámetros 5211a 5219 como valores de decalaje de X Y Z A B C U V W para cada eje. Los valores de los parámetros 
son coordenadas de máquina absolutas en las unidades originales, definidas en el archivo *ini*. Si un eje no ha sido definido en el comando *G92* el decalaje 
será nulo.

Por ejemplo, suponiendo que la posición actual es X=4 y no hay un comando *G92* activo. Si se ejecuta *G92 X7*, los origenes de todos los sistemas de coordenadas
se mueven -3 en X para que el punto actual tenga un valor de X=7. Este valor de -3 es guardado en en parámetro 5211.

Si el modo de posición incremental G91 está activo no tiene efecto en el comando *G92*.

Los decalajes G92 pueden estar ya activos cunado se ejecuta el comando *G92*. Si esto sucede el decalaje es reemplazado con un nuevo valor que hace que el punto
actual tenga las coordenadas especificadas.

Da un error si:

   * Se omiten todos los ejes en la definición

Este controlador guarda los decalajes G92 y los reutiliza la próxima vez que se corre un programa. Para prevenir esto se puede utilizar el comando *G92.1) para 
borrar los valores o *G92.2* para desactivarlos.

Este comando está relacionado con el comando *G52*, para más información ver la sección :ref:`G52 <refG52>`

**Los comandos G92**

*G92* es utilizado típicamente en dos maneras conceptualmente diferentes: como un *Decalaje del sistema de coordenadas global* o como un *decalaje local del sistema de coordendas*.
El grupo de comandos *G92* incluye los comandos:

   * *G92* Este comando, cuando se especifican ejes, cambia los valores de decalaje
   * *G92.1* Este comando sobreescribe los valores a 0 de las variables G92
   * *G92.2* Este comando suspende el efecto pero no cambia los valores de las variables G92
   * *G92.3* Este comando activa los decalajes que fueron suspendidos

Como un decalaje global, *G92* es utilizado para mover todos los sistemas de coordenadas de piezas desde *G54* a *G59.3*. Un ejemplo de este uso es cuando se mecanizan diferentes
partes idénticas en una bancada con posiciones conocidas en un dispositivo de agarre pero la posición del dispositivo puede cambiar entre corridas o máquinas. Cada posición relativa
de las piezas en el dispositivo se maneja con los decalajes *G54* a *G59.3* y la posición del dispositivo se maneja con el comando *G92*. Luego, para cada parte, se selecciona el 
sistema coordenado local y se ejecuta el programa de mecanizado de la pieza.

.. admonition:: Nota
   :class: Note

   El comando *G10 R-* para rotar el sistema de coordenadas de una pieza es específico de los interpretadores *rs274ngc, y el decalaje *G92* se aplica luego de la rotación. Cuando se utiliza
   *G92* como un decalaje global, las rotaciones de los sistemas coordenados pueden tener resultados inesperados.

Aclaración: *rs274ngc* es estándar del NIST - National Institute of Satndards and Technology.

Como un decalaje local del sistema de coordenadas, *G92* es utilizado como un decalaje temporal dentro del sistema de coordenadas de la pieza. Un ejemplo de este uso es cuando se 
mecaniza una pieza con varias geometrías idénticas en diferentes posiciones. Para cada geometría se utiliza un punto de referencia diferente mediante *G92* y se ejecuta un subprograma
para cada punto de referencia.

.. admonition:: Nota
   :class: Note

   Se recomienda evitar el uso de *G92* para programar como sistena de coordenadas local en partes de un programa. En vez de esto utilice el comando *G52* para definir el decalaje local de 
   una manera más intuitiva cuando se conoce el decalaje deseado del sistema de coordenadas de la pieza pero se desconoce la posición de la herramienta.

Ejecutar el comando *G92 X0 Y0 Z0* graba la posición de la herramienta actual a las coordenadas X0, Y0 y Z0, sin ejecutar movimiento. *G92* no trabaja referido a las coordenadas absolutas de máquina,
trabaja referido a la posición actual.

El comando *G92* también trabaja referido a la posición actual incluyendo las modificaciones de otros decalajes que estén activos al ejecutar *G92*. Tenga en cuenta que el decalaje *G54* puede 
cancelar el efecto de *G92* y por ende dar a entender que no hay decalajes activos. Sin embargo el decalaeje *G92* puede estar activo para los otros sistemas de coordenadas.

Por defecto, los decalajes *G92* son restaurados al iniciar la máquina. Los programadores que desean un comportamiento tipo Fanuc, donde los valores de *G92* son anulados al inicio de la máquina y 
luego del reinicio o fin del programa, desactive la persistencia de *G92* cambiando la instrucción *DISABLE_G92_PERSISTENCE = 1* en la sección *[RS274NGC]* del archivo .ini.

.. admonition:: Nota
   :class: Note

   Es una buena práctica borrar los decalajes *G92* al finalizar su uso con *G92.1* o *G92.2*. Cuando se inicia el controlador con la persistencia de *G92* activada (por defecto) los decalajes de 
   *G92* se aplicarán cuando se hace el referenciado (homing) de los ejes. Ver la sección de *Precauciones sobre Persistencia de G92* más abajo.

**Definiendo valores de G92**

Los comandos *G92* trabajan con la posición de ejes actual y suman o substraen para que la coordenada actual de eje coincida con los valores dados en la instrucción *G92*. El efecto funciona aún cuando 
hay decalajes activos.
Por lo tanto si el eje X actualmente muestra la posición 2.0 y se ejecuta el comando *G92 X0* se modificará el decalaje a -2.0 para que la posición actual sea nula. Si en cambio se ejecuta el comando 
*G92 X2* hará que el decalaje sea 0.0 y la posición mostrada no cambie. Ejecutar *G92 X5.0* hará que el decalaje sea 3.0 y la posición mostrada pase a ser 5.0.

**Precauciones sobre Persistencia de G92**

Por defecto los valores de decalajes de *G92* serán guardados en un archivo de base de datos y serán restaurados en el prendido o reinicio de la máquina. Los parámetrs de G92 son:

+----------------+------------------------------------------+
|      5210      | Bandera de Activo / Desactivo (1/0)      |
+----------------+------------------------------------------+
|      5211      | Decalaje de eje X                        |
+----------------+------------------------------------------+
|      5212      | Decalaje de eje Y                        |
+----------------+------------------------------------------+
|      5213      | Decalaje de eje Z                        |
+----------------+------------------------------------------+
|      5214      | Decalaje de eje A                        |
+----------------+------------------------------------------+
|      5215      | Decalaje de eje B                        |
+----------------+------------------------------------------+
|      5216      | Decalaje de eje C                        |
+----------------+------------------------------------------+
|      5217      | Decalaje de eje U                        |
+----------------+------------------------------------------+
|      5218      | Decalaje de eje V                        |
+----------------+------------------------------------------+
|      5219      | Decalaje de eje W                        |
+----------------+------------------------------------------+

Si se muestran valores inesperados de las posiciones al ejecutar un comando de movimiento, como resultado de haber guardado valores de decalaje en un programa
anterior y no borrar al terminar de utilizalos, ejecute el comando *G92.1* en la interfaz gráfica para borrar los decalajes guardados.

Si hay valores de decalajes de *G92* guardados en el archivo cunado el controlador se inicia, estos valores se aplicarán a los valores que tengan los ejes en ese momento.
Si esta posición es el origen y este origen es el centro de coordenadas de máquina estará correctamente definido. Una vez que se referenciaron los ejes utilizando los 
interruptores de límite o utilizando posiciones conocidas y ejecutando un comando de referencia de ejes, los decalajes *G92* serán aplicados. 
Si tiene un comando *G92 X1* en efecto cuando realiza el referencias del eje X, la pantalla mostrará *X: 1.0* en vez del valor esperado *X: 0.0* debido a que el comando *G92* 
fue aplicado al origen de la máquina. Si ejecuta el comando *G92.1* y la pantalla muestra ahora todos valores nulos de posición, tenía un comando *G92* activo de una corrida anterior.
A no ser que la intensión sea utilizar los decalajes *G92* en el próximo programa, una buena práctica es programar un comando *G92.1* al fin de cualquier código G que utilice 
decalajes *G92*.

**Precauciones de Interacción entre G52 y G92**

Los comandos *G52* y *G92* comparten los registros de decalajes. A no ser que la persistencia de *G92* está desactivada en el achivo .ini, el decalaje *G52* también será 
persistente luego de un reinicion de máquina, *M02* o *M03*. Sea conciente que un decalaje *G52* que esté activo durante una terminación inesperada de un programa puede resultar
en valores inesperados de decalajes.


.. _refG92.1:

G92.1 G92.2 Resetear Decalaje de Sistema de Coordenadas G92
-----------------------------------------------------------

* *G92.1* desactiva los decalajes *G92* y sobreescribe sus valores 5211 - 5219 a valores a cero.
* *G92.2* desactiva los decalajes *G92* pero mantiene los valores 5211 - 5219 existentes.

.. admonition:: Nota
   :class: Note

   *G92.1* solo modifica a cero los decalajes *G92*, para cambiar los decalajes de los sistemas de coordenadas *G53* a *G59.3* utilice los comandos :ref:`G10 L2 <refG10L2>` o :ref:`G10 L20 <refG10L20>`


.. _refG92.3:

G92.3 Restablecer Decalaje de Sistema de CoordenadasG92
-------------------------------------------------------

* *G92.3* activa los decalajes de *G92* con los valores guardados en los parámetros 5211 a 5219

Se pueden grabar los valores de decalajes en un programa y utilizarlos en otro. Programe el comando *G92* en el primer programa. Esto guardará los valores en los parámetros 5211 a 5219.
No utilice *G92.1* en el resto del programa. Los valores guardados se pueden utilizar en el segundo programa utilizando el comando *G92.3*.


.. _refG93:

G93 G94 G95 Modo de Avance
--------------------------

* *G93* indica el modo de definición de la velocidad de avance por inversa del tiempo. En este modo el valor de F significa que el movimiento deberá ser completado en 1 dividido el valor de F minutos. Por ejemplo, si el número F es 2.0, el movimiento tendrá que ser completado en medio minuto o 30 segundos.

Cuando el modo de avance de inversa del tiempo está activo, se deberá especificar el valor F en cada línea que implique movimiento a velocidad de avance (*G1*, *G2* o *G3*) y cualquier valor 
de F que no esté en una línea que no tiene *G1*, *G2* o *G3* es ignorado. Este modo no afecta a los movimientos rápidos *G0*.

* *G94* es el modo de definición de velocidad de avance en unidades por minuto. En este modo el valor de F es interpretado como la cantidad de unidades que se desplaza por minuto, ya sea pulgada por minuto o milímetros por minuto dependiendo las unidades de longitud seleccionadas. Para ejes de rotación, la velocidad de avance se define en grados por minuto.

* *G95* es el modo de definición de velocidad de avance en unidades por revolución. En este modo el valor de F es interpretado como la cantidad de unidades que se desplaza por revolución de husillo, dependiendo de las unidades seleccionadas y el tipo de eje que se desplaza. *G95* no es aplicable a roscado, para lo que se debe utilizar *G33* o *G67*. *G95* requiere que el testigo *spindle.N.speed-in* esté conectado. El husillo al cual se sincroniza el movimiento se determina con el valor de $.

Da error si:

   * Si el modo por inversa del tiempo (*G93*) está activo y se utiliza un comando *G1*, *G2* o *G3* (explícitamente o implícitamente) y la línea no defina el valor de F
   * Si no se especifica un nuevo valor al cambiar a *G94* o *G95*

.. _refG96:

G96 G97 Modo de Control de Husillo
----------------------------------

::

   G96 <D-> S- <$-> (Modo de velocidad superficial constante)
   G97 S- <$-> (Modo de revoluciones por minuto RPM)

* *D* Velocidad máxima de husillo en RPM
* *S* Velocidad superficial
* *$* Husillo para el cual la velocidad se define
* *G96 D- S-* Selecciona velocidad superficial constante de *S* pies por minuto (si *G20* está activo) o metros por minuto (si *G21* está activo. D- es opcional.

Para programar el modo de velocidad superficial constante en varios husillos utilice comandos *G96* sucesivos antes de ejecutar *M3*.

   * *G97* selecciona el modo de revoluciones por minuto.

   **Ejemplo de G96**

::

   G96 D2500 S250 (activa el modo de velocidad superficial constante con un máximo de 2500 RPM y velocidad superficial de 250)

Da error si:

   * S no se especifica en *G96*
   * Se especifica una velocidad de avance con *G96* cuando el husillo no está girando

.. _refG98:

G98 G99 Nivel de Retorno de Ciclos Cerrados
-------------------------------------------

* *G98* define la posición de retracción a la posición en la que el eje estaba justo antes de la serie de movimientos de ciclo cerrado
* *G99* define la posición de retracción al valor especificado por R en el comando de ciclo cerrado

Utilice el comando *G98* para que los ciclos cerrados utilicen la posición en el eje Z previa al ciclo cerrado como posición de rtracción si 
ésta es mayor que el valor de R especificado en el comando. Si es menor, el valor de R será utilizado. El valor de R tiene diferentes significados
dependiendo si el modo de posición absoluta o relativa está activo.

**Retracción al origen**

::

   G0 X1 Y2 Z3
   G90 G98 G81 X4 Y5 Z-0.6 R1.8 F10

El comando *G98* en la segunda línea de arriba indica que el movimiento de retracción se realizará al valor de Z en la primer línea ya que es 
mayor al valor de R especificado.

El plano inicial (*G98*) se resetea cada vez que se finaliza el ciclo cerrado, ya sea explícitamente (*G80*) o implícitamente (por cualquier 
movimiento que no sea un ciclo cerrado). El cambio entre modos de ciclos (por ejemplo *G81* y *G83*) no resetea el plano inicial. Es posible cambiar entre
*G98* y *G99* durante una serie de ciclos.


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
|  :ref:`M60 <refM60>`          | Pausa de Cambio de Pieza                                          |
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
| :ref:`M53 <refM53>`           | Control de Parada de Avance                                       |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M61 <refM61>`           | Definir Número de Herramienta Actual                              |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M62-M65 <refM62>`       | Control de Salidas Digitales                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M66 <refM66>`           | Espera Señal de Entrada                                           |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M67 <refM67>`           | Salidas Analógicas Sincronizadas                                  |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M68 <refM68>`           | Salidas Analógicas Inmediatas                                     |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M70 <refM70>`           | Guardar Estados Modales                                           |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M71 <refM71>`           | Invalidar Estados Modales Guardados                               |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M72 <refM72>`           | Reestablecer Estados Modales                                      |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M71 <refM73>`           | Guardar y Autorestablecer Estados Modales                         |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M98 M99 <refM98>`       | Llamada y Retorno a Subrutinas                                    |
+-------------------------------+-------------------------------------------------------------------+
| :ref:`M100-M199 <refM100>`    | Códigos M Definidos por el Usuario                                |
+-------------------------------+-------------------------------------------------------------------+


.. _refM0:

M0 M1 Pausa de Programa
-----------------------

* *M0* pausa temporariamente al programa en ejecución. El controlador permanece en modo Automático por lo que las acciones manuales no están habilitadas. Al presionar el botón Reanudar el programa continuará en la siguiente línea.

* *M1* pausa temporariamente al programa en ejecución si está activado el interruptor opcional de parada. El controlador permanece en modo Automático por lo que las acciones manuales no están habilitadas. Al presionar el botón Reanudar el programa continuará en la siguiente línea.

.. admonition:: Nota
   :class: Note

   Está permitido programar un comando *M0* o *M1* desde el modo Manual de Input, pero el efecto probablemente no será percibido, ya que el modo normal de comportamiento
   de este modo es que frenar la ejecución luego de cáda comando de todas formas.


.. _refM2:

M2 M30 Fin de Programa
----------------------

* *M2* fin de programa. Al presionar *Comienzo de Ciclo* (*R* en la Interfaz de Usuario) se reiniciará el programa desde el principio del archivo.
* *M30* acciona cambiador de piezas y fin de programa. Al presionar *Comienzo de Ciclo* se reiniciará el programa desde el principio del archivo.

Ambos comandos tienen los siguientes efectos:

#. Cambian el modo de Automático a Manual
#. Los decalajes de origen pasan a los valores por defecto (*G54*)
#. El plano de trabajo activo para a ser el plano XY (*G17*)
#. El modo de distancia para a ser el absoluto (*G90*)
#. El modo de velocidad de avance se activa en unidaes por minuto (*G94*)
#. Los overrides de velocidad de husillo y velocidad de avance pasan a estar activos (*M48*)
#. La compensación de herramientas se desactiva (*G40*)
#. El husillo se frena (*G5*)
#. El modo de movimiento pasa a movimiento con velocidad de avance (*G1*)
#. La bomba de refrigerante se apaga (*M9*)

.. admonition:: Nota
   :class: Note

   Las líneas de código luego de M2/M30 no serán ejecutadas. Al presionar *Comienzo de Ciclo* se reiniciará el programa desde el principio del archivo

.. admonition:: Precaución
   :class: Warning

   Utilizar *%* para encerrar el código G no tiene el mismo efecto que un comando de *Fin de Programa*. Para más información sobre el efecto de los signos *%*
   vea la sección :ref:`Requerimientos de Archivos <fileReq>`


.. _refM60:

M60 Pausa de Cambio de Pieza
----------------------------

* *M60* activa cambiador de pieza y luego pausa el programa temporalmente (independientemente de si está activado el interruptor opcional de parada).
  Al presionar *Comienzo de Ciclo* se reiniciará el programa desde la línea siguiente.


.. _refM3:

M3 M4 M5 Control de Husillo
---------------------------

* *M3 [$]n* arranca el husillo seleccionado en sentido horario a la velocidad *S*
* *M4 [$]n* arranca el husillo seleccionado en sentido antihorario a la velocidad *S*
* *M5 [$]n* frena el husillo seleccionado

El símbolo *$* se utiliza para seleccionar el husillo. Si *$* no se utiliza el comando tiene efecto sobre el husillo *spindle.0*. Use $-1 para operar sobre 
todos los husillos activos.

Este ejemplo enciende los husillo 0, 1 y 2 simultáneamente a diferentes velocidades::

   S100 $0
   S200 $1
   S300 $2
   M3 $-1

Este ejemplo invertirá el sentido de giro del husillo 1 pero dejará a los otros husillos girando en el mismo sentido::

   M4 $1

Y este comando frenará al husillo 2 pero dejará girando a los otros husillos::

   M5 $2

Si no se utiliza el símbolo *$* el comportamiento es igual para una máquina de un solo husillo.
Está permitido utilizar los comandos *M3* y *M4* si la velocidad de husillo es nula S=0. Si esto se hace (o si el override de velocidad está habilitado y con valor cero) 
el husillo no comenzará a girar. Si, luego, la velocidad de husillo se cambia a un valor no nulo (o si el override de velocidad está habilitado y se eleva su valor),
el husillo comenzará a girar. Está permitido utilizar los comandos *M3* y *M4* si el husillo ya está girando o utilizar *M5* si el husillo está frenado.


.. _refM6:

M6 Cambio de Herramienta
------------------------

::

   T2 (define la próxima herramienta a utilizar)
   M6 (realizar cambio a la herramienta)

**Cambio de Herramienta Manual**

Si el componente de HAL (Hardware abstraction Layer) *hal_manualtoolchange * está cargado, *M6* frenará el husillo y mostrará el mensaje en pantalla al usuario para que cambien a la 
herramienta definida por el número *T-*. Luego de que el usuario realice el cambio de herramienta, al presionar el botón *OK*, la ejecución del programa continuará.

Este componente de HAL incluye una conexión que permite conectar un botón físico en vez del mensaje en pantalla (*hal_manualtoolchange.change_button*).

El archivo de configuración de HAL *lib/hallib/axis_manualtoolchange.hal* muestra los comandos necesarios para utilizar este componente.

**Cambio de Herramienta Automático**

*M6* realiza el cambio de la herramienta que se encuentra actualmente en el husillo a la herramienta que se seleccionó más recientemente (ver sección :ref:`T <refT>`).
Cuando el cambio de herramienta se complete:

* El husillo permanecerá frenado
* Si la herramienta seleccionada no estaba en el husillo la herramienta que estaba en el husillo (si había una) quedará en el cargador de herramientas.
* Si estaba en el archivo de configuración .ini algunos ejes se podrán mover al ejecutar *M6*. Para más información sobre las opciones de cambio de herramientas
  ver la :ref:`Seccción EMCIO <sectionEMCIO>`
* No se realizará algún otro cambio. Por ejemplo, si la bomba de refrigerante estaba encendida quedará encendida durante el cambio de herramienta

.. admonition:: Precaución
   :class: warning

   El decalaje de largo de herramienta no se modificado por *M6*, utilice *G43* luego de un cambiar a una herramienta *M6* con otro largo

El cambio de herramienta podrá incluir el movimiento de ejes. Está permitido (pero no es útil) programar un cambio a la herramienta que ya está en el husillo. 
Está permitido realizar un cambio a un número en el que el cargador no tiene herramienta, en este caso el husillo quedará vacío luego del cambio de herramienta.
Si se selecciona el número 0 el husillo quedará vacío luego del cambio de herramienta. El cambiador de herramientas debe ser configurado para poder realizar los 
cambios de herramientas en el HAL y posiblemente en el PLC (Programmable logic controller).

.. admonition:: Nota
   :class: note

   Consultar con el integrador de máquina si el comando *M6* se ejecuta implícitamente con el comnado *T*. Generalmente en tornos y en centros de mecanizados con 
   cambiador de herramientas no aleatorio la ejecución de *T* implica la ejecución implícita de *M6*.

.. _refM7:

M7 M8 M9 Control de Refrigerante
--------------------------------

* *M7* prender la bomba del refrigerante de niebla. *M7* controla el testigo *iocontrol.0.coolant-mist*
* *M8* prender la bomba del refrigerante líquido. *M7* controla el testigo *iocontrol.0.coolant-flood*
* *M9* apagar ambas bombas *M7* y *M8* de refrigerante

Conecte uno o ambos testigos del refrigerante en el HAL antes de poder prender/apagar las bombas de refrigerante. *M7* y *M8* pueden ser utilizados para encender / apagar
cualquier salida a través de Código G.
Está permitido utilizar cualquiera de estos comandos independientemente del estado del bombeo de refrigerante.


.. _refM19:

M19 Orientación de Husillo
--------------------------
::

   M19 R- Q- [P-] [$-]

* *R* Posición a la cual rotar, el rango válido es de 0 a 360 grados
* *Q* Número de segundos de espera para que la orientación se realice. Si el valor de *spindle.N.is-oriented* no se convierte en *verdadero* dentro del lapso de *Q* segundos, se emite un error.
* P Dirección de rotación para orientar
   * 0 para orientar con el ángulo más pequeño (por defecto)
   * 1 para rotar sólo en el sentido horario (en el mismo sentido que *M3*)
   * 2 para rotar sólo en el sentido antihorario (en el mismo sentido que *M4*)
* *$* selección de husillo (determina cuales testigos del HAL se tienen en cuenta para los comandos de orientación)

*M19* se desactiva con cualquiera de *M3*, *M4* o *M5*.

La orientación de husillo requiere de un encoder de cuadratura con un índice para poder determinar la posición y sentido de giro.

La configuración se puede editar en la :ref:`Seccción RS274NGC <sectionRS>` del archivo .ini. El parámetro *ORIENT_OFFSET* con valores de 0 a 360 grados se agrega al valor indicado
por *R-*.

Testigos de HAL (Hardware Abstraction Layer):

* *spindle.N.orient-angle* (out float) orientación deseada por comando *M19*. El valor de *R* especificada en el *M19* más el valor del parámetro *[RS274NGC]ORIENT_OFFSET* del archivo .ini.
* *spindle.N.orient-mode* (out S32) modo de rotación para orientación, o sea el parámetro *P* en el *M19*, por defecto = 0
* *spindle.N.orient* (out bit) Indica el inicio del ciclo de orientación. Activado por *M19* y desactivado por *M3*, *M4* o *M5*. Si el valor de *spindle-orient-fault* no es cero durante *spindle-orient*, el comando *M19* da mensaje de error.
* *spindle.N.is-oriented* (in bit) acusa recibo de que el husillo está orientado. Completa el ciclo de orientación. Si *spindle-orient* es verdadero cuando *spindle-is-oriented* se volvió verdadero, *spindle-orient* se vuelve falso y *spindle-locked* se prende. También se prende el testigo * spindle-brake*.
* *spindle.N.orient-fault* (in s32) código que indica falla del ciclo de orientación. Cualquier valor salvo cero causa la anulación del ciclo.
* *spindle.N.locked* (out bit) indica orientación de husillo realizada. Se apaga con cualquier comando *M3*, *M4* o *M5*.


.. _refM48:

M48 M49 Activar / Desactivar Override de Avance y Husillo
---------------------------------------------------------

* *M48* activa el control de override de velocidad de husillo y de velocidad de avance
* *M49* desactiva ambos controles de override

Estos comandos también aceptan el s+imbolo opcional *$* para indicar en cuál husillo operan.
Está permitido activar o desactivar los controles de override si ya están en el mismo estado. Para más información ver la sección de :ref:`Modo de Avance <refG93>`.


.. _refM50:

M50 Control de Override de Avance
---------------------------------

* *M50 <P1>* activa el control de override de velocidad de avance. El parámetro P1 es opcional.
* *M50 <P0>* desactiva el control de override de velocidad de avance.

Cuando está desactivado el control de override no tiene infuencia y el programa realizará movimientos a la velocidad de avance programada, salvo que esté activo
 el modo adaptativo de override de control de avance.


.. _refM51:

M51 Control de Override de Husillo
----------------------------------

* *M51 <P1> <$->* activa el control de override de velocidad de husillo. El parámetro P1 es opcional.
* *M51 P0 <$->* desactiva el control de override de velocidad de husillo. Cuando está desactivado el control de override no tiene infuencia y la velocidad del husillo será la determinada por el comando *S-*.

.. _refM52:

M52 Control Adaptativo de Avance
--------------------------------

* *M52 <P1>* activa el modo adaptativo de velocidad de avance. El parámetro P1 es opcional.
* *M52 P0* desactiva modo adaptativo de velocidad de avance.

Cuando el modo adaptativo de avance está activo, se utiliza algún input externo en conjunto con el control de override de usuario y valor de velocidad programado para
determinar la velocidad real de avance. En este control el testigo de HAL *motion.adaptive-feed* se utiliza con este propósito. Los valores *motion.adaptive-feed* 
deberían variar entre -1 (velocidad programada en reversa) y 1 (velocidad plena). El valor 0 equivale a anular el avance.


.. admonition:: Nota
   :class: note

   El uso de la velocidad programada en reversa está indicada para corte de plasma o corte por hilo pero no se limita a estos usos


.. _refM53:

M53 Control de Parada de Avance
-------------------------------

* *M53 <P1>* activa el interruptor de parada de avance. P1 es opcional. Activar el interruptor de parada de avance permitirá al interruptor frenar el movimiento. En este controlador el testigo de HAL *motion.feed-hold* se utiliza para este propósito. Un valor verdadero causará la interrupción del movimiento si el comando *M53* está activo.
* *M53 P0* desactiva el interruptor de parada de avance. El valor de *motion.feed-hold* no tendrá efecto cuando *M53* no está activo.


.. _refM61:

M61 Definir Número de Herramienta Actual
----------------------------------------

* *M61 Q-* cambiar el número de la herramienta actual sin realizar cambio de herramienta. Se utiliza cuando se inicia el controlador y hay una herramienta colocada en
    el husillo, con este comando se puede determinar el número de la herramienta sin ejecutar ninguna acción. *M61 Q0* hará que el husillo quede en modo descargado.

.. admonition:: Precaución
   :class: warning

   El decalaje de largo de herramienta no se cambia por el comando *M61*, utilice *G43* luego de *M61* para cambiar el decalaje de largo de herramienta


Da error si:

   * *Q-* no es mayor o igual a 0


.. _refM62:

M62-M65 Control de Salidas Digitales
------------------------------------

* *M62 P-* activa una salida digital sincronizada con el movimiento. El parámetro *P-* especifica el número de la salida digital.
* *M63 P-* desactiva una salida digital sincronizada con el movimiento. El parámetro *P-* especifica el número de la salida digital.
* *M64 P-* activa una salida digital inmediatamente. El parámetro *P-* especifica el número de la salida digital.
* *M65 P-* desactiva una salida digital inmediatamente. El parámetro *P-* especifica el número de la salida digital.

El valor de *P-* tiene un rango desde 0 a un valor por defecto de 3. De ser necesario el número de I/O (entradas/salidas) puede ser incrementado cambiando el valor de *num_dio* al cargar el controlador de movimiento. Para más información ver la sección de :ref:`Movimiento <refMotion>`.

Los comandos *M62* y *M63* serán puestos en agenda. Los comandos subsiguientes que hagan referencia a la misma salida sobreescribirán el valor de configuraciones 
anteriores. Se puede definir el valor de más de una salida utilizando varios comandos *M62*/*M63*.

El cambio de los valores de las salidas se realizará en el comienzo del próximo comando de movimiento. Si no hay un comando de movimiento subsiguiente, el cambio 
agendado de la/s salida/s no se llevará a cabo. Es usual utilizar un comando de movimiento (*G0*, *G1*, etc.) inmediatamente luego de *M62*/*M63*.

*M64*/*M65* implementan realizan el cambio del valor de la salida inmediatamente ya que son recibidos por el controlador de movimiento. No están sincronizados con el 
movimiento, y cancelarán el suavizado de trayectoria.

.. admonition:: Nota
   :class: note

   *M62*-*M65* no funcionarán a no ser que se conecte el testigo adecuado *motion.digital-out-nn* en el archivo HAL a las salidas


.. _refM66:

M66 Espera Señal de Entrada
---------------------------

::

   M66 P- | E- <L->

* *P-* especifica el número de entrada digital de 0 a 3
* *E-* especifica el número de entrada analógica de 0 a 3
* *P-* especifica el tipo de modo de espera

   * Modo 0: Inmediato. No espera, retorna inmediatamente. El valor actual de la entrada es guardado en el parámetro #5399
   * Modo 1: Flanco positivo. Espera que la entrada pase desde un valor negativo a uno positivo. 
   * Modo 2: Flanco negativo. Espera que la entrada pase desde un valor positivo a uno negativo.
   * Modo 3: Positivo. Espera a que la entrada tenga un valor positivo.
   * Modo 4: Negativo. Espera a que la entrada tenga un valor negativo.

* *Q-* especifica el tiempo de espera en segundos. Si el tiempo se excede, el comando de espera se interrumpe, y la variable #5399 pasará a tener un valor de -1. El valor de *Q-* es ignorado si el valor de *L-* es cero (comportamiento inmediato). Un valor de *Q-* de cero da error si el valor de *L-* no es cero.
* El modo 0 es el único permitido para entradas analógicas

**Ejemplo de M66**::

   M66 P0 L3 Q5 (espera hasta 5 segundos a que la entrada digital número 0 se encienda)

*M66* frena la ejecución del progrma hasta que ocurre el evento determinado en la entrada especificada o hasta que el tiempo de espera se supera. 
Es un error programar *M66* con ambos, un parámetro *P-* y un parámetro *E-*, se debe seleccionar un tipo de entrada, analógica o digital. En el control estas 
entradas no son monitorizadas en tiempo real y por lo tanto no deben utilizarse para aplicaciones en las que el tiempo sea crítico.
El número de I/O (entradas/salidas) puede ser incrementado cambiando el valor de *num_dio* o *num_aio* al cargar el controlador de movimiento.
Para más información ver la sección de :ref:`Movimiento <refMotion>`.

.. admonition:: Nota
   :class: note

   *M66* no funcionarán a no ser que se conecte el testigo adecuado *motion.digital-in-nn* o el *motion.analog-in-nn* en el archivo HAL a las entradas

**Ejemplo de conección de HAL**::

   net signal-name motion.digital-in-00 <= parport.0.pin10-in


.. _refM67:

M67 Salidas Analógicas Sincronizadas
------------------------------------

::

   M67 E- Q-

* *M67* configura una salida analógica sincronizada con el movimiento
* *E-* número de salida con un rango desde 0 a 3
* *Q-* es el valor a configurar (configurar a 0 para apagar)

El cambio de los valores de las salidas se realizará en el comienzo del próximo comando de movimiento. Si no hay un comando de movimiento subsiguiente, el cambio 
agendado de la/s salida/s no se llevará a cabo. Es usual utilizar un comando de movimiento (*G0*, *G1*, etc.) inmediatamente luego de *M67*. *M67* funciona de igual
manera a *62*-*63*.

De ser necesario el número de I/O (entradas/salidas) analógicas puede ser incrementado cambiando el valor de *num_aio* al cargar el controlador de movimiento. Para más información ver la sección de :ref:`Movimiento <refMotion>`.

.. admonition:: Nota
   :class: note

   *M67* no funcionarán a no ser que se conecte el testigo adecuado *motion.analog-out-nn* o el *motion.analog-in-nn* en el archivo HAL a las salidas


.. _refM68:

M68 Salidas Analógicas Inmediatas
---------------------------------

::

   M68 E- Q-

* *M67* configura una salida analógica inmediatamente
* *E-* número de salida con un rango desde 0 a 3
* *Q-* es el valor a configurar (configurar a 0 para apagar)

El cambio de los valores de las salidas se realizará inmediatamente ya que son recibidos por el controlador de movimiento. No están sincronizados con el 
movimiento, y cancelarán el suavizado de trayectoria. *M68* funciona de igual manera que *64*-*65*.

De ser necesario el número de I/O (entradas/salidas) analógicas puede ser incrementado cambiando el valor de *num_dio* o *num_aio* al cargar el controlador de movimiento. Para más información ver la sección de :ref:`Movimiento <refMotion>`.

.. admonition:: Nota
   :class: note

   *M68* no funcionarán a no ser que se conecte el testigo adecuado *motion.analog-out-nn* o el *motion.analog-in-nn* en el archivo HAL a las salidas


.. _refM70: 

M70 Guardar Estados Modales
---------------------------

Para guardar explícitamente los estados modales con los valores actuales utilice el comando *M70*. Una vez que el estado modal ha sido guardado con *M70*, puede ser
restaurado a los mismos valores con el comando *M72*.
El par de comandos *M70* y *M72* típicamente se utiliza para proteger a un programa de cualquier cambio modal inadvertido que pueda ocurrir en las subrutinas.
El estado modal guardado consiste de:

   * definición del tipo de unidad G20/G21 (imperiales/métricas)
   * plano de trabajo seleccionado (G17/G18/G19 G17.1,G18.1,G19.1)
   * estado de compensación del radio de herramienta (G40,G41,G42,G41.1,G42,1)
   * modo de distancia - relativa/absoluta (G90/G91)
   * modo de velocidad de avance (G93/G94,G95)
   * sistema de coordenadas actual (G54-G59.3)
   * modo de compensación de largo de herramienta (G43,G43.1,G49)
   * modo de retracción (*G98*,*G99*)
   * modo de velocidad de husillo (G96-css or G97-RPM)
   * modo de distancia de arco de círculo (G90.1, G91.1)
   * modo radial/diametral en tornos (G7,G8)
   * modo de control de trayectoria (G61, G61.1, G64)
   * valores actuales de velocidad de husillo y de avance (valores F y S)
   * estado de husillo (M3,M4,M5) - en movimiento o frenado y dirección
   * estado de bombas de refrigerantes (M7 y M8)
   * valores de override de velocidad de husillo (M51) y de velocidad de avance (M50)
   * configuración de avance adaptativo (M52)
   * configuración de parada de avance (M53)

Notar que el modo de movimiento (*G1*,etc) No se reestablece.

El nivel de llamada actual refiere a una de las siguientes opciones:

   * Al ejecutar el programa principal. Hay un solo almacenamiento para el estado modal en el nivel del programa principal; si se realizan varias llamadas a la instrucción *M70* se ejecutan en turno, sólo el estado en la última llamada se restaura por medio del comando *M72*.

   * Al ejecutar en una subrutina. El comportamiento de *M70* es igual al comportamiento de un parámetro local, puede ser referido sólo dentro de esta subrutina al llamar a *M72* y cuando la subrutina retorna al nivel superior el parámetro desaparece.

Una invocación recursiva a una subrutina introduce un nuevo nivel a la llamada.


.. _refM71:

M71 Invalidar Estados Modales Guardados
---------------------------------------

Al ejecutar *M71* el estado modal guardado con *M70* o por *M73* es invalidado en el nivel actual y no puede ser restaurado.

Un llamado posterior a *M72* en el mismo nivel emite error.

Si se ejecuta *M71* en una subrutina en la que el estado modal está protegida por el comando *M73* un retorno o *endsub* posterior **no** restaurará el estadoo modal.

En la práctica este comando no es muy útil.


.. _refM72:

M72 Reestablecer Estados Modales
--------------------------------

El estado modal guardado con *M70* puede ser reestablecido al ejecutar *M72*.

El manejo de *G20*/*G21* es tratado especialmente e interpretado de manera diferente dependiendo de *G20*/*G21*:

Si las unidades (mm/in) están por ser cambiadas por la operación de restauración *M72*, se restaura el modo de distancia primero, y luego todos los
otros estados incluyendo el avance para asegurarse de que el valor de velocidad de avance se interpreta en la con la unidad de longitud correcta.

Se produce un error si se ejecuta *M72* sin haber guardado previamente el estado modal con *M70*.

El siguiente ejemplo demuestra el guardado y restaura el estado modal explícitamente luego de llamar a una subrutina. Notar que la subrutina
*imperialsub* no se "entera" de los comandos *M70* y * M72* y puede ser utilizada sin cambios.

::

   O<mostarestado> sub
   (DEBUG, imperial=#<_imperial> absolute=#<_absolute> avance=#<_avance> rpm=#<_rpm>)
   O<mostarestado> endsub
   
   O<imperialsub> sub
   g20 (imperial)
   g91 (modo relativo)
   F5 (avance bajo)
   S300 (bajo rpm)
   (debug, en subrutina, estado actual:)
   o<mostarestado> call
   O<imperialsub> endsub
   
   ; programa principal
   g21 (metrica)
   g90 (absoluta)
   f200 (velocidad alta)
   S2500 (alto rpm)
   
   (debug, en principal, estado actual:)
   o<mostarestado> call
   
   M70 (grabar estados en principal a nivel global)
   O<imperialsub> call
   M72 (restaurar estados explicitamente)
   
   (debug, de vuelta en principal, estado actual:)
   o<mostarestado> call
   m2


.. _refM73:

M73 Guardar y Autorestablecer Estados Modales
---------------------------------------------

Se utiliza el comando *M73* para guardar el estado modal en una subrutina y restaurarlo al volver a la función que la llama, ya sea por llegar al final de la misma *endsub* 
o por un comando *return*.

Si se aborta la corrida de un programa en una subrutina que contiene *M73* **no** restaura el estado modal.

De la misma manera, el fin de programa (*M2*) en un programa principal que contenga *M73* **no** restaura el estado modal.

El modo de uso sugerido luego de la palabra *O-* de subrutina se muestra en el siguiente ejemplo. Utilizar *M73* de esta manera permite diseñar subrutinas que pueden modificar 
el estado modal pero protengen al programa que las llama de los cambios modales que realicen. Note el uso de los mensajes en los que se muestran los valores de los parámetros en 
la subrutina *mostrarestado*.

::

   O<mostarestado> sub
   (DEBUG, imperial=#<_imperial> absolute=#<_absolute> avance=#<_avance> rpm=#<_rpm>)
   O<mostarestado> endsub
   
   O<imperialsub> sub
   M73 (grabar estados en el contexto actual de subrutina, restaurar al retorno o endub)
   g20 (imperial)
   g91 (modo relativo)
   F5 (avance bajo)
   S300 (bajo rpm)
   (debug, en subrutina, estado actual:)
   o<mostarestado> call
   
   ; nota - no hace falta M72 acá - el siguiente endsub o
   ; un comando return restaurará el estado de la rutina que llama
   O<imperialsub> endsub
   
   ; programa principal
   g21 (metrica)
   g90 (absoluta)
   f200 (velocidad alta)
   S2500 (alto rpm)
   (debug, en principal, estado actual:)
   o<mostarestado> call
   O<imperialsub> call
   (debug, de vuelta en principal, estado actual:)
   o<mostarestado> call
   m2


.. _refM98:

M98 M99 Llamada y Retorno a Subrutinas
--------------------------------------

El interpretador soporta el estilo tipo Fanuc de programa principal y subprogramas con los códigos *M98* y *M99*. Para más información ver la sección :ref:`Códigos O <refOcodes>`.

**Restaurar estados modales selectivamente**

Al ejecutar *M72* o retornar desde una subrutina que contenga un código *M73* se restauran *todos* los estados modales.

Si se desea preservar determinados estados modales, una alternativa es utilizar :ref:`Parámetros con Nombre Predefinidos <refNamedPredefParam>`, parámetros locales y declaraciones condicionales.
El concepto es guardar los modos de operación a ser restaurados al principio de la subrutina, y reestablecerlos antes del retorno. A continuación se muestra un ejemplo::

   O<medicion> sub (medicion de herramienta de referencia)
   ;
   #<absoluto> = #<_absoluto> (guardar en variable local si se utilizó G90)
   ;
   g30 (sobre interruptor)
   g38.2 z0 f15 (medicion)
   g91 g0z.2 (interruptor accionado)
   #1000=#5063 (guardar la longitud de referencia de la herramienta)
   (print, la longitud de referencia es #1000)
   ;
   O<restaurar_abs> if [#<absoluto>]
       g90 (restaurar G90 sólo si estaba activo al inicio:)
   O<restaurar_abs> endif
   ;
   O<medicion> endsub


.. _refM100:

M100-M199 Códigos M Definidos por el Usuario
--------------------------------------------

::

   M1-- <P- Q->

* *M1* entero en el rango de 100 a 199
* *P-* número que pasa a archivo como primer parámetro
* *Q-* número que pasa a archivo como segundo parámetro

.. admonition:: Nota
   :class: note

   Luego de crear un nuevo archivo *M1nn* debe reiniciar la Interfaz de Usuario para incorporar el archivo nuevo, en caso contrario el resultado será *Código M desconocido*

El programa externo *M100* a *M199* (sin extención y con M mayúscula) será ejecutado con los valores opcionales de *P* y *Q* como argumentos. La ejecución del código G se pausa
hasta que finalice la ejecución del programa externo. Cualquier archivo ejecutable puede ser utilizado. El archivo debe etar ubicado en la dirección de búsqueda especificado en 
el archivo de configuración .ini. Para más información ver la :ref:`Sección de Display <sectionDISPLAY>`.

.. admonition:: Precaución
   :class: warning

   No utilice un procesador de texto enriquecido para crear o editar los archivos. Este tipo de procesador dejará código oculto que causará problemas. Utilice un procesador de 
   texto simple como Geany en Linux o Notepad++ en otros sistemas operativos para crear o editar los archivos.

Da error si:

   * Se utiliza un comando definido por el usuario que no existe
   * El archivo no es ejecutable
   * El archivo tiene extensión
   * El nombre del archivo no sigue el formato *Mnnn*, donde *nnn* es igual a 100 a 199
   * El nombre del archivo utiliza m minúscula

Un ejemplo de utilización puede ser abrir y cerrar un mandril que es controlado por un testigo en un puerto paralelo utilizando un archivo de ejecución de sistema (bash script) 
utilizando *M101* y *M102*. Crear dos archivos con nombre M101 y M102. Configurarlos como archivos ejecutables modificando sus propiedades antes de correr el controlador.
Asegurarse que el testigo del puerto paralelo no está conectado en el archivo HAL.

**Ejemplo de M101**

::

   #!/bin/bash
   # file to turn on parport pin 14 to open the collet closer
   halcmd setp parport.0.pin-14-out True
   exit 0

**Ejemplo de M102**

::

   #!/bin/bash
   # file to turn on parport pin 14 to open the collet closer
   halcmd setp parport.0.pin-14-out False
   exit 0

Para pasar una variable a un archivo M1nn utilice los párametros opcionales *P-* y/o *Q-*::

   M100 P123.456 Q321.654

**Ejemplo de M100**

::

   #!/bin/bash
   voltage=$1
   feedrate=$2
   halcmd setp thc.voltage $voltage
   halcmd setp thc.feedrate $feedrate
   exit 0

Para mostrar un mensaje en ventana y frenar hasta que la ventana se cierre utilice un programa gráfico como Eye of Gnome. Cuando cierre la ventana la ejecución del programa se 
reanudará.

**Ejemplo de M110**

::

   #!/bin/bash
   eog /home/john/linuxcnc/nc_files/message.png
   exit 0

Para mostrar un mensaje en ventana y continuar procesando el còdigo G utilice el símbolo & al final de la línea.

**Ejemplo de M110 con continuación**

::

   #!/bin/bash
   eog /home/john/linuxcnc/nc_files/message.png &
   exit 0


.. _refOcodes:

Códigos O
=========

Los códigos O proveen un control de flujo en los programas de control numérico. Cada bloque (o línea) tiene un número asociado, que es el número utilizado luego de la O.
Se debe tener cuidado para que haya correspondencia de los números O. Notar que los códigos O utilizan la letra o minúscula o O mayúscula pero no el número 0, por ejemplo
o100 o O100.

Numeración
----------

Los números de los códigos O deben tener una numeración única para cada subrutina. Por ejemplo::

   (comienzo de o100)
   o100 sub
   (notar que el if-endif utilizan una numeración diferente)
     (comienzo de o110)
     o110 if [#2 GT 5]
       (algo de código acá)
     (fin de o110)
     o110 endif
     (algo de código acá)
   (fin de o100)
   o100 endsub

Comentarios
-----------

No se deben utilizar los comentarios en la misma línea que el código O debido a que el comportamiento puede cambiar en el futuro.

El comportamiento es indefinido si:

   * El mismo número se utiliza para más de un bloque
   * Se utilizan otras letras en la misma línea que la letra O
   * Se utilizan comentarios en la misma línea que la letra O

.. admonition:: Nota
   :class: note

   Utilizar la letra o minúscula hace más fácil diferenciar cuando hay un error de escritura. Por ejemplo o100 se diferencia más fácil
   que O100 (con O mayúscula) de 0100 (con cero)

Subrutinas
----------

Las subrutinas empiezan con *Onnn sub* y terminan con *Onnn endsub*. Las líneas entre estos dos marcadores no se ejecutan hasta que 
se las llama con *Onnn call*. Cada subrutina debe tener una numeración única.

**Ejemplo de Subrutina**

::

   o100 sub
     G53 G0 X0 Y0 Z0 (movimiento rápido al origen)
   o100 endsub
   
   (se llama a la subroutina)
   o100 call
   M2

**Retorno O-**

Dentro de una subrutina, el comando *O- return* puede ser ejecutado. Esto retorna inmediatamente al programa que llamó a la subrutina, de manera similar 
a cuando se encuentra el comando *O- endsub*.

**Ejemplo de Retorno O-**

::

   o100 sub
     (testear si el parámetro #2 es mayor que 5)
     o110 if [#2 GT 5]
       (retornar al inicio de subrutina si la condición se cumple)
       o100 return
     o110 endif
       (esto se ejecuta solamente si el parámetro #2 no es mayor que 5)
       (DEBUG, parameter 2 is [#2])
   o100 endsub

**Llamadas O-**

Las llamadas *O- call* pueden tomar hasta 30 parámetros opcionales, que son pasados a la subrutina como #1, #2, ... #N.
Los parámetros desde #N+1 a #30 tienen el mismo valor que en el contexto de llamada. En el retorno desde la subrutina, los parámetros #1 a #30 
(independientemente del número de argumentos) serán restaurados a los valores que tenían antes de la llamada. Los parámetros #1 a #30 son locales de 
la subrutina. 

Debido a que *1 2 3* son interpretados como el número 123, los parámetros deben ser encerrados en corchetes. El siguiente ejemplo llama a una subrutina con
3 argumentos.

**Ejemplo de llamada O-**

::

   o100 sub
     (testear si el parámetro #2 es mayor que 5)
     o110 if [#2 GT 5]
       (retornar al inicio de subrutina si la condición se cumple)
       o100 return
     o110 endif
       (esto se ejecuta solamente si el parámetro #2 no es mayor que 5)
       (DEBUG, parameter 1 es [#1])
       (DEBUG, parameter 3 es [#3])
   o100 endsub
   
   o100 call [100] [2] [325]

Los líneas que componen a las subrutinas no pueden estar anidadas. Además sólo pueden ser llamadas luego de que son definidas. Pueden ser llamadas desde otras 
funciones y pueden ser llamarse a ellas mismas de manera recursiva si tiene sentido hacerlo. El máximo nivel de anidación es de 10.

Las subrutinas pueden cambiar los valores de los parámetros arriba de #30 y esos cambios van a ser visibles en el código que llama a a la subrutina. También las 
subrutinas pueden cambiar el valore de parámetros con nombre globales.


Programas numerados con estilo Fanuc
------------------------------------

Los programas numerados, tanto principal como subprogramas, los códigos de retorno *M98* y *M99, y sus respectivas diferencias semánticas son una alternativa
a las subrutinas *rs274ngc* descripatas más arriba, provisto para compatibilidad con Fanuc y otros controladores de máquinas.

Los programas numerados están permitidos por defecto, y pueden ser deshabilitados con la línea *DISABLE_FANUC_STYLE_SUB = 1* en la sección *[RS274NGC]* del
archivo de configuración .ini.

.. admonition:: Nota
   :class: note

   Las llamadas y definiciones de los programas numerados principales y subprogramas difiere del estándar *rs274ngc* tanto en sintáxis cómo en ejecución. Para
   reducir las posibilidades de confución, el intepretador dará error si las definiciones de un estilo están mezcladas con el otro.

**Ejemplo Simple de Subprograma Numerado**

::

   o1 (Example 1)    ; Programa principal 1, "Ejemplo 1"
   M98 P100          ; Llamada a subprograma 100
   M30               ; Fin de programa principal
   
   o100              ; Inicio de subprograma 100
     G53 G0 X0 Y0 Z0 ; Movimiento rápido a origen de máquina
   M99               ; Retorno desde subprograma 100

*o1 (Título)*

El bloque (línea) inicial del programa principal es opcional y le asigna el número 1. Algunos controladores considerar un comentario en paréntesis opcional que 
representa el título del programa *Ejemplo 1* en este ejemplo, pero no tiene un sentido especial en el interpretador *rs274ngc*.

*M98 P- <L\->*

Llamada a un subprograma. La línea *M98 P100* es análoga a la sintáxis tradicional *o100 call*, pero puede ser utilizada solo para llamar a un subprograma numerado
que se encuentre definido más adelante con *o100 ... M99*. El parámetro opcional *L-* especifica la cantidad de bucles a ejecutar.

*M30*

El programa principal debe estar terminado con *M02* o *M30* (o *M99*, ver más abajo).

*O- Inicio de definición de subprograma*

Marca el inicio de la defición de un subprograma numerado. El bloque *O100* es simialr a *o100 sub*, excepto que debe ser ubicado más adelante en el archivo que la
línea de llamada *M98 P100*.

*M99 Retorno desde subrutina numerada*

El bloque *M99* es análogo a la sintáxis *o100 endsub*, pero solo puede terminar un programa numerdao (*o100* en este ejemplo) y no puede terminar una subrutina que 
empiece con la sintáxis *o100 sub*.

La llamada a subprograma *M98* difiere de *rs274ngc* *O call* de las siguientes maneras:

   * El subprograma numerado debe estar por debajo de la llamada en el archivo del programa. El interpretador dará error si el subprograma precede a la línea de llamada.
   * Los parámetros *#1*, *#2*, *...*, *#30* son globales y accesibles en los subprogramas numerados, similarmente a los subprogramas numerados de más alto nivel en las 
     llamadas tradicionales. Las modificaciones a estos parámetros dentro de un subprograma son modificaciones globales y serán persistentes al retorno desde el subprogramas.
   * La llamada *M98* a subprograma no tiene valor de retorno.
   * El bloque de la llamada a subprograma *M98* puede contener el parámetro opcional *L-* especificando la cantidad de bucles a ejecutar. Si no se especifica el parámetro
     *L* el subprograma se ejecutará 1 vez (equivalente a *M98 L1*). Un comando *M98 L0* no ejecutarpa el subprograma.

En casos poco comunes el código *M99* puede ser utilizado para terminar el programa principal, donde indica un programa sin final. Cuando el interpretador llega al *M99* en 
el programa principal, empezará nuevamente en la primer línea del archivo. Un ejemplo de un programa sin fin puede ser un ciclo de entrada en calor; en donde se puede utilizar 
la línea */M30* para parar el ciclo en algún punto cuando el operador esté listo.

**Ejemplo Completo de Subprograma Numerado**

::

   O1                             ; Programa principal 1
     #1 = 0
     (PRINT,X MAIN BEGIN:  1=#1)
     M98 P100 L5                  ; Llamada a subprograma 100
     (PRINT,X MAIN END:  1=#1)
   M30                            ; Fin de programa principal
   
   O100                           ; Subprograma 100
     #1 = [#1 + 1]
     M98 P200 L5                  ; Llamada a subprograma 200
     (PRINT,>> O100:  #1)
   M99                            ; Retorno desde subprograma 100
   
   O200                           ; Subprograma 200
     #1 = [#1 + 0.01]
     (PRINT,>>>> O200:  #1)
   M99                            ; Retorno desde subprograma 200

En este ejemplo, el parámetro *#1* es inicializado a 0. El subprograma *O100* es llamado 5 veces, en la que cada vez que se ejecuta llama a su vez 5 veces al subprograma *O200*, completando
un total de 25 veces. 

Notar que el parámetro #1 es global. Al final del programa principal luego de las modificaciones de los subprogramas *O100* y *O200* el valor del mismo será de *5.25*.

Bucles
------

Los bucles del tipo *while* pueden ser de dos tipos, los del tipo *while/endwhile* y los del tipo *do/while*. En ambos tipos la ejecución del bucle se termina cuando se llega a la condición 
*while* es evaluada a *falso*. La diferencia entre ambos es cuándo sucede esto. En los bucles *do/while* primero se ejecutan los comandos en el cuerpo del bucle y luego se verifica la condición, en
cambio en los bucles *while/endwhile* primero se verifica la condición y luego se ejecutan los comandos en el cuerpo del bucle.

**Ejemplo de bucle Endwhile**

::

   (realizar un movimiento tipo diente de sierra)
   G0 X1 Y0 (mover a posicion inicial)
   #1 = 0 (asignar al parametro #1 el valor 0)
   F25 (configurar la velocidad de avance)
   o101 while [#1 LT 10]
     G1 X0
     G1 Y[#1/10] X1
     #1 = [#1+1] (incrementar el parámetro #1)
   o101 endwhile
   M2 (fin de program)

**Ejemplo de bucle Do While**

::

   #1 = 0 (asignar al parametro #1 el valor 0)
   o100 do
     (debug, parametro 1 = #1)
     o110 if [#1 EQ 2]
       #1 = 3 (asignar al parametro #1 el valor 3)
       (msg, #1 fue asignado con valor de 3)
       o100 continue (saltar a inicio del bucle)
     o110 endif
     (algún código acá)
     #1 = [#1 + 1] (incrementar el parámetro #1)
   o100 while [#1 LT 3]
   (msg, Loop Terminado!)
   M2

Dentro del bucle *while*, el comando *O- break* se utiliza para salir del bucle inmediatamente, y el comando *O- continue* salta a la próxima evaluación de la condición *while*. Si resulta 
en *verdadero* el bucle comienza nuevamente desde el inicio y si es *falso* la ejecución continúa fuera del bucle.


Condicionales
-------------

El condicional *if* consiste en un grupo instrucciones con el mismo número *O-* que empizan con la instrucción *if* y terminan con la instrucción *endif*. Opcionalmente se pueden utilizar
las instrucciones *elseif* o *else* entre la línea inicial *if* y la final *endif*.

Si la condición de la expresión *if* se evalúa a *verdadero* se ejecuta el grupo de comandos que sigue del *if* hasta la siguiente línea condicional.

Si la condición de la expresión *if* se evalúa a *falso* se evalúan las siguientes condiciones *elseif* en el orden que aparecen hasta que alguna de ellas sea *verdadera*. Si el condicional 
*elseif* es *verdadero* se ejecuta el grupo de comandos que siguen al *elseif* hasta la siguiente línea condicional. Si ninguno de los *if* o *elseif* se evalúa *verdadero* entonces se 
ejecutan los comandos que siguen al *else*. Cuando un condicional se evalúa a *verdadero* no se ejecutan bloques de los demás condicionales.

**Ejemplo de If y Endif**

::

   (si el parametro #31 es igual a 3 definir S2000)
   o101 if [#31 EQ 3]
     S2000
   o101 endif


**Ejemplo de If Elseif Else y Endif**

::

   (si el parametro #2 es mayor a 5 definir F100)
   o102 if [#2 GT 5]
     F100
   o102 elseif [#2 LT 2]
   (else if -en caso contrario, si- el parametro #2 es menor a 2 definir F200)
     F200
   (else -en caso contrario- el parametro #2 está entre 2 y 5 definir F150)
   o102 else
     F150
   o102 endif

Varios condicionales pueden ser evaluados por *elseif* hasta que el grupo *else* sea finalmente ejecutado si es que todos los condicionales previos son *falsos*.

Repetición
----------

El comando *repeat* ejecutará los comandos que se encuentren dentro de las líneas *repeat/endrepeat* la cantidad especificadas de veces. El ejemplo muestra cómo se puede mecanizar en una
serie de movimientos empezando en la posición actual.

**Ejemplo de Repeat**

::

   (Mecanizar en 5 diagonales)
   G91 (Modo incremental)
   o103 repeat [5]
   ... (insertar còdigo de mecanizado acá)
   G0 X1 Y1 (movimiento diagonal a la próxima posición)
   o103 endrepeat
   G90 (Modo Absoluto)

Direccionamiento Indirecto
--------------------------

El número de comando *O-* puede estar dado por un parámetro o un cálculo.

**Ejemplo de Direccionamiento Indirecto**

::

   o[#101+2] call

**Calculando los valores de los Comandos O-**

Para más información en el cálculo de los valores ver las siguientes secciones:

* :ref:`Parámetros <refParameters>`
* :ref:`Expresiones <refExpresions>`
* :ref:`Operadores Lógicos <refBinaryOps>`
* :ref:`Funciones <refFunctions>`


Llamado a Archivos
------------------

Para llamar a una subrutina que se encuentra en un archivo separado, el nombre del archivo debe ser el mismo de la subrutina que se llama y debe incluir las líneas *sub* y *endsub*.
El archivo debe estar en el directorio indicado en *PROGRAM_PREFIX* o por *SUBROUTINE_PATH* en el archivo de configuración .ini. El nombre del archivo puede incluir letras en
minúscula, números, guión o guión bajo. Un archivo de una subrutina con nombre puede contener sólo la definición de una subrutina.

**Ejemplo de Llamada a archivo con nombre**

::

   o<miarchivo> call

**Ejemplo de Llamada a archivo con número**

::

   o123 call

En el archivo llamado debe incluir las líneas *oxxx sub* y *endsub* y el archivo debe ser válido.

**Ejemplo de Archivo llamado**

::

   (nombre de archivo miarchivo.ngc)
   o<miarhivo> sub
     (algo de código acá)
   o<miarchivo> endsub
   M2

.. admonition:: Nota
   :class: note

   El nombre de archivo debe ser con minúsculas solamente por lo que el interpretador convierte <MiArchivo> en <miarchivo>. Más información sobre el directorio de búsqueda y opciones
   para el directorio se encuentran en la sección de configuración INI.


Valores de Retorno de Subrutinas
--------------------------------

Las subrutinas opcionalmente pueden retornar un valor a través de una expresión opcional en los comandos *endsub* o *return*.

**Ejemplo de Retorno de un valor desde Subrutina**

::

   o123 return [#2 *5]
   ...
   o123 endsub [3 * 4]

El valor de retorno de las subrutinas se guarda en el parámetro con nombre predeterminado *<_value>*, adicionalmente el parámetro predefinido *<_value_returned>* toma un 
valor igual a 1 para indicar que ha retornado un valor. Ambos parámetros son globales y son borrados justo antes del llamado a la próxima subrutina.

Errores
-------

Las siguientes situaciones pueden causar un mensaje de error y abortar la ejecución:

   * No se define la línea *return* o *endsub* en una subrutina
   * Se utiliza la expresión *repeat* en un lugar cualquiera
   * Se utiliza la expresión *while* en un lugar cualquiera que no refiere a un *do*
   * Se utiliza la expresión *if* en un lugar cualquiera
   * Se utiliza la expresión *else*, *elseif* o *endif* que no refiere a un *if*
   * Se utiliza la expresión *break* o *continue* que no refiere a un *while* o *do*
   * Se utiliza la expresión *endrepeat* o *endwhile* que no refiere a un *while* o *repeat*

Para hacer que estos errores no sean del tipo fatal, configure el bit *0X20* en la sección *[RS274NGC] FEATURE=* en la máscara de la opción ini.


.. _otrosCodigos:

Otros Códigos 
=============

.. _refF:

F Definir Velocidad de Avance
-----------------------------

*Fx* define la velocidad de avance programada en x unidades de longitud (pulgadas o milìmetros por minuto.

La aplicación de la velocidad de avance se explica en la sección :ref:`Velocidad de Avance <refMachineFeedRate>`, a no ser que el modo de avance inverso o avance por revoluciòn se utilicen, 
en cuyo caso la aplicación se describe en la sección :ref:`G93 G94 G95 <refG93>`.

.. _refS:

S Definir Velocidad de Husillo
------------------------------

*Sx [$n]* configura la velocidad de husillo programada en x revoluciones por minuto (RPM) con el par+ametro opcional *$* que indica el número de husillo que se configura.
Sin el parámetro *$* configura por defecto al husillo número 0.

El husillo girará a la velocidad programada al ejecutar *M3* o *M4*. Está permitido utilizar el comando cuando el husillo está en girando o está frenado. Si el interruptor de 
override de velocidad de husillo está activo y tiene un valor menor al 100% la velocidad de giro real será menor a la programada.
Está permitido programar *S0*, en ese caso el husillo no girará.

Da error si:

   *S* es un número negativo.

.. _refT:

T Selección de Herramienta
--------------------------

*Tx* prepara el cambio a la herramienta x.

El cambio de herramienta no se lleva a cabo hasta que se ejecuta el comando *M6*. El valor de *T* puede aparecer en la misma línea que *M6* o en una línea previa.
Está permitido que el comando *T* aparezca más de una vez sin ejecutar el cambio de herramienta. Sólo la última herramienta seleccionada tendrá efecto el ejecutar el 
cambo de herramienta.

.. admonition:: Nota
   :class: note

   Cuando el controlador se configura con una cambiador de herramientas no aleatorio (ver *RANDOM_TOOLCHANGER* en la :ref:`sección EMCIO <sectionEMCIO>`), *T0* 
   tiene un efecto especial: ninguna herramienta se selecciona. Esto es útil si se quiere que el husillo quede vacío luego de un cambio de herramienta.

.. admonition:: Nota
   :class: note

   Cuando el controlador se configura con una cambiador de herramientas aleatorio (ver *RANDOM_TOOLCHANGER* en la :ref:`sección EMCIO <sectionEMCIO>`), *T0* 
   no tiene un efecto especial: T0 es válido como cualquier otra herramienta. Es usual utilizar T0 cuando hay cambiador aleatorio para un portaherramienta vacío,
   de esta forma se comporta como en el caso de cambiador no aleatorio y utilizarlo para descargar el husillo.

Da error si:

   * Se utiliza un número negativo de T.
   * El número de T que se define no aparece en el archivo de tabla de herramientas (con la exepción de T0 que se acepta en cambiadores de herramientas no aleatorios)

En algunas máquinas, el carrusel se moverá al leer el comando *T*, al mismo tiempo que la máquina mecaniza. En estas máquinas es común programar el comando *T* varias líneas 
antes del cambio de herramientas. Es común programar el comando *T* de la próxima herramienta a utilizar en la línea siguiente al cambio de herramientas. Esto maximiza 
el tiempo disponible para el movimiento del carrusel.

Los movimientos rápidos luego de un comando *T* no se muestran en el previsualizador AXIS hasta que se produce un movimiento a velocidad de avance. Para contrarrestar este
efecto programe por ejemplo un *G1* sin movimiento luego de los comandos *T*.


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



