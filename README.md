# Dockerize an ASP.NET Core application

1. Create a web app using .Net CLI
```
dotnet new webapp -o name-of-your-project
```
2. Add a Docker file and dockerignore file
```
touch Dockerfile
echo "bin/" > .dockerignore
echo "obj/" >> .dockerignore
```
3. Run the project using the file watcher
```
dotnet watch run
```
4. Deployment
    * manual deployment
```
dotnet publish -c Release -o published
dotnet ./published/webapp.dll
docker build -t "urname/webapp" .
```
    * Automatic deployment in Dockerfile
```
    FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
    WORKDIR /app

    # Copy csproj and restore as distinct layers
    COPY *.csproj ./
    RUN dotnet restore

    # Copy everything else and build
    COPY . ./
    RUN dotnet publish -c Release -o out

    # Build runtime image
    FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
    WORKDIR /app
    COPY --from=build-env /app/out .
    ENTRYPOINT ["dotnet", "webapp.dll"]
```
