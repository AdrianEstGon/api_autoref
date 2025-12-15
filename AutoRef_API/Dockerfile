# Imagen base con .NET 7 SDK para compilar
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copiar csproj y restaurar dependencias
COPY *.csproj ./
RUN dotnet restore

# Copiar el resto del código
COPY . .
RUN dotnet publish -c Release -o /app/publish

# Imagen final más ligera solo para ejecución
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final
WORKDIR /app

# Render usa la variable PORT
ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}

# Copiar la app publicada
COPY --from=build /app/publish .

# ⚠️ CAMBIA AutoRef_API.dll si tu proyecto se llama distinto
ENTRYPOINT ["dotnet", "AutoRef_API.dll"]