---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-lang-golang-docker/","title":"Docker"}
---


<https://azureserv.com/create-the-smallest-and-secured-golang-docker-image-based-on-scratch-4752223b7324?__cpo=aHR0cHM6Ly9jaGVtaWR5Lm1lZGl1bS5jb20>

Написано на основе статьи о построении самого маленького и защищенного docker image

Для построения образов лучше всего использовать multi-stage билды.

- первый стейдж отвечает за построение образа
- второй содержит только необходимую для запуска

В приведенном билде применены такие рекомендации, как

- в финальном image не должно быть лишних зависимостей
- процессы не должны запускаться из под root пользователя
- импорт происходит только из доверенных (конкретных) образов

```dockerfile
############################
# STEP 1 build executable binary
############################
FROM golang@sha256:0991060a1447cf648bab7f6bb60335d1243930e38420bee8fec3db1267b84cfa as builder
# Install git + SSL ca certificates.
# Git is required for fetching the dependencies.
# Ca-certificates is required to call HTTPS endpoints.
RUN apk update && apk add --no-cache git ca-certificates && update-ca-certificates
# Create appuser
ENV USER=appuser
ENV UID=10001
# See https://stackoverflow.com/a/55757473/12429735RUN 
RUN adduser \    
    --disabled-password \    
    --gecos "" \    
    --home "/nonexistent" \    
    --shell "/sbin/nologin" \    
    --no-create-home \    
    --uid "${UID}" \    
    "${USER}"WORKDIR $GOPATH/src/mypackage/myapp/
COPY . .
# Fetch dependencies.
# Using go mod with go 1.11
RUN go mod download
RUN go mod verify
# Build the binary
RUN GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/hello
############################
# STEP 2 build a small image
############################
FROM scratch
# Import from builder.
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /etc/passwd /etc/passwd
COPY --from=builder /etc/group /etc/group
# Copy our static executable
COPY --from=builder /go/bin/hello /go/bin/hello
# Use an unprivileged user.
USER appuser:appuser
# Run the hello binary.
ENTRYPOINT ["/go/bin/hello"]
```