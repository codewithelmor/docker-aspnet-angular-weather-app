#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 80
EXPOSE 8080
EXPOSE 8081
EXPOSE 5032
EXPOSE 7038

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Install NodeJs
RUN apt-get update && \
apt-get install -y wget && \
apt-get install -y gnupg2 && \
wget -qO- https://deb.nodesource.com/setup_20.x | bash - && \
apt-get install -y build-essential nodejs
# End Install

ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["weather-app.client/nuget.config", "weather-app.client/"]
COPY ["weather-app.Server/weather-app.Server.csproj", "weather-app.Server/"]
COPY ["weather-app.client/weather-app.client.esproj", "weather-app.client/"]
RUN dotnet restore "./weather-app.Server/./weather-app.Server.csproj"
COPY . .
WORKDIR "/src/weather-app.Server"
RUN dotnet build "weather-app.Server.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "weather-app.Server.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "weather-app.Server.dll"]