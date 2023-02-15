FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Macini.WebApi/Macini.WebApi.csproj", "Macini.WebApi/"]
RUN dotnet restore "Macini.WebApi/Macini.WebApi.csproj"
COPY . .
WORKDIR "/src/Macini.WebApi"
RUN dotnet build "Macini.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Macini.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Macini.WebApi.dll"]
