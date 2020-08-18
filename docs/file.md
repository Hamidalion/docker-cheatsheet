## Dockerfile

**Usage:**  docker build Dockerfile -t tag_name

```
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["src/Masny.WebApi/Masny.WebApi.csproj", "src/Masny.WebApi/"]
RUN dotnet restore "src/Masny.WebApi/Masny.WebApi.csproj"
COPY . .
WORKDIR "/src/src/Masny.WebApi"
RUN dotnet build "Masny.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Masny.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Masny.WebApi.dll"]
```

**.dockerignore**

```
**/.classpath
**/.dockerignore
**/.env
**/.git
**/.gitignore
**/.project
**/.settings
**/.toolstarget
**/.vs
**/.vscode
**/*.*proj.user
**/*.dbmdl
**/*.jfm
**/azds.yaml
**/bin
**/charts
**/docker-compose*
**/Dockerfile*
**/node_modules
**/npm-debug.log
**/obj
**/secrets.dev.yaml
**/values.dev.yaml
LICENSE
README.md
```
