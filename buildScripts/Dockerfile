#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_URLS=http://*:8000

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["BlazorSampleApp.csproj", "."]
RUN dotnet restore "./BlazorSampleApp.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "BlazorSampleApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorSampleApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorSampleApp.dll"]