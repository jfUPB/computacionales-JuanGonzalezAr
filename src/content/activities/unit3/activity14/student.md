## Solucion:


En esta unidad aprendí cómo funciona la memoria cuando programamos en C++. Aprendí que cuando creo un objeto normal, se guarda en el stack y se borra solo al terminar la función. Pero si uso `new`, el objeto se guarda en el heap y yo mismo debo borrarlo con `delete`. También entendí que si paso un objeto por valor a una función, se hace una copia y el original no cambia. En cambio, si lo paso por referencia, sí se puede modificar el original. Esto lo vi en un ejemplo donde cambié el nombre de un objeto.

Lo que más me costó fue entender la diferencia entre punteros y referencias, y también saber en qué parte de la memoria está cada cosa. A veces me confundía con si estaba trabajando con la copia o con el objeto original.

Para entender mejor estos temas, probé varios códigos y les puse mensajes con `cout` para ver qué pasaba. También usé el debugger del programa para mirar las direcciones de memoria. Dibujar esquemas de memoria también me ayudó a imaginar mejor dónde estaban los datos.

Lo que más me sirvió fue hacer pruebas pequeñas y cambiar el código poco a poco. Así veía claramente los resultados. También me ayudó mucho anotar mis dudas para resolverlas después.

En las próximas unidades quiero entender mejor los punteros, así que voy a practicar con ejercicios simples cada vez que vea un tema nuevo. También voy a revisar mis errores pasados antes de empezar y seguir usando el debugger para ver bien cómo se comporta el programa. Además, voy a escribir lo que entienda en palabras sencillas para no olvidarlo.
