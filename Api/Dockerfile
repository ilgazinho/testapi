# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app


COPY *.csproj .

RUN dotnet restore 

# copy and publish app and libraries
COPY . ./
RUN dotnet publish -c release -o api

# final stage/image
FROM mcr.microsoft.com/dotnet/core/aspnet:6.0
WORKDIR /app
COPY --from=build-env app/api .
ENV ASPNETCORE_URLS http://*:1000
ENV ASPNETCORE_ENVIRONMENT docker
EXPOSE 1000
ENTRYPOINT ["dotnet", "API.dll"]