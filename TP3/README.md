1)
* a)
 Al ejecutar los códigos sin hilos y con hilos, se nota que el tiempo de ejecución entre un programa y otro tiene una diferencia.
 En el caso de sin hilos, todas las tareas se ejecutan secuencialmente, una después de la otra,
 lo que significa que el tiempo de ejecución total será la suma de los tiempos de ejecución de cada tarea individual.
 Con hilos, las tareas se ejecutan en paralelo, lo que debería reducir el tiempo total de ejecución.
 Sin embargo, debido a la sobrecarga de administración de hilos y posibles problemas de concurrencia, el tiempo de ejecución real puede variar.
 1)
 * b)
 Al  comparar el tiempo de ejecución con un compañero,se obtuvo resultados diferentes,
 ya que las computadoras tienen configuraciones y  hardware diferentes.
 Factores como la velocidad del procesador, la cantidad de núcleos, la memoria disponible y la carga del sistema pueden afectar el rendimiento
 por lo tanto  el tiempo de ejecución, sin embargo 
 el código con hilos debería mostrar una mejora en el tiempo de ejecución en comparación con el código sin hilos, especialmente en sistemas con múltiples núcleos o CPU.
 1)
 * c)  Al eliminar las líneas 11, 12, 19 y 20 nos introducimos  un bucle interno que no hace nada útil pero consume tiempo de CPU. 
 Esto puede ralentizar el programa. Además de que   los hilos no están sincronizados en el acceso a la variable acumulador, puede haber resultados inconsistentes debido a condiciones de carrera.
 
 2)
 * a)
 <img src="./TP3/codigo_funcionando.png>
<a href="./tp3_2a.c">puzzle resuelto</a>
2)
* b)
<img src="./TP3/2b-1.png>






