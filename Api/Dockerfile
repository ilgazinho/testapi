# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /

COPY *.sln ./
COPY ./Api/ ./Api/
COPY *.csproj ./Api/



RUN dotnet restore ./Api/Api.csproj

# copy and publish app and libraries
COPY . .
RUN dotnet publish -c release -o api

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /
COPY --from=build ./api ./app
COPY --from=build ./Api/appsettings.json ./app/appsettings.json
WORKDIR /app
ENV ASPNETCORE_URLS http://*:1000
ENV ASPNETCORE_ENVIRONMENT docker
EXPOSE 7002
ENTRYPOINT ["dotnet", "API.dll"]