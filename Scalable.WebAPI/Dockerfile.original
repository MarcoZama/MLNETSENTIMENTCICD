FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Scalable.WebAPI/Scalable.WebAPI.csproj", "Scalable.WebAPI/"]
RUN dotnet restore "Scalable.WebAPI/Scalable.WebAPI.csproj"
COPY . .
WORKDIR "/src/Scalable.WebAPI"
RUN dotnet build "Scalable.WebAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Scalable.WebAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Scalable.WebAPI.dll"]