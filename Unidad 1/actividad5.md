# EJERCICIOS ACTIVIDAD 5  

## Carga en D el valor 1978.
``` ams
@1978
D = A
```  
## Guarda en la posición 100 de la RAM el número 69.  
``` ams
@69
D = A
@100
M = D 

``` 
##  Guarda en la posición 200 de la RAM el contenido de la posición 24 de la RAM  
 ``` ams
@24
D = M
@200
M = D

```
## Lee lo que hay en la posición 100 de la RAM, resta 15 y guarda el resultado en la posición 100 de la RAM.

``` ams
@100
D = M
@15
D = D - A
@100
M = D
```
## Suma el contenido de la posición 0 de la RAM, el contenido de la posición 1 de la RAM y con la constante 69. Guarda el resultado en la posición 2 de la RAM.

``` AMS
@0
D = M
@1
D = D + M
@69
D = D + A
@2
M = D 
```
## Si el valor almacenado en D es igual a 0 salta a la posición 100 de la ROM.  
``` AMS
@100
D;JEQ
```
## Si el valor almacenado en la posición 100 de la RAM es menor a 100 salta a la posición 20 de la ROM.
``` ams
@100
D = M
@100 
D = D - A
@20
D;JLT
```
## Considera el siguiente programa:
``` ams
@var1
D = M
@var2
D = D + M
@var3
M = D
```
### ¿Qué hace este programa?

@var1   // Cargar la dirección de var1 en el registro A  
D = M   // Guardar el valor almacenado en var1 en el registro D

@var2   // Cargar la dirección de var2 en el registro A  
D = D + M   // Sumar el valor de D con el valor almacenado en var2 

@var3   // Cargar la dirección de var3 en el registro A  
M = D   // Guardar el valor de D en var3  

### En qué posición de la memoria está var1, var2 y var3? ¿Por qué en esas posiciones?

En el lenguaje ensamblador de hack las variables que defines con @var1, @var2, @var3, etc., se almacenan automáticamente a partir de la posición RAM[16]. ya que la arquitectura hack tiene reservadas las primeras 16 posiciones (contando la ram0) para un uso especial

RAM[x]	Uso  
RAM[0]	SP (Stack Pointer)  
RAM[1]	LCL (Local)  
RAM[2]	ARG (Argument)  
RAM[3]	THIS  
RAM[4]	THAT  
RAM[5-12]	Temporales (R5 a R12)  
RAM[13-15]	Registros generales (R13 a R15).  

## Considera el siguiente programa:

i = 1
sum = 0
sum = sum + i
i = i + 1  

## La traducción a lenguaje ensamblador del programa anterior es:  
// i = 1  
@i  
M=1  
// sum = 0  
@sum  
M=0  
// sum = sum + i  
@i  
D=M  
@sum  
M=D+M  
// i = i + 1  
@i  
D=M+1  
@i  
M=D  

### ¿Qué hace este programa?

// i = 1   
@i  // accede a la direccion de la ram donde se encuentra almacenada la variable i  
M=1 // asigna 1 a i   

// sum = 0  
@sum   accede a la direccion de la ram sum  
M=0 asigna 0 a sum  

// sum = sum + i  
@i  accede a la posicion en la ram de i
D=M  carga el valor que se encuentra en i en el registro D
@sum  accede a la posicion de la ram de sum
M=D+M  Suma el valor de i (almacenado en D) con sum y guarda el resultado en sum

// i = i + 1  
@i          // Accede a la dirección de i (variable en RAM)  
D = M       // Carga el valor de i en el registro D  
D = D + 1   // Incrementa i en 1 (D = i + 1)  
@i          // Accede a la dirección de i (variable en RAM)  
M = D       // Asigna el valor de D (i + 1) a i  

## ¿En qué parte de la memoria RAM está la variable i y sum? ¿Por qué en esas posiciones?

las variables se asignan a direcciones especificas de la ram y se determinan por el ensamblador, de no ser asi comienzan por la ram16 al estar las 16 anteriores reservadas.  

## Optimiza esta parte del código para que use solo dos instrucciones:  
``` AMS
// i = i + 1
@i
D=M+1
@i
M=D
```
codigo optimizado:

``` ams
@i
M = M + 1
```
## Las posiciones de memoria RAM de 0 a 15 tienen los nombres simbólico R0 a R15. Escribe un programa en lenguaje ensamblador que guarde en R1 la operación 2 * R0.

``` AMS
@R0
D = M
D = D + D
@R1
M=D
```  

## Considera el siguiente programa:  

i = 1000  
LOOP:  
if (i == 0) goto CONT  
i = i - 1  
goto LOOP  
CONT:  

### La traducción a lenguaje ensamblador del programa anterior es:

// i = 1000  
@1000  
D=A  
@i  
M=D  
(LOOP)  
// if (i == 0) goto CONT  
@i  
D=M  
@CONT  
D;JEQ  
// i = i - 1  
@i  
M=M-1  
// goto LOOP  
@LOOP  
0;JMP  
(CONT)  

### ¿Qué hace este programa?  
 
// i = 1000  
@1000      // Carga el valor 1000 en D.  
D=A        // D = 1000  
@i         // Apunta a la dirección de la variable i.  
M=D        // Guarda 1000 en i.  
 
// LOOP  
(LOOP)       
@i         // Apunta a i.  
D=M        // Carga el valor de i en D.  
@CONT      // Apunta a la etiqueta CONT.  (etiqueta utilizada como un marcador para indicar un punto en el código.)  
D;JEQ      // Si D es 0 (i == 0), salta a CONT.  
 
// i = i - 1  
@i         // Apunta a i.  
M=M-1      // Decrementa el valor de i por 1.  

// goto LOOP  
@LOOP      // Vuelve a la etiqueta LOOP.  
0;JMP      // Salta incondicionalmente a LOOP.  

// CONT  
(CONT)       

Inicialización: El programa comienza asignando a i el valor 1000.  
Ciclo (LOOP): El programa verifica si i es igual a 0. Si no lo es, decrementa i en 1 y vuelve a verificar.  
Condición de parada: El ciclo continúa hasta que i llegue a 0, momento en el cual el programa salta a la etiqueta CONT y termina.  

### ¿En qué memoria está almacenada la variable i? ¿En qué dirección de esa memoria?
Como no se especifico de forma explicita a que direccion esta asignada la variable simbolica de i, se intuye que es la r16 de la memoria RAM
### ¿En qué memoria y en qué dirección de memoria está almacenado el comentario //i = 1000?

la memoria i se intuye que esta en la r16 y la direccion de memoria almacenada en ese comentario corresponde a 1000.

### ¿Cuál es la primera instrucción del programa anterior? ¿En qué memoria y en qué dirección de memoria está almacenada esa instrucción?

la primera instruccion del programa es @1000 esta almacenada en la memoria ROM donde se asigna el valor 1000 al registro A, en el caso del programa usado las instrucciones ROM comienzan en la direccion 0 y se van asignando secuencialmente.

### ¿Qué son CONT y LOOP?
En el programa que proporcionaste, CONT y LOOP son etiquetas o marcadores que se utilizan para hacer referencia a ciertas ubicaciones dentro del código. Las etiquetas se emplean para organizar el flujo de control del programa, permitiendo usar instrucciones de salto (como JMP o JEQ) para saltar a esas ubicaciones.

LOOP: Marca el inicio de un bucle o ciclo en el programa.  
CONT: Marca el final del bucle o el punto donde el programa debe continuar después de que el ciclo termine.

### ¿Cuál es la diferencia entre los símbolos i y CONT?
i: es un tipo de variable de memoria que representa una ubicacion en la RAM donde se guarda su valor, en el contexto de este programa almacena un valor numerico

cont: Es una etiqueta que marca un punto específico dentro del código del programa, usado para el flujo de control (por ejemplo, en saltos condicionales o no condicionales).

## Implemente en ensamblador:
R4 = R1 + R2 + 69  

``` AMS
@69
D = A
@R2
D = M + D
@R1
D = M + D
@R4
M = D
```
## Implementa en ensamblador:
if R0 >= 0 then R1 = 1  
else R1 = –1

(LOOP)
goto LOOP

``` AMS
@R0
D = M
@POSITIVO
D;JGE  

Si D < 0  

@R1
M = -1
@LOOP
0;JMP

(POSITIVO) Si D >= 0
@R1
M = 1
@LOOP
0;JMP

LOOP
@LOOP
0;JMP
```
## Implementa en ensamblador:
R4 = RAM[R1]

``` AMS
    @R1
    D = M
    A = D
    D = M
    @R4
    M = D
```

## Implementa en ensamblador el siguiente problema. En la posición R0 está almacenada la dirección inicial de una región de memoria. En la posición R1 está almacenado el tamaño de la región de memoria. Almacena un -1 en esa región de memoria.

// Cargar la dirección inicial de la región de memoria en A  
@R0  
D = M      // D = Dirección inicial  
@addr
M = D      // Guardar la dirección en la etiqueta addr  

// Cargar el tamaño de la región de memoria  
@R1
D = M      // D = Tamaño de la región  
@size
M = D      // Guardar el tamaño en la etiqueta size  

(LOOP)  
// Verificar si el tamaño es 0, si es así, terminar el bucle    
@size   
D = M      // D = Tamaño    
@END
D;JEQ     // Si D == 0, saltar a END    

// Almacenar -1 en la dirección de memoria actual   
@addr   
A = M      // A = Dirección actual  
M = -1     // Almacenar -1 en la dirección de memoria   

// Incrementar la dirección en 1 (mover a la siguiente posición)    
@addr   
M = M + 1  // addr = addr + 1   

// Decrementar el tamaño restante   
@size   
M = M - 1  // size = size - 1   

// Repetir el bucle 
@LOOP   
0;JMP     // Volver al principio del bucle  

(END)   
// Fin del programa, bucle infinito para detener la ejecución   
@END    
0;JMP     // Bucle infinito 

## Implementa en lenguaje ensamblador el siguiente programa:
int[] arr = new int[10];    
int sum = 0;    
for (int j = 0; j < 10; j++) {  
    sum = sum + arr[j]; 
}   

``` AMS
@R2
M = 0
@R3
M = 0
@R1
D = M
@size
M = D
(LOOP)
@R3
D = M
@R1
D = D - M
@END
D;JGE
@R0
D = M
@R3
A = D + M
D = M
@R2
M = M + D
@R3
M = M + 1
@LOOP
0;JMP
(END)
@END
0;JMP
```
 ### ¿Qué hace este programa?
 Inicializa un arreglo arr con 10 elementos (en la memoria RAM).    
Inicializa la variable sum en 0.    
Utiliza un ciclo for para recorrer los 10 elementos del arreglo arr, sumando sus valores a la variable sum. 
Después de recorrer todo el arreglo, sum contendrá la suma total de todos los valores almacenados en el arreglo arr.
### ¿Cuál es la dirección base de arr en la memoria RAM?
La dirección base de arr sería la dirección a la que apunta el registro R0, ya que en este caso R0 almacena la dirección inicial del arreglo.
### ¿Cuál es la dirección base de sum en la memoria RAM y por qué?
Dado que no se especifica el registro o la dirección exacta de sum en el código proporcionado, se podría suponer que R2 es la que se usa.
### ¿Cuál es la dirección base de j en la memoria RAM y por qué?
De nuevo, la dirección base de j dependerá de la implementación y de qué registro se le haya asignado.
## Implementa en lenguaje ensamblador:
if ( (D - 7) == 0) goto a la instrucción en ROM[69]
``` AMS
D = M
D = D - 7
@69
D;JEQ
```
## Analiza el siguiente programa en lenguaje de máquina:
0100000000000000
1110110000010000
0000000000010000
1110001100001000
0110000000000000
1111110000010000
0000000000010011
1110001100000101
0000000000010000
1111110000010000
0100000000000000
1110010011010000
0000000000000100
1110001100000110
0000000000010000
1111110010101000
1110101010001000
0000000000000100
1110101010000111
0000000000010000
1111110000010000
0110000000000000
1110010011010000
0000000000000100
1110001100000011
0000000000010000
1111110000100000
1110111010001000
0000000000010000
1111110111001000
0000000000000100
1110101010000111

### ¿Qué hace este programa?
Línea 1: 0100000000000000
Esta es una A-instrucción que contiene la dirección 0 (A = 0).solo carga la dirección en el registro A. 

Línea 2: 1110110000010000
Es una C-instrucción 

111 indica que es una instrucción de tipo C.
011000 es la operación a realizar, que representa "D = D + A".
001 indica el destino D.
000 indica que no hay salto.
Esta instrucción realiza una suma entre D y A, y almacena el resultado en D.

Línea 3: 0000000000010000
Es una A-instrucción que carga la dirección 32 en el registro A (A = 32).

Línea 4: 1110001100001000
Es una C-instrucción. Desglosándola:

111 indica que es una instrucción de tipo C.
000110 representa la operación "D = D - A".
001 es el destino D.
000 no hay salto.
Esta instrucción realiza una resta entre D y A, y almacena el resultado en D.

Línea 5: 0110000000000000
Es una A-instrucción que carga la dirección 0 en A (A = 0).

Línea 6: 1111110000010000
Es una C-instrucción. Desglosando:

111 indica que es de tipo C.
111000 realiza la operación "D = -1".
001 indica el destino D.
000 no hay salto.
Esta instrucción asigna -1 al registro D.

Línea 7: 0000000000010011
Es una A-instrucción que carga la dirección 35 en A (A = 35).

Línea 8: 1110001100000101
Es una C-instrucción. Desglosando:

111 indica que es de tipo C.
000110 representa la operación "D = D - A".
001 es el destino D.
000 no hay salto.
Esta instrucción realiza una resta entre D y A, y almacena el resultado en D.

Línea 9: 0000000000010000
Es una A-instrucción que carga la dirección 32 en A (A = 32).

Línea 10: 1111110000010000
Es una C-instrucción igual a la anterior en la línea 6, que asigna -1 a D.

## Implementa un programa en lenguaje ensamblador que dibuje el bitmap que diseñaste en la pantalla solo si se presiona la tecla “d”.

``` AMS

@KBD          // Dirección de memoria del teclado
D=M           // Cargar el valor de KBD en D
@checkD       // Etiqueta para verificar si "d" está presionado
D;JEQ         // Si D es 0 (no presionado), saltar a la etiqueta checkD


@16384        // Dirección base para dibujar en la pantalla
D=A           // Asignar la dirección base en D
@memAddress   // Guardar la dirección base en memAddress
M=D           // memAddress = 16384



@memAddress
D=M
@252
M=D
@memAddress+32
D=M
@252
M=D
@memAddress+64
D=M
@252
M=D
@memAddress+96
D=M
@252
M=D
@memAddress+128
D=M
@252
M=D
@memAddress+160
D=M
@252
M=D
@memAddress+192
D=M
@252
M=D
@memAddress+352
D=M
@-8192
M=D
@memAddress+384
D=M
@15360
M=D
@memAddress+416
D=M
@896
M=D
@memAddress+448
D=M
@252
M=D
@memAddress+480
D=M
@7
M=D
@memAddress+512
D=M
@31
M=D
@memAddress+544
D=M
@992
M=D
@memAddress+576
D=M
@-1024
M=D
@memAddress+608
D=M
@32767
M=D


@memAddress+1
D=M
@126
M=D
@memAddress+33
D=M
@126
M=D
@memAddress+65
D=M
@126
M=D
@memAddress+97
D=M
@126
M=D
@memAddress+129
D=M
@126
M=D
@memAddress+161
D=M
@126
M=D
@memAddress+193
D=M
@126
M=D
@memAddress+257
D=M
@96
M=D
@memAddress+289
D=M
@48
M=D
@memAddress+321
D=M
@15
M=D
@memAddress+609
D=M
@3
M=D
@memAddress+641
D=M
@14
M=D
@memAddress+673
D=M
@56
M=D
@memAddress+705
D=M
@480
M=D

@END       
0;JMP

// 
(checkD)
@END
0;JMP
```



