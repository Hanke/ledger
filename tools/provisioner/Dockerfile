FROM golang:1.23.0-bookworm AS builder
WORKDIR /usr/src/app

# Copy only the necessary files first
COPY pkg/client ./pkg/client/
COPY go.mod go.sum ./

# Now go mod download will work with the replacement directive
RUN go mod download && go mod verify

# Copy the rest of the application
COPY . .

# Build the application
RUN go build -o app

FROM debian:bookworm
LABEL org.opencontainers.image.source=https://github.com/formancehq/ledger
COPY --from=builder /usr/src/app/app /app
ENTRYPOINT ["/app"]
CMD ["--help"] 