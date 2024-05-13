1a)
 Al ejecutar los códigos sin hilos y con hilos, se nota que el tiempo de ejecución entre un programa y otro tiene una diferencia.
 En el caso de sin hilos, todas las tareas se ejecutan secuencialmente, una después de la otra,
 lo que significa que el tiempo de ejecución total será la suma de los tiempos de ejecución de cada tarea individual.
 Con hilos, las tareas se ejecutan en paralelo, lo que debería reducir el tiempo total de ejecución.
 Sin embargo, debido a la sobrecarga de administración de hilos y posibles problemas de concurrencia, el tiempo de ejecución real puede variar.
 1b)
 Al  comparar el tiempo de ejecución con un compañero,se obtuvo resultados diferentes,
 ya que las computadoras tienen configuraciones y  hardware diferentes.
 Factores como la velocidad del procesador, la cantidad de núcleos, la memoria disponible y la carga del sistema pueden afectar el rendimiento
 por lo tanto  el tiempo de ejecución, sin embargo 
 el código con hilos debería mostrar una mejora en el tiempo de ejecución en comparación con el código sin hilos, especialmente en sistemas con múltiples núcleos o CPU.
 1c)  Al eliminar las líneas 11, 12, 19 y 20 nos introducimos  un bucle interno que no hace nada útil pero consume tiempo de CPU. 
 Esto puede ralentizar el programa. Además de que   los hilos no están sincronizados en el acceso a la variable acumulador, puede haber resultados inconsistentes debido a condiciones de carrera.
 
 2a)
 #include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#define NUMBER_OF_THREADS 2
#define CANTIDAD_INICIAL_HAMBURGUESAS 20
int cantidad_restante_hamburguesas = CANTIDAD_INICIAL_HAMBURGUESAS;
int turno = 0; // Línea añadida para controlar el turno

void *comer_hamburguesa(void *tid)
{
	while (1 == 1)
	{ 
		// INICIO DE LA ZONA CRÍTICA
		while(turno!=(int)tid); // Control del turno
		// turno = (turno + 1)% NUMBER_OF_THREADS;  // Línea eliminada

		if (cantidad_restante_hamburguesas > 0)
		{
			printf("Hola! soy el hilo(comensal) %d , me voy a comer una hamburguesa ! ya que todavia queda/n %d \n", (int) tid, cantidad_restante_hamburguesas);
			cantidad_restante_hamburguesas--; // me como una hamburguesa
		}
		else
		{
			printf("SE TERMINARON LAS HAMBURGUESAS :( \n");
			pthread_exit(NULL); // forzar terminacion del hilo
		}
		turno = (turno + 1)% NUMBER_OF_THREADS; // Cambio de turno
		// SALIDA DE LA ZONA CRÍTICA   
	}
}

int main(int argc, char *argv[])
{
	pthread_t threads[NUMBER_OF_THREADS];
	int status, i, ret;
	for (int i = 0; i < NUMBER_OF_THREADS; i++)
	{
		printf("Hola!, soy el hilo principal. Estoy creando el hilo %d \n", i);
		status = pthread_create(&threads[i], NULL, comer_hamburguesa, (void *)i);
		if (status != 0)
		{
			printf("Algo salio mal, al crear el hilo recibi el codigo de error %d \n", status);
			exit(-1);
		}
	}

	for (i = 0; i < NUMBER_OF_THREADS; i++)
	{
		void *retval;
		ret = pthread_join(threads[i], &retval); // espero por la terminacion de los hilos que cree
	}
	pthread_exit(NULL); // como los hilos que cree ya terminaron de ejecutarse, termino yo tambien.
}

2b)







