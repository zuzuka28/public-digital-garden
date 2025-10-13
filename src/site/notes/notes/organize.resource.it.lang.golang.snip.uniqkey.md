---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-snip-uniqkey/","title":"Uniqkey"}
---


Генерация уникальных ключей.
Хоть передача невидимых параметров нежелательна, иногда приходится прибегать к ней.

Данный код можно использовать для генерации ключей, которые можно использовать вместе с context.Context и map.

```go
var lastID int32 = 1

// DataKey used to maintain the uniqueness of properties between different packages.
type DataKey struct{ id int32 }

func (d DataKey) String() string {
	return strconv.Itoa(int(d.id))
}

// Gen generates new unique key for property.
func Gen() DataKey { return DataKey{id: atomic.AddInt32(&lastID, 1)} }
```
