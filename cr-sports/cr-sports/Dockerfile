#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["cr-sports/cr-sports.csproj", "cr-sports/"]
RUN dotnet restore "cr-sports/cr-sports.csproj"
COPY . .
WORKDIR "/src/cr-sports"
RUN dotnet build "cr-sports.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "cr-sports.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "cr-sports.dll"]