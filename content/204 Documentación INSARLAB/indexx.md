
## Comandos básicos

- **`sinfo`**: Para ver cuántos nodos hay y si están libres, ocupados o apagados.
- **`squeue`**: Para ver la fila de trabajos (quién está corriendo qué y en qué nodo).
- **`scancel <ID_del_trabajo>`**: El botón de pánico para cancelar un trabajo si se equivocaron.
### Modo interactivo
Cuando se necesita una terminal para compilar algo pesado o hacer pruebas rápidas que no requieren automatización, en lugar de hacerlo en el máster, se puede usar una terminal de un nodo secundario:
```bash
srun --pty bash
```

>Esto te llevará a uno de los 4 nodos para trabajar en vivo en él


## Forma de trabajo
En Slurm se crean archivos `.sh` (scripts) para enviar los trabajos de manera automática cuando haya recursos disponibles para completar dicha tarea

```bash
#!/bin/bash
#SBATCH --job-name=mi_simulacion
#SBATCH --output=resultado_%j.txt
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --gres=gpu:a100:1       # Petición de hardware específico
#SBATCH --time=02:00:00         # Tiempo máximo de ejecución

# Aquí va el comando que el usuario quiere ejecutar
python mi_codigo_pesado.py
```

## Solicitar gpu
```bash
#SBATCH --gress=gpu:l4:1
```



---



---
El administrador crea tu usuario

- Documentar la creación de usuario

- Documentar la creación de nodos
- Configuración del `slurm.conf`


