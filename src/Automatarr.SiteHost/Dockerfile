FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Automatarr.SiteHost/Automatarr.SiteHost.csproj", "Automatarr.SiteHost/"]
RUN dotnet restore "Automatarr.SiteHost/Automatarr.SiteHost.csproj"
COPY . .
WORKDIR "/src/Automatarr.SiteHost"
RUN dotnet build "Automatarr.SiteHost.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Automatarr.SiteHost.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Automatarr.SiteHost.dll"]
