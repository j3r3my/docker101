# ASP.NET Core Docker Production Sample

This ASP.NET Core Docker sample demonstrates a best practice pattern for building Docker images for ASP.NET Core apps for production. The sample works with both Linux and Windows containers.

The [sample Dockerfile](Dockerfile) creates an ASP.NET Core application Docker image based off of the [ASP.NET Core Runtime Docker image](https://hub.docker.com/r/microsoft/aspnetcore/).

It uses the [Docker multi-stage build feature](https://github.com/dotnet/announcements/issues/18) to build the sample in a container based on the larger [ASP.NET Core Build Docker image](https://hub.docker.com/r/microsoft/aspnetcore-build/) and then copies the final build result into a Docker image based on the smaller [ASP.NET Core Docker Runtime image](https://hub.docker.com/r/microsoft/aspnetcore/). The build image contains tools that are required to build applications while the runtime image does not.

This sample requires [Docker 17.06](https://docs.docker.com/release-notes/docker-ce) or later of the [Docker client](https://www.docker.com/products/docker). You need the latest Windows 10 or Windows Server 2016 to use [Windows containers](http://aka.ms/windowscontainers). The instructions assume you have the [Git](https://git-scm.com/downloads) client installed.

## Getting the sample

The easiest way to get the sample is by cloning the samples repository with git, using the following instructions.

```console
git clone https://github.com/j3r3my/docker101.git
```

You can also [download the repository as a zip](https://github.com/j3r3my/docker101.git/archive/master.zip).

## Build and run the sample with Docker for Linux containers

You can build and run the sample in Docker using Linux containers using the following commands. The instructions assume that you are in the root of the repository.

```console
docker build --no-cache -f Dockerfile -t dotnettest .
docker run -it --rm -p 8000:80 dotnettest
```

After the application starts, visit `http://localhost:8000` in your web browser.

Note: The `-p` argument maps port 8000 on you local machine to port 80 in the container (the form of the port mapping is `host:container`). See the [Docker run reference](https://docs.docker.com/engine/reference/commandline/run/) for more information on commandline paramaters.

## Run the sample with Docker Compose

You can launch the sample with docker-compose along with some helper images (Traefik and Portainer)

```console
# attached - see all logs in console
docker-compose up

# detached - run as a local stack
docker-compose up -d
```

You must navigate to the relevant end-points to see the apps in the browser:
* Portainer Dashboard [http://portainer.localhost:8000/#/containers](http://portainer.localhost:8000/#/containers)
* Traefik Dashboard [http://localhost:8080/dashboard/](http://localhost:8080/dashboard/)
* Front End App [http://frontend.localhost:8081/](http://frontend.localhost:8081/)

## Build and run the sample locally

You can build and run the sample locally with the [.NET Core 2.0 SDK](https://www.microsoft.com/net/download/core) using the following commands. The commands assume that you are in the root of the repository.

```console
cd aspnetapp
dotnet run
```

After the application starts, visit `http://localhost:8000` in your web browser.

You can produce an application that is ready to deploy to production locally using the following command.

```console
dotnet publish -c release -o out
```

You can run the application on **Windows** using the following command.

```console
dotnet out\aspnetapp.dll
```

You can run the application on **Linux or macOS** using the following command.

```console
dotnet out/aspnetapp.dll
```

Note: The `-c release` argument builds the application in release mode (the default is debug mode). See the [dotnet run reference](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) for more information on commandline parameters.

## Docker Images used in this sample

The following Docker images are used in this sample

* [microsoft/aspnetcore-build:2.0](https://hub.docker.com/r/microsoft/aspnetcore-build)
* [microsoft/aspnetcore:2.0](https://hub.docker.com/r/microsoft/aspnetcore/)

## Related Resources

* [ASP.NET Core Getting Started Tutorials](https://www.asp.net/get-started)
* [.NET Core Production Docker sample](../dotnetapp-prod/README.md)
* [.NET Core Docker samples](../README.md)
* [.NET Framework Docker samples](https://github.com/Microsoft/dotnet-framework-docker-samples)
