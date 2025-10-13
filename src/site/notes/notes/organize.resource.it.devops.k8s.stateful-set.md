---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.devops.k8s.stateful-set/","title":"Stateful Set"}
---


<https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>

StatefulSets - так же как и [[notes/organize.resource.it.devops.k8s.deployment\|organize.resource.it.devops.k8s.deployment]], управляет развертыванием и масштабированием набора подов, но сохраняет набор идентификаторов и состояние для каждого пода, а не генерирует случайный.

В основном используется для организации работы приложений с Persistent хранилищами.
