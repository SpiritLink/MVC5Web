#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MVC5Web/MVC5Web.csproj", "MVC5Web/"]
RUN dotnet restore "MVC5Web/MVC5Web.csproj"
COPY . .
WORKDIR "/src/MVC5Web"
RUN dotnet build "MVC5Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MVC5Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MVC5Web.dll"]