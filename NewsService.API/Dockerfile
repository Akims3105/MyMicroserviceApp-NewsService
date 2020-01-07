#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["NewsService.API/NewsService.API.csproj", "NewsService.API/"]
RUN dotnet restore "NewsService.API/NewsService.API.csproj"
COPY . .
WORKDIR "/src/NewsService.API"
RUN dotnet build "NewsService.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NewsService.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NewsService.API.dll"]