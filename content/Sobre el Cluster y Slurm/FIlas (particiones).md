¿Cómo elegir el nodo correcto?

## Opción 1: Trabajos de CPU (sin GPU)
>Análisis de datos, compilar código en C
>Si el código no usa tarjetas gráficas, se deben manejar en la partición general para no ocupar GPU valiosa

El [^1]script se verá algo así
```bash
#SBATCH --partition=cpu_general  # Lo mandamos a los nodos sin GPU
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8        # Pide 8 núcleos de procesador
#SBATCH --mem=16G                # Pide 16 GB de RAM
```


## Opción 2: Trabajos de GPU (Machine Learning, Simulaciones pesadas)
Si se necesita GPU para tu trabajo, puede hacer el script como el siguiente:
```
#SBATCH --partition=gpu_nodes    # Lo mandamos a la zona de GPUs
#SBATCH --gres=gpu:l4:1          # Pide estrictamente 1 tarjeta L4
#SBATCH --cpus-per-task=4
#SBATCH --mem=32G
```





[^1]: - [ ] Redireccionarlo a como hacer un script
