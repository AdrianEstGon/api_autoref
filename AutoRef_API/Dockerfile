# =========================
# BUILD STAGE
# =========================
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copiar el csproj y restaurar
COPY AutoRef_API.csproj ./
RUN dotnet restore AutoRef_API.csproj

# Copiar todo el código
COPY . ./
RUN dotnet publish AutoRef_API.csproj -c Release -o /app/publish

# =========================
# RUNTIME STAGE
# =========================
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final
WORKDIR /app

# Render expone el puerto en PORT
ENV ASPNETCORE_URLS=http://0.0.0.0:${PORT}

# Copiar la app publicada
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "AutoRef_API.dll"]
