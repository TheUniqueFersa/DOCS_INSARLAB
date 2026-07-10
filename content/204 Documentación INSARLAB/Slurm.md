Hola soy slurm

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