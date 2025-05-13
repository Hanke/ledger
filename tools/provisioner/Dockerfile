FROM golang:1.23.0-bookworm AS builder
WORKDIR /usr/src/app

# Copy the entire project first
COPY . .

# Verify the pkg/client directory exists
RUN ls -la pkg/client || echo "pkg/client directory not found"

# Now go mod download will work with the replacement directive
RUN go mod download && go mod verify

# Build the application
RUN go build -o app

FROM debian:bookworm
LABEL org.opencontainers.image.source=https://github.com/formancehq/ledger
COPY --from=builder /usr/src/app/app /app
ENTRYPOINT ["/app"]
CMD ["--help"]
