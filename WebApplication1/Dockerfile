FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /

COPY *.sln ./
COPY *.csproj ./WebApplication1/
COPY ./WebApplication1/. ./WebApplication1/

RUN dotnet restore ./WebApplication1/WebApplication1.csproj


# copy and publish app and libraries
COPY . .
RUN dotnet publish -c release -o api

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /
COPY --from=build ./WebApplication1/appsettings.json ./WebApplication1/appsettings.json
WORKDIR /app
ENV ASPNETCORE_URLS http://*:7002
ENV ASPNETCORE_ENVIRONMENT docker
EXPOSE 7002
ENTRYPOINT ["dotnet", "API.dll"]