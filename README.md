## Tres en raya (tic-tac-toe)
Juego que consiste en una cuadr�cula de 3x3 en la que dos jugadores deber�n de poner una ficha en cada turno. Si uno de los jugadores logra realizar una l�nea de 3 gana el juego, si ninguno lo consigue es empate.

Tradicionalmente la ficha de cada jugador es representada por 'X' o por 'O'.

Los jugadores no tardan en descubrir que el juego perfecto termina en empate sin importar con qu� juega el primer jugador.

--------------------------------------------------------------------------------

### Caracter�sticas
* Juego realizado en WPF y C#
* Framework: .Net Framework 4.5

*Facilmente se puede compilar en .Net Core (para ejecutarlo en Linux).

--------------------------------------------------------------------------------

## Resumen
El proyecto consta de:
* Por un lado, la clase **`TresEnRaya.cs`** se encarga de controlar toda la l�gica del juego. 
* Por otro lado, est� la parte m�s gr�fica y de l�gica de eventos:
  *  Fichero XAML **`TresEnRayaWPF.xaml`**: Es la interfaz de la aplicaci�n.
  *  Clase **`TresEnRayaWPF.xaml.cs`** es la que se encarga de conectar la l�gica del juego con la interfaz gr�fica mediante eventos.

--------------------------------------------------------------------------------

## `TresEnRaya.cs`

#### **Constructor**
|Firma|Descripci�n|
|==|==|
|TresEnRaya()|Se inicializan las autopropiedades `Tablero` y `UltimaJugadaIA`|

<br/>

#### **Propiedades**

|Firma|Descripci�n|
|==|==|
|`int[,] Tablero`|Obtienes un array bidimensional que representa al tablero 3x3 de la partida.|
|`int[] UltimaJugadaIA`|Obtienes un array que contiene:<br/> -Posici�n [0] -> fila<br/> -Posici�n [1] -> columna<br/>que es la posici�n del tablero donde la IA pone su ficha cuando se ejecuta el m�todo p�blico `PulsarBoton(int n, int m)`. |
|`int GanadorPartida`|Obtienes los valores:<br/> -Sin ganador*=-1 <br/> -Gana jugador1=0<br/> -Gana jugador2=1. <br/><br/> ^****O la partida ha acabado en empate o todav�a no exite todav�a un ganador.***^|
|`bool IsTableroCompleto`|Devuelve `true` en caso de que est� completo el tablero, es decir, que est�n todas las fichas colocadas, `false` en caso contrario.|
|`bool FinPartida`|Devuelve `true` en caso de que se haya acabado la partida, `false` en caso contrario.|

<br/>

#### **M�todos**

|Firma|Descripci�n|
|==|==|
|`void EmpezarPartida()`||