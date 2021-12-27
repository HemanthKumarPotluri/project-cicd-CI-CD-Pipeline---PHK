# TODO

# We use Golang version 1.15.14 for the build, with the 
# environment variable CGO_ENABLED set to 0.
FROM golang:1.15.14-alpine3.14 AS builder
ENV CGO_ENABLED=0

# Run the build scripts:
WORKDIR /go/stock-api
COPY src/stock-api/. .

RUN chmod +x restore.sh && ./restore.sh
RUN chmod +x build.sh  && ./build.sh
#  you'll need to make the files executable first with chmod +x <filename>.

# Build output is a single executable file:
#  /server

# The app should run on a minimal OS.

# We need to set four environment variables - 
FROM alpine:3.14

ENV POSTGRES_CONNECTION_STRING="host=products-db port=5432 user=postgres password=widgetario dbname=postgres sslmode=disable" \
    CACHE_EXPIRY_SECONDS="45" \
    GOLANG_VERSION="1.15.14" \
    APP_VERSION="0.4.0"

EXPOSE 8080
CMD ["/app/server"]
# The startup command needs to run the executable from the build:
#  /server

# We also need to create an empty directory at /cache.
WORKDIR /cache
WORKDIR /app
COPY --from=builder /server .

ARG BUILD_VERSION=local
ARG GIT_COMMIT=local
LABEL build_version=${BUILD_VERSION}
LABEL commit_sha=${GIT_COMMIT}