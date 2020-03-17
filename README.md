## Tres en raya (tic-tac-toe)
Juego que consiste en una cuadrícula de 3x3 en la que dos jugadores deberán de poner una ficha en cada turno. Si uno de los jugadores logra realizar una línea de 3 gana el juego, si ninguno lo consigue es empate.

Tradicionalmente la ficha de cada jugador es representada por 'X' o por 'O'.

Los jugadores no tardan en descubrir que el juego perfecto termina en empate sin importar con qué juega el primer jugador.

--------------------------------------------------------------------------------

<br/>

### Características
* Juego realizado en WPF y C#
* Framework: .Net Framework 4.5

*Facilmente se puede compilar en .Net Core (para ejecutarlo en Linux).

--------------------------------------------------------------------------------

<br/>

## Resumen
El proyecto consta de:
* Por un lado, la clase **`TresEnRaya.cs`** se encarga de controlar toda la lógica del juego. 
* Por otro lado, está la parte gráfica y la parte de lógica de eventos:
  *  Fichero XAML **`TresEnRayaWPF.xaml`**: Es la interfaz de la aplicación.
  *  Clase **`TresEnRayaWPF.xaml.cs`** es la que se encarga de conectar la lógica del juego con la interfaz gráfica mediante eventos.

--------------------------------------------------------------------------------

<br/>

## `TresEnRaya.cs`

#### **Constructor**
|Firma|Descripción|
|--|--|
|`TresEnRaya()`|Se inicializan las autopropiedades `Tablero` y `UltimaJugadaIA`|

<br/>

#### **Propiedades**

|Firma|Descripción|
|--|--|
|`int[,] Tablero`|Obtienes un array bidimensional que representa al tablero 3x3 de la partida.|
|`int[] UltimaJugadaIA`|Obtienes un array que contiene:<br/> -Posición [0] -> fila<br/> -Posición [1] -> columna<br/>que es la posición del tablero donde la IA pone su ficha cuando se ejecuta el método público `PulsarBoton(int n, int m)`. |
|`int GanadorPartida`|Obtienes los valores:<br/> -Sin ganador*=-1 <br/> -Gana jugador1=0<br/> -Gana jugador2=1. <br/><br/> <sup>****O la partida ha acabado en empate o todavía no exite todavía un ganador.***<sup/>|
|`bool IsTableroCompleto`|Devuelve `true` en caso de que esté completo el tablero, es decir, que estén todas las fichas colocadas, `false` en caso contrario.|
|`bool FinPartida`|Devuelve `true` en caso de que se haya acabado la partida, `false` en caso contrario.|

<br/>

#### **Métodos públicos**

|Firma|Descripción|
|--|--|
|`void PulsarBoton(int n, int m)`|Método que permite pulsar un botón para partidas contra la IA.|
|`void PulsarBoton(int n, int m, bool jugador)`|Método que permite pulsar un botón para partidas sin IA, es decir, contra otra persona (en local).|

<br/>

#### **Métodos privados**

|Firma|Descripción|
|--|--|
|`void PonerFichaOrdenador()`|Método que comienza el algoritmo Minimax, se encarga de recoger la posición dónde coloca la ficha la IA.|
|`int Max()`|Esta función se encarga de maximizar el beneficio de la maquina ante el jugador. Se queda con la partida que más beneficio le aporte a la máquina.|
|`int Min()`|Esta función se encarga de minimizar el beneficio del jugador ante la máquina. Se queda con la partida que menos beneficio le aporte al jugador.|

<br/>

-----------------------------------------------------------------------------------

<br/>

## Algoritmo Minimax
En teoría de juegos, minimax es un método de decisión para minimizar la pérdida máxima esperada en juegos con adversario y con información perfecta. Minimax es un algoritmo recursivo.

El funcionamiento de minimax puede resumirse en cómo elegir el mejor movimiento para ti mismo suponiendo que tu contrincante escogerá el peor para ti. <br/><sup>Fuente: ([Wikipedia](https://es.wikipedia.org/wiki/Minimax))<sup/>*

![Imagen funcionamiento juego vida](https://raw.githubusercontent.com/construk/TresEnRayaMinimaxWPF/master/Minimax3enraya.png)

<br/>

#### **Comprobación recursiva:** 
##### **Max:** 
La IA comenzará su movimiento desde el método `Max()` donde:
1. Comprobará si es el fin del cálculo recursivo. Si lo es, devuelve el valor que le corresponde.
2. Si no lo es, realizará la comprobación recursiva donde deberá de ir comprobando todas las posibilidades posibles y quedarse con la opción más optima.
   * Recorrer todas las casillas.
   * Si la casilla está libre, simular que se coloca la ficha en ella, realizar llamada al método `Min()` y luego de recibir el valor del método `Min()` volver a quitar la casilla que se ha simulado.
   * El valor que se obtiene de `Min()` se almacena, y si es mayor que en la jugada anterior (como jugada más beneficiosa) también se almacena en `UltimaJugadaIA` la posición en el tablero donde coloca la ficha la IA.

##### **Min:** 
Es llamado desde `Max`, y realiza lo mismo que `Max` pero en un sentido contrario, es decir, mientras que en Max se almacena el valor de la jugada anterior si es mayor, en `Min`se comprueba que el valor de la jugada es menor, y si es así se almacena.
También en este método se coloca la ficha del jugador como "simulación" que luego se quita.

##### **Posición de decisión**
* `Max` representa la posición de decisión de la IA.
* `Min` representa la posición de decisión del jugador.

##### **Objetivo**
* En `Max` se pretende obtener la elección que más beneficie a la IA.
* En `Min` se pretende obtener la elección que menos perjudique a la IA.