FROM golang:1.25-alpine AS builder

WORKDIR /app

RUN apk add --no-cache git ca-certificates

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
    go build -mod=vendor -o muchtodo-api ./cmd/api

FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/muchtodo-api .

EXPOSE 8080

CMD ["./muchtodo-api"]
