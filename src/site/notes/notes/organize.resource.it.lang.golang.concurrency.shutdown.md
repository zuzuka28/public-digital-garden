---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-concurrency-shutdown/","title":"Shutdown"}
---


Сниппет для реализации Graceful Shutdown.

```go
package main

import (
	"log/slog"
	"os"

	"github.com/urfave/cli/v2"
)

func runServer(c *cli.Context) error {
	api, err := ...

	errCh := make(chan error)

	go func() {
		if err := api.Start(c.Context); err != nil {
			errCh <- fmt.Errorf("run webserver: %w", err)
		}
	}()

	osSignals := make(chan os.Signal, 1)
	signal.Notify(osSignals, os.Interrupt, syscall.SIGINT, syscall.SIGTERM)

	select {
	case err := <-errCh:
		return err

	case sig := <-osSignals:
		slog.Warn("got signal", "sig", sig)

		// TODO: Add graceful shutdown logic here

		return nil
	}
}

func main() {
	app := &cli.App{
		Name:  "myapp",
		Action: runServer,
	}

	if err := app.Run(os.Args); err != nil {
		slog.Error("can't run application: " + err.Error())
	}
}
```
