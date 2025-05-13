FROM golang:1.24-alpine AS compiler
WORKDIR /src

# Copy the entire project first to ensure pkg/client is available
COPY . .

# Now go mod download will work with the replacement directive
RUN --mount=type=cache,target=$GOPATH go mod download

# Build the application
RUN --mount=type=cache,target=$GOPATH go build -o provisioner

FROM alpine:3.21
LABEL org.opencontainers.image.source=https://github.com/formancehq/ledger
COPY --from=compiler /src/provisioner /bin/provisioner
ENTRYPOINT ["/bin/provisioner"]
CMD ["--help"]
