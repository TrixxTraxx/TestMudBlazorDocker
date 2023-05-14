FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["TestMudBlazorDocker/TestMudBlazorDocker.csproj", "TestMudBlazorDocker/"]
RUN dotnet restore "TestMudBlazorDocker/TestMudBlazorDocker.csproj"
COPY . .
WORKDIR "/src/TestMudBlazorDocker"
RUN dotnet build "TestMudBlazorDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestMudBlazorDocker.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TestMudBlazorDocker.dll"]
