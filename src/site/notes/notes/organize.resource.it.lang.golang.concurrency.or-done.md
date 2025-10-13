---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.lang.golang.concurrency.or-done/","title":"Or Done"}
---


Функция для инкапсуляции обработки завершений.

Данная функция пересылает сообщения из `in` до тех пор, пока не будет прислано сообщение в `done`.

```go
func orDone(done <-chan struct{}, in <-chan string) <-chan string {
	out := make(chan string)

	go func() {
		defer close(out)
		for {
			select {
			case <-done:
				return

			case v, inputChanStillOpen := <-in:
				if !inputChanStillOpen {
					return
				}

				out <- v
			}
		}
	}()

	return out
}
```