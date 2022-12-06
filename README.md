# Visualizador de audio Interactivo

El presente proyecto desarrollado con ayuda de three.js tiene como objetivo poder visualizar la diferencia entre las frecuencias de audio de distintas canciones a través del análisis de audio y la manipulación de atributos como geometría, luces, sombras y colores, temas vistos en la materia de Computación Visual Interactiva. 
![Screenshot_19](https://user-images.githubusercontent.com/111076222/205846240-0e0f8023-7009-434c-b907-dc54ff2dcc1b.png)

Una demostración del proyecto puede ser encontrada en el siguiente enlace: [Visualizador de Audio - CVI](https://emmanuelbmanzo.github.io/threejs-audio/)

---

## Desarrollo
Para el desarrollo de este proyecto se tomó como inspiración las capacidades que el AudioAnalyser() de three.js proporciona, pues gracias a este objeto es posible manipular visualmente los valores de un audio, y asignar los parámetros de estas frecuencias a objetos tridimensionales. 


### Escena
Para lograr un mayor enfoque en las partes importantes de la aplicación se optó por tener una escena simple con un suelo plano en donde los únicos elementos que destaquen sean precisamente las representaciones visuales de las canciones, por lo que se comienzan inicializando los objetos renderer y scene de three.js para posteriormente agregar una geometría de plano para el suelo. Para agregarle complejidad y mejor visualización al mapa, también se agregó una luz ambiental, una luz focal y propiedades reflectantes al suelo. 


### Interactividad con controles
Para poder hacer el proyecto interactivo y hacer que el usuario se sienta como en un videojuego se utilizó el elemento PointerLockControls, que permite controlar los eventos del teclado y mouse para actualizar la posición de la cámara. Los controles que se establecieron fueron:
- Teclas WASD para moverse dentro de la escena
- Tecla Espacio para saltar
- Movimiento del mouse para mover la cámara del jugador

Así pues, con esto se puso en práctica el tema de manejo de cámara y eventos visto en el curso.


### Objetos
Para la visualización del audio se eligió representar cada canción con un "aura" hecha a partir de esferas 3D, que a su vez por su posicionamiento dan un aspecto de cúpula. Dentro de cada cúpula se pusieron los elementos que darían vida a la canción correspondiente y el usuario al entrar a cada cúpula puede comenzar a escuchar el audio.
Para representar los cambios en las frecuencias de audio se crearon figuras con geometría de caja posicionadas una al lado de la otra, lo que facilita la visualización secuencial de cada onda. A cada una de estas cajas se le modificaría la posición y color conforme el analizador de audio cambie de valores, lo que permite visualizar claramente la diferencia entre ambas canciones.


![Screenshot_21](https://user-images.githubusercontent.com/111076222/205846401-561d3b16-fb1b-4c5e-bfcb-4193b69c662e.png)


### AudioAnalyser
El componente principal del proyecto que permite "escuchar" en tiempo real un archivo de audio y tenerlo disponible en forma de un arreglo de 256 posiciones, cada una representando un nodo de frecuencia de audio.

![Screenshot_20](https://user-images.githubusercontent.com/111076222/205846436-7d3ab544-d8f3-4489-b2b8-aa3e237c3ef7.png)

Una vez que se carga y reproduce el audio con la función loadAudio(), es posible obtener los valores del analyser por cada frame de la función render. Así pues, estas frecuencias que son valores de 0 a 256 se convierten a una representación decimal del rango 0-1 con los que sea sencillo manipular los objetos de la escena. El fragmento de código a continuación es un ejemplo de la manera en que se utilizaron los valores del analyser.

```
if(isSong1Active){
   analyser1.getFrequencyData();
     for(let i=0; i<64; i++){
        objectsS1[i].position.y = Math.floor( (analyser1.data[i]/64) * 5 );
        ...
      }
}
```

## Código fuente
Un enlace al código fuente desarrollado puede ser encontrado aquí
