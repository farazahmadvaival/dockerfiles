FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore "App.UI/App.UI.csproj"

FROM build AS publish
RUN dotnet publish "App.UI/App.UI.csproj" -c Release -o /app/publish /p:self-contained=false

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .

COPY --from=build /src/appsettings.json appsettings.json
ENTRYPOINT ["dotnet", "App.UI.dll"]
