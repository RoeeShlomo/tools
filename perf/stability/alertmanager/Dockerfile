FROM golang:1.12 as builder
WORKDIR /webhook
COPY webhook.go .
RUN go get github.com/prometheus/alertmanager/template
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo webhook.go

FROM alpine:3.7
WORKDIR /bin/
COPY --from=builder /webhook/webhook .
CMD ["./webhook"]
EXPOSE 5001
