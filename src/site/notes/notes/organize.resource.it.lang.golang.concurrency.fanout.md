---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-concurrency-fanout/","title":"Fanout"}
---


Распределение сообщений из канала по нескольким каналам.

```go
func fanOut(ch <-chan int, n int) []<-chan int {

  cs := make([]chan int)
  for i := 0; i < n; i++ {
    cs = append(cs, make(chan int))
  }

  toChannels := func(ch <-chan int, cs []chan<- int) {
    defer func(cs []chan<- int) {
      for _, c := range cs {
        close(c)
      }
    }(cs)

    for {
      for _, c := range cs {
        select {
        case val, ok := <-ch:
          if !ok {
            return
          }

          c <- val
        }
      }
    }
  }

  go toChannels(ch, cs)

  return cs
}
```