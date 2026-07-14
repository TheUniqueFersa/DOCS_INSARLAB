---
title: Catálogo de estados de los nodos en sinfo
---
Los nodos del clúster transitan por diferentes estados dependiendo de la carga de trabajo asignada por los usuarios o de las condiciones de su propio hardware.

A continuación, se detallan los estados más importantes que se pueden presentar en el clúster:

|**Estado**|**Significado Técnico**|**Contexto en el InSAR lab**|
|---|---|---|
|**`idle`**|El nodo está completamente libre.|No hay ningún trabajo ejecutándose en él. Todos sus núcleos de CPU y su memoria RAM están disponibles para recibir tareas de inmediato.|
|**`mix`** _(Mixed)_|El nodo está parcialmente ocupado.|Significa que algunos núcleos (CPUs) o porciones de memoria RAM están siendo usados por el trabajo de un usuario, pero el equipo todavía tiene recursos sobrantes para aceptar más trabajos en paralelo.|
|**`alloc`** _(Allocated)_|El nodo está completamente ocupado.|Todos los recursos del equipo (procesadores, memoria o GPUs) han sido reservados en su totalidad. Cualquier trabajo nuevo enviado a este nodo se quedará esperando en la cola.|
|**`down`**|El nodo está fuera de servicio.|El equipo no está disponible para ejecutar tareas debido a una falla crítica de hardware, un reinicio o una intervención del administrador del sistema.|
|**`drain`** _(Draining)_|El nodo está en proceso de vaciado.|El nodo está terminando de ejecutar los trabajos que ya tenía asignados, pero Slurm tiene prohibido asignarle nuevas tareas. Suele activarse de forma manual antes de un mantenimiento programado.|
|**`maint`** _(Maintenance)_|El nodo se encuentra en una reserva de mantenimiento.|El equipo está apartado temporalmente para tareas administrativas y solo los usuarios autorizados o administradores pueden lanzar procesos en él.|
