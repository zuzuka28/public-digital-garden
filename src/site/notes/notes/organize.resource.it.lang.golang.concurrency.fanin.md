---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-concurrency-fanin/","title":"Fanin"}
---


Объединение нескольких каналов в один.

```go
func fanIn(in ...<-chan int) <-chan int {
   var wg sync.WaitGroup
   out := make(chan int)
 
   output := func(c <-chan int) {
       for n := range c {
           out <- n
       }
       wg.Done()
   }

   wg.Add(len(in))
   for _, c := range in {
       go output(c)
   }

   go func() {
       wg.Wait()
   }()

   return out
}
```