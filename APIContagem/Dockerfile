FROM mcr.microsoft.com/dotnet/core/sdk:3.1-alpine AS build-env
WORKDIR /app

# Copiar csproj e restaurar dependencias
COPY /ASPNETCore3.1-API-REST_Docker-Alpine/APIContagem/*.csproj ./
RUN dotnet restore

RUN pwsh -Command Write-Host "APIContagem: Gerando uma nova imagem Docker com Alpine e testando o PowerShell Core"

# Build da aplicacao
COPY . ./
RUN dotnet publish -c Release -o out

# Build da imagem
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "APIContagem.dll"]
