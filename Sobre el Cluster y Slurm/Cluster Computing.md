
Para aprovechar al máximo los recursos del laboratorio InSAR, es indispensable comprender qué es exactamente la herramienta que estamos utilizando. En términos generales, la computación en clúster, o cluster computing, es la integración de varias computadoras independientes que están conectadas a través de una red de alta velocidad. 

Al trabajar juntas y de forma coordinada mediante software especializado, estas computadoras funcionan y se presentan al usuario como si fueran un único y masivo sistema. Esto nos permite resolver **problemas matemáticos**, **realizar simulaciones** o **procesar volúmenes de datos** mucho *más grandes* y en *mucho menor tiempo* de lo que podría lograr una computadora de escritorio convencional o un servidor solitario.

A cada una de estas computadoras individuales que conforman el sistema se le conoce como *nodo*. ^DefinicionNodo

Dentro de la arquitectura de un clúster, interactuamos principalmente con dos tipos:
- **Nodo maestro**, que actúa como el director de la orquesta. Es el punto de acceso al cual te conectarás como usuario y es el administrador central, encargado de recibir tus instrucciones y distribuir el trabajo de forma equitativa. ^DefinicionNodoMaestro

- **Nodos de cómputo**, encargados únicamente de procesar la información y ejecutar las tareas pesadas que el nodo maestro les delega. ^DefinicionNodosComputo

> [!todo] Repasando
> 
> > [!info] Computación basada en Clusters
> > Cuando la computación ya no ocurre solo 1 un computadora, pero en un conjunto de máquinas similares, donde todas se configuran para hacer procesamiento y ejecución similar, se está hablando de **Computación basada en Clusters**
> 
> - Involucra varias computadoras unidas para resolver un problema
> - Incrementa la velocidad de computación
> - Divides el trabajo en varias partes y las mandas a cada nodo
> - Esparce el trabajo hecho a lo largo de muchas CPUs que tiene el sistema
> - No se maneja cada equipo individualmente, sino que uno (el máster) delega las tareas a realizar
 
![[Arquitectura del Cluster del InSAR lab]]

## Job Scheduler
En un entorno como nuestro clúster, donde varios miembros del laboratorio necesitan realizar simulaciones o procesar datos al mismo tiempo, enviar todas las tareas de forma directa colapsaría el sistema. Aquí es donde entra en juego la figura del **job scheduler** o planificador de trabajos.

Se puede pensar en el planificador como el coordinador central de los recursos. Es un software especializado que recibe las solicitudes de trabajo de todos los usuarios, revisa qué recursos del hardware están libres en ese momento (==cuántos núcleos, cuánta memoria, si la GPU está en uso==) y organiza una **fila de espera ordenada**. Su propósito principal es asegurar que cada proceso reciba lo que necesita para ejecutarse correctamente, *evitando que las tareas de distintos usuarios interfieran entre sí y garantizando que el clúster opere a su máxima capacidad sin sobrecargarse.*

> [!info]
> InSAR lab utiliza el job scheduler conocido como [[Que es Slurm]]
