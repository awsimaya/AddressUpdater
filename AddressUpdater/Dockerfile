FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY . .
RUN dotnet restore "AddressUpdater.csproj"
RUN dotnet build "AddressUpdater.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AddressUpdater.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AddressUpdater.dll"]