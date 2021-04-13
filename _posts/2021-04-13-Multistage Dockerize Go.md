## Prerequisites

- [Dockerfile commands](https://docs.docker.com/engine/reference/builder/)
- [This Issue](https://stackoverflow.com/questions/27158840/docker-executable-file-not-found-in-path)
- [This Golang 1.16 Change](https://blog.golang.org/go116-module-changes)
- [Golang Dockerhub](https://hub.docker.com/_/golang)

Ok, let's go Then...

## 0. Why Go?

Golang has efficient server resource consumption.

## 1. Why Dockerize?

Because of Docker benefits themselves, ye?

## 2. Why Mulstistage?

Golang Docker Too Big yanno.

main.go

```Go

package main

import (
  "fmt"
  "log"
)

func main() {
  fmt.Println("Hello")

  log.Printf(" [*] Waiting for messages. To exit press CTRL+C")
}
```

```Dockerfile
FROM golang:buster AS builder

WORKDIR /app/
COPY main.go .
RUN go env -w GO111MODULE=on
RUN go env -w GOPROXY=https://proxy.golang.org,direct

RUN go build ./main.go

FROM alpine:latest
WORKDIR /app/
COPY --from=builder /app .

CMD ["./main"]
```

In case you found some error like:

```cmd
go.mod file not found in current directory or any parent directory; see 'go help modules'
```

Means your Go, not the latest enough.
Add go.mod

```mod
module shohiebsense.com/hello
```
