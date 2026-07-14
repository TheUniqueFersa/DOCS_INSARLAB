---
title: Códigos de razón de un Job (Job Reason Codes)
---

|**Código de Razón**|**Descripción**|**Acción recomendada**|
|---|---|---|
|**Resources**|Es la razón más común. Significa que los nodos están actualmente ocupados por los trabajos de otros compañeros.|Ninguna. Solo hay que ser paciente y esperar tu turno.|
|**Priority**|Hay recursos libres (o se están liberando), pero existen otros trabajos en la cola con mayor prioridad que el tuyo.|Esperar. Tu trabajo irá ganando prioridad conforme pase el tiempo.|
|**Dependency**|Tu trabajo está configurado para esperar a que otro trabajo termine antes de poder iniciar.|Verificar que el trabajo del cual depende no haya fallado.|
|**QOSMaxCpuPerUserLimit**|Has alcanzado el límite máximo de núcleos que un solo usuario puede usar simultáneamente en el clúster.|Esperar a que tus trabajos actuales terminen para que los pendientes inicien.|
|**ReqNodeNotAvail**|Solicitaste un nodo específico que actualmente está en mantenimiento, apagado o reservado.|Revisar con `sinfo` el estado del nodo y considerar cambiar de partición.|
>Si algún código de estado no se encuentra documentado por nuestra parte, puedes consultar la [documentación oficial](https://slurm.schedmd.com/job_reason_codes.html)