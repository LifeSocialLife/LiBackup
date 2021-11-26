#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ClientSoftware/ClientSoftware.csproj", "ClientSoftware/"]
RUN dotnet restore "ClientSoftware/ClientSoftware.csproj"
COPY . .
WORKDIR "/src/ClientSoftware"
RUN dotnet build "ClientSoftware.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ClientSoftware.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ClientSoftware.dll"]