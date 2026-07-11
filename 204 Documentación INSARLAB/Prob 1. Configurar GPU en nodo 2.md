Se creo un archivo
```bash
sudo nano /etc/slurm/gres.conf
```

Se pegó esta línea:
```bash
Name=gpu Type=l4 File=/dev/nvidia0
```

Reiniciar master:
```bash
sudo systemctl restart slurmctld
```

Reiniciar nodo 2
```bash
sudo systemctl restart slurmd
```

