FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ProjectService/ProjectService.csproj", "ProjectService/"]
RUN dotnet restore "ProjectService/ProjectService.csproj"
COPY . .
WORKDIR "/src/ProjectService"
RUN dotnet build "ProjectService.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProjectService.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProjectService.dll"]
