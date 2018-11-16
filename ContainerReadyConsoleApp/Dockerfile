FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ContainerReadyConsoleApp/ContainerReadyConsoleApp.csproj ContainerReadyConsoleApp/
RUN dotnet restore ContainerReadyConsoleApp/ContainerReadyConsoleApp.csproj
COPY . .
WORKDIR /src/ContainerReadyConsoleApp
RUN dotnet build ContainerReadyConsoleApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ContainerReadyConsoleApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ContainerReadyConsoleApp.dll"]
