---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-devops-k8s-service/","title":"Service"}
---


<https://kubernetes.io/docs/concepts/services-networking/service/>

Сервисы - способ предоставить доступ к сети для подов в кластере.

```yaml
kind: Service
apiVersion: v1
metadata:
  name: service-name
spec:
  selector:
    app: my-pod-selector # селектор подов для которых работает сервис
  ports:
    - protocol: TCP
      port: 80 # порт, на который будут прилетать коннекты извне
      targetPort: 8080 # порт внутри пода, на который будут переноситься коннекты
```