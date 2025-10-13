---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.lang.golang.concurrency.generator/","title":"Generator"}
---


Генератор генерирует значения и шлет их в канал

```go
func genValues() <-chan int {
	ch := make(chan int)

	go func() {
		for i := range 10 {
			ch <- i
		}
	}()

	return ch
}
```