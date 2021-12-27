# TODO

# We use Postgres for the database, version 11.6 - it can use a minimal OS.
FROM postgres:11.6
# There's an init script which populates the reference data that we need to include:
COPY src/db/init-products-db.sh /docker-entrypoint-initdb.d/

ENV POSTGRES_PASSWORD=widgetario
# Your base image should make it easy to run that script as part of the container startup.
ARG BUILD_VERSION=local
ARG GIT_COMMIT=local
LABEL build_version=${BUILD_VERSION}
LABEL commit_sha=${GIT_COMMIT}