FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["gRPCClient/gRPCClient.csproj", "gRPCClient/"]
RUN dotnet restore "gRPCClient/gRPCClient.csproj"
COPY . .
WORKDIR "/src/gRPCClient"
RUN dotnet build "gRPCClient.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "gRPCClient.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "gRPCClient.dll"]
