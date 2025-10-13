---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-t-func/","title":"Func"}
---


## Function Closure

При создании замыкания захваченные переменные перемещаются на кучу (heap), создается указатель на новую функцию.
Код замыкания хранится в сегменте с кодом.

### Как инициализируется замыкание

Задался этим вопросом, когда столкнулся с ошибкой в таком коде:

```go
func (s *dothing) Fetch(
	query MyQuery,
) (...) {
	errg, ctx := errgroup.WithContext(ctx)

	errg.Go(func() error {
		res, err := s.fetchPart(ctx, query)
		if err != nil { ... }

        ...

		return nil
	})

	errg.Go(func() error {
        query.Filter = getFilter()

		res, err := s.fetchPart(ctx, query)
		if err != nil { ... }

        ...

		return nil
	})

	if err := errg.Wait(); err != nil { ...	}

	return &result, nil
}
```

Спросил у ChatGPT, вот ответ

```
Сlosures in Go are functions that reference variables from their surrounding lexical scope. This means they capture and "close over" the variables that are in scope when the function is defined, not when it is called. Here's a step-by-step explanation of the workflow:

1. Function Definition: When a closure is defined, it captures the variables from its surrounding scope.
2. Function Invocation: When the closure is invoked, it uses the captured variables.
3. Variable Capture: If the captured variables are modified outside the closure before the closure is invoked, the closure sees the modified values.
```

То есть корректная версия выглядит так:

```go
func (s *dothing) Fetch(
	query MyQuery,
) (...) {
	errg, ctx := errgroup.WithContext(ctx)

	errg.Go(func() error {
		query := query

		res, err := s.fetchPart(ctx, query)
		if err != nil { ... }

        ...

		return nil
	})

	errg.Go(func() error {
        query := query
        
        query.Filter = getFilter()

		res, err := s.fetchPart(ctx, query)
		if err != nil { ... }

        ...

		return nil
	})

	if err := errg.Wait(); err != nil { ...	}

	return &result, nil
}
```