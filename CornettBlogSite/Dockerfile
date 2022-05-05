FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CornettBlogSite/CornettBlogSite.csproj", "CornettBlogSite/"]
RUN dotnet restore "CornettBlogSite/CornettBlogSite.csproj"
COPY . .
WORKDIR "/src/CornettBlogSite"
RUN dotnet build "CornettBlogSite.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CornettBlogSite.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CornettBlogSite.dll"]
