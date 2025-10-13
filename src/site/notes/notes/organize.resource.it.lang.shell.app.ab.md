---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-shell-app-ab/","title":"Ab","tags":["source.app"]}
---


<https://httpd.apache.org/docs/2.4/programs/ab.html> - утилита для бенчмарк тестирования API

## Golang Profile

роутинги, которые надо добавить

```
router.HandleFunc("/debug/pprof/", pprof.Index)
router.HandleFunc("/debug/pprof/cmdline", pprof.Cmdline)
router.HandleFunc("/debug/pprof/profile", pprof.Profile)
router.HandleFunc("/debug/pprof/symbol", pprof.Symbol)
router.HandleFunc("/debug/pprof/trace", pprof.Trace)
router.HandleFunc("/debug/pprof/goroutine", pprof.Trace)

симуляция 100000 запросов(8 параллельно)

```sh
ab -k -c 8 -n 100000 http://localhost:8001/api/web
```

профилирование 30сек

```
go tool pprof goprofex http://127.0.0.1:8001/debug/pprof/profile
```