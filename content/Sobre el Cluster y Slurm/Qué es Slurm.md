---
title: ¿Qué es Slurm?
---

Dentro de la variedad de planificadores que existen, InSAR lab utiliza **Slurm** (**S**imple **L**inux **U**tility for **R**esource **M**anagement). De acuerdo con su documentación oficial[^1], Slurm es un sistema de gestión de cargas de trabajo (_workload manager_) de código abierto, diseñado para ser tolerante a fallos y altamente escalable. Hoy en día es el estándar de la industria, utilizado por gran parte de los centros de supercómputo más grandes del mundo.

Slurm se encarga de tres tareas fundamentales dentro de nuestra arquitectura:

- **Asignación de recursos:** Otorga a los usuarios el acceso a los componentes de los nodos de cómputo durante un periodo de tiempo determinado para que puedan realizar sus cálculos o pruebas.
- **Gestión de ejecución:** Proporciona un entorno estructurado y seguro para iniciar, ejecutar y monitorear el trabajo en los nodos que el sistema te ha asignado.
- **Arbitraje de la cola:** Resuelve los conflictos de demanda administrando inteligentemente la fila de trabajos pendientes. Si hay más trabajo que recursos disponibles, Slurm decide qué tarea es la siguiente en ejecutarse basándose en reglas de prioridad y disponibilidad.

Gracias a esta herramienta, como usuario del InSAR lab no tienes que preocuparte por conectarte nodo por nodo para ver cuál está desocupado. Simplemente empaquetas tu trabajo, le describes a Slurm qué recursos necesitas, y el sistema se encarga de acomodarlo y ejecutarlo en el momento ideal.
