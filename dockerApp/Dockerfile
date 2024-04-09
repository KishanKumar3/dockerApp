FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
ENV ASPNETCORE_ENVIRONMENT="Development"
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dockerApp.csproj", "."]
RUN dotnet restore "dockerApp.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dockerApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dockerApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dockerApp.dll"]