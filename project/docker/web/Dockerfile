# TODO

# We use .NET SDK version 6.0 for the build.
FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine AS builder
# Run the build scripts:
WORKDIR /src
COPY src/web/ .

RUN chmod +x restore.sh && ./restore.sh
RUN chmod +x build.sh  && ./build.sh
#  you'll need to make the files executable first with chmod +x <filename>.


# Build output is in the folder:
#  /out

# The app should run using a .NET ASP.NET 6.0 image, with a minimal OS.
FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine
# We need to set four environment variables - 
ENV Widgetario__ProductsApi__Url="http://products-api/products" \
    Widgetario__StockApi__Url="http://stock-api:8080/stock" \
    DOTNET_VERSION="6.0" \
    APP_VERSION="1.0.0"

ENTRYPOINT ["dotnet", "/app/Widgetario.Web.dll"]
# The startup command needs to run the DLL from the build:
WORKDIR /app
COPY --from=builder /out/ .

ARG BUILD_VERSION=local
ARG GIT_COMMIT=local
LABEL build_version=${BUILD_VERSION}
LABEL commit_sha=${GIT_COMMIT}