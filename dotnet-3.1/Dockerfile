FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY . .
RUN dotnet restore "App.UI/App.UI.csproj"

FROM build AS publish
RUN dotnet publish "App.UI/App.UI.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-alpine AS runtime
RUN apk add libgdiplus
WORKDIR /app
COPY --from=publish /app/publish .

COPY --from=awscli /app/target-folder/app-settings-dev.json appsettings.json

ENTRYPOINT ["dotnet", "App.UI.dll"]
