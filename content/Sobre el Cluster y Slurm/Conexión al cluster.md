> [!summary]
> Una vez hecho todos los pasos de [[Creación de Usuario]], se podrá establecer la conexión con el cluster


> [!example] Tomando como ejemplo que el archivo `~/.ssh/config` se vea así:
> ```
> Host insarFalcon
> 	HostName 132.248.59.7
> 	User falcon
> 	IdentityFile ~/.ssh/insar_key
> ```

El comando para ingresar al cluster será:
```bash
ssh insarFalcon
```

`ssh` detectará que el hostname `insarFalcon` está asociada con `132.248.59.7` gracias a la configuración previamente hecha, así como detectará que la llave de acceso es la especificada por `IdentityFile` y que el usuario que se loggeará será `falcon` .

Al momento de ingresar, el prompt de la terminal se verá algo así;
```bash
[falcon@master ~]$ 
```


