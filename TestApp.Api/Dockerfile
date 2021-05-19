#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false
ENV DOTNET_RUNNING_IN_CONTAINER=true

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["TestApp.Api/TestApp.Api.csproj", "TestApp.Api/"]
RUN dotnet restore "TestApp.Api/TestApp.Api.csproj"
COPY . .
WORKDIR "/src/TestApp.Api"
RUN dotnet build "TestApp.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestApp.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestApp.Api.dll"]