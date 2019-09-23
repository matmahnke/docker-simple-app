FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["PeerOne/PeerOne.csproj", "PeerOne/"]
RUN dotnet restore "PeerOne/PeerOne.csproj"
COPY . .
WORKDIR "/src/PeerOne"
RUN dotnet build "PeerOne.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PeerOne.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PeerOne.dll"]