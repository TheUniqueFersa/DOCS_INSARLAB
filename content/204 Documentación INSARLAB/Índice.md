# Bienvenido a INSARLAB
Te damos la bienvenida al manual de usuario de **INSARLAB**.

Este manual está hecho para aprender a manejar 

Para el uso del Cluster, es útil revisar lo siguiente:
- [[Cluster Computing]]
- [[Arquitectura del Cluster de INSARLAB]]
- [[Slurm]]
- 



El nodo máster es exclusivamente para **escribir código**, **compilar** y **enviar trabajos**



# Manual de Usuario
> [!important]
> Para poder utilizar el Cluster, [[Creación de Usuario|necesitas un usuario]]

Una vez que tengas :
- Usuario
- Llave

- [[#Configurar Llave para ingreso al Cluster]]
- [[#Ingresar al Cluster]]

- Usando slurm, encolar sus tareas
- Proceso de creación de scripts con todas las directivas de SLURM
- Como cancelar
- Como ver el estado de su job


# Configurar Llave para ingreso al Cluster

Tener a la mano:
- La llave que el **usuario administrador te entregó**

> [!important]
> SI estás usando windows, utilizar la **terminal Powershell**

1. Dirígete a la ruta `~/.ssh`
2. Crear el archivo que guardará tu llave proporcionada por el usuario administrador
*Puede ser cualquier nombre*, pero se sugiere usar `llave_insarlab`

> [!note] Puede ser algo como el siguiente procedimiento:
> 
> - Crear el archivo con
> ```bash
> touch llave_insarlab
> ```
> - Abrir con tu editor predeterminado, por ejemplo si usas `nvim`
> ```bash
> nvim llave_insarlab
> ```
> 
> - Una vez que abra la interfaz de nvim, pegar la llave en dicho archivo
> 


El archivo `llave_insarlab` terminaría viéndose algo así:
```
-----BEGIN OPENSSH PRIVATE KEY-----
Aquí esta tu llave
-----END OPENSSH PRIVATE KEY-----
```

- Guardar el contenido del archivo

3. Modificar el archivo `config` para que `ssh` pueda ingresar correctamente al cluster
En la misma ruta (`~/.ssh/`), modificar el archivo `config` o en su defecto crearlo y escribir dentro de él:
```
Host <nombreHost>
	HostName 132.248.59.7                                
	User <usuario>
	IdentityFile ~/.ssh/<ruta de la llave>
```

Reemplazar los valores entre `<>` por tus datos:
- `<nombreHost>`: El nombre que se usará para ingresar mediante `ssh`, se sugiere usar: `InsarNombreUsuario`
- `<usuario>`: Es el usuario que te proporcionó el administrador al momento de crear tu usuario
- `<ruta de la llave>`: El nombre del archivo con tu llave, se sugirió usar `llave_insarlab`


> [!example] Un ejemplo real del archivo `config`
> ```
> Host insarFalcon
> 	HostName 132.248.59.7
> 	User falcon
> 	IdentityFile ~/.ssh/llave_insarlab
> ```


# Ingresar al Cluster
Una vez hayas [[#Configurar Llave para ingreso al Cluster|configurado tu llave]], podrás ingresar al Cluster de la siguiente forma:
```bash
ssh <nombreHost>
```
Donde nombreHost es el nombre que se le asignó al hostName del Cluster (`132.248.59.7`) en el archivo `config`

> [!example]
> ```bash
> ssh insarFalcon
> ```
> 

>Supóngase que el usuario `falcon` ingresó a Cluster

Al momento de ingresar, el prompt de la terminal se verá algo así;
```bash
[falcon@master ~]$ 
```

