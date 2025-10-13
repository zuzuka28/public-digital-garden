---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-concurrency-done/","title":"Done"}
---


Завершение работы по сигналу из канала `done`

```go
func withDone(done <-chan struct{}, in int) <-chan int {
	out := make(chan int)

	go func() {
		defer close(out)
		for {
			select {
			case <-done:
				return

			default:
				// do something interesting
                in += 1
				out <- in
			}
		}
	}()

	return out
}
```