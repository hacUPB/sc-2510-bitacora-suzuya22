## Que son los vertices?

los vertices son puntos en el espacio 3D que estan determinados por coordenadas y definen la forma de los objetos graficos, cada uno de estos vertices poseen atributos como posicion,
color y coordenadas de textura

## Con que figura geometrica se dibuja en 3D?
La figura geometrica con la que se dibuja en 3D es el triangulo, esto debido a que es la figura geometrica mas basica con la cual se puede definir una superficie en el espacio tridimensional

## Que es un shader?
Un shader es un programa que se ejecuta en la GPU, este programa esta encargado de administrar como se procesan los vertices y los fragmentos (pixeles) durante el renderizado, se usa el lenguaje GLSL para escribirlo

## Como se llaman los grupos de pixeles de un solo triangulo?
a estos grupos de pixeles se les llama "fragmentos", cada fragmento representa una contribucion a un pixel en la pantalla y contiene informacion como el color y la profundidad (controlado por el Depht), estos fragmentos se generan en el momento de la renderizacion

## Que es el fragment shader?
Es un tipo de shader que se ejecuta para cada fragmento y esta encargado de determinar el color final de cada pixel en pantalla, aplicando los efectos de iluminacion, texturizado y la transparencia

## Que es el vertex shader?
Es un tipo de shader que se ejecuta para cada vertices y se encarga de guardar la informacion de posicion final del vertice, tambien puede generar otros valores como colores o coordenadas de textura

## ¿Al proceso de determinar qué píxeles del display va a cubrir cada triángulo de una mesh se le llama?
Este proceso se llama "rasterización". Durante la rasterización, se determinan los fragmentos que corresponden a cada triángulo y se interpolan los valores necesarios para cada fragmento.


## ¿Qué es el render pipeline?
El render pipeline es la secuencia de pasos que sigue la GPU para convertir los datos de una escena 3D en una imagen 2D en la pantalla. Incluye etapas como la transformación de vértices, ensamblado de primitivas, rasterización, ejecución de shaders y operaciones finales de píxel.

## ¿Hay alguna diferencia entre aplicar un color a una superficie de una mesh o aplicar una textura?
Sí, hay una diferencia. Aplicar un color significa asignar un valor de color uniforme o por vértice a la superficie. Aplicar una textura implica mapear una imagen sobre la superficie, lo que permite detalles más complejos y variados.

## ¿Cuál es la diferencia entre una textura y un material?
Una textura es una imagen que se aplica a la superficie de un objeto para darle detalle visual. Un material es una colección de propiedades que define cómo la superficie de un objeto interactúa con la luz, incluyendo texturas, colores, reflectividad y otros parámetros.

## ¿Qué transformaciones se requieren para mover un vértice del 3D world al View Screen?
Se requieren varias transformaciones:

Transformación del modelo: posiciona el objeto en el mundo.

Transformación de vista: posiciona y orienta la cámara.
sistemascomputacionales.readthedocs.io

Transformación de proyección: convierte las coordenadas 3D en coordenadas 2D de pantalla.

Estas transformaciones se combinan en una matriz que se aplica a cada vértice en el vertex shader.

## ¿Al proceso de convertir los triángulos en fragmentos se le llama?
Este proceso también se llama "rasterización". Es la etapa en la que se determinan los fragmentos que corresponden a cada triángulo para su posterior procesamiento en el fragment shader.

## ¿Qué es el framebuffer?
El framebuffer es una memoria en la GPU que almacena la imagen final que se mostrará en la pantalla. Contiene información de color, profundidad y otros datos necesarios para componer la imagen final.

## ¿Para qué se usa el Z-buffer o depth buffer en el render pipeline?
El Z-buffer, o depth buffer, se utiliza para almacenar la información de profundidad de cada píxel. Permite determinar qué objetos están delante de otros y asegurar que los objetos más cercanos a la cámara oculten a los que están detrás.

#Actividad #2

Comienza realizando la lectura de la introducción del tutorial [Introducing Shaders](https://openframeworks.cc/ofBook/chapters/shaders.html). Realiza la sección Your First Shader, pero antes de ejecutar el código, realiza un pequeño experimento. Modifica ligeramente el método draw:

```cpp
void ofApp::draw(){
    ofSetColor(255);

    //shader.begin();

    ofDrawRectangle(0, 0, ofGetWidth(), ofGetHeight());

    //shader.end();
}
```

Observa la salida.

### salida
Con esta salida solo aparece un rectangulo blanco debido al setcolor(255), esto debido a que al comentar el shader begin y el shader end no estas accediendo directamente a ellos, solo estas dibujando un cuadrado blanco

"ofDrawRectangle(0, 0, ofGetWidth(), ofGetHeight());"

## ¿Qué resultados obtuviste?
Resultado esperado: El rectángulo muestra un degradado de color. El color varía dependiendo de la posición en pantalla (más rojo a la derecha, más verde hacia arriba).
En la práctica: Al principio no se veía correctamente, pero después de ubicar bien los archivos shader.vert y shader.frag en la carpeta bin/data/shadersGL3/, funcionó.

## ¿Cómo funciona?
El shader se aplica a los fragmentos (pixeles) que forman el rectángulo. Se calcula el color en tiempo real en el fragment shader, usando las coordenadas de cada fragmento.

## ¿Estás usando un vertex shader?
Sí. El archivo shader.vert actúa como vertex shader. Su función es transformar la posición de los vértices mediante una matriz (modelViewProjectionMatrix), algo esencial para que los objetos se muestren correctamente en la pantalla.

## ¿Estás usando un fragment shader?
Sí. El archivo shader.frag actúa como fragment shader. Es el que define el color final de cada píxel del rectángulo, utilizando las coordenadas gl_FragCoord.x y gl_FragCoord.y para calcular los valores rojo y verde.

## Analasis de los codigos de los shader

### vertex shader
``` cpp
#version 150

uniform mat4 modelViewProjectionMatrix;
in vec4 position;

void main(){
    gl_Position = modelViewProjectionMatrix * position;
}
```

este codigo lo que esta haciendo es que por medio de una matriz de transformacion esta controlando y transformando cada vertice del rectangulo que creamos, lo que hace en es transformar esos vertices en coordenadas de pantalla

 ### fragment shader

  ``` cpp
  #version 150

out vec4 outputColor;

void main()
{
    float windowWidth = 1024.0;
    float windowHeight = 768.0;

    float r = gl_FragCoord.x / windowWidth;
    float g = gl_FragCoord.y / windowHeight;
    float b = 1.0;
    float a = 1.0;
    outputColor = vec4(r, g, b, a);
}
```
el fragment shader lo que esta haciendo es que para cada fragmento (pixel) estan controlando el color que va a mostrar dependiendo de su posicion en la pantalla usando el rgb para esto

   float r = gl_FragCoord.x / windowWidth;

   con esto entendemos que el el valor r del rgb depende de la posicion horizontal del cuadro, tambien vemos que g depende del vertical y "b" tiene un valor constante de 1.0

  ## Conclusión
El experimento muestra la diferencia clara entre usar y no usar shaders. Cuando los shaders están activos, se puede personalizar completamente la forma en que se dibuja cada píxel. Este ejemplo sirve como una excelente introducción al potencial de los shaders en gráficos computacionales.

¿Quieres que te dé un ejemplo más interactivo con movimiento o textura?

## Actividad 3

siguiendo los pasos de la seccion "Adding Uniforms" hemos creado una malla que utiliza un uniform que controla el tiempo para animar la geometria de la malla creada (el efecto agua)
mueve los vertices en el shader en base a tiempo basicamente, y usando  ofSetColor() para que OpenFrameworks pase automáticamente ese color al shader como uniform vec4 globalColor.

time es un número que aumenta constantemente con cada frame.

Usando sin(time + algo), creas un movimiento ondulante que cambia en el tiempo.

Al multiplicar por displacementHeight, haces que los vértices suban y bajen como una ola.

### ¿que es un uniform?

un uniform es una variable global en el shader que no cambia por vértice o por píxel, sino por draw call.

Es una forma de enviar datos desde tu app en C++ hacia el shader.

Ejemplos comunes:

Tiempo (time)

Color global (globalColor)

Matrices (modelViewProjectionMatrix)

## ¿Cómo funciona el código de aplicación, los shaders y cómo se comunican estos?

El codigo de la aplicacion funciona con el archivo cpp controlando lo que van a hacer los shaders mediante el control de la variable uniform global que tienen estos, se comunican de esta forma con un call draw
 shader.setUniform1f("time", ofGetElapsedTimef());
 con esto desde el offApp.cpp se controla la variable del uniform para definir lo que se va a hacer en el shader, NO cambia en tiempo de ejecucion, solo se actualiza cada frame
    

 ## Actividad 4

 ### ¿Qué hace el código del ejemplo?

 El codigo del ejemplo hace que se cree la malla del ejemplo anterior el cual se controla el color entre magenta y azul mediante la posicion del mouse, solo que ahora se elimino el uniform del tiempo para la animacion de esta y se añadio un uniform de

  shader.setUniform1f("mouseRange", 150); // SET A UNIFORM

  y

   shader.setUniform2f("mousePos", mx, my);  // SET A UNIFORM


   para controlar mediante el programa la distorsion de los vertices haciendo un efecto donde esta el mouse


 ### ¿Cómo funciona el código de aplicación, los shaders y cómo se comunican?
 ### ofApp.cpp (código de aplicación)
Calcula la posición del mouse respecto al centro de la pantalla.

Usa funciones como setUniform1f, setUniform2f y setUniform4fv para enviar datos al shader:

mouseRange: un flotante que define el radio de influencia del mouse.

mousePos: un vec2 con la posición relativa del mouse.

mouseColor: un vec4 que mezcla colores según la posición del mouse.

 ### Vertex Shader
Recibe la posición de cada vértice.

Calcula la distancia desde cada vértice hasta el mouse.

Si el vértice está dentro del rango (mouseRange), lo aleja del mouse en proporción inversa a la distancia.

Esta nueva posición se multiplica por modelViewProjectionMatrix para ser renderizada.

 ### Fragment Shader
Pinta cada píxel del plano con el color que viene desde el uniforme mouseColor, calculado en C++.

🔁 Comunicación
Se realiza mediante uniforms, que permiten pasar datos desde el CPU (C++) al GPU (shader) una vez por frame.

## Modificacion

Modificación en Vertex Shader
Podemos cambiar la dirección del efecto para que los vértices se acerquen al mouse (atracción en vez de repulsión):
``` cpp
// En lugar de alejarse del mouse
pos.x -= dir.x;
pos.y -= dir.y;
```

## Modificación en Fragment Shader

Agrega una variación de color basada en la posición de fragmento:


#version 150

out vec4 outputColor;
uniform vec4 mouseColor;

void main()
{
    // Usa el color original pero haz que el rojo dependa de la coordenada y.
    outputColor = vec4(mouseColor.r * gl_FragCoord.y / 800.0, mouseColor.g, mouseColor.b, 1.0);
}

# RETO

RAE1

para la construccion de esta aplicacion lo que primero hice fue pensar que era lo que queria controlar con los shaders y la app, pense en un crear una malla como las anteriores pero dandole un efecto de rotacion y cambio de color en base a la posicion del mouse, para esto debia identificar como crear la variable de rotacion que controlaria despues en la app con los uniforms, para esto busque en internet y me ayude con ia para entender como se controlaba esta parte


  
    float angle = time * rotationSpeed * 5.0; 

  
    float x = pos.x * cos(angle) - pos.y * sin(angle);
    float y = pos.x * sin(angle) + pos.y * cos(angle);
    pos.x = x;
    pos.y = y;

    gl_Position = modelViewProjectionMatrix * pos;

lo que se esta haciendo desde el vertex es mediante el time calcular la velocidad de rotacion y haciendose una multiplicacion para que sea mas visible, luego se controla la posicion de los vertices para rotarlos en el eje Z (Esta parte fue la que mas ayuda de ia necesite, queria definir bien como era la operacion matematica para calcular esta rotacion de angulo)



Para la parte del fragment shader fue más sencillo, solo creé las variables de color rápido y lento y les asigné los valores correctos de RGB.

El color lento lo puse blanco (1.0, 1.0, 1.0) y el color rápido lo puse rojo (1.0, 0.0, 0.0). Luego usé la función mix() para mezclar esos dos colores según el valor de rotationSpeed.

Así, cuando la velocidad es baja, el color se acerca al blanco, y cuando la velocidad es alta, se acerca al rojo. Esto hace que el color de la malla cambie visualmente dependiendo de qué tan rápido esté rotando.

## codigo fuente

### .cpp

```cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
    plane.set(400, 400, 40, 40);
    plane.mapTexCoordsFromTexture(ofTexture());

    shader.load("shadersGL3/shader");
}

//--------------------------------------------------------------
void ofApp::update() { }

//--------------------------------------------------------------
void ofApp::draw() {
    shader.begin();

   
    float percentX = mouseX / float(ofGetWidth());
    percentX = ofClamp(percentX, 0.0, 1.0);

    shader.setUniform1f("rotationSpeed", percentX); 
    shader.setUniform1f("time", ofGetElapsedTimef());

    ofPushMatrix();
    ofTranslate(ofGetWidth() / 2, ofGetHeight() / 2);
    plane.drawWireframe();
    ofPopMatrix();

    shader.end();
}
```

### vertex

```cpp
#version 150

uniform mat4 modelViewProjectionMatrix;
uniform float time;
uniform float rotationSpeed;

in vec4 position;

void main(){
    vec4 pos = position;

  
    float angle = time * rotationSpeed * 5.0; 


    float x = pos.x * cos(angle) - pos.y * sin(angle);
    float y = pos.x * sin(angle) + pos.y * cos(angle);
    pos.x = x;
    pos.y = y;

    gl_Position = modelViewProjectionMatrix * pos;
}
```

### Fragment
```cpp

#version 150

out vec4 outputColor;
uniform float rotationSpeed;

void main(){
   
    vec3 slowColor = vec3(1.0);            
    vec3 fastColor = vec3(1.0, 0.0, 0.0);  
    vec3 color = mix(slowColor, fastColor, rotationSpeed);
    outputColor = vec4(color, 1.0);
}

```

### Explica y muestra cómo probaste la aplicación en ofApp.cpp:

Para probar la aplicación en ofApp.cpp, primero me aseguré de inicializar correctamente la malla con plane.set(...) y de cargar el shader con shader.load(...). Luego, dentro del método update(), calculé la velocidad de rotación (rotationSpeed) mapeando la posición horizontal del mouse a un valor entre 0.0 y 1.0 usando ofMap(). Esta variable se pasó al shader como un uniform usando shader.setUniform1f("rotationSpeed", rotationSpeed);.

Para observar el efecto, ejecuté la aplicación y moví el mouse de izquierda a derecha en la ventana. Verifiqué que la malla giraba más rápido hacia la derecha y más lento hacia la izquierda, como se esperaba.

### Explica y muestra cómo probaste el vertex shader:

En el vertex shader, probé el comportamiento manipulando directamente las posiciones de los vértices. Usé una matriz de rotación en 2D para girar los vértices en el plano XY. La velocidad de rotación dependía del valor del uniform float rotationSpeed recibido desde la aplicación. Usé funciones trigonométricas (cos y sin) para construir la matriz de rotación y aplicar la transformación a cada vértice.

Para probarlo, ejecuté la aplicación y confirmé que la malla rotaba más lentamente cuando el mouse estaba a la izquierda de la ventana, y más rápidamente cuando el mouse se movía hacia la derecha.

### Explica y muestra cómo probaste el fragment shader:

Para la parte del fragment shader fue más sencillo. Solo creé las variables de color rápido y lento y les asigné los valores correctos de RGB. El color lento lo puse blanco (1.0, 1.0, 1.0) y el color rápido lo puse rojo (1.0, 0.0, 0.0). Luego usé la función mix() para mezclar esos dos colores según el valor de rotationSpeed.

Probé este shader ejecutando la aplicación y observando los cambios de color. Al mover el mouse a la izquierda, los fragmentos de la malla se mostraban en color blanco; al moverlo a la derecha, el color cambiaba progresivamente hasta llegar al rojo, lo cual confirmó que el shader estaba funcionando correctamente.

### Explica y muestra cómo probaste toda la aplicación completa:

Finalmente, para probar toda la aplicación completa, corrí el programa en OpenFrameworks y observé que la malla reaccionaba correctamente tanto en movimiento como en color. La rotación de la malla respondía en tiempo real a la posición del mouse en el eje X, y el color de los fragmentos cambiaba de blanco a rojo según esa misma velocidad.

Verifiqué que no aparecieran errores en consola y que la respuesta visual fuera fluida y coherente con lo esperado. Esta prueba me permitió confirmar que tanto el código en ofApp.cpp como los shaders estaban funcionando en conjunto de forma correcta y sin conflictos.

### link:

https://youtu.be/QGw8kWIO6tY
