---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-concurrency-pipeline/","title":"Pipeline"}
---


Разделенная на несколько этапов обработка данных.

```go
func stage1(in <-chan string) <-chan string {
	out := make(chan string)

	go func() {
		defer close(out)
		for el := range in {
			out <- el + "1"
		}
	}()

	return out
}

func stage2(in <-chan string) <-chan string {
	output := make(chan string)

	go func() {
		defer close(out)
		for el := range in {
			out <- el + "2"
		}
	}()

	return out
}

func stage3(in <-chan string) <-chan string {
	out := make(chan string)

	go func() {
		defer close(out)
		for el := range in {
			out <- el + "3"
		}
	}()

	return out
}
```