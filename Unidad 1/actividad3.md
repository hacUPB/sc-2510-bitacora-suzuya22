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
