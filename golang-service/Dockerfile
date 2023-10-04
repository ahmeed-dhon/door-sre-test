#build stage
FROM golang:1.13 AS builder

WORKDIR $GOPATH/src/golang-service

COPY . .

RUN CGO_ENABLED=0 go build -o /golang-service

# final stage
FROM alpine:3.13

# Labels
LABEL Name="golang-service" \
      Version="1.0"

### set root as working directory
WORKDIR /

## COPY binary file
COPY --from=builder /golang-service /golang-service

# Service ports
EXPOSE 8090/tcp

CMD ["/golang-service"]