#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/Tm3k.Api/Tm3k.Api.csproj", "src/Tm3k.Api/"]
RUN dotnet restore "src/Tm3k.Api/Tm3k.Api.csproj"
COPY . .
WORKDIR "/src/src/Tm3k.Api"
RUN dotnet build "Tm3k.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Tm3k.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Tm3k.Api.dll"]