---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-devops-k8s-job/","title":"Job"}
---


<https://kubernetes.io/docs/concepts/workloads/controllers/job/>

Job создает определенное количество [[notes/organize.resource.it.devops.k8s.pod\|notes/organize.resource.it.devops.k8s.pod]] и смотрит, пока они успешно не завершат работу. 
Если под завершился с ошибкой, то пересоздает его до тех пор, пока он не завершится успешно, либо пока не достигнет лимита по попыткам.
Если под успешно отработал, записывает это журнал.