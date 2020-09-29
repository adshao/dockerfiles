# Build Clef in a stock Go builder container
FROM golang:1.15-alpine as builder

RUN apk add --no-cache make gcc musl-dev linux-headers git
RUN GO111MODULE=on go get github.com/ethereum/go-ethereum/cmd/clef

# Pull Clef into a second stage deploy alpine container
FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=builder /go/bin/clef /usr/local/bin/
COPY . /clef/

EXPOSE 8550 30303 30303/udp
ENTRYPOINT ["clef"]
