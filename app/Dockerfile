FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

#Copy csproj and restore as distinct lapers
COPY DockerWebApp/*.csproj .
RUN dotnet restore

# Copy everything else and build website
COPY DockerWebApp/. .
RUN dotnet publish -c release -o /WebApp --no-restore

#Final stage / image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /WebApp
COPY --from=build /WebApp ./
ENRTYPOINT ["dotnet", "DockerWebApp,dll"]