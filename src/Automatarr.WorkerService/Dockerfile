FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Automatarr.WorkerService/Automatarr.WorkerService.csproj", "Automatarr.WorkerService/"]
RUN dotnet restore "Automatarr.WorkerService/Automatarr.WorkerService.csproj"
COPY . .
WORKDIR "/src/Automatarr.WorkerService"
RUN dotnet build "Automatarr.WorkerService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Automatarr.WorkerService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Automatarr.WorkerService.dll"]
