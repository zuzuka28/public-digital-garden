---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-sysdesign-asynchronous-http-request-processing/","title":"Asynchronous HTTP Request Processing"}
---


Asynchronous HTTP Request Processing

Тут хотел почитать про асинхронное взаимодействие клиент-сервер, когда запросов очень много.

Запрос rest -> ответ от фасада о том что запрос получен -> запрос к сервисам -> реальный ответ для клиента приходит на эндпоинт самого клиента через запрос от сервиса. 