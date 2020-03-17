## Tres en raya (tic-tac-toe)
Juego que consiste en una cuadrícula de 3x3 en la que dos jugadores deberán de poner una ficha en cada turno. Si uno de los jugadores logra realizar una línea de 3 gana el juego, si ninguno lo consigue es empate.

Tradicionalmente la ficha de cada jugador es representada por 'X' o por 'O'.

Los jugadores no tardan en descubrir que el juego perfecto termina en empate sin importar con qué juega el primer jugador.

--------------------------------------------------------------------------------

### Características
* Juego realizado en WPF y C#
* Framework: .Net Framework 4.5

*Facilmente se puede compilar en .Net Core (para ejecutarlo en Linux).

--------------------------------------------------------------------------------

## Resumen
El proyecto consta de:
* Por un lado, la clase **`TresEnRaya.cs`** se encarga de controlar toda la lógica del juego. 
* Por otro lado, está la parte más gráfica y de lógica de eventos:
  *  Fichero XAML **`TresEnRayaWPF.xaml`**: Es la interfaz de la aplicación.
  *  Clase **`TresEnRayaWPF.xaml.cs`** es la que se encarga de conectar la lógica del juego con la interfaz gráfica mediante eventos.

--------------------------------------------------------------------------------

## `TresEnRaya.cs`

#### **Constructor**
|Firma|Descripción|
|==|==|
|TresEnRaya()|Se inicializan las autopropiedades `Tablero` y `UltimaJugadaIA`|

<br/>

#### **Propiedades**

|Firma|Descripción|
|==|==|
|`int[,] Tablero`|Obtienes un array bidimensional que representa al tablero 3x3 de la partida.|
|`int[] UltimaJugadaIA`|Obtienes un array que contiene:<br/> -Posición [0] -> fila<br/> -Posición [1] -> columna<br/>que es la posición del tablero donde la IA pone su ficha cuando se ejecuta el método público `PulsarBoton(int n, int m)`. |
|`int GanadorPartida`|Obtienes los valores:<br/> -Sin ganador*=-1 <br/> -Gana jugador1=0<br/> -Gana jugador2=1. <br/><br/> ^****O la partida ha acabado en empate o todavía no exite todavía un ganador.***^|
|`bool IsTableroCompleto`|Devuelve `true` en caso de que esté completo el tablero, es decir, que estén todas las fichas colocadas, `false` en caso contrario.|
|`bool FinPartida`|Devuelve `true` en caso de que se haya acabado la partida, `false` en caso contrario.|

<br/>

#### **Métodos**

|Firma|Descripción|
|==|==|
|`void EmpezarPartida()`||
