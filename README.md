![IIS Docker Image](https://avatars2.githubusercontent.com/u/6154722?v=3&s=200)
# IIS Docker Image

# Supported Windows Server, version 1909 amd64 tags

 `docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-1909`

 [`windowsservercore-1909, latest` (*windowsserver/Dockerfile*)](https://github.com/Microsoft/iis-docker/blob/master/windowsservercore-1909/Dockerfile)

# Supported Windows Server, version 1903 amd64 tags

 `docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-1903`

 [`windowsservercore-1903, latest` (*windowsserver/Dockerfile*)](https://github.com/Microsoft/iis-docker/blob/master/windowsservercore-1903/Dockerfile)

# Supported Windows Server 2019 amd64 tags

 `docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2019`

 [`windowsservercore-ltsc2019, latest` (*windowsserver/Dockerfile*)](https://github.com/Microsoft/iis-docker/blob/master/windowsservercore-ltsc2019/Dockerfile)

# Supported Windows Server, version 1803 amd64 tags

 `docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-1803`

 [`windowsservercore-1803, latest` (*windowsserver/Dockerfile*)](https://github.com/Microsoft/iis-docker/blob/master/windowsservercore-1803/Dockerfile)

# Supported Windows Server 2016 amd64 tags

 `docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2016`

 [`windowsservercore-ltsc2016, latest` (*windowsserver/Dockerfile*)](https://github.com/Microsoft/iis-docker/blob/master/windowsservercore-ltsc2016/Dockerfile)

## What is IIS?
Internet Information Services (IIS) for Windows® Server is a flexible, secure and manageable Web server for hosting anything on the Web.

## How to use this image?
### Create a Dockerfile with your website
```Dockerfile
FROM microsoft/iis

RUN powershell -NoProfile -Command Remove-Item -Recurse C:\inetpub\wwwroot\*

WORKDIR /inetpub/wwwroot

COPY content/ .
```
You can then build and run the Docker image:
```
$ docker build -t iis-site .
$ docker run -d -p 8000:80 --name my-running-site iis-site
```

There is no need to specify an `ENTRYPOINT` in your Dockerfile since the `microsoft/iis` base image already includes an entrypoint application that monitors the status of the IIS World Wide Web Publishing Service (W3SVC).

### Verify in the browser

#### On newer hosts (Windows Server, version 1803 and newer)

You can connect to the running container using `http://localhost:8000` in the example shown.

#### On older hosts (Windows Server, version 1709 and older)

> If you are running an older host, you cannot use `http://localhost` to browse your site from the container host. This is because of a known behavior in WinNAT and you need to use the IP address of the container.

 Once the container starts, you'll need to finds its IP address so that you can connect to your running container from a browser. You use the `docker inspect` command to do that:	
 `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-running-site`	
 You will see an output similar to this:	
 ```	
172.28.103.186	
```	
 You can connect the running container using the IP address and configured port, `http://172.28.103.186:80` in the example shown.

In addition to static content, IIS can run other workloads including, but not limited to ASP.NET, ASP.NET Core, NodeJS, PHP, and Apache Tomcat.

For a comprehensive tutorial on running an ASP.NET app in a container, check out [the tutorial on the docs site](https://docs.microsoft.com/en-us/dotnet/articles/framework/docker/aspnetmvc).

## Supported Docker Versions
This image has been tested on Docker Versions 17.10 or higher.

## License
MICROSOFT SOFTWARE SUPPLEMENTAL LICENSE TERMS

CONTAINER OS IMAGE

Microsoft Corporation (or based on where you live, one of its affiliates) (referenced as “us,” “we,” or “Microsoft”) licenses this Container OS Image supplement to you (“Supplement”). You are licensed to use this Supplement in conjunction with the underlying host operating system software (“Host Software”) solely to assist running the containers feature in the Host Software. The Host Software license terms apply to your use of the Supplement. You may not use it if you do not have a license for the Host Software. You may use this Supplement with each validly licensed copy of the Host Software.

## User Feedback
If you have any issues or concerns, reach out to us through a [GitHub issue](https://github.com/Microsoft/iis-docker/issues/new).