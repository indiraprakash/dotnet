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
..* Build and deploy manually
```
dotnet publish -c Release -o published
dotnet ./published/webapp.dll
```
