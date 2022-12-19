FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnet-sample-api/dotnet-sample-api.csproj", "dotnet-sample-api/"]
RUN dotnet restore "dotnet-sample-api/dotnet-sample-api.csproj"
COPY . .
WORKDIR "/src/dotnet-sample-api"
RUN dotnet build "dotnet-sample-api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-sample-api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-sample-api.dll"]
