#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AksPOC/AksPOC.csproj", "AksPOC/"]
RUN dotnet restore "AksPOC/AksPOC.csproj"
COPY . .
WORKDIR "/src/AksPOC"
RUN dotnet build "AksPOC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AksPOC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AksPOC.dll"]