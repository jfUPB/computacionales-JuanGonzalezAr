## Desifrando el hack:
1. ¿En qué direcciones de memoria se implementan las variables i, sum?
- La i se implementa en la 16 y la sum en la 17
2. Basado en esta experiencia, ¿Cuál es la diferencia entre la dirección de una variable y su contenido?
- La dirección de una variable es la ubicación en memoria donde se almacena la variable, por ejemplo i, i no es su valor, sino la dirección en memoria donde está almacenado su contenido.
- El contenido de una variable es el valor almacenado en la dirección de memoria de la variable se accede con M que indica el contenido de la celda de memoria referenciada por A o i en este caso
3. Explica cómo se implementa la condición i <= 100:
- la condición i ≤ 100 se implementa verificando si i - 100 es mayor que 0 (i > 100). Si es así, el programa sale del bucle.
