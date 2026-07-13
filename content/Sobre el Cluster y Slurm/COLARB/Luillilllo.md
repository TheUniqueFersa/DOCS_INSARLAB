Comandos realizados para poder lograr identificar completamente a la gpu
sudo dnf update -y

sudo dnf config-manager --set-enabled crb

sudo dnf install epel-release -y

sudo dnf install kernel-devel-matched kernel-headers -y

sudo dnf config-manager --add-repo \
  https://developer.download.nvidia.com/compute/cuda/repos/rhel10/x86_64/cuda-rhel10.repo

sudo dnf clean all

sudo dnf install nvidia-open -y

reboot


![[Pasted image 20260610130018.png]]





# Configurar la gpu para que la reconozca slurm
(en master)
/etc/slurm/slurm.conf

Se modifica el archivo para agregar GRES (gerenric resources) e indicar que el nodo 2 trabajará también con gpu:l4:1
Adicionalmente en el nodo 2 se modificó el archivo gres.conf (o en su defecto, se creó) para añadir e indicar que ese nodo cuenta con gpu:l4:1. El sistema slurm detecta automáticamente el archivo.

Se creó una cola adicional exclusivamente para la gpu del nodo 2. Es muy importante que los cambios realizados en el máster de slurm.conf se vean reflejados en los demás nodos.

Al final la configuración de las colas quedaron así.
	[admin@master slurm]$ sinfo
	PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
		all*         up            infinite                 3              idle        master,node[1-2]
		all*         up            infinite                  1             down      node4
	    n2gpu        up       infinite                  1              idle         node2


### Mini Problema con sincronización de BeeGFS en el nodo 2.
Se presentó un problema con BeeGFS en el nodo 2, el comportamiento de compartir archivos en la misma localidad en nodos diferentes no funcionaba, se debió a que estaba "apagado" ese comportamiento en el nodo 2. Únicamente se ejecutó el siguiente comando para despertar BeeGFS en el nodo 2 y que pudiera compartir los archivos del nodo 2 en el máster.
	systemctl restart beegfs-client




Aclarando que todos los archivos de resultado y error se habían creado de forma exitosa dentro del nodo 2 pero no se compartieron en el master. Recordando que los usuarios únicamente pueden acceder a su carpeta en máster, por lo tanto no podían ver los resultados arrojados por Slurm.




Los únicos archivos que se comparten entre nodos son los que se encuentran en /mnt/beegfs/ 
Todos esos archivos se comparten, también dentro de esa ubicación está el home de los usuarios

Los usuarios solamente pueden navegar en su carpeta en *master*, no pueden entrar a los demás nodos
Recordando que la ubicación de la carpeta de cada usuario se encuentra en 



(Ignorar lo siguiente por la situación explicada arriba de sincronización de beegfs en el nodo 2 )
#### Otorgar permiso de ejecución (travesía) a la carpeta del grupo
	sudo chmod 755 /mnt/beegfs/insarlab/
Esto en el nodo 2 para que se pueda migrar datos del nodo 2 al master


## Configurando Slurm en un nodo (3)
Corremos el comando *sinfo* en el nodo 3 y podemos ver que no está instalado por el resultado, por lo tanto tenemos que hacer la instalación de slurm en el nodo 3.
Como tenemos Ansible en el cluster, podemos ocuparlo para instalar slurm en el nodo 3.

	admin@master ansible]$ cat inventory/hosts.ini 
	[master]
	master-node ansible_host=192.168.1.254 ansible_connection=local
	
	[workers]
	node1 ansible_host=192.168.1.1
	node2 ansible_host=192.168.1.2
	#node3 ansible_host=192.168.1.3
	node4 ansible_host=192.168.1.4
	
	[cluster:children]
	master
	workers
	[admin@master ansible]$ 

Podemos observar que el nodo 3 está comentado, por lo que Ansible simplemente lo ignoró.

Se descomentó la línea comentada en 'inventory/hosts.ini' 

**Ocurrió un error y tal parece que no puede entrar automático al nodo3, por lo que se le otorga la ssh para entrar sin pedir contraseña (como los demás nodos)
	ssh-copy-id admin@192.168.1.3
**

Se ejectua el comando rpmbuild -ta slurm-25.05.5.tar.bz2 para poder crear el rpm que no reconoce.

	cp ~/rpmbuild/RPMS/x86_64/slurm-25.05.5-1.el10.x86_64.rpm /tmp/
	cp ~/rpmbuild/RPMS/x86_64/slurm-slurmd-25.05.5-1.el10.x86_64.rpm /tmp/
Se mueven archivos necesarios para el siguente comando
(En ~/ansible)
	ansible-playbook -i inventory/hosts.ini playbooks/slurmd.yaml --limit node3 -K


	sudo cp /etc/munge/munge.key /tmp/
	sudo chown admin:admin /tmp/munge.key

Luego se ejecuta el comando para añadir slurm al nodo 3 (va a recorrer todos los nodos pero no hará nada porque ya está instalado en los demás)
	 ansible-playbook -i inventory/hosts.ini playbooks/slurmd.yaml -K








## Modificando queues de Slurm
N1, máster (Llamada All, ya existe)
N2, N3, N4 - (Llamada extra)

Se modifica el archivo '/etc/slurm/slurm.conf' y se reconfigura las queues.
Cuando se modifique el archivo se tiene que correr el comando para refrescar los cambios

	sudo scontrol reconfigure

	[admin@master ~]$ sinfo
	PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
	all          up   infinite      2   idle master,node1
	n2gpu        up   infinite      1   idle node2
	extra*       up   infinite      1   idle node2
	extra*       up   infinite      1   down node4





## Revivir el nodo 4
	sudo scontrol update NodeName=node4 State=RESUME




