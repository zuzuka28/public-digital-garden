---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-devops-k8s-replica-set/","title":"Replica Set"}
---


<https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/>

ReplicaSet гарантирует, что определенное количество экземпляров [[notes/organize.resource.it.devops.k8s.pod\|notes/organize.resource.it.devops.k8s.pod]] всегда будет запущено в кластере.

Не рекомендуется использовать ReplicaSet напрямую, для большинства задач нужно использовать более высокоуровневую абстракцию в виде [[notes/organize.resource.it.devops.k8s.deployment\|notes/organize.resource.it.devops.k8s.deployment]]. 
