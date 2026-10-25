# Dijkstra Maze

Juego de laberintos en Python donde una tortuga tiene que volver a su nido. Cada casilla tiene un costo de movimiento distinto y la energía es limitada, así que no basta con llegar: hay que encontrar un camino barato. El algoritmo de Dijkstra está implementado desde cero y se usa en tres partes del juego.

## Dónde se usa Dijkstra

- **Balance de niveles**: al generar cada nivel se calcula el costo del camino óptimo y la energía disponible es ese costo × 1.8. Así cada nivel es posible pero no regalado.
- **Pistas**: con `H` se dibuja el camino de menor costo desde la posición actual hasta el nido. Hay 3 pistas por partida.
- **Enemigos**: los cangrejos recalculan el camino más corto hacia la tortuga cada vez que se mueven.

La implementación (`dijkstra.py`) usa una cola de prioridad con `heapq` y sigue el pseudocódigo clásico: distancias en infinito, extracción del nodo de menor distancia y relajación de aristas. Para comprobar que un mapa generado tiene solución se usa BFS, que es más barato porque ahí no importan los costos.

## Reglas

- Las casillas tienen costo 1 a 4 (más oscuras = más caras) o son muro.
- Cada paso descuenta el costo de la casilla. Si la energía llega a 0, se pierde una vida.
- Hay 3 vidas por partida.
- Si un cangrejo alcanza a la tortuga, se pierde una vida. Si es la tortuga la que se mueve sobre el cangrejo, lo elimina, recupera 20 de energía, gana velocidad y suma 50 puntos.
- Pasar un nivel da 100 × número de nivel.

Son 10 niveles. Los mapas se generan con semillas fijas, así que cada nivel es siempre el mismo, y crecen en tamaño, densidad de muros y número de enemigos.

El mejor puntaje y las últimas 10 partidas se guardan en `progreso.json`.

## Controles

| Tecla | Acción |
|---|---|
| Flechas | Mover |
| `H` en el menú | Ver el historial de partidas |
| `H` jugando | Mostrar u ocultar la pista |
| `Enter` | Empezar partida / volver al menú |
| `Espacio` | Empezar el nivel después de la historia |

## Cómo jugar

Requisitos: Python 3.10+.

```bash
pip install -r requirements.txt
python main.py
```

## Estructura

```
main.py       bucle del juego, estados (menú, historial, historia, jugando, victoria, derrota) y HUD
dijkstra.py   Dijkstra y reconstrucción del camino
niveles.py    generación de mapas por semilla y cálculo de la energía de cada nivel
grid.py       celdas, costos y dibujo del tablero
avatar.py     movimiento y energía de la tortuga
enemigo.py    persecución de los cangrejos
progreso.py   lectura y escritura del progreso
```

## Autor

**Juan Diego Negrete Portillo**
Estudiante de Ingeniería de Sistemas — Universidad de Córdoba
[Portafolio](https://juanchiz1.github.io/Portafolio-Juan_Diego_Negrete/) · [LinkedIn](https://www.linkedin.com/in/juan-diego-negrete-portillo-352111195/) · [GitHub](https://github.com/Juanchiz1)
