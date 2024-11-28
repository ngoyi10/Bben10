FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BankingApp.csproj", "./"]
RUN dotnet restore "BankingApp.csproj"
COPY . .
RUN dotnet build "BankingApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BankingApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BankingApp.dll"]
