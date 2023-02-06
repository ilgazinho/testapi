FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

COPY *.csproj .

RUN dotnet restore 
COPY . ./

# copy and publish app and libraries
COPY . .
RUN dotnet publish -c release -o out

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /
COPY --from=build ./WebApplication1/appsettings.json ./WebApplication1/appsettings.json
WORKDIR /app
ENV ASPNETCORE_URLS http://*:7002
ENV ASPNETCORE_ENVIRONMENT docker
EXPOSE 7002
ENTRYPOINT ["dotnet", "API.dll"]