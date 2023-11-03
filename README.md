# docker-development

Docker development guide for C#, Nodejs & Python

## Guide 1

Key concepts to understand while doing docker development

1. Navigating file-systems for Linux and Windows OS
2. Making working directories dynamic instead of hardcoding
3. Understanding working with docker volumes

we use docker & docker compose to build our services

```
# build a service
docker-compose build <service-name>

# build all services
docker-compose build

# start up services
docker-compose up -d

# view running containers
docker ps

# stop services when done
docker-compose down
```

## Guide 2:

This guide covers developer experience in docker development

1. Entering the development containers
2. Generate some source code: C# | Nodejs | Python
3. Installing dependencies:
   - C# - nuget
   - Nodejs: npm install
   - Python: pip install
4. Compile and Run code

### Csharp

```
# enter development container
docker exec -it csharp sh

# create new app
dotnet new webapp

# compile app
dotnet build

# run app
dotnet dev-certs https
dotnet dev-certs https --trust
dotnet run
```

### Nodejs

```
# enter development container
docker exec -it nodejs sh

# install dependencies (express)
npm install

# start up app
npm start
```

### Python

```
# enter development container
docker exec -it python sh

# note flask dependency was install via dockerfile

# start up app
FLASK_APP=server.py flask run -h 0.0.0 -p 5000
```

## Guide 3

Multistage and Layers in docker development:

1. Each stage in a dockerfile can be given an alias
2. Its best practice to include processes that will change often in the bottom part of each stage

## Guide 4

### Debugging .NET Core in Docker with VSCode:

Note: Install C# Extension on VScode, Setup debugger using `launch.json` file.

```
# build service - make sure docker-compose build context is set to debug
docker-compose build csharp

# start service
docker-compose up csharp
```

Use .NET Core debugger via VScode

### Debugging NodeJS in Docker

```
# build nodejs service as debug
docker-compose build nodejs

# start up nodejs service
docker-compose up nodejs
```

Debug Process:

- Install the VSCode Docker extension
- Setup Debug launch.json file
- Add breakpoints to src code & run Docker: Attach to Node debugger
- Visit website at localhost:5002 & notice breakpoint has been hit on VSCode
- You can also make changes and watch the debugger automatically reload website

## Guide 5

Building Docker containers with GitHub Actions:

create a github actions workflow on the repository with `docker.yaml` file.
create secrets for your docker login credentials on the repository as well.
