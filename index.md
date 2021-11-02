Open terminal and execute the below commands to create a new .NET web api.

```
cd c:\

mkdir Api1

cd Api1

dotnet new webapi

dotnet run
```

Open a web browser and test the api with `http://localhost:5000/weatherforecast`. Next publish the api in a 
separate folder.

```
cd c:\

mkdir Api1Publish

cd Api1Publish

mkdir publish

cd..

cd Api1

dotnet publish -c Release -o ../Api1Publish/publish

cd..

cd Api1Publish\publish

dotnet Api1.dll
```

Open a web browser and test the api with `http://localhost:5000/weatherforecast`. Next create a `Dockerfile` 
inside `Api1Publish` folder. Write the below code inside that.

```
FROM mcr.microsoft.com/dotnet/aspnet:5.0
COPY publish/ ./app
WORKDIR /app
ENTRYPOINT ["dotnet", "Api1.dll"]
```

Create docker image.

```
cd c:\

cd Api1Publish

docker build -t api1:1.0.0 .
```

Create container from that image.

```
docker create --name c1 -p 80:80 api1:1.0.0
```

Open a web browser and test the api with `http://localhost:80/weatherforecast`.

## Clean up
```
docker rm c1

docker rmi api1:1.0.0
```

Delete the `Api1` and `Api1Publish` folders.