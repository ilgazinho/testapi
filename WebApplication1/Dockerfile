FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 1000
EXPOSE 1001
RUN dotnet restore
COPY . ./
RUN dotnet publish --no-restore -c Realese -o out

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
COPY  --from=build-env /app/out .
ENTRYPOINT ["dotnet","Api.dll"]
