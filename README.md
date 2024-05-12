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
 
 2a)#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

#define NUMBER_OF_THREADS 2
#define CANTIDAD_INICIAL_HAMBURGUESAS 20

int cantidad_restante_hamburguesas = CANTIDAD_INICIAL_HAMBURGUESAS;
pthread_mutex_t mutex;

void *comer_hamburguesa(void *tid)
{
    while (1)
    {
        pthread_mutex_lock(&mutex); // Bloquea el mutex antes de acceder a la variable compartida
        if (cantidad_restante_hamburguesas > 0)
        {
            printf("Hola! soy el hilo(comensal) %d, me voy a comer una hamburguesa! Quedan %d\n", (int) tid, cantidad_restante_hamburguesas);
            cantidad_restante_hamburguesas--; // Me como una hamburguesa
        }
        else
        {
            printf("SE TERMINARON LAS HAMBURGUESAS :( \n");
            pthread_mutex_unlock(&mutex); // Desbloquea el mutex antes de salir
            pthread_exit(NULL);
        }
        pthread_mutex_unlock(&mutex); // Desbloquea el mutex después de acceder a la variable compartida
    }
}

int main(int argc, char *argv[])
{
    pthread_t threads[NUMBER_OF_THREADS];
    int status, i, ret;
    pthread_mutex_init(&mutex, NULL); // Inicializa el mutex

    for (int i = 0; i < NUMBER_OF_THREADS; i++)
    {
        printf("Hola!, soy el hilo principal. Estoy creando el hilo %d\n", i);
        status = pthread_create(&threads[i], NULL, comer_hamburguesa, (void *)i);
        if (status != 0)
        {
            printf("Algo salió mal al crear el hilo. Recibí el código de error %d\n", status);
            exit(-1);
        }
    }

    for (i = 0; i < NUMBER_OF_THREADS; i++)
    {
        void *retval;
        ret = pthread_join(threads[i], &retval); // Espera por la terminación de los hilos
    }

    pthread_mutex_destroy(&mutex); // Destruye el mutex
    pthread_exit(NULL);
}
2b)







