---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.devops.k8s.istio.virtual-service/","title":"Virtual Service"}
---


<https://istio.io/latest/docs/reference/config/networking/virtual-service/>

Виртуальные сервисы используются для перенаправления трафика в адресуемые сервисы в кластере.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService 
metadata:
  name: vs-name
spec:
  hosts:
    - my-cluster-domain # селектор хостов кластера
  gateways:
    - istio-system/cluster-gateway # типы разные бывают, они задают откуда будет виден сервис
  http:
    - match:
        - uri:
            prefix: /
      route:
        - destination:
            port:
              number: 80
            host: my-service-selector
```