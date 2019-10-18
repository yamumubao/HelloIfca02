FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["HelloIfca02/HelloIfca02.csproj", "HelloIfca02/"]
RUN dotnet restore "HelloIfca02/HelloIfca02.csproj"
COPY . .
WORKDIR "/src/HelloIfca02"
RUN dotnet build "HelloIfca02.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloIfca02.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloIfca02.dll"]