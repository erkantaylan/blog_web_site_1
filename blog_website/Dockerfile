FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["blog_website/blog_website.csproj", "blog_website/"]
COPY ["myLib/myLib.csproj", "myLib/"]
RUN dotnet restore "blog_website/blog_website.csproj"
COPY . .
WORKDIR "/src/blog_website"
RUN dotnet build "blog_website.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "blog_website.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "blog_website.dll"]
