---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.db.elasticsearch/","title":"Elasticsearch"}
---


Elasticsearch это поисковой движок, хранение данных в нем оправдано если требуется часто искать и фильтровать данные.

---

- Размер scroll_id при запросе /scroll может отличаться в зависимости от количества шардов у индекса, его рекомендуется передавать через body, потому что в url params он может просто не поместиться

- Если проблемы с elastic и kibana docker image, можно использовать образы от bitnami