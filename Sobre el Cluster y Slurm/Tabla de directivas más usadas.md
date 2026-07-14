---
title: Tabla de Directivas Principales de `sbatch`
---
El comando `sbatch` cuenta con una amplia variedad de opciones para gestionar con precisión cómo, cuándo y dónde se ejecutará tu código. Estas directivas se colocan al inicio de tu script de bash, siempre precedidas por la etiqueta `#SBATCH`.

A continuación, se presenta una tabla de referencia con las directivas más utilizadas en el entorno de cluster computing:

|**Directiva**|**Descripción**|**Ejemplo de uso**|
|---|---|---|
|**`--job-name=<nombre>`**|Asigna un nombre personalizado al trabajo. Esto facilita su identificación al consultar la cola con `squeue`.|`#SBATCH --job-name=modelo_clima`|
|**`--output=<archivo>`**|Define la ruta y nombre del archivo donde se guardará la salida estándar (stdout). Soporta variables de entorno como `%j` (Job ID).|`#SBATCH --output=resultados_%j.out`|
|**`--error=<archivo>`**|Define la ruta y nombre del archivo donde se registrarán exclusivamente los mensajes de error (stderr).|`#SBATCH --error=errores_%j.err`|
|**`--partition=<nombre>`**|Indica la cola lógica a la que se enviará el trabajo. En nuestro clúster puede ser `all`, `extra` o `n2gpu`.|`#SBATCH --partition=extra`|
|**`--time=<tiempo>`**|Establece el límite de tiempo máximo que el trabajo tiene permitido ejecutarse. Si excede este límite, Slurm lo detendrá. Acepta formatos como `minutos`, `horas:minutos:segundos` o `días-horas`.|`#SBATCH --time=12:30:00` _(12 horas y media)_|
|**`--nodes=<cantidad>`**|Solicita el número de nodos físicos distintos que el trabajo requiere para ejecutarse.|`#SBATCH --nodes=2`|
|**`--ntasks=<cantidad>`**|Define el número total de tareas (procesos independientes) a ejecutar. Es fundamental cuando se trabaja con arquitecturas de memoria distribuida (como MPI).|`#SBATCH --ntasks=4`|
|**`--cpus-per-task=<cantidad>`**|Asigna una cantidad específica de núcleos (CPUs) a cada tarea. Es indispensable para programas de memoria compartida o procesamiento multihilo (como OpenMP).|`#SBATCH --cpus-per-task=8`|
|**`--mem=<tamaño>`**|Solicita la cantidad máxima de memoria RAM requerida por nodo. Se especifica utilizando sufijos como `M` (Megabytes) o `G` (Gigabytes).|`#SBATCH --mem=64G`|
|**`--gres=<recursos>`**|Solicita recursos genéricos del nodo. En el contexto del procesamiento de alto rendimiento, se utiliza principalmente para reservar aceleradores gráficos (GPUs).|`#SBATCH --gres=gpu:l4:1`|
|**`--nodelist=<nodos>`**|Obliga al planificador a ejecutar el trabajo estrictamente en los nodos listados, ignorando los demás equipos disponibles.|`#SBATCH --nodelist=node3,node4`|
|**`--exclude=<nodos>`**|Funciona de manera inversa a `--nodelist`. Le indica a Slurm los nodos específicos en los que **no** debe ejecutar el trabajo.|`#SBATCH --exclude=node1`|
|**`--mail-type=<eventos>`**|Configura el envío de alertas automáticas por correo electrónico ante cambios de estado del trabajo. Valores comunes: `BEGIN`, `END`, `FAIL` o `ALL`.|`#SBATCH --mail-type=ALL`|
|**`--mail-user=<correo>`**|Especifica la dirección de correo electrónico a la cual se enviarán las alertas configuradas en la directiva `--mail-type`.|`#SBATCH --mail-user=usuario@dominio.com`|
