FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Medium_gRPC_Example/Medium_gRPC_Example.csproj", "Medium_gRPC_Example/"]
RUN dotnet restore "Medium_gRPC_Example/Medium_gRPC_Example.csproj"
COPY . .
WORKDIR "/src/Medium_gRPC_Example"
RUN dotnet build "Medium_gRPC_Example.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Medium_gRPC_Example.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Medium_gRPC_Example.dll"]
