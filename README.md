# Retos con listas simples, dobles y circulares

## Integrantes
- Pedro García Mata
- Cristopher Gerardo Villanueva Ramirez

## Datos de la actividad
- **Asignatura:** Estructuras de Datos / Desarrollo de Software Multiplataforma
- **Institución:** Universidad Tecnológica del Norte de Guanajuato (UTNG)
- **Fecha:** Octubre 2026
- **Versión asignada:** Versión A (Biblioteca de libros)

## Conceptos aprendidos
- **Lista simple:** Estructura de datos lineal en la que cada nodo almacena un valor y un único puntero que apunta al siguiente elemento. Su recorrido se realiza en un solo sentido, desde la cabeza hasta encontrar un valor nulo null. Presenta un costo de tiempo de $O(n)$ para inserciones o búsquedas al final si no se mantiene una referencia directa a la cola, pero resulta ideal para colecciones sencillas donde la sobrecarga de memoria debe ser mínima.
- **Lista doble:** Estructura en la que cada nodo contiene un dato y dos punteros siguiente y anterior. Esto permite un recorrido bidireccional (hacia adelante y hacia atrás), facilitando enormemente operaciones como la eliminación de nodos conocidos sin necesidad de buscar previamente al elemento predecesor. Su desventaja principal radica en el mayor consumo de memoria y la necesidad de actualizar cuidadosamente los enlaces dobles en cada modificación.
- **Lista circular:** Variante de lista enlazada (simple o doble) donde el último nodo apunta de regreso al primero, eliminando por completo la existencia de un valor nulo al final del recorrido. Es sumamente útil para modelar turnos equitativos, sistemas de rotación de procesos (Round-Robin) y buffers de datos continuos, requiriendo mecanismos de control específicos como bucles do-while para evitar ciclos infinitos durante su lectura.

## Reto 1 - Qué se pidió y cómo lo resolvió
En este reto se completó una lista simple para gestionar un catálogo de libros. 
- **TODO 1 y 3:** Se validó si la lista estaba vacía para asignar directamente el nuevo nodo a la cabeza, o bien se recorrió la lista hasta el último elemento TODO 2 para enlazar el nuevo nodo al final.
- **TODO 4:** Se implementó la búsqueda comparando los títulos mediante el método equals.
- **TODO 5, 6 y 7:** Se manejó la lógica de eliminación cubriendo el caso especial de remover la cabeza, así como la inspección del nodo siguiente para saltarlo y desconectarlo correctamente de la estructura.
- **Evidencias:** Las capturas de compilación y ejecución se encuentran almacenadas en capturas/reto1-compilacion.png y capturas/reto1-ejecucion.png.

## Reto 2 - Qué se pidió y cómo lo resolvió
Se desarrolló un historial de lectura implementado mediante una lista doble.
- **TODO 1 al 4:** Se programó la inserción al inicio asegurando la actualización simultánea de los punteros `cabeza` y `cola`, así como el reajuste de los enlaces siguiente y anterior de los nodos adyacentes.
- **TODO 5 y 6:** En la eliminación, se actualizaron de manera condicional los punteros de los nodos vecinos, contemplando los cambios necesarios si el nodo afectado correspondía a los extremos de la lista.
- **TODO 7:** Se completó el método de recorrido inverso partiendo desde la cola hacia atrás mediante el uso sistemático del puntero `anterior`.
- **Evidencias:** Las capturas correspondientes están en `capturas/reto2-compilacion.png` y `capturas/reto2-ejecucion.png`.

## Reto 3 - Qué se pidió y cómo lo resolvió
Se programó el sistema de turnos de préstamo utilizando una lista circular.
- **TODO 1 al 3:** Se implementó la inserción asegurando que el nuevo nodo cerrara el círculo apuntando de regreso a la cabeza y actualizando adecuadamente la referencia de la cola.
- **TODO 4, 5 y 6:** Para el despliegue y conteo seguro de los elementos, se estructuraron bucles `do-while` controlados por la posición inicial de la cabeza, previniendo así un bucle infinito.
- **TODO 7:** En la eliminación del turno siguiente a un estudiante dado, se localizó el nodo de referencia y se reestructuraron los enlaces cuidando los casos especiales de un único nodo o la alteración de los punteros extremos.
- **Evidencias:** Las capturas están guardadas en `capturas/reto3-compilacion.png` y `capturas/reto3-ejecucion.png`.

## Reflexión final
1. **¿Qué punteros tuvieron que actualizar en la eliminación de una lista doble y por qué son más que en la simple?**  
   En la lista doble fue necesario actualizar tanto el puntero siguiente del nodo anterior como el puntero `anterior` del nodo siguiente con respecto al elemento eliminado. Son más que en la simple porque la naturaleza bidireccional de la estructura exige mantener la integridad de los enlaces en ambas direcciones para no romper la continuidad de la navegación en reversa, a diferencia de la lista simple que solo requiere modificar un único enlace direccional.

2. **¿Qué error cometieron (o evitaron) por no considerar el caso de lista vacía o de un solo nodo?**  
   Al inicio del desarrollo corríamos el riesgo de provocar excepciones por referencias nulas NullPointerException al intentar manipular propiedades de nodos inexistentes. Este error se evitó implementando guardas condicionales estrictas al inicio de cada método, comprobando explícitamente si la cabeza era nula o si la operación dejaba la lista completamente vacía tras eliminar el único elemento disponible.

3. **¿Qué pasaría si en la lista circular se recorre con while (actual != null)?**  
   Provocaría un ciclo infinito bucle colgado que congelaría la ejecución del programa. Como el último nodo de una lista circular apunta de regreso al inicio en lugar de apuntar a null, una condición basada en evaluar la nulidad del puntero jamás evaluaría como falsa, atrapando al hilo de ejecución indefinidamente en el bucle de recorrido.

4. **¿En qué situación elegirían cada tipo de lista?**  
   La lista simple se elige para escenarios donde la memoria es sumamente estricta y las operaciones de recorrido se realizan en un único sentido, priorizando la simplicidad del código. La lista doble se selecciona cuando se requiere alta eficiencia en operaciones de eliminación y navegación bidireccional frecuente, tal como ocurre en historiales de navegación o reproductores multimedia. La lista circular es perfecta para modelar turnos equitativos, sistemas operativos de planificación rotativa Round-Robin y buffers de datos continuos.

5. **¿Qué fue lo más difícil y cómo lo resolvieron como bina?**  
   Lo más complejo fue asegurar que los punteros extremos cabeza y cola no se perdieran ni dejaran referencias huérfanas durante las operaciones de eliminación en la lista circular y la lista doble. Lo resolvimos trabajando en equipo mediante la técnica de diagramación en papel: dibujamos los nodos paso a paso, trazamos visualmente las flechas de los punteros para cada caso de borde y verificamos la lógica conjuntamente antes de escribir y probar el código definitivo en Java.
