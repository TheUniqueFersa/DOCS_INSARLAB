Login Node o Head Node (Master): solo se usa para rescribir código, compilar y enviar instrucciones


- [ ] Qué es un demonio (daemon)
- [ ] Recordar la arquitectura de los nodos y cómo quedaron con un diagramita
- [ ] Entonces, Luilli me dijo que había configurado el slurm, pero algo se borró?

>Máster: es el cerebro

`slurmctld`
- Recibe peticiones de los usuarios y decide a qué nodo secundario enviarlas

>Los otros 4 nodos

`slurmd`
- Reciben tareas del mástel
- Las ejecutan
- Devuelven el resultado


Comandos de slurm:
- `sbatch`
- `srun`

>Comandos que empaqueta el trabajo y lo mandan a los nodos


## Reservar recursos
- Mediante particiones (colas)
- Sesoines interactivas: si un usuario necesita una terminal en un nodo secundario para hacer pruebas en tiempo real:
`salloc` o `srun --pty bash`

Esto le prestaría una terminal en uno de los 4 nodos temporalmente y, cuando termina, el nodo queda libre.


## Gestión de cuentas de usuario
Para que Slurm funcione correctamente, el usuario $A$ debe existir y tener el mismo ID (UID) en el máster y en los 4 nodos. 
Su carpeta personal (`/home/pepito`) debe ser accesible desde todas las máquinas.

>Esto se resuelve gracias al uso de [[BeeGFS]]
- [ ] Cómo hacemos o nos aseguramos de eso?

> [!example]
> Si un usuario $A$ guarda un archivo o su código en el nodo maestro, ese archivo ya es visible en los 4 nodos secundarios


- [ ] cómo puedo ver le usuario que le crearon a falcon?
>[[Cómo ver usuarios que existen]]

---

- [ ] Límites? con `cgroups`, `ulimit` para matar cualquier proceso que consuma demasiad RAM o CPU, por si a algún usuario se le olvide usar Slurm


# Inventario de Nodos
- `lscpu` -> Cuantos núcleos de CPU tiene cada nodo
- `free -h` cuanta memoria RAM tiene cada nodo
- `nvidia-smi` -> si marca error es que no tiene GPU

Particiones y GRES (Generic Resources)

---
El usuario que ejecuta el domonio `slurmd` (en nuestro caso `root`) debe tener permisos de escritura en la carpeta donde redirijas estos archivos

Instalar lxd:
```BASH
sudo snap install lxd
```

- **Snap** es la "tienda" y el formato de empaquetado.
    
- **LXD** es la herramienta de virtualización/contenedores que descargas desde esa tienda.

---


`snap lxd`



---
Arcihvos d