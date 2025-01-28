# ¿Qué son PC, D y A?

## PC: Program Counter (Contador de Programa)
Definición: El PC es un registro del procesador que contiene la dirección de memoria de la siguiente instrucción que se debe ejecutar.

Función:

A medida que el procesador ejecuta instrucciones, el PC se actualiza para apuntar a la siguiente instrucción.
Es esencial para mantener el flujo de ejecución secuencial de un programa.
En caso de un salto (como un bucle o función), el PC se actualiza con la dirección especificada.
Ejemplo práctico: Si el procesador está ejecutando la instrucción en la dirección 0x1000, el PC apuntará a 0x1004 (la dirección de la siguiente instrucción, suponiendo que cada instrucción ocupa 4 bytes).

## D: Datos (Data)
Definición: D hace referencia a los datos que el procesador utiliza durante la ejecución de un programa.

Función:

Estos datos pueden ser números, direcciones de memoria, cadenas de texto o cualquier información procesada por la CPU.
Los datos pueden residir en:
Memoria principal (RAM).
Registros internos del procesador.
Caché.
Contexto en instrucciones: En el ciclo de ejecución de instrucciones, el procesador extrae los datos (D) necesarios para completar una operación, como sumar dos números o mover información de un lugar a otro.

## A: Acumulador (Accumulator)
Definición: El A es un registro especial del procesador donde se almacenan temporalmente los resultados de operaciones aritméticas o lógicas.

Función:

El acumulador es usado como un lugar de paso para realizar cálculos.
Por ejemplo, si necesitas sumar dos números, uno de ellos se cargará en el acumulador, y el resultado final también se guardará allí.
Ejemplo práctico:

Cargar el valor 5 en el acumulador.
Sumar 3 al acumulador.
El acumulador ahora contiene 8.  

## Relación entre PC, D y A:
PC apunta a la instrucción que debe ejecutarse.
El procesador decodifica la instrucción y extrae D (los datos necesarios) desde la memoria o registros.
La operación se realiza en el acumulador (A), y el resultado puede ser almacenado nuevamente en memoria o usado en otra instrucción.   

  

 
    
# ¿Para qué los usa la CPU?
La CPU utiliza el PC, D y A para ejecutar programas siguiendo el Ciclo de Instrucción, que consiste en buscar, decodificar y ejecutar instrucciones. Cada uno tiene un propósito clave dentro de este proceso:

## 1. PC (Program Counter):
¿Para qué lo usa la CPU?

El PC es el "navegador" de las instrucciones.
Rol principal: La CPU lo usa para saber qué instrucción ejecutar a continuación.
Pasos específicos:
Al comienzo de un ciclo, el PC apunta a la dirección de memoria donde se encuentra la siguiente instrucción.
La CPU toma esa dirección para buscar la instrucción en la memoria.
Una vez recuperada, el PC se actualiza automáticamente para apuntar a la instrucción siguiente (a menos que ocurra un salto o interrupción).
Ejemplo práctico:

Inicia con el PC apuntando a la instrucción en 0x1000.
La CPU ejecuta esa instrucción y actualiza el PC a 0x1004 (siguiente instrucción).
## 2. D (Datos):
¿Para qué lo usa la CPU?

Rol principal: Los datos son los valores sobre los que las instrucciones trabajan.
Los datos se usan en operaciones como:
Sumar dos números.
Comparar valores.
Mover información entre registros y memoria.
Origen de los datos:

Los datos pueden estar:
En la memoria principal (RAM).
En registros internos de la CPU.
En dispositivos de entrada/salida.
Pasos específicos:

La CPU recupera los datos necesarios de la memoria o registros.
Los usa como entrada para las instrucciones ejecutadas.
Ejemplo práctico:

Si la instrucción es ADD A, 5, el procesador necesita cargar el dato 5 para sumarlo al contenido del acumulador.
## 3. A (Acumulador):
¿Para qué lo usa la CPU?

Rol principal: El acumulador es un registro especial usado para almacenar temporalmente:
Datos intermedios durante cálculos.
Resultados de operaciones.
Cómo lo utiliza la CPU:

Carga de datos: El acumulador se usa como punto de entrada/salida para realizar cálculos.
Procesamiento: Las operaciones como suma, resta, multiplicación, comparación, etc., usan el acumulador para trabajar con los datos.
Almacenar resultados: Una vez realizada una operación, el resultado queda en el acumulador, listo para ser usado por la siguiente instrucción.
Ejemplo práctico:

Si quieres sumar 5 y 10:
La CPU carga 5 en el acumulador.
Suma 10 al acumulador.
El acumulador ahora tiene el resultado 15.
Relación entre PC, D y A en el Ciclo de Instrucción:
Buscar:
El PC indica la dirección de memoria de la instrucción que la CPU debe recuperar.
Decodificar:
La instrucción recuperada indica qué operación realizar y qué datos (D) necesita.
Ejecutar:
La operación se realiza utilizando el acumulador (A) para procesar los datos.
Los resultados pueden guardarse en el acumulador o almacenarse nuevamente en la memoria.
