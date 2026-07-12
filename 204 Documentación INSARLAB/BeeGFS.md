FhGFS
Parallel file sYstem designed for linux clusters

Lets you distribute data across multiple storage servers, so you get really fast access and scalability.

Sigo realizando el manual para que un usuario pueda usar los nodos mediante slurm
Y justo sobre la creación de mi usuario, esa es mi duda de cuál tipo de usuario quiero crear
Me dijeron que cree un usuario usando slurm y documente como crearlo
Justo hay que recordar que el objetivo es que un usuario A entre al master con su usuario y llave mediante ssh y pueda encolar tareas usando slurm.
Pero justo además, hay que recordar que estamos usando beegfs para compartir los archivos entre nodos

Me meto en la carpeta /mnt/beegfs/insarlab
y dentro me listan algunas carpetas con los usuarios que tengo que se pueden meter mediante ssh y que pueden hacer jobs mediante slurm

Mi duda es entonces, como debería crear mis usuarios?
usaría slurm? uso beegfs? o como creo ese usuario?, que debería crear su carpeta dentro de /mnt/beegfs/insarlab y que además puedo acceder mediante ssh 