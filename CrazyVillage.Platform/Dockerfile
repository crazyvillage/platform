FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["CrazyVillage.Platform/CrazyVillage.Platform.csproj", "CrazyVillage.Platform/"]
RUN dotnet restore "CrazyVillage.Platform/CrazyVillage.Platform.csproj"
COPY . .
WORKDIR "/src/CrazyVillage.Platform"
RUN dotnet build "CrazyVillage.Platform.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CrazyVillage.Platform.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CrazyVillage.Platform.dll"]
