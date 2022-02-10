#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Razor50NoDocker/Razor50NoDocker.csproj", "Razor50NoDocker/"]
RUN dotnet restore "Razor50NoDocker/Razor50NoDocker.csproj"
COPY . .
WORKDIR "/src/Razor50NoDocker"
RUN dotnet build "Razor50NoDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Razor50NoDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Razor50NoDocker.dll"]