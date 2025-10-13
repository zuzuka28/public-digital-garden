---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-devops-k8s-deployment/","title":"Deployment"}
---


<https://kubernetes.io/docs/concepts/workloads/controllers/deployment/>

Деплоймент - контроллер, который управляет состоянием развертывания [[notes/organize.resource.it.devops.k8s.pod\|notes/organize.resource.it.devops.k8s.pod]], которое описывается в манифесте, следит за удалением и созданием экземпляров подов. Управляет контроллерами [[notes/organize.resource.it.devops.k8s.replica-set\|ReplicaSet]].

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment # название деплоймента
  labels:
    app: nginx # лейбл
spec:
  replicas: 3 # количество реплик подов
  selector:
    matchLabels: # селектор, по которому деплоймент определяет свои поды
      app: nginx
  template: # описание пода, типа темплейт, который будет использован для создания подов
    metadata: # дальше все как при описании пода
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```