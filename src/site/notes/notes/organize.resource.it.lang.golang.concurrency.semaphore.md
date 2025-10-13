---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.lang.golang.concurrency.semaphore/","title":"Semaphore"}
---


Семафор

```go
type Semaphore struct {
    semaCh chan struct{}
}

func NewSemaphore(maxReq int) *Semaphore {
    return &Semaphore{
        semaCh: make(chan struct{}, maxReq),
    }
}

func (s *Semaphore) Acquire() {
    s.semaCh <- struct{}{}
}

func (s *Semaphore) Release() {
    <-s.semaCh
}
```