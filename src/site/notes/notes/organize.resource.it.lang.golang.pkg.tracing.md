---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-pkg-tracing/","title":"Tracing"}
---


Интеграция OTEL с net/http - <go.opentelemetry.io/contrib/instrumentation/net/http/otelhttp>.
Тут есть мидлвари и обертки для хэндлеров, чтобы инжектить спаны в запрос.

Sentry с otel - совместить приятное с полезным и использовать sentryotel для всего трейсинга не выйдет.
Спаны не энричатся данными, которые проставляет sentryhttp, в jaeger дополнительная информация не будет отображена.
Нужно поисследовать этот момент, может я где-то накосячил.