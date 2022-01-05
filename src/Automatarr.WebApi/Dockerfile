FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Automatarr.WebApi/Automatarr.WebApi.csproj", "Automatarr.WebApi/"]
RUN dotnet restore "Automatarr.WebApi/Automatarr.WebApi.csproj"
COPY . .
WORKDIR "/src/Automatarr.WebApi"
RUN dotnet build "Automatarr.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Automatarr.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Automatarr.WebApi.dll"]
