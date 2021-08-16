FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["aspApiTest210816/aspApiTest210816.csproj", "aspApiTest210816/"]
RUN dotnet restore "aspApiTest210816/aspApiTest210816.csproj"
COPY . .
WORKDIR "/src/aspApiTest210816"
RUN dotnet build "aspApiTest210816.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspApiTest210816.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspApiTest210816.dll"]
