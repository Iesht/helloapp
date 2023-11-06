FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Hello/Hello.csproj", "Hello/"]
RUN dotnet restore "Hello/Hello.csproj"
COPY . .
WORKDIR "/src/Hello"
RUN dotnet build "Hello.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hello.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hello.dll"]
