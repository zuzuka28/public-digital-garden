---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-concurrency-hashtable/","title":"Hashtable"}
---


<https://www.youtube.com/watch?v=39FVKa9liZU>
<https://github.com/orcaman/concurrent-map>
<https://pkg.go.dev/sync#Map>
<https://ru.wikipedia.org/wiki/FNV>
<https://habr.com/ru/articles/250383/>
<https://habr.com/ru/articles/317882/>

- deadlock и livelock
  - способ анализа deadlock блокировок - wait-for graph
    - https://en.wikipedia.org/wiki/Wait-for_graph

- hashtable
  - способы обработки коллизий
    - chaining
    - probing
    - <https://stackoverflow.com/questions/36531119/what-is-the-difference-between-chaining-and-probing-in-hash-tables>
  - способы организации конкурентного доступа
    - для m бакетов использовать n locker, которые будут защищать от одновременной модификации
      - при расширении хэштаблицы брать блокировку монотонно (те с 1 по n locker) всех locker
      - для лучшего доступа на чтение лучше использовать shared mutex или rw mutex
    - wait-free lookups - неблокируемое чтение (в сочетании с идеей выше)
      - RCU Lock (Read/Copy/Update)
        - операции
          - read lock
          - read unlock
          - syncronize
            - syncronize операция кончается только когда заканчиваются все операции read ДО вызова syncronize
      - идея
        - использование RCU Lock
        - разделение операции на 
          - sync - обновление значения писателем и вызов syncronize
          - memory reclamition - читатели берут read lock unlock