Dentro de la variedad de planificadores que existen, InSAR lab utiliza **Slurm** (**S**imple **L**inux **U**tility for **R**esource **M**anagement). De acuerdo con su documentación oficial[^1], Slurm es un sistema de gestión de cargas de trabajo (_workload manager_) de código abierto, diseñado para ser tolerante a fallos y altamente escalable. Hoy en día es el estándar de la industria, utilizado por gran parte de los centros de supercómputo más grandes del mundo.

Slurm se encarga de tres tareas fundamentales dentro de nuestra arquitectura:

- **Asignación de recursos:** Otorga a los usuarios el acceso a los componentes de los nodos de cómputo durante un periodo de tiempo determinado para que puedan realizar sus cálculos o pruebas.
- **Gestión de ejecución:** Proporciona un entorno estructurado y seguro para iniciar, ejecutar y monitorear el trabajo en los nodos que el sistema te ha asignado.
- **Arbitraje de la cola:** Resuelve los conflictos de demanda administrando inteligentemente la fila de trabajos pendientes. Si hay más trabajo que recursos disponibles, Slurm decide qué tarea es la siguiente en ejecutarse basándose en reglas de prioridad y disponibilidad.

Gracias a esta herramienta, como usuario del InSAR lab no tienes que preocuparte por conectarte nodo por nodo para ver cuál está desocupado. Simplemente empaquetas tu trabajo, le describes a Slurm qué recursos necesitas, y el sistema se encarga de acomodarlo y ejecutarlo en el momento ideal.



---

Request jobs
- Submits jobs into the queue
### `-c <NUM CPUS>`
Indica el número de CPUs

Ejemplo
```
-c 10
```

### `--mem-per-cpu <mem>`
Ejemplo
```
--mem-per-cpu 100M 
```

### `-t <time>`
Por cuanto tiempo
```
-t 10:00
```
Para 10 minutos
`3-0:0:0` -> 3 días


# Comandos útiles
## `sbatch`
Llamada **no bloqueante**, lo ejecuta en segundo plano
Ejemplo
```
sbatch -c 2 --mem-per-cpu 2G -t 5:0:0 \
-J crunchy --wrap "python crunchy.py"
```
- `5:0:0` -> 5 horas
- `-J` -> para nombrar el *job*


- `--gres gpu` solicita **gpu**

## `srun`
**Llamada bloqueante**
No podrás ejecutar la terminar, porque srun la bloquea

## `salloc`
Put a job in the queue
Mismos comandos que [[#`sbatch`|sbatch]]

---
## `scancel`
Cancel a job
```
scancel <JOBID>
```
--- 
## `squeue`

Queries de slurm queue
Qué trabajos hay en la cola

## `sinfo`
Info about the complete cluster



## `sacct`
Query information about jobs and users and other aspects of the environment


**Job scheduler**


Manejar la cola

Request jobs
- Submits jobs into the queue
### `-c <NUM CPUS>`
Indica el número de CPUs

Ejemplo
```
-c 10
```

### `--mem-per-cpu <mem>`
Ejemplo
```
--mem-per-cpu 100M 
```

### `-t <time>`
Por cuanto tiempo
```
-t 10:00
```
Para 10 minutos
`3-0:0:0` -> 3 días



## `sbatch`
Llamada **no bloqueante**, lo ejecuta en segundo plano
Ejemplo
```
sbatch -c 2 --mem-per-cpu 2G -t 5:0:0 \
-J crunchy --wrap "python crunchy.py"
```
- `5:0:0` -> 5 horas
- `-J` -> para nombrar el *job*


- `--gres gpu` solicita **gpu**

## `srun`
**Llamada bloqueante**
No podrás ejecutar la terminar, porque srun la bloquea

## `salloc`
Put a job in the queue
Mismos comandos que [[#`sbatch`|sbatch]]

---
## `scancel`
Cancel a job
```
scancel <JOBID>
```
--- 
## `squeue`

Queries de slurm queue
Qué trabajos hay en la cola

## `sinfo`
Info about the complete cluster



## `sacct`
Query information about jobs and users and other aspects of the environment


## `scontrol`
### `show job <jobid>`


## Estados

| Estado |     |
| ------ | --- |
| idle   |     |
| mix    |     |

## ST

| State |           |
| ----- | --------- |
| R     | Running   |
| PD    | Pendiente |

## Ejemplo de bash
```bash
#!/bin/bash
#SBATCH --job-name=gpu_job
#SBATCH --gres=gpu
#SBATCH --time=5:00
python -u train.py
```

```bash
sbatch train.sh
```

Redirecciona a nu fichero llamado `slurm-<JOBID>.out`
# Referencias

|                                                                           |     |
| ------------------------------------------------------------------------- | --- |
| [Slurm Job Scheduler Basics](https://www.youtube.com/watch?v=Juo_mb3otJ0) |     |
| [Slurm Example in HPC](https://www.youtube.com/watch?v=51SyuTBk72k)       |     |


# BEYOND
- `screen`



- **`#SBATCH --output=<ruta_del_archivo>`**: Redirige la salida estándar (`stdout`) a un archivo.

- **`#SBATCH --error=<ruta_del_archivo>`**: Redirige la salida de errores (`stderr`) a un archivo.


Incluyendo el Job ID
```bash
#SBATCH --output=resultado_%j.out
#SBATCH --error=error_%j.err
```

**Si no especificas nada:** Slurm crea un archivo llamado `slurm-%j.out` en el directorio donde ejecutaste el comando `sbatch`, el cual contendrá tanto el `stdout` como el `stderr`
**Redirección combinada:** Si quieres que tanto los errores como la salida normal vayan al mismo archivo, puedes omitir la directiva `#SBATCH --error` o usar el mismo nombre en ambas.

[^1]: [Documentación oficial de Slurm](https://slurm.schedmd.com/documentation.html)
