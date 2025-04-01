# ¿Qué es entonces un programa?

Un programa es un conjunto de instrucciones escritas en un lenguaje específico que un computador puede interpretar y ejecutar para realizar una tarea o resolver un problema. Estas instrucciones le indican al computador qué hacer, cómo hacerlo y en qué orden.

## Características principales de un programa:
Escrito en un lenguaje de programación: Puede ser de bajo nivel (cerca del hardware, como ensamblador) o de alto nivel (más cercano al lenguaje humano, como Python, Java, C++).
Almacenado como código ejecutable: Una vez compilado o interpretado, el programa se traduce a instrucciones binarias (0s y 1s) que la CPU puede procesar.
Secuencial o modular: Los programas pueden ejecutarse línea por línea o dividirse en módulos (funciones, clases) para organizar las tareas.
¿Cómo funciona un programa en un computador moderno?
Escrito por un humano:

Un desarrollador escribe el código fuente usando un lenguaje de programación.
Traducción del código:

Compilación: El código se convierte a lenguaje máquina en un archivo ejecutable (por ejemplo, .exe).
Interpretación: El código se traduce y ejecuta línea por línea, como en Python.
Cargado en memoria:

El programa se transfiere desde el almacenamiento al sistema operativo, que lo coloca en la memoria RAM para que la CPU lo procese.
Ejecución:

La CPU sigue el flujo de instrucciones del programa (fetch-decode-execute), ejecutando cálculos, moviendo datos o mostrando resultados.
Resultado:

El programa produce una salida, ya sea en pantalla, un archivo, o interactuando con otros dispositivos.  

## ¿QUE ES UN LENGUAJE ENSAMBLADOR?  

Un lenguaje ensamblador es un lenguaje de programación de bajo nivel que se utiliza para escribir programas que interactúan directamente con el hardware de un computador. Cada instrucción en ensamblador corresponde a una instrucción específica del procesador en su conjunto de instrucciones (ISA, Instruction Set Architecture).

Características del lenguaje ensamblador:
Cercano al hardware:

Está diseñado específicamente para un tipo de procesador o arquitectura (como x86, ARM, MIPS, etc.).
Las instrucciones reflejan las operaciones básicas que el procesador puede realizar, como mover datos, realizar cálculos, o controlar el flujo del programa.
Legibilidad humana relativa:

Utiliza mnemonics (abreviaturas legibles) para representar instrucciones binarias.
Por ejemplo:
MOV AX, 5 es más comprensible que 10111000 00000101.
Traducción directa al lenguaje máquina:

El ensamblador traduce las instrucciones a código binario (el lenguaje que entiende la CPU).
Control total del hardware:

Permite un control detallado del procesador, memoria y periféricos, lo que lo hace ideal para optimización o sistemas embebidos.

## ¿QUE ES EL LENGUAJE DE MAQUINA?  
El lenguaje de máquina es el lenguaje más básico que entiende y ejecuta directamente el procesador de un computador. Está compuesto exclusivamente por instrucciones representadas en formato binario (secuencias de 0s y 1s). Estas instrucciones controlan el hardware y dictan las operaciones que debe realizar la CPU, como cálculos, movimiento de datos, o control de flujo.

Características del lenguaje de máquina:
Formato binario:

Todas las instrucciones están codificadas en bits (0 y 1), ya que es el único lenguaje que entiende el hardware.
Por ejemplo: 10101000 00000101.
Específico de la arquitectura:

Cada tipo de procesador (x86, ARM, MIPS, etc.) tiene su propio conjunto de instrucciones y formato binario.
Difícil de entender para los humanos:

No es legible ni práctico para programar directamente debido a la complejidad y falta de abstracción.
Directamente ejecutable:

El procesador no necesita ninguna traducción adicional para ejecutar el código en lenguaje de máquina.
Estructura de una instrucción en lenguaje de máquina:
Una instrucción binaria suele dividirse en varias partes, dependiendo de la arquitectura. Un ejemplo típico incluye:

Opcode (Código de operación):

Especifica qué operación debe realizarse (suma, movimiento de datos, comparación, etc.).
Por ejemplo: 101010 podría significar "sumar".
Operandos:

Indican los datos sobre los que se debe realizar la operación o dónde encontrarlos (como registros, direcciones de memoria, o valores constantes).
Otros bits de control:

Pueden incluir banderas, modos de operación, o formatos especiales.
