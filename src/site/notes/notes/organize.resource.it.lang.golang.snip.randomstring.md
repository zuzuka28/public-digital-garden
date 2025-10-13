---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.lang.golang.snip.randomstring/","title":"Randomstring"}
---


Генерация случайной строки из n символов

```go
const defaultCharset = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"

func RandomString(n int, charset ...byte) (string, error) {
	chars := defaultCharset
	if len(charset) > 0 {
		chars = string(charset)
	}

	cnt := len(chars)
	max := 255 / cnt * cnt //nolint:gomnd

	bytes := make([]byte, n)

	randread := n * 5 / 4 //nolint:gomnd
	randbytes := make([]byte, randread)

	for i := 0; i < n; {
		if _, err := rand.Read(randbytes); err != nil {
			return "", err //nolint:wrapcheck
		}

		for j := 0; i < n && j < randread; j++ {
			b := int(randbytes[j])
			if b >= max {
				continue
			}

			bytes[i] = chars[b%cnt]
			i++
		}
	}

	return string(bytes), nil
}
```
