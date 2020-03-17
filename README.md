## Tres en raya (tic-tac-toe)
Juego que consiste en una cuadr�cula de 3x3 en la que dos jugadores deber�n de poner una ficha en cada turno. Si uno de los jugadores logra realizar una l�nea de 3 gana el juego, si ninguno lo consigue es empate.

Tradicionalmente la ficha de cada jugador es representada por 'X' o por 'O'.

Los jugadores no tardan en descubrir que el juego perfecto termina en empate sin importar con qu� juega el primer jugador.

--------------------------------------------------------------------------------

<br/>

### Caracter�sticas
* Juego realizado en WPF y C#
* Framework: .Net Framework 4.5

*Facilmente se puede compilar en .Net Core (para ejecutarlo en Linux).

--------------------------------------------------------------------------------

<br/>

## Resumen
El proyecto consta de:
* Por un lado, la clase **`TresEnRaya.cs`** se encarga de controlar toda la l�gica del juego. 
* Por otro lado, est� la parte gr�fica y la parte de l�gica de eventos:
  *  Fichero XAML **`TresEnRayaWPF.xaml`**: Es la interfaz de la aplicaci�n.
  *  Clase **`TresEnRayaWPF.xaml.cs`** es la que se encarga de conectar la l�gica del juego con la interfaz gr�fica mediante eventos.

--------------------------------------------------------------------------------

<br/>

## `TresEnRaya.cs`

#### **Constructor**
|Firma|Descripci�n|
|--|--|
|`TresEnRaya()`|Se inicializan las autopropiedades `Tablero` y `UltimaJugadaIA`|

<br/>

#### **Propiedades**

|Firma|Descripci�n|
|--|--|
|`int[,] Tablero`|Obtienes un array bidimensional que representa al tablero 3x3 de la partida.|
|`int[] UltimaJugadaIA`|Obtienes un array que contiene:<br/> -Posici�n [0] -> fila<br/> -Posici�n [1] -> columna<br/>que es la posici�n del tablero donde la IA pone su ficha cuando se ejecuta el m�todo p�blico `PulsarBoton(int n, int m)`. |
|`int GanadorPartida`|Obtienes los valores:<br/> -Sin ganador*=-1 <br/> -Gana jugador1=0<br/> -Gana jugador2=1. <br/><br/> <sup>****O la partida ha acabado en empate o todav�a no exite todav�a un ganador.***<sup/>|
|`bool IsTableroCompleto`|Devuelve `true` en caso de que est� completo el tablero, es decir, que est�n todas las fichas colocadas, `false` en caso contrario.|
|`bool FinPartida`|Devuelve `true` en caso de que se haya acabado la partida, `false` en caso contrario.|

<br/>

#### **M�todos p�blicos**

|Firma|Descripci�n|
|--|--|
|`void PulsarBoton(int n, int m)`|M�todo que permite pulsar un bot�n para partidas contra la IA.|
|`void PulsarBoton(int n, int m, bool jugador)`|M�todo que permite pulsar un bot�n para partidas sin IA, es decir, contra otra persona (en local).|

<br/>

#### **M�todos privados**

|Firma|Descripci�n|
|--|--|
|`void PonerFichaOrdenador()`|M�todo que comienza el algoritmo Minimax, se encarga de recoger la posici�n d�nde coloca la ficha la IA.|
|`int Max()`|Esta funci�n se encarga de maximizar el beneficio de la maquina ante el jugador. Se queda con la partida que m�s beneficio le aporte a la m�quina.|
|`int Min()`|Esta funci�n se encarga de minimizar el beneficio del jugador ante la m�quina. Se queda con la partida que menos beneficio le aporte al jugador.|

<br/>

-----------------------------------------------------------------------------------

<br/>

## Algoritmo Minimax
En teor�a de juegos, minimax es un m�todo de decisi�n para minimizar la p�rdida m�xima esperada en juegos con adversario y con informaci�n perfecta. Minimax es un algoritmo recursivo.

El funcionamiento de minimax puede resumirse en c�mo elegir el mejor movimiento para ti mismo suponiendo que tu contrincante escoger� el peor para ti. <br/><sup>Fuente: ([Wikipedia](https://es.wikipedia.org/wiki/Minimax))<sup/>*

![Imagen funcionamiento juego vida](https://raw.githubusercontent.com/construk/TresEnRayaMinimaxWPF/master/Minimax3enraya.png)

<br/>

#### **Comprobaci�n recursiva:** 
##### **Max:** 
La IA comenzar� su movimiento desde el m�todo `Max()` donde:
1. Comprobar� si es el fin del c�lculo recursivo. Si lo es, devuelve el valor que le corresponde.
2. Si no lo es, realizar� la comprobaci�n recursiva donde deber� de ir comprobando todas las posibilidades posibles y quedarse con la opci�n m�s optima.
   * Recorrer todas las casillas.
   * Si la casilla est� libre, simular que se coloca la ficha en ella, realizar llamada al m�todo `Min()` y luego de recibir el valor del m�todo `Min()` volver a quitar la casilla que se ha simulado.
   * El valor que se obtiene de `Min()` se almacena, y si es mayor que en la jugada anterior (como jugada m�s beneficiosa) tambi�n se almacena en `UltimaJugadaIA` la posici�n en el tablero donde coloca la ficha la IA.

##### **Min:** 
Es llamado desde `Max`, y realiza lo mismo que `Max` pero en un sentido contrario, es decir, mientras que en Max se almacena el valor de la jugada anterior si es mayor, en `Min`se comprueba que el valor de la jugada es menor, y si es as� se almacena.
Tambi�n en este m�todo se coloca la ficha del jugador como "simulaci�n" que luego se quita.

##### **Posici�n de decisi�n**
* `Max` representa la posici�n de decisi�n de la IA.
* `Min` representa la posici�n de decisi�n del jugador.

##### **Objetivo**
* En `Max` se pretende obtener la elecci�n que m�s beneficie a la IA.
* En `Min` se pretende obtener la elecci�n que menos perjudique a la IA.