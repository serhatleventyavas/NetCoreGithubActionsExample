FROM mcr.microsoft.com/dotnet/sdk:7.0.102-alpine3.17-arm64v8 as base
WORKDIR /build

RUN apk add --no-cache icu-libs

COPY Http/Http.csproj Http/

RUN ls -la
RUN dotnet restore Http/Http.csproj

COPY . .

FROM base as build

WORKDIR /build

RUN dotnet publish Http \ 
-c Release \
-o /app

FROM mcr.microsoft.com/dotnet/aspnet:7.0

WORKDIR /app

COPY --from=build /app .

ENV ASPNETCORE_URLS=http://*:5000

ENTRYPOINT [ "dotnet", "Http.dll" ]